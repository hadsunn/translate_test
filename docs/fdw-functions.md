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

Supported Versions: [Current](/docs/current/fdw-functions.html "PostgreSQL 17
- 59.1. Foreign Data Wrapper Functions") ([17](/docs/17/fdw-functions.html
"PostgreSQL 17 - 59.1. Foreign Data Wrapper Functions")) / [16](/docs/16/fdw-
functions.html "PostgreSQL 16 - 59.1. Foreign Data Wrapper Functions") /
[15](/docs/15/fdw-functions.html "PostgreSQL 15 - 59.1. Foreign Data Wrapper
Functions") / [14](/docs/14/fdw-functions.html "PostgreSQL 14 - 59.1. Foreign
Data Wrapper Functions") / [13](/docs/13/fdw-functions.html "PostgreSQL 13 -
59.1. Foreign Data Wrapper Functions")

Development Versions: [18](/docs/18/fdw-functions.html "PostgreSQL 18 -
59.1. Foreign Data Wrapper Functions") / [devel](/docs/devel/fdw-
functions.html "PostgreSQL devel - 59.1. Foreign Data Wrapper Functions")

Unsupported versions: [12](/docs/12/fdw-functions.html "PostgreSQL 12 -
59.1. Foreign Data Wrapper Functions") / [11](/docs/11/fdw-functions.html
"PostgreSQL 11 - 59.1. Foreign Data Wrapper Functions") / [10](/docs/10/fdw-
functions.html "PostgreSQL 10 - 59.1. Foreign Data Wrapper Functions") /
[9.6](/docs/9.6/fdw-functions.html "PostgreSQL 9.6 - 59.1. Foreign Data
Wrapper Functions") / [9.5](/docs/9.5/fdw-functions.html "PostgreSQL 9.5 -
59.1. Foreign Data Wrapper Functions") / [9.4](/docs/9.4/fdw-functions.html
"PostgreSQL 9.4 - 59.1. Foreign Data Wrapper Functions") /
[9.3](/docs/9.3/fdw-functions.html "PostgreSQL 9.3 - 59.1. Foreign Data
Wrapper Functions") / [9.2](/docs/9.2/fdw-functions.html "PostgreSQL 9.2 -
59.1. Foreign Data Wrapper Functions") / [9.1](/docs/9.1/fdw-functions.html
"PostgreSQL 9.1 - 59.1. Foreign Data Wrapper Functions")

__

59.1. Foreign Data Wrapper Functions  
---  
[Prev](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") | Chapter 59. Writing a Foreign Data Wrapper | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](fdw-callbacks.html "59.2. Foreign Data Wrapper Callback Routines")  
  
* * *

## 59.1. Foreign Data Wrapper Functions #

The FDW author needs to implement a handler function, and optionally a
validator function. Both functions must be written in a compiled language such
as C, using the version-1 interface. For details on C language calling
conventions and dynamic loading, see [Section 38.10](xfunc-c.html
"38.10. C-Language Functions").

The handler function simply returns a struct of function pointers to callback
functions that will be called by the planner, executor, and various
maintenance commands. Most of the effort in writing an FDW is in implementing
these callback functions. The handler function must be registered with
PostgreSQL as taking no arguments and returning the special pseudo-type
`fdw_handler`. The callback functions are plain C functions and are not
visible or callable at the SQL level. The callback functions are described in
[Section 59.2](fdw-callbacks.html "59.2. Foreign Data Wrapper Callback
Routines").

The validator function is responsible for validating options given in `CREATE`
and `ALTER` commands for its foreign data wrapper, as well as foreign servers,
user mappings, and foreign tables using the wrapper. The validator function
must be registered as taking two arguments, a text array containing the
options to be validated, and an OID representing the type of object the
options are associated with. The latter corresponds to the OID of the system
catalog the object would be stored in, one of:

  * `AttributeRelationId`

  * `ForeignDataWrapperRelationId`

  * `ForeignServerRelationId`

  * `ForeignTableRelationId`

  * `UserMappingRelationId`

If no validator function is supplied, options are not checked at object
creation time or object alteration time.

* * *

[Prev](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") |  [Next](fdw-callbacks.html "59.2. Foreign Data Wrapper Callback Routines")  
---|---|---  
Chapter 59. Writing a Foreign Data Wrapper  | [Home](index.html "PostgreSQL 16.9 Documentation") |  59.2. Foreign Data Wrapper Callback Routines  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/fdw-functions.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

