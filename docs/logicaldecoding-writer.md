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

Supported Versions: [Current](/docs/current/logicaldecoding-writer.html
"PostgreSQL 17 - 49.7. Logical Decoding Output Writers")
([17](/docs/17/logicaldecoding-writer.html "PostgreSQL 17 - 49.7. Logical
Decoding Output Writers")) / [16](/docs/16/logicaldecoding-writer.html
"PostgreSQL 16 - 49.7. Logical Decoding Output Writers") /
[15](/docs/15/logicaldecoding-writer.html "PostgreSQL 15 - 49.7. Logical
Decoding Output Writers") / [14](/docs/14/logicaldecoding-writer.html
"PostgreSQL 14 - 49.7. Logical Decoding Output Writers") /
[13](/docs/13/logicaldecoding-writer.html "PostgreSQL 13 - 49.7. Logical
Decoding Output Writers")

Development Versions: [18](/docs/18/logicaldecoding-writer.html "PostgreSQL 18
- 49.7. Logical Decoding Output Writers") /
[devel](/docs/devel/logicaldecoding-writer.html "PostgreSQL devel -
49.7. Logical Decoding Output Writers")

Unsupported versions: [12](/docs/12/logicaldecoding-writer.html "PostgreSQL 12
- 49.7. Logical Decoding Output Writers") / [11](/docs/11/logicaldecoding-
writer.html "PostgreSQL 11 - 49.7. Logical Decoding Output Writers") /
[10](/docs/10/logicaldecoding-writer.html "PostgreSQL 10 - 49.7. Logical
Decoding Output Writers") / [9.6](/docs/9.6/logicaldecoding-writer.html
"PostgreSQL 9.6 - 49.7. Logical Decoding Output Writers") /
[9.5](/docs/9.5/logicaldecoding-writer.html "PostgreSQL 9.5 - 49.7. Logical
Decoding Output Writers") / [9.4](/docs/9.4/logicaldecoding-writer.html
"PostgreSQL 9.4 - 49.7. Logical Decoding Output Writers")

__

49.7. Logical Decoding Output Writers  
---  
[Prev](logicaldecoding-output-plugin.html "49.6. Logical Decoding Output Plugins")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-synchronous.html "49.8. Synchronous Replication Support for Logical Decoding")  
  
* * *

## 49.7. Logical Decoding Output Writers #

It is possible to add more output methods for logical decoding. For details,
see `src/backend/replication/logical/logicalfuncs.c`. Essentially, three
functions need to be provided: one to read WAL, one to prepare writing output,
and one to write the output (see [Section 49.6.5](logicaldecoding-output-
plugin.html#LOGICALDECODING-OUTPUT-PLUGIN-OUTPUT "49.6.5. Functions for
Producing Output")).

* * *

[Prev](logicaldecoding-output-plugin.html "49.6. Logical Decoding Output Plugins")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-synchronous.html "49.8. Synchronous Replication Support for Logical Decoding")  
---|---|---  
49.6. Logical Decoding Output Plugins  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.8. Synchronous Replication Support for Logical Decoding  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-writer.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

