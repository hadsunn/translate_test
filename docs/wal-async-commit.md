[ ![PostgreSQL Elephant Logo](/media/img/about/press/elephant.png) ](/)

  * [Home](/ "Home")
  * [About](/about/ "About")
  * [Download](/download/ "Download")
  * [Documentation](/docs/ "Documentation")
  * [Community](/community/ "Community")
  * [Developers](/developer/ "Developers")
  * [Support](/support/ "Support")
  * [Donate](/about/donate/ "Donate")
  * [Your account](/account/ "Your account")

__

May 8, 2025: [ PostgreSQL 17.5, 16.9, 15.13, 14.18, and 13.21 Released! ](/about/news/postgresql-175-169-1513-1418-and-1321-released-3072/) | [ PostgreSQL 18 Beta 1 Released! ](/about/news/postgresql-18-beta-1-released-3070/)

[Documentation](/docs/ "Documentation") -> [PostgreSQL
16](/docs/16/index.html)

Supported Versions: [Current](/docs/current/wal-async-commit.html "PostgreSQL
17 - 30.4. Asynchronous Commit") ([17](/docs/17/wal-async-commit.html
"PostgreSQL 17 - 30.4. Asynchronous Commit")) / [16](/docs/16/wal-async-
commit.html "PostgreSQL 16 - 30.4. Asynchronous Commit") / [15](/docs/15/wal-
async-commit.html "PostgreSQL 15 - 30.4. Asynchronous Commit") /
[14](/docs/14/wal-async-commit.html "PostgreSQL 14 - 30.4. Asynchronous
Commit") / [13](/docs/13/wal-async-commit.html "PostgreSQL 13 -
30.4. Asynchronous Commit")

Development Versions: [18](/docs/18/wal-async-commit.html "PostgreSQL 18 -
30.4. Asynchronous Commit") / [devel](/docs/devel/wal-async-commit.html
"PostgreSQL devel - 30.4. Asynchronous Commit")

Unsupported versions: [12](/docs/12/wal-async-commit.html "PostgreSQL 12 -
30.4. Asynchronous Commit") / [11](/docs/11/wal-async-commit.html "PostgreSQL
11 - 30.4. Asynchronous Commit") / [10](/docs/10/wal-async-commit.html
"PostgreSQL 10 - 30.4. Asynchronous Commit") / [9.6](/docs/9.6/wal-async-
commit.html "PostgreSQL 9.6 - 30.4. Asynchronous Commit") /
[9.5](/docs/9.5/wal-async-commit.html "PostgreSQL 9.5 - 30.4. Asynchronous
Commit") / [9.4](/docs/9.4/wal-async-commit.html "PostgreSQL 9.4 -
30.4. Asynchronous Commit") / [9.3](/docs/9.3/wal-async-commit.html
"PostgreSQL 9.3 - 30.4. Asynchronous Commit") / [9.2](/docs/9.2/wal-async-
commit.html "PostgreSQL 9.2 - 30.4. Asynchronous Commit") /
[9.1](/docs/9.1/wal-async-commit.html "PostgreSQL 9.1 - 30.4. Asynchronous
Commit") / [9.0](/docs/9.0/wal-async-commit.html "PostgreSQL 9.0 -
30.4. Asynchronous Commit") / [8.4](/docs/8.4/wal-async-commit.html
"PostgreSQL 8.4 - 30.4. Asynchronous Commit") / [8.3](/docs/8.3/wal-async-
commit.html "PostgreSQL 8.3 - 30.4. Asynchronous Commit")

__

30.4. Asynchronous Commit  
---  
[Prev](wal-intro.html "30.3. Write-Ahead Logging \(WAL\)")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") | Chapter 30. Reliability and the Write-Ahead Log | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](wal-configuration.html "30.5. WAL Configuration")  
  
* * *

## 30.4. Asynchronous Commit #

_Asynchronous commit_ is an option that allows transactions to complete more
quickly, at the cost that the most recent transactions may be lost if the
database should crash. In many applications this is an acceptable trade-off.

As described in the previous section, transaction commit is normally
_synchronous_ : the server waits for the transaction's WAL records to be
flushed to permanent storage before returning a success indication to the
client. The client is therefore guaranteed that a transaction reported to be
committed will be preserved, even in the event of a server crash immediately
after. However, for short transactions this delay is a major component of the
total transaction time. Selecting asynchronous commit mode means that the
server returns success as soon as the transaction is logically completed,
before the WAL records it generated have actually made their way to disk. This
can provide a significant boost in throughput for small transactions.

Asynchronous commit introduces the risk of data loss. There is a short time
window between the report of transaction completion to the client and the time
that the transaction is truly committed (that is, it is guaranteed not to be
lost if the server crashes). Thus asynchronous commit should not be used if
the client will take external actions relying on the assumption that the
transaction will be remembered. As an example, a bank would certainly not use
asynchronous commit for a transaction recording an ATM's dispensing of cash.
But in many scenarios, such as event logging, there is no need for a strong
guarantee of this kind.

The risk that is taken by using asynchronous commit is of data loss, not data
corruption. If the database should crash, it will recover by replaying WAL up
to the last record that was flushed. The database will therefore be restored
to a self-consistent state, but any transactions that were not yet flushed to
disk will not be reflected in that state. The net effect is therefore loss of
the last few transactions. Because the transactions are replayed in commit
order, no inconsistency can be introduced — for example, if transaction B made
changes relying on the effects of a previous transaction A, it is not possible
for A's effects to be lost while B's effects are preserved.

The user can select the commit mode of each transaction, so that it is
possible to have both synchronous and asynchronous commit transactions running
concurrently. This allows flexible trade-offs between performance and
certainty of transaction durability. The commit mode is controlled by the
user-settable parameter [synchronous_commit](runtime-config-wal.html#GUC-
SYNCHRONOUS-COMMIT), which can be changed in any of the ways that a
configuration parameter can be set. The mode used for any one transaction
depends on the value of `synchronous_commit` when transaction commit begins.

Certain utility commands, for instance `DROP TABLE`, are forced to commit
synchronously regardless of the setting of `synchronous_commit`. This is to
ensure consistency between the server's file system and the logical state of
the database. The commands supporting two-phase commit, such as `PREPARE
TRANSACTION`, are also always synchronous.

If the database crashes during the risk window between an asynchronous commit
and the writing of the transaction's WAL records, then changes made during
that transaction _will_ be lost. The duration of the risk window is limited
because a background process (the “WAL writer”) flushes unwritten WAL records
to disk every [wal_writer_delay](runtime-config-wal.html#GUC-WAL-WRITER-DELAY)
milliseconds. The actual maximum duration of the risk window is three times
`wal_writer_delay` because the WAL writer is designed to favor writing whole
pages at a time during busy periods.

### Caution

An immediate-mode shutdown is equivalent to a server crash, and will therefore
cause loss of any unflushed asynchronous commits.

Asynchronous commit provides behavior different from setting [fsync](runtime-
config-wal.html#GUC-FSYNC) = off. `fsync` is a server-wide setting that will
alter the behavior of all transactions. It disables all logic within
PostgreSQL that attempts to synchronize writes to different portions of the
database, and therefore a system crash (that is, a hardware or operating
system crash, not a failure of PostgreSQL itself) could result in arbitrarily
bad corruption of the database state. In many scenarios, asynchronous commit
provides most of the performance improvement that could be obtained by turning
off `fsync`, but without the risk of data corruption.

[commit_delay](runtime-config-wal.html#GUC-COMMIT-DELAY) also sounds very
similar to asynchronous commit, but it is actually a synchronous commit method
(in fact, `commit_delay` is ignored during an asynchronous commit).
`commit_delay` causes a delay just before a transaction flushes WAL to disk,
in the hope that a single flush executed by one such transaction can also
serve other transactions committing at about the same time. The setting can be
thought of as a way of increasing the time window in which transactions can
join a group about to participate in a single flush, to amortize the cost of
the flush among multiple transactions.

* * *

[Prev](wal-intro.html "30.3. Write-Ahead Logging \(WAL\)")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") |  [Next](wal-configuration.html "30.5. WAL Configuration")  
---|---|---  
30.3. Write-Ahead Logging (WAL)  | [Home](index.html "PostgreSQL 16.9 Documentation") |  30.5. WAL Configuration  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/wal-async-commit.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

