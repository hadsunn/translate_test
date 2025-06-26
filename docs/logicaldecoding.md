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

Supported Versions: [Current](/docs/current/logicaldecoding.html "PostgreSQL
17 - Chapter 49. Logical Decoding") ([17](/docs/17/logicaldecoding.html
"PostgreSQL 17 - Chapter 49. Logical Decoding")) /
[16](/docs/16/logicaldecoding.html "PostgreSQL 16 - Chapter 49. Logical
Decoding") / [15](/docs/15/logicaldecoding.html "PostgreSQL 15 -
Chapter 49. Logical Decoding") / [14](/docs/14/logicaldecoding.html
"PostgreSQL 14 - Chapter 49. Logical Decoding") /
[13](/docs/13/logicaldecoding.html "PostgreSQL 13 - Chapter 49. Logical
Decoding")

Development Versions: [18](/docs/18/logicaldecoding.html "PostgreSQL 18 -
Chapter 49. Logical Decoding") / [devel](/docs/devel/logicaldecoding.html
"PostgreSQL devel - Chapter 49. Logical Decoding")

Unsupported versions: [12](/docs/12/logicaldecoding.html "PostgreSQL 12 -
Chapter 49. Logical Decoding") / [11](/docs/11/logicaldecoding.html
"PostgreSQL 11 - Chapter 49. Logical Decoding") /
[10](/docs/10/logicaldecoding.html "PostgreSQL 10 - Chapter 49. Logical
Decoding") / [9.6](/docs/9.6/logicaldecoding.html "PostgreSQL 9.6 -
Chapter 49. Logical Decoding") / [9.5](/docs/9.5/logicaldecoding.html
"PostgreSQL 9.5 - Chapter 49. Logical Decoding") /
[9.4](/docs/9.4/logicaldecoding.html "PostgreSQL 9.4 - Chapter 49. Logical
Decoding")

__

Chapter 49. Logical Decoding  
---  
[Prev](bgworker.html "Chapter 48. Background Worker Processes")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-example.html "49.1. Logical Decoding Examples")  
  
* * *

## Chapter 49. Logical Decoding

**Table of Contents**

[49.1. Logical Decoding Examples](logicaldecoding-example.html)

[49.2. Logical Decoding Concepts](logicaldecoding-explanation.html)

    

[49.2.1. Logical Decoding](logicaldecoding-explanation.html#LOGICALDECODING-
EXPLANATION-LOG-DEC)

[49.2.2. Replication Slots](logicaldecoding-explanation.html#LOGICALDECODING-
REPLICATION-SLOTS)

[49.2.3. Output Plugins](logicaldecoding-explanation.html#LOGICALDECODING-
EXPLANATION-OUTPUT-PLUGINS)

[49.2.4. Exported Snapshots](logicaldecoding-explanation.html#LOGICALDECODING-
EXPLANATION-EXPORTED-SNAPSHOTS)

[49.3. Streaming Replication Protocol Interface](logicaldecoding-
walsender.html)

[49.4. Logical Decoding SQL Interface](logicaldecoding-sql.html)

[49.5. System Catalogs Related to Logical Decoding](logicaldecoding-
catalogs.html)

[49.6. Logical Decoding Output Plugins](logicaldecoding-output-plugin.html)

    

[49.6.1. Initialization Function](logicaldecoding-output-
plugin.html#LOGICALDECODING-OUTPUT-INIT)

[49.6.2. Capabilities](logicaldecoding-output-plugin.html#LOGICALDECODING-
CAPABILITIES)

[49.6.3. Output Modes](logicaldecoding-output-plugin.html#LOGICALDECODING-
OUTPUT-MODE)

[49.6.4. Output Plugin Callbacks](logicaldecoding-output-
plugin.html#LOGICALDECODING-OUTPUT-PLUGIN-CALLBACKS)

[49.6.5. Functions for Producing Output](logicaldecoding-output-
plugin.html#LOGICALDECODING-OUTPUT-PLUGIN-OUTPUT)

[49.7. Logical Decoding Output Writers](logicaldecoding-writer.html)

[49.8. Synchronous Replication Support for Logical Decoding](logicaldecoding-
synchronous.html)

    

[49.8.1. Overview](logicaldecoding-synchronous.html#LOGICALDECODING-
SYNCHRONOUS-OVERVIEW)

[49.8.2. Caveats](logicaldecoding-synchronous.html#LOGICALDECODING-
SYNCHRONOUS-CAVEATS)

[49.9. Streaming of Large Transactions for Logical Decoding](logicaldecoding-
streaming.html)

[49.10. Two-phase Commit Support for Logical Decoding](logicaldecoding-two-
phase-commits.html)

PostgreSQL provides infrastructure to stream the modifications performed via
SQL to external consumers. This functionality can be used for a variety of
purposes, including replication solutions and auditing.

Changes are sent out in streams identified by logical replication slots.

The format in which those changes are streamed is determined by the output
plugin used. An example plugin is provided in the PostgreSQL distribution.
Additional plugins can be written to extend the choice of available formats
without modifying any core code. Every output plugin has access to each
individual new row produced by `INSERT` and the new row version created by
`UPDATE`. Availability of old row versions for `UPDATE` and `DELETE` depends
on the configured replica identity (see [`REPLICA IDENTITY`](sql-
altertable.html#SQL-ALTERTABLE-REPLICA-IDENTITY)).

Changes can be consumed either using the streaming replication protocol (see
[Section 55.4](protocol-replication.html "55.4. Streaming Replication
Protocol") and [Section 49.3](logicaldecoding-walsender.html "49.3. Streaming
Replication Protocol Interface")), or by calling functions via SQL (see
[Section 49.4](logicaldecoding-sql.html "49.4. Logical Decoding SQL
Interface")). It is also possible to write additional methods of consuming the
output of a replication slot without modifying core code (see [Section
49.7](logicaldecoding-writer.html "49.7. Logical Decoding Output Writers")).

* * *

[Prev](bgworker.html "Chapter 48. Background Worker Processes")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](logicaldecoding-example.html "49.1. Logical Decoding Examples")  
---|---|---  
Chapter 48. Background Worker Processes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.1. Logical Decoding Examples  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

