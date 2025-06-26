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

Supported Versions: [Current](/docs/current/mvcc-caveats.html "PostgreSQL 17 -
13.6. Caveats") ([17](/docs/17/mvcc-caveats.html "PostgreSQL 17 -
13.6. Caveats")) / [16](/docs/16/mvcc-caveats.html "PostgreSQL 16 -
13.6. Caveats") / [15](/docs/15/mvcc-caveats.html "PostgreSQL 15 -
13.6. Caveats") / [14](/docs/14/mvcc-caveats.html "PostgreSQL 14 -
13.6. Caveats") / [13](/docs/13/mvcc-caveats.html "PostgreSQL 13 -
13.6. Caveats")

Development Versions: [18](/docs/18/mvcc-caveats.html "PostgreSQL 18 -
13.6. Caveats") / [devel](/docs/devel/mvcc-caveats.html "PostgreSQL devel -
13.6. Caveats")

Unsupported versions: [12](/docs/12/mvcc-caveats.html "PostgreSQL 12 -
13.6. Caveats") / [11](/docs/11/mvcc-caveats.html "PostgreSQL 11 -
13.6. Caveats") / [10](/docs/10/mvcc-caveats.html "PostgreSQL 10 -
13.6. Caveats") / [9.6](/docs/9.6/mvcc-caveats.html "PostgreSQL 9.6 -
13.6. Caveats") / [9.5](/docs/9.5/mvcc-caveats.html "PostgreSQL 9.5 -
13.6. Caveats") / [9.4](/docs/9.4/mvcc-caveats.html "PostgreSQL 9.4 -
13.6. Caveats") / [9.3](/docs/9.3/mvcc-caveats.html "PostgreSQL 9.3 -
13.6. Caveats") / [9.2](/docs/9.2/mvcc-caveats.html "PostgreSQL 9.2 -
13.6. Caveats") / [9.1](/docs/9.1/mvcc-caveats.html "PostgreSQL 9.1 -
13.6. Caveats") / [9.0](/docs/9.0/mvcc-caveats.html "PostgreSQL 9.0 -
13.6. Caveats")

__

13.6. Caveats  
---  
[Prev](mvcc-serialization-failure-handling.html "13.5. Serialization Failure Handling")  | [Up](mvcc.html "Chapter 13. Concurrency Control") | Chapter 13. Concurrency Control | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](locking-indexes.html "13.7. Locking and Indexes")  
  
* * *

## 13.6. Caveats #

Some DDL commands, currently only [`TRUNCATE`](sql-truncate.html "TRUNCATE")
and the table-rewriting forms of [`ALTER TABLE`](sql-altertable.html "ALTER
TABLE"), are not MVCC-safe. This means that after the truncation or rewrite
commits, the table will appear empty to concurrent transactions, if they are
using a snapshot taken before the DDL command committed. This will only be an
issue for a transaction that did not access the table in question before the
DDL command started — any transaction that has done so would hold at least an
`ACCESS SHARE` table lock, which would block the DDL command until that
transaction completes. So these commands will not cause any apparent
inconsistency in the table contents for successive queries on the target
table, but they could cause visible inconsistency between the contents of the
target table and other tables in the database.

Support for the Serializable transaction isolation level has not yet been
added to hot standby replication targets (described in [Section 27.4](hot-
standby.html "27.4. Hot Standby")). The strictest isolation level currently
supported in hot standby mode is Repeatable Read. While performing all
permanent database writes within Serializable transactions on the primary will
ensure that all standbys will eventually reach a consistent state, a
Repeatable Read transaction run on the standby can sometimes see a transient
state that is inconsistent with any serial execution of the transactions on
the primary.

Internal access to the system catalogs is not done using the isolation level
of the current transaction. This means that newly created database objects
such as tables are visible to concurrent Repeatable Read and Serializable
transactions, even though the rows they contain are not. In contrast, queries
that explicitly examine the system catalogs don't see rows representing
concurrently created database objects, in the higher isolation levels.

* * *

[Prev](mvcc-serialization-failure-handling.html "13.5. Serialization Failure Handling")  | [Up](mvcc.html "Chapter 13. Concurrency Control") |  [Next](locking-indexes.html "13.7. Locking and Indexes")  
---|---|---  
13.5. Serialization Failure Handling  | [Home](index.html "PostgreSQL 16.9 Documentation") |  13.7. Locking and Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/mvcc-caveats.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

