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

Supported Versions: [Current](/docs/current/logicaldecoding-synchronous.html
"PostgreSQL 17 - 49.8. Synchronous Replication Support for Logical Decoding")
([17](/docs/17/logicaldecoding-synchronous.html "PostgreSQL 17 -
49.8. Synchronous Replication Support for Logical Decoding")) /
[16](/docs/16/logicaldecoding-synchronous.html "PostgreSQL 16 -
49.8. Synchronous Replication Support for Logical Decoding") /
[15](/docs/15/logicaldecoding-synchronous.html "PostgreSQL 15 -
49.8. Synchronous Replication Support for Logical Decoding") /
[14](/docs/14/logicaldecoding-synchronous.html "PostgreSQL 14 -
49.8. Synchronous Replication Support for Logical Decoding") /
[13](/docs/13/logicaldecoding-synchronous.html "PostgreSQL 13 -
49.8. Synchronous Replication Support for Logical Decoding")

Development Versions: [18](/docs/18/logicaldecoding-synchronous.html
"PostgreSQL 18 - 49.8. Synchronous Replication Support for Logical Decoding")
/ [devel](/docs/devel/logicaldecoding-synchronous.html "PostgreSQL devel -
49.8. Synchronous Replication Support for Logical Decoding")

Unsupported versions: [12](/docs/12/logicaldecoding-synchronous.html
"PostgreSQL 12 - 49.8. Synchronous Replication Support for Logical Decoding")
/ [11](/docs/11/logicaldecoding-synchronous.html "PostgreSQL 11 -
49.8. Synchronous Replication Support for Logical Decoding") /
[10](/docs/10/logicaldecoding-synchronous.html "PostgreSQL 10 -
49.8. Synchronous Replication Support for Logical Decoding") /
[9.6](/docs/9.6/logicaldecoding-synchronous.html "PostgreSQL 9.6 -
49.8. Synchronous Replication Support for Logical Decoding") /
[9.5](/docs/9.5/logicaldecoding-synchronous.html "PostgreSQL 9.5 -
49.8. Synchronous Replication Support for Logical Decoding") /
[9.4](/docs/9.4/logicaldecoding-synchronous.html "PostgreSQL 9.4 -
49.8. Synchronous Replication Support for Logical Decoding")

__

49.8. Synchronous Replication Support for Logical Decoding  
---  
[Prev](logicaldecoding-writer.html "49.7. Logical Decoding Output Writers")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-streaming.html "49.9. Streaming of Large Transactions for Logical Decoding")  
  
* * *

## 49.8. Synchronous Replication Support for Logical Decoding #

[49.8.1. Overview](logicaldecoding-synchronous.html#LOGICALDECODING-
SYNCHRONOUS-OVERVIEW)

[49.8.2. Caveats](logicaldecoding-synchronous.html#LOGICALDECODING-
SYNCHRONOUS-CAVEATS)

### 49.8.1. Overview #

Logical decoding can be used to build [synchronous replication](warm-
standby.html#SYNCHRONOUS-REPLICATION "27.2.8. Synchronous Replication")
solutions with the same user interface as synchronous replication for
[streaming replication](warm-standby.html#STREAMING-REPLICATION
"27.2.5. Streaming Replication"). To do this, the streaming replication
interface (see [Section 49.3](logicaldecoding-walsender.html "49.3. Streaming
Replication Protocol Interface")) must be used to stream out data. Clients
have to send `Standby status update (F)` (see [Section 55.4](protocol-
replication.html "55.4. Streaming Replication Protocol")) messages, just like
streaming replication clients do.

### Note

A synchronous replica receiving changes via logical decoding will work in the
scope of a single database. Since, in contrast to that,
_`synchronous_standby_names`_ currently is server wide, this means this
technique will not work properly if more than one database is actively used.

### 49.8.2. Caveats #

In synchronous replication setup, a deadlock can happen, if the transaction
has locked [user] catalog tables exclusively. See [Section
49.6.2](logicaldecoding-output-plugin.html#LOGICALDECODING-CAPABILITIES
"49.6.2. Capabilities") for information on user catalog tables. This is
because logical decoding of transactions can lock catalog tables to access
them. To avoid this users must refrain from taking an exclusive lock on [user]
catalog tables. This can happen in the following ways:

  * Issuing an explicit `LOCK` on `pg_class` in a transaction.

  * Perform `CLUSTER` on `pg_class` in a transaction.

  * `PREPARE TRANSACTION` after `LOCK` command on `pg_class` and allow logical decoding of two-phase transactions.

  * `PREPARE TRANSACTION` after `CLUSTER` command on `pg_trigger` and allow logical decoding of two-phase transactions. This will lead to deadlock only when published table have a trigger.

  * Executing `TRUNCATE` on [user] catalog table in a transaction.

Note that these commands that can cause deadlock apply to not only explicitly
indicated system catalog tables above but also to any other [user] catalog
table.

* * *

[Prev](logicaldecoding-writer.html "49.7. Logical Decoding Output Writers")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-streaming.html "49.9. Streaming of Large Transactions for Logical Decoding")  
---|---|---  
49.7. Logical Decoding Output Writers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.9. Streaming of Large Transactions for Logical Decoding  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-
synchronous.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

