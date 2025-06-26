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

Supported Versions: [Current](/docs/current/logicaldecoding-sql.html
"PostgreSQL 17 - 49.4. Logical Decoding SQL Interface")
([17](/docs/17/logicaldecoding-sql.html "PostgreSQL 17 - 49.4. Logical
Decoding SQL Interface")) / [16](/docs/16/logicaldecoding-sql.html "PostgreSQL
16 - 49.4. Logical Decoding SQL Interface") / [15](/docs/15/logicaldecoding-
sql.html "PostgreSQL 15 - 49.4. Logical Decoding SQL Interface") /
[14](/docs/14/logicaldecoding-sql.html "PostgreSQL 14 - 49.4. Logical Decoding
SQL Interface") / [13](/docs/13/logicaldecoding-sql.html "PostgreSQL 13 -
49.4. Logical Decoding SQL Interface")

Development Versions: [18](/docs/18/logicaldecoding-sql.html "PostgreSQL 18 -
49.4. Logical Decoding SQL Interface") / [devel](/docs/devel/logicaldecoding-
sql.html "PostgreSQL devel - 49.4. Logical Decoding SQL Interface")

Unsupported versions: [12](/docs/12/logicaldecoding-sql.html "PostgreSQL 12 -
49.4. Logical Decoding SQL Interface") / [11](/docs/11/logicaldecoding-
sql.html "PostgreSQL 11 - 49.4. Logical Decoding SQL Interface") /
[10](/docs/10/logicaldecoding-sql.html "PostgreSQL 10 - 49.4. Logical Decoding
SQL Interface") / [9.6](/docs/9.6/logicaldecoding-sql.html "PostgreSQL 9.6 -
49.4. Logical Decoding SQL Interface") / [9.5](/docs/9.5/logicaldecoding-
sql.html "PostgreSQL 9.5 - 49.4. Logical Decoding SQL Interface") /
[9.4](/docs/9.4/logicaldecoding-sql.html "PostgreSQL 9.4 - 49.4. Logical
Decoding SQL Interface")

__

49.4. Logical Decoding SQL Interface  
---  
[Prev](logicaldecoding-walsender.html "49.3. Streaming Replication Protocol Interface")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-catalogs.html "49.5. System Catalogs Related to Logical Decoding")  
  
* * *

## 49.4. Logical Decoding SQL Interface #

See [Section 9.27.6](functions-admin.html#FUNCTIONS-REPLICATION
"9.27.6. Replication Management Functions") for detailed documentation on the
SQL-level API for interacting with logical decoding.

Synchronous replication (see [Section 27.2.8](warm-standby.html#SYNCHRONOUS-
REPLICATION "27.2.8. Synchronous Replication")) is only supported on
replication slots used over the streaming replication interface. The function
interface and additional, non-core interfaces do not support synchronous
replication.

* * *

[Prev](logicaldecoding-walsender.html "49.3. Streaming Replication Protocol Interface")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-catalogs.html "49.5. System Catalogs Related to Logical Decoding")  
---|---|---  
49.3. Streaming Replication Protocol Interface  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.5. System Catalogs Related to Logical Decoding  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-sql.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

