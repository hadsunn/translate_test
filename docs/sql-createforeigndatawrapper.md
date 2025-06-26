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

Supported Versions: [Current](/docs/current/sql-createforeigndatawrapper.html
"PostgreSQL 17 - CREATE FOREIGN DATA WRAPPER") ([17](/docs/17/sql-
createforeigndatawrapper.html "PostgreSQL 17 - CREATE FOREIGN DATA WRAPPER"))
/ [16](/docs/16/sql-createforeigndatawrapper.html "PostgreSQL 16 - CREATE
FOREIGN DATA WRAPPER") / [15](/docs/15/sql-createforeigndatawrapper.html
"PostgreSQL 15 - CREATE FOREIGN DATA WRAPPER") / [14](/docs/14/sql-
createforeigndatawrapper.html "PostgreSQL 14 - CREATE FOREIGN DATA WRAPPER") /
[13](/docs/13/sql-createforeigndatawrapper.html "PostgreSQL 13 - CREATE
FOREIGN DATA WRAPPER")

Development Versions: [18](/docs/18/sql-createforeigndatawrapper.html
"PostgreSQL 18 - CREATE FOREIGN DATA WRAPPER") / [devel](/docs/devel/sql-
createforeigndatawrapper.html "PostgreSQL devel - CREATE FOREIGN DATA
WRAPPER")

Unsupported versions: [12](/docs/12/sql-createforeigndatawrapper.html
"PostgreSQL 12 - CREATE FOREIGN DATA WRAPPER") / [11](/docs/11/sql-
createforeigndatawrapper.html "PostgreSQL 11 - CREATE FOREIGN DATA WRAPPER") /
[10](/docs/10/sql-createforeigndatawrapper.html "PostgreSQL 10 - CREATE
FOREIGN DATA WRAPPER") / [9.6](/docs/9.6/sql-createforeigndatawrapper.html
"PostgreSQL 9.6 - CREATE FOREIGN DATA WRAPPER") / [9.5](/docs/9.5/sql-
createforeigndatawrapper.html "PostgreSQL 9.5 - CREATE FOREIGN DATA WRAPPER")
/ [9.4](/docs/9.4/sql-createforeigndatawrapper.html "PostgreSQL 9.4 - CREATE
FOREIGN DATA WRAPPER") / [9.3](/docs/9.3/sql-createforeigndatawrapper.html
"PostgreSQL 9.3 - CREATE FOREIGN DATA WRAPPER") / [9.2](/docs/9.2/sql-
createforeigndatawrapper.html "PostgreSQL 9.2 - CREATE FOREIGN DATA WRAPPER")
/ [9.1](/docs/9.1/sql-createforeigndatawrapper.html "PostgreSQL 9.1 - CREATE
FOREIGN DATA WRAPPER") / [9.0](/docs/9.0/sql-createforeigndatawrapper.html
"PostgreSQL 9.0 - CREATE FOREIGN DATA WRAPPER") / [8.4](/docs/8.4/sql-
createforeigndatawrapper.html "PostgreSQL 8.4 - CREATE FOREIGN DATA WRAPPER")

__

CREATE FOREIGN DATA WRAPPER  
---  
[Prev](sql-createextension.html "CREATE EXTENSION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createforeigntable.html "CREATE FOREIGN TABLE")  
  
* * *

## CREATE FOREIGN DATA WRAPPER

CREATE FOREIGN DATA WRAPPER — define a new foreign-data wrapper

## Synopsis

    
    
    CREATE FOREIGN DATA WRAPPER _name_
        [ HANDLER _handler_function_ | NO HANDLER ]
        [ VALIDATOR _validator_function_ | NO VALIDATOR ]
        [ OPTIONS ( _option_ '_value_ ' [, ... ] ) ]
    

## Description

`CREATE FOREIGN DATA WRAPPER` creates a new foreign-data wrapper. The user who
defines a foreign-data wrapper becomes its owner.

The foreign-data wrapper name must be unique within the database.

Only superusers can create foreign-data wrappers.

## Parameters

_`name`_

    

The name of the foreign-data wrapper to be created.

`HANDLER _`handler_function`_`

    

_`handler_function`_ is the name of a previously registered function that will
be called to retrieve the execution functions for foreign tables. The handler
function must take no arguments, and its return type must be `fdw_handler`.

It is possible to create a foreign-data wrapper with no handler function, but
foreign tables using such a wrapper can only be declared, not accessed.

`VALIDATOR _`validator_function`_`

    

_`validator_function`_ is the name of a previously registered function that
will be called to check the generic options given to the foreign-data wrapper,
as well as options for foreign servers, user mappings and foreign tables using
the foreign-data wrapper. If no validator function or `NO VALIDATOR` is
specified, then options will not be checked at creation time. (Foreign-data
wrappers will possibly ignore or reject invalid option specifications at run
time, depending on the implementation.) The validator function must take two
arguments: one of type `text[]`, which will contain the array of options as
stored in the system catalogs, and one of type `oid`, which will be the OID of
the system catalog containing the options. The return type is ignored; the
function should report invalid options using the `ereport(ERROR)` function.

`OPTIONS ( _`option`_ '_`value`_ ' [, ... ] )`

    

This clause specifies options for the new foreign-data wrapper. The allowed
option names and values are specific to each foreign data wrapper and are
validated using the foreign-data wrapper's validator function. Option names
must be unique.

## Notes

PostgreSQL's foreign-data functionality is still under active development.
Optimization of queries is primitive (and mostly left to the wrapper, too).
Thus, there is considerable room for future performance improvements.

## Examples

Create a useless foreign-data wrapper `dummy`:

    
    
    CREATE FOREIGN DATA WRAPPER dummy;
    

Create a foreign-data wrapper `file` with handler function `file_fdw_handler`:

    
    
    CREATE FOREIGN DATA WRAPPER file HANDLER file_fdw_handler;
    

Create a foreign-data wrapper `mywrapper` with some options:

    
    
    CREATE FOREIGN DATA WRAPPER mywrapper
        OPTIONS (debug 'true');
    

## Compatibility

`CREATE FOREIGN DATA WRAPPER` conforms to ISO/IEC 9075-9 (SQL/MED), with the
exception that the `HANDLER` and `VALIDATOR` clauses are extensions and the
standard clauses `LIBRARY` and `LANGUAGE` are not implemented in PostgreSQL.

Note, however, that the SQL/MED functionality as a whole is not yet
conforming.

## See Also

[ALTER FOREIGN DATA WRAPPER](sql-alterforeigndatawrapper.html "ALTER FOREIGN
DATA WRAPPER"), [DROP FOREIGN DATA WRAPPER](sql-dropforeigndatawrapper.html
"DROP FOREIGN DATA WRAPPER"), [CREATE SERVER](sql-createserver.html "CREATE
SERVER"), [CREATE USER MAPPING](sql-createusermapping.html "CREATE USER
MAPPING"), [CREATE FOREIGN TABLE](sql-createforeigntable.html "CREATE FOREIGN
TABLE")

* * *

[Prev](sql-createextension.html "CREATE EXTENSION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createforeigntable.html "CREATE FOREIGN TABLE")  
---|---|---  
CREATE EXTENSION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE FOREIGN TABLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
createforeigndatawrapper.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

