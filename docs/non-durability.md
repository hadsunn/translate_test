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

Supported Versions: [Current](/docs/current/non-durability.html "PostgreSQL 17
- 14.5. Non-Durable Settings") ([17](/docs/17/non-durability.html "PostgreSQL
17 - 14.5. Non-Durable Settings")) / [16](/docs/16/non-durability.html
"PostgreSQL 16 - 14.5. Non-Durable Settings") / [15](/docs/15/non-
durability.html "PostgreSQL 15 - 14.5. Non-Durable Settings") /
[14](/docs/14/non-durability.html "PostgreSQL 14 - 14.5. Non-Durable
Settings") / [13](/docs/13/non-durability.html "PostgreSQL 13 - 14.5. Non-
Durable Settings")

Development Versions: [18](/docs/18/non-durability.html "PostgreSQL 18 -
14.5. Non-Durable Settings") / [devel](/docs/devel/non-durability.html
"PostgreSQL devel - 14.5. Non-Durable Settings")

Unsupported versions: [12](/docs/12/non-durability.html "PostgreSQL 12 -
14.5. Non-Durable Settings") / [11](/docs/11/non-durability.html "PostgreSQL
11 - 14.5. Non-Durable Settings") / [10](/docs/10/non-durability.html
"PostgreSQL 10 - 14.5. Non-Durable Settings") / [9.6](/docs/9.6/non-
durability.html "PostgreSQL 9.6 - 14.5. Non-Durable Settings") /
[9.5](/docs/9.5/non-durability.html "PostgreSQL 9.5 - 14.5. Non-Durable
Settings") / [9.4](/docs/9.4/non-durability.html "PostgreSQL 9.4 - 14.5. Non-
Durable Settings") / [9.3](/docs/9.3/non-durability.html "PostgreSQL 9.3 -
14.5. Non-Durable Settings") / [9.2](/docs/9.2/non-durability.html "PostgreSQL
9.2 - 14.5. Non-Durable Settings") / [9.1](/docs/9.1/non-durability.html
"PostgreSQL 9.1 - 14.5. Non-Durable Settings") / [9.0](/docs/9.0/non-
durability.html "PostgreSQL 9.0 - 14.5. Non-Durable Settings")

__

14.5. Non-Durable Settings  
---  
[Prev](populate.html "14.4. Populating a Database")  | [Up](performance-tips.html "Chapter 14. Performance Tips") | Chapter 14. Performance Tips | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](parallel-query.html "Chapter 15. Parallel Query")  
  
* * *

## 14.5. Non-Durable Settings #

Durability is a database feature that guarantees the recording of committed
transactions even if the server crashes or loses power. However, durability
adds significant database overhead, so if your site does not require such a
guarantee, PostgreSQL can be configured to run much faster. The following are
configuration changes you can make to improve performance in such cases.
Except as noted below, durability is still guaranteed in case of a crash of
the database software; only an abrupt operating system crash creates a risk of
data loss or corruption when these settings are used.

  * Place the database cluster's data directory in a memory-backed file system (i.e., RAM disk). This eliminates all database disk I/O, but limits data storage to the amount of available memory (and perhaps swap).

  * Turn off [fsync](runtime-config-wal.html#GUC-FSYNC); there is no need to flush data to disk.

  * Turn off [synchronous_commit](runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT); there might be no need to force WAL writes to disk on every commit. This setting does risk transaction loss (though not data corruption) in case of a crash of the _database_.

  * Turn off [full_page_writes](runtime-config-wal.html#GUC-FULL-PAGE-WRITES); there is no need to guard against partial page writes.

  * Increase [max_wal_size](runtime-config-wal.html#GUC-MAX-WAL-SIZE) and [checkpoint_timeout](runtime-config-wal.html#GUC-CHECKPOINT-TIMEOUT); this reduces the frequency of checkpoints, but increases the storage requirements of `/pg_wal`.

  * Create [unlogged tables](sql-createtable.html#SQL-CREATETABLE-UNLOGGED) to avoid WAL writes, though it makes the tables non-crash-safe.

* * *

[Prev](populate.html "14.4. Populating a Database")  | [Up](performance-tips.html "Chapter 14. Performance Tips") |  [Next](parallel-query.html "Chapter 15. Parallel Query")  
---|---|---  
14.4. Populating a Database  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 15. Parallel Query  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/non-durability.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

