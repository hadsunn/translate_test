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

Supported Versions: [Current](/docs/current/sql-load.html "PostgreSQL 17 -
LOAD") ([17](/docs/17/sql-load.html "PostgreSQL 17 - LOAD")) /
[16](/docs/16/sql-load.html "PostgreSQL 16 - LOAD") / [15](/docs/15/sql-
load.html "PostgreSQL 15 - LOAD") / [14](/docs/14/sql-load.html "PostgreSQL 14
- LOAD") / [13](/docs/13/sql-load.html "PostgreSQL 13 - LOAD")

Development Versions: [18](/docs/18/sql-load.html "PostgreSQL 18 - LOAD") /
[devel](/docs/devel/sql-load.html "PostgreSQL devel - LOAD")

Unsupported versions: [12](/docs/12/sql-load.html "PostgreSQL 12 - LOAD") /
[11](/docs/11/sql-load.html "PostgreSQL 11 - LOAD") / [10](/docs/10/sql-
load.html "PostgreSQL 10 - LOAD") / [9.6](/docs/9.6/sql-load.html "PostgreSQL
9.6 - LOAD") / [9.5](/docs/9.5/sql-load.html "PostgreSQL 9.5 - LOAD") /
[9.4](/docs/9.4/sql-load.html "PostgreSQL 9.4 - LOAD") / [9.3](/docs/9.3/sql-
load.html "PostgreSQL 9.3 - LOAD") / [9.2](/docs/9.2/sql-load.html "PostgreSQL
9.2 - LOAD") / [9.1](/docs/9.1/sql-load.html "PostgreSQL 9.1 - LOAD") /
[9.0](/docs/9.0/sql-load.html "PostgreSQL 9.0 - LOAD") / [8.4](/docs/8.4/sql-
load.html "PostgreSQL 8.4 - LOAD") / [8.3](/docs/8.3/sql-load.html "PostgreSQL
8.3 - LOAD") / [8.2](/docs/8.2/sql-load.html "PostgreSQL 8.2 - LOAD") /
[8.1](/docs/8.1/sql-load.html "PostgreSQL 8.1 - LOAD") / [8.0](/docs/8.0/sql-
load.html "PostgreSQL 8.0 - LOAD") / [7.4](/docs/7.4/sql-load.html "PostgreSQL
7.4 - LOAD") / [7.3](/docs/7.3/sql-load.html "PostgreSQL 7.3 - LOAD") /
[7.2](/docs/7.2/sql-load.html "PostgreSQL 7.2 - LOAD") / [7.1](/docs/7.1/sql-
load.html "PostgreSQL 7.1 - LOAD")

__

LOAD  
---  
[Prev](sql-listen.html "LISTEN")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-lock.html "LOCK")  
  
* * *

## LOAD

LOAD — load a shared library file

## Synopsis

    
    
    LOAD '_filename_ '
    

## Description

This command loads a shared library file into the PostgreSQL server's address
space. If the file has been loaded already, the command does nothing. Shared
library files that contain C functions are automatically loaded whenever one
of their functions is called. Therefore, an explicit `LOAD` is usually only
needed to load a library that modifies the server's behavior through “hooks”
rather than providing a set of functions.

The library file name is typically given as just a bare file name, which is
sought in the server's library search path (set by
[dynamic_library_path](runtime-config-client.html#GUC-DYNAMIC-LIBRARY-PATH)).
Alternatively it can be given as a full path name. In either case the
platform's standard shared library file name extension may be omitted. See
[Section 38.10.1](xfunc-c.html#XFUNC-C-DYNLOAD "38.10.1. Dynamic Loading") for
more information on this topic.

Non-superusers can only apply `LOAD` to library files located in
`$libdir/plugins/` — the specified _`filename`_ must begin with exactly that
string. (It is the database administrator's responsibility to ensure that only
“safe” libraries are installed there.)

## Compatibility

`LOAD` is a PostgreSQL extension.

## See Also

[CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION")

* * *

[Prev](sql-listen.html "LISTEN")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-lock.html "LOCK")  
---|---|---  
LISTEN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  LOCK  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-load.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

