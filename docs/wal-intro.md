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

Supported Versions: [Current](/docs/current/wal-intro.html "PostgreSQL 17 -
30.3. Write-Ahead Logging \(WAL\)") ([17](/docs/17/wal-intro.html "PostgreSQL
17 - 30.3. Write-Ahead Logging \(WAL\)")) / [16](/docs/16/wal-intro.html
"PostgreSQL 16 - 30.3. Write-Ahead Logging \(WAL\)") / [15](/docs/15/wal-
intro.html "PostgreSQL 15 - 30.3. Write-Ahead Logging \(WAL\)") /
[14](/docs/14/wal-intro.html "PostgreSQL 14 - 30.3. Write-Ahead Logging
\(WAL\)") / [13](/docs/13/wal-intro.html "PostgreSQL 13 - 30.3. Write-Ahead
Logging \(WAL\)")

Development Versions: [18](/docs/18/wal-intro.html "PostgreSQL 18 -
30.3. Write-Ahead Logging \(WAL\)") / [devel](/docs/devel/wal-intro.html
"PostgreSQL devel - 30.3. Write-Ahead Logging \(WAL\)")

Unsupported versions: [12](/docs/12/wal-intro.html "PostgreSQL 12 -
30.3. Write-Ahead Logging \(WAL\)") / [11](/docs/11/wal-intro.html "PostgreSQL
11 - 30.3. Write-Ahead Logging \(WAL\)") / [10](/docs/10/wal-intro.html
"PostgreSQL 10 - 30.3. Write-Ahead Logging \(WAL\)") / [9.6](/docs/9.6/wal-
intro.html "PostgreSQL 9.6 - 30.3. Write-Ahead Logging \(WAL\)") /
[9.5](/docs/9.5/wal-intro.html "PostgreSQL 9.5 - 30.3. Write-Ahead Logging
\(WAL\)") / [9.4](/docs/9.4/wal-intro.html "PostgreSQL 9.4 - 30.3. Write-Ahead
Logging \(WAL\)") / [9.3](/docs/9.3/wal-intro.html "PostgreSQL 9.3 -
30.3. Write-Ahead Logging \(WAL\)") / [9.2](/docs/9.2/wal-intro.html
"PostgreSQL 9.2 - 30.3. Write-Ahead Logging \(WAL\)") / [9.1](/docs/9.1/wal-
intro.html "PostgreSQL 9.1 - 30.3. Write-Ahead Logging \(WAL\)") /
[9.0](/docs/9.0/wal-intro.html "PostgreSQL 9.0 - 30.3. Write-Ahead Logging
\(WAL\)") / [8.4](/docs/8.4/wal-intro.html "PostgreSQL 8.4 - 30.3. Write-Ahead
Logging \(WAL\)") / [8.3](/docs/8.3/wal-intro.html "PostgreSQL 8.3 -
30.3. Write-Ahead Logging \(WAL\)") / [8.2](/docs/8.2/wal-intro.html
"PostgreSQL 8.2 - 30.3. Write-Ahead Logging \(WAL\)") / [8.1](/docs/8.1/wal-
intro.html "PostgreSQL 8.1 - 30.3. Write-Ahead Logging \(WAL\)")

__

30.3. Write-Ahead Logging (WAL)  
---  
[Prev](checksums.html "30.2. Data Checksums")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") | Chapter 30. Reliability and the Write-Ahead Log | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](wal-async-commit.html "30.4. Asynchronous Commit")  
  
* * *

## 30.3. Write-Ahead Logging (WAL) #

_Write-Ahead Logging_ (WAL) is a standard method for ensuring data integrity.
A detailed description can be found in most (if not all) books about
transaction processing. Briefly, WAL's central concept is that changes to data
files (where tables and indexes reside) must be written only after those
changes have been logged, that is, after WAL records describing the changes
have been flushed to permanent storage. If we follow this procedure, we do not
need to flush data pages to disk on every transaction commit, because we know
that in the event of a crash we will be able to recover the database using the
log: any changes that have not been applied to the data pages can be redone
from the WAL records. (This is roll-forward recovery, also known as REDO.)

### Tip

Because WAL restores database file contents after a crash, journaled file
systems are not necessary for reliable storage of the data files or WAL files.
In fact, journaling overhead can reduce performance, especially if journaling
causes file system _data_ to be flushed to disk. Fortunately, data flushing
during journaling can often be disabled with a file system mount option, e.g.,
`data=writeback` on a Linux ext3 file system. Journaled file systems do
improve boot speed after a crash.

Using WAL results in a significantly reduced number of disk writes, because
only the WAL file needs to be flushed to disk to guarantee that a transaction
is committed, rather than every data file changed by the transaction. The WAL
file is written sequentially, and so the cost of syncing the WAL is much less
than the cost of flushing the data pages. This is especially true for servers
handling many small transactions touching different parts of the data store.
Furthermore, when the server is processing many small concurrent transactions,
one `fsync` of the WAL file may suffice to commit many transactions.

WAL also makes it possible to support on-line backup and point-in-time
recovery, as described in [Section 26.3](continuous-archiving.html
"26.3. Continuous Archiving and Point-in-Time Recovery \(PITR\)"). By
archiving the WAL data we can support reverting to any time instant covered by
the available WAL data: we simply install a prior physical backup of the
database, and replay the WAL just as far as the desired time. What's more, the
physical backup doesn't have to be an instantaneous snapshot of the database
state — if it is made over some period of time, then replaying the WAL for
that period will fix any internal inconsistencies.

* * *

[Prev](checksums.html "30.2. Data Checksums")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") |  [Next](wal-async-commit.html "30.4. Asynchronous Commit")  
---|---|---  
30.2. Data Checksums  | [Home](index.html "PostgreSQL 16.9 Documentation") |  30.4. Asynchronous Commit  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/wal-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

