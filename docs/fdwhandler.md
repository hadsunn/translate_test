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

Supported Versions: [Current](/docs/current/fdwhandler.html "PostgreSQL 17 -
Chapter 59. Writing a Foreign Data Wrapper") ([17](/docs/17/fdwhandler.html
"PostgreSQL 17 - Chapter 59. Writing a Foreign Data Wrapper")) /
[16](/docs/16/fdwhandler.html "PostgreSQL 16 - Chapter 59. Writing a Foreign
Data Wrapper") / [15](/docs/15/fdwhandler.html "PostgreSQL 15 -
Chapter 59. Writing a Foreign Data Wrapper") / [14](/docs/14/fdwhandler.html
"PostgreSQL 14 - Chapter 59. Writing a Foreign Data Wrapper") /
[13](/docs/13/fdwhandler.html "PostgreSQL 13 - Chapter 59. Writing a Foreign
Data Wrapper")

Development Versions: [18](/docs/18/fdwhandler.html "PostgreSQL 18 -
Chapter 59. Writing a Foreign Data Wrapper") /
[devel](/docs/devel/fdwhandler.html "PostgreSQL devel - Chapter 59. Writing a
Foreign Data Wrapper")

Unsupported versions: [12](/docs/12/fdwhandler.html "PostgreSQL 12 -
Chapter 59. Writing a Foreign Data Wrapper") / [11](/docs/11/fdwhandler.html
"PostgreSQL 11 - Chapter 59. Writing a Foreign Data Wrapper") /
[10](/docs/10/fdwhandler.html "PostgreSQL 10 - Chapter 59. Writing a Foreign
Data Wrapper") / [9.6](/docs/9.6/fdwhandler.html "PostgreSQL 9.6 -
Chapter 59. Writing a Foreign Data Wrapper") / [9.5](/docs/9.5/fdwhandler.html
"PostgreSQL 9.5 - Chapter 59. Writing a Foreign Data Wrapper") /
[9.4](/docs/9.4/fdwhandler.html "PostgreSQL 9.4 - Chapter 59. Writing a
Foreign Data Wrapper") / [9.3](/docs/9.3/fdwhandler.html "PostgreSQL 9.3 -
Chapter 59. Writing a Foreign Data Wrapper") / [9.2](/docs/9.2/fdwhandler.html
"PostgreSQL 9.2 - Chapter 59. Writing a Foreign Data Wrapper") /
[9.1](/docs/9.1/fdwhandler.html "PostgreSQL 9.1 - Chapter 59. Writing a
Foreign Data Wrapper")

__

Chapter 59. Writing a Foreign Data Wrapper  
---  
[Prev](plhandler.html "Chapter 58. Writing a Procedural Language Handler")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](fdw-functions.html "59.1. Foreign Data Wrapper Functions")  
  
* * *

## Chapter 59. Writing a Foreign Data Wrapper

**Table of Contents**

[59.1. Foreign Data Wrapper Functions](fdw-functions.html)

[59.2. Foreign Data Wrapper Callback Routines](fdw-callbacks.html)

    

[59.2.1. FDW Routines for Scanning Foreign Tables](fdw-callbacks.html#FDW-
CALLBACKS-SCAN)

[59.2.2. FDW Routines for Scanning Foreign Joins](fdw-callbacks.html#FDW-
CALLBACKS-JOIN-SCAN)

[59.2.3. FDW Routines for Planning Post-Scan/Join Processing](fdw-
callbacks.html#FDW-CALLBACKS-UPPER-PLANNING)

[59.2.4. FDW Routines for Updating Foreign Tables](fdw-callbacks.html#FDW-
CALLBACKS-UPDATE)

[59.2.5. FDW Routines for `TRUNCATE`](fdw-callbacks.html#FDW-CALLBACKS-
TRUNCATE)

[59.2.6. FDW Routines for Row Locking](fdw-callbacks.html#FDW-CALLBACKS-ROW-
LOCKING)

[59.2.7. FDW Routines for `EXPLAIN`](fdw-callbacks.html#FDW-CALLBACKS-EXPLAIN)

[59.2.8. FDW Routines for `ANALYZE`](fdw-callbacks.html#FDW-CALLBACKS-ANALYZE)

[59.2.9. FDW Routines for `IMPORT FOREIGN SCHEMA`](fdw-callbacks.html#FDW-
CALLBACKS-IMPORT)

[59.2.10. FDW Routines for Parallel Execution](fdw-callbacks.html#FDW-
CALLBACKS-PARALLEL)

[59.2.11. FDW Routines for Asynchronous Execution](fdw-callbacks.html#FDW-
CALLBACKS-ASYNC)

[59.2.12. FDW Routines for Reparameterization of Paths](fdw-
callbacks.html#FDW-CALLBACKS-REPARAMETERIZE-PATHS)

[59.3. Foreign Data Wrapper Helper Functions](fdw-helpers.html)

[59.4. Foreign Data Wrapper Query Planning](fdw-planning.html)

[59.5. Row Locking in Foreign Data Wrappers](fdw-row-locking.html)

All operations on a foreign table are handled through its foreign data
wrapper, which consists of a set of functions that the core server calls. The
foreign data wrapper is responsible for fetching data from the remote data
source and returning it to the PostgreSQL executor. If updating foreign tables
is to be supported, the wrapper must handle that, too. This chapter outlines
how to write a new foreign data wrapper.

The foreign data wrappers included in the standard distribution are good
references when trying to write your own. Look into the `contrib` subdirectory
of the source tree. The [CREATE FOREIGN DATA WRAPPER](sql-
createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER") reference page
also has some useful details.

### Note

The SQL standard specifies an interface for writing foreign data wrappers.
However, PostgreSQL does not implement that API, because the effort to
accommodate it into PostgreSQL would be large, and the standard API hasn't
gained wide adoption anyway.

* * *

[Prev](plhandler.html "Chapter 58. Writing a Procedural Language Handler")  | [Up](internals.html "Part VII. Internals") |  [Next](fdw-functions.html "59.1. Foreign Data Wrapper Functions")  
---|---|---  
Chapter 58. Writing a Procedural Language Handler  | [Home](index.html "PostgreSQL 16.9 Documentation") |  59.1. Foreign Data Wrapper Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/fdwhandler.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

