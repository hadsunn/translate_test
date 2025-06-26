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

Supported Versions: [Current](/docs/current/logicaldecoding-walsender.html
"PostgreSQL 17 - 49.3. Streaming Replication Protocol Interface")
([17](/docs/17/logicaldecoding-walsender.html "PostgreSQL 17 - 49.3. Streaming
Replication Protocol Interface")) / [16](/docs/16/logicaldecoding-
walsender.html "PostgreSQL 16 - 49.3. Streaming Replication Protocol
Interface") / [15](/docs/15/logicaldecoding-walsender.html "PostgreSQL 15 -
49.3. Streaming Replication Protocol Interface") /
[14](/docs/14/logicaldecoding-walsender.html "PostgreSQL 14 - 49.3. Streaming
Replication Protocol Interface") / [13](/docs/13/logicaldecoding-
walsender.html "PostgreSQL 13 - 49.3. Streaming Replication Protocol
Interface")

Development Versions: [18](/docs/18/logicaldecoding-walsender.html "PostgreSQL
18 - 49.3. Streaming Replication Protocol Interface") /
[devel](/docs/devel/logicaldecoding-walsender.html "PostgreSQL devel -
49.3. Streaming Replication Protocol Interface")

Unsupported versions: [12](/docs/12/logicaldecoding-walsender.html "PostgreSQL
12 - 49.3. Streaming Replication Protocol Interface") /
[11](/docs/11/logicaldecoding-walsender.html "PostgreSQL 11 - 49.3. Streaming
Replication Protocol Interface") / [10](/docs/10/logicaldecoding-
walsender.html "PostgreSQL 10 - 49.3. Streaming Replication Protocol
Interface") / [9.6](/docs/9.6/logicaldecoding-walsender.html "PostgreSQL 9.6 -
49.3. Streaming Replication Protocol Interface") /
[9.5](/docs/9.5/logicaldecoding-walsender.html "PostgreSQL 9.5 -
49.3. Streaming Replication Protocol Interface") /
[9.4](/docs/9.4/logicaldecoding-walsender.html "PostgreSQL 9.4 -
49.3. Streaming Replication Protocol Interface")

__

49.3. Streaming Replication Protocol Interface  
---  
[Prev](logicaldecoding-explanation.html "49.2. Logical Decoding Concepts")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-sql.html "49.4. Logical Decoding SQL Interface")  
  
* * *

## 49.3. Streaming Replication Protocol Interface #

The commands

  * `CREATE_REPLICATION_SLOT _`slot_name`_ LOGICAL _`output_plugin`_`

  * `DROP_REPLICATION_SLOT _`slot_name`_` [ `WAIT` ]

  * `START_REPLICATION SLOT _`slot_name`_ LOGICAL ...`

are used to create, drop, and stream changes from a replication slot,
respectively. These commands are only available over a replication connection;
they cannot be used via SQL. See [Section 55.4](protocol-replication.html
"55.4. Streaming Replication Protocol") for details on these commands.

The command [pg_recvlogical](app-pgrecvlogical.html "pg_recvlogical") can be
used to control logical decoding over a streaming replication connection. (It
uses these commands internally.)

* * *

[Prev](logicaldecoding-explanation.html "49.2. Logical Decoding Concepts")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-sql.html "49.4. Logical Decoding SQL Interface")  
---|---|---  
49.2. Logical Decoding Concepts  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.4. Logical Decoding SQL Interface  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-
walsender.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

