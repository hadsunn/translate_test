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

Supported Versions: [Current](/docs/current/ecpg-library.html "PostgreSQL 17 -
36.11. Library Functions") ([17](/docs/17/ecpg-library.html "PostgreSQL 17 -
36.11. Library Functions")) / [16](/docs/16/ecpg-library.html "PostgreSQL 16 -
36.11. Library Functions") / [15](/docs/15/ecpg-library.html "PostgreSQL 15 -
36.11. Library Functions") / [14](/docs/14/ecpg-library.html "PostgreSQL 14 -
36.11. Library Functions") / [13](/docs/13/ecpg-library.html "PostgreSQL 13 -
36.11. Library Functions")

Development Versions: [18](/docs/18/ecpg-library.html "PostgreSQL 18 -
36.11. Library Functions") / [devel](/docs/devel/ecpg-library.html "PostgreSQL
devel - 36.11. Library Functions")

Unsupported versions: [12](/docs/12/ecpg-library.html "PostgreSQL 12 -
36.11. Library Functions") / [11](/docs/11/ecpg-library.html "PostgreSQL 11 -
36.11. Library Functions") / [10](/docs/10/ecpg-library.html "PostgreSQL 10 -
36.11. Library Functions") / [9.6](/docs/9.6/ecpg-library.html "PostgreSQL 9.6
- 36.11. Library Functions") / [9.5](/docs/9.5/ecpg-library.html "PostgreSQL
9.5 - 36.11. Library Functions") / [9.4](/docs/9.4/ecpg-library.html
"PostgreSQL 9.4 - 36.11. Library Functions") / [9.3](/docs/9.3/ecpg-
library.html "PostgreSQL 9.3 - 36.11. Library Functions") /
[9.2](/docs/9.2/ecpg-library.html "PostgreSQL 9.2 - 36.11. Library Functions")
/ [9.1](/docs/9.1/ecpg-library.html "PostgreSQL 9.1 - 36.11. Library
Functions") / [9.0](/docs/9.0/ecpg-library.html "PostgreSQL 9.0 -
36.11. Library Functions") / [8.4](/docs/8.4/ecpg-library.html "PostgreSQL 8.4
- 36.11. Library Functions") / [8.3](/docs/8.3/ecpg-library.html "PostgreSQL
8.3 - 36.11. Library Functions") / [8.2](/docs/8.2/ecpg-library.html
"PostgreSQL 8.2 - 36.11. Library Functions") / [8.1](/docs/8.1/ecpg-
library.html "PostgreSQL 8.1 - 36.11. Library Functions") /
[8.0](/docs/8.0/ecpg-library.html "PostgreSQL 8.0 - 36.11. Library Functions")
/ [7.4](/docs/7.4/ecpg-library.html "PostgreSQL 7.4 - 36.11. Library
Functions") / [7.3](/docs/7.3/ecpg-library.html "PostgreSQL 7.3 -
36.11. Library Functions")

__

36.11. Library Functions  
---  
[Prev](ecpg-process.html "36.10. Processing Embedded SQL Programs")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-lo.html "36.12. Large Objects")  
  
* * *

## 36.11. Library Functions #

The `libecpg` library primarily contains “hidden” functions that are used to
implement the functionality expressed by the embedded SQL commands. But there
are some functions that can usefully be called directly. Note that this makes
your code unportable.

  * `ECPGdebug(int _`on`_ , FILE *_`stream`_)` turns on debug logging if called with the first argument non-zero. Debug logging is done on _`stream`_. The log contains all SQL statements with all the input variables inserted, and the results from the PostgreSQL server. This can be very useful when searching for errors in your SQL statements.

### Note

On Windows, if the ecpg libraries and an application are compiled with
different flags, this function call will crash the application because the
internal representation of the `FILE` pointers differ. Specifically,
multithreaded/single-threaded, release/debug, and static/dynamic flags should
be the same for the library and all applications using that library.

  * `ECPGget_PGconn(const char *_`connection_name`_)` returns the library database connection handle identified by the given name. If _`connection_name`_ is set to `NULL`, the current connection handle is returned. If no connection handle can be identified, the function returns `NULL`. The returned connection handle can be used to call any other functions from libpq, if necessary.

### Note

It is a bad idea to manipulate database connection handles made from ecpg
directly with libpq routines.

  * `ECPGtransactionStatus(const char *_`connection_name`_)` returns the current transaction status of the given connection identified by _`connection_name`_. See [Section 34.2](libpq-status.html "34.2. Connection Status Functions") and libpq's [`PQtransactionStatus`](libpq-status.html#LIBPQ-PQTRANSACTIONSTATUS) for details about the returned status codes.

  * `ECPGstatus(int _`lineno`_ , const char* _`connection_name`_)` returns true if you are connected to a database and false if not. _`connection_name`_ can be `NULL` if a single connection is being used.

* * *

[Prev](ecpg-process.html "36.10. Processing Embedded SQL Programs")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-lo.html "36.12. Large Objects")  
---|---|---  
36.10. Processing Embedded SQL Programs  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.12. Large Objects  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-library.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

