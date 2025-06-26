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

Supported Versions: [Current](/docs/current/applevel-consistency.html
"PostgreSQL 17 - 13.4. Data Consistency Checks at the Application Level")
([17](/docs/17/applevel-consistency.html "PostgreSQL 17 - 13.4. Data
Consistency Checks at the Application Level")) / [16](/docs/16/applevel-
consistency.html "PostgreSQL 16 - 13.4. Data Consistency Checks at the
Application Level") / [15](/docs/15/applevel-consistency.html "PostgreSQL 15 -
13.4. Data Consistency Checks at the Application Level") /
[14](/docs/14/applevel-consistency.html "PostgreSQL 14 - 13.4. Data
Consistency Checks at the Application Level") / [13](/docs/13/applevel-
consistency.html "PostgreSQL 13 - 13.4. Data Consistency Checks at the
Application Level")

Development Versions: [18](/docs/18/applevel-consistency.html "PostgreSQL 18 -
13.4. Data Consistency Checks at the Application Level") /
[devel](/docs/devel/applevel-consistency.html "PostgreSQL devel - 13.4. Data
Consistency Checks at the Application Level")

Unsupported versions: [12](/docs/12/applevel-consistency.html "PostgreSQL 12 -
13.4. Data Consistency Checks at the Application Level") /
[11](/docs/11/applevel-consistency.html "PostgreSQL 11 - 13.4. Data
Consistency Checks at the Application Level") / [10](/docs/10/applevel-
consistency.html "PostgreSQL 10 - 13.4. Data Consistency Checks at the
Application Level") / [9.6](/docs/9.6/applevel-consistency.html "PostgreSQL
9.6 - 13.4. Data Consistency Checks at the Application Level") /
[9.5](/docs/9.5/applevel-consistency.html "PostgreSQL 9.5 - 13.4. Data
Consistency Checks at the Application Level") / [9.4](/docs/9.4/applevel-
consistency.html "PostgreSQL 9.4 - 13.4. Data Consistency Checks at the
Application Level") / [9.3](/docs/9.3/applevel-consistency.html "PostgreSQL
9.3 - 13.4. Data Consistency Checks at the Application Level") /
[9.2](/docs/9.2/applevel-consistency.html "PostgreSQL 9.2 - 13.4. Data
Consistency Checks at the Application Level") / [9.1](/docs/9.1/applevel-
consistency.html "PostgreSQL 9.1 - 13.4. Data Consistency Checks at the
Application Level") / [9.0](/docs/9.0/applevel-consistency.html "PostgreSQL
9.0 - 13.4. Data Consistency Checks at the Application Level") /
[8.4](/docs/8.4/applevel-consistency.html "PostgreSQL 8.4 - 13.4. Data
Consistency Checks at the Application Level") / [8.3](/docs/8.3/applevel-
consistency.html "PostgreSQL 8.3 - 13.4. Data Consistency Checks at the
Application Level") / [8.2](/docs/8.2/applevel-consistency.html "PostgreSQL
8.2 - 13.4. Data Consistency Checks at the Application Level") /
[8.1](/docs/8.1/applevel-consistency.html "PostgreSQL 8.1 - 13.4. Data
Consistency Checks at the Application Level") / [8.0](/docs/8.0/applevel-
consistency.html "PostgreSQL 8.0 - 13.4. Data Consistency Checks at the
Application Level") / [7.4](/docs/7.4/applevel-consistency.html "PostgreSQL
7.4 - 13.4. Data Consistency Checks at the Application Level") /
[7.3](/docs/7.3/applevel-consistency.html "PostgreSQL 7.3 - 13.4. Data
Consistency Checks at the Application Level") / [7.2](/docs/7.2/applevel-
consistency.html "PostgreSQL 7.2 - 13.4. Data Consistency Checks at the
Application Level") / [7.1](/docs/7.1/applevel-consistency.html "PostgreSQL
7.1 - 13.4. Data Consistency Checks at the Application Level")

__

13.4. Data Consistency Checks at the Application Level  
---  
[Prev](explicit-locking.html "13.3. Explicit Locking")  | [Up](mvcc.html "Chapter 13. Concurrency Control") | Chapter 13. Concurrency Control | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](mvcc-serialization-failure-handling.html "13.5. Serialization Failure Handling")  
  
* * *

## 13.4. Data Consistency Checks at the Application Level #

[13.4.1. Enforcing Consistency with Serializable Transactions](applevel-
consistency.html#SERIALIZABLE-CONSISTENCY)

[13.4.2. Enforcing Consistency with Explicit Blocking Locks](applevel-
consistency.html#NON-SERIALIZABLE-CONSISTENCY)

It is very difficult to enforce business rules regarding data integrity using
Read Committed transactions because the view of the data is shifting with each
statement, and even a single statement may not restrict itself to the
statement's snapshot if a write conflict occurs.

While a Repeatable Read transaction has a stable view of the data throughout
its execution, there is a subtle issue with using MVCC snapshots for data
consistency checks, involving something known as _read/write conflicts_. If
one transaction writes data and a concurrent transaction attempts to read the
same data (whether before or after the write), it cannot see the work of the
other transaction. The reader then appears to have executed first regardless
of which started first or which committed first. If that is as far as it goes,
there is no problem, but if the reader also writes data which is read by a
concurrent transaction there is now a transaction which appears to have run
before either of the previously mentioned transactions. If the transaction
which appears to have executed last actually commits first, it is very easy
for a cycle to appear in a graph of the order of execution of the
transactions. When such a cycle appears, integrity checks will not work
correctly without some help.

As mentioned in [Section 13.2.3](transaction-iso.html#XACT-SERIALIZABLE
"13.2.3. Serializable Isolation Level"), Serializable transactions are just
Repeatable Read transactions which add nonblocking monitoring for dangerous
patterns of read/write conflicts. When a pattern is detected which could cause
a cycle in the apparent order of execution, one of the transactions involved
is rolled back to break the cycle.

### 13.4.1. Enforcing Consistency with Serializable Transactions #

If the Serializable transaction isolation level is used for all writes and for
all reads which need a consistent view of the data, no other effort is
required to ensure consistency. Software from other environments which is
written to use serializable transactions to ensure consistency should “just
work” in this regard in PostgreSQL.

When using this technique, it will avoid creating an unnecessary burden for
application programmers if the application software goes through a framework
which automatically retries transactions which are rolled back with a
serialization failure. It may be a good idea to set
`default_transaction_isolation` to `serializable`. It would also be wise to
take some action to ensure that no other transaction isolation level is used,
either inadvertently or to subvert integrity checks, through checks of the
transaction isolation level in triggers.

See [Section 13.2.3](transaction-iso.html#XACT-SERIALIZABLE
"13.2.3. Serializable Isolation Level") for performance suggestions.

### Warning: Serializable Transactions and Data Replication

This level of integrity protection using Serializable transactions does not
yet extend to hot standby mode ([Section 27.4](hot-standby.html "27.4. Hot
Standby")) or logical replicas. Because of that, those using hot standby or
logical replication may want to use Repeatable Read and explicit locking on
the primary.

### 13.4.2. Enforcing Consistency with Explicit Blocking Locks #

When non-serializable writes are possible, to ensure the current validity of a
row and protect it against concurrent updates one must use `SELECT FOR
UPDATE`, `SELECT FOR SHARE`, or an appropriate `LOCK TABLE` statement.
(`SELECT FOR UPDATE` and `SELECT FOR SHARE` lock just the returned rows
against concurrent updates, while `LOCK TABLE` locks the whole table.) This
should be taken into account when porting applications to PostgreSQL from
other environments.

Also of note to those converting from other environments is the fact that
`SELECT FOR UPDATE` does not ensure that a concurrent transaction will not
update or delete a selected row. To do that in PostgreSQL you must actually
update the row, even if no values need to be changed. `SELECT FOR UPDATE`
_temporarily blocks_ other transactions from acquiring the same lock or
executing an `UPDATE` or `DELETE` which would affect the locked row, but once
the transaction holding this lock commits or rolls back, a blocked transaction
will proceed with the conflicting operation unless an actual `UPDATE` of the
row was performed while the lock was held.

Global validity checks require extra thought under non-serializable MVCC. For
example, a banking application might wish to check that the sum of all credits
in one table equals the sum of debits in another table, when both tables are
being actively updated. Comparing the results of two successive `SELECT
sum(...)` commands will not work reliably in Read Committed mode, since the
second query will likely include the results of transactions not counted by
the first. Doing the two sums in a single repeatable read transaction will
give an accurate picture of only the effects of transactions that committed
before the repeatable read transaction started — but one might legitimately
wonder whether the answer is still relevant by the time it is delivered. If
the repeatable read transaction itself applied some changes before trying to
make the consistency check, the usefulness of the check becomes even more
debatable, since now it includes some but not all post-transaction-start
changes. In such cases a careful person might wish to lock all tables needed
for the check, in order to get an indisputable picture of current reality. A
`SHARE` mode (or higher) lock guarantees that there are no uncommitted changes
in the locked table, other than those of the current transaction.

Note also that if one is relying on explicit locking to prevent concurrent
changes, one should either use Read Committed mode, or in Repeatable Read mode
be careful to obtain locks before performing queries. A lock obtained by a
repeatable read transaction guarantees that no other transactions modifying
the table are still running, but if the snapshot seen by the transaction
predates obtaining the lock, it might predate some now-committed changes in
the table. A repeatable read transaction's snapshot is actually frozen at the
start of its first query or data-modification command (`SELECT`, `INSERT`,
`UPDATE`, `DELETE`, or `MERGE`), so it is possible to obtain locks explicitly
before the snapshot is frozen.

* * *

[Prev](explicit-locking.html "13.3. Explicit Locking")  | [Up](mvcc.html "Chapter 13. Concurrency Control") |  [Next](mvcc-serialization-failure-handling.html "13.5. Serialization Failure Handling")  
---|---|---  
13.3. Explicit Locking  | [Home](index.html "PostgreSQL 16.9 Documentation") |  13.5. Serialization Failure Handling  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/applevel-consistency.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

