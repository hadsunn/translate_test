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

Supported Versions: [Current](/docs/current/sql-importforeignschema.html
"PostgreSQL 17 - IMPORT FOREIGN SCHEMA") ([17](/docs/17/sql-
importforeignschema.html "PostgreSQL 17 - IMPORT FOREIGN SCHEMA")) /
[16](/docs/16/sql-importforeignschema.html "PostgreSQL 16 - IMPORT FOREIGN
SCHEMA") / [15](/docs/15/sql-importforeignschema.html "PostgreSQL 15 - IMPORT
FOREIGN SCHEMA") / [14](/docs/14/sql-importforeignschema.html "PostgreSQL 14 -
IMPORT FOREIGN SCHEMA") / [13](/docs/13/sql-importforeignschema.html
"PostgreSQL 13 - IMPORT FOREIGN SCHEMA")

Development Versions: [18](/docs/18/sql-importforeignschema.html "PostgreSQL
18 - IMPORT FOREIGN SCHEMA") / [devel](/docs/devel/sql-
importforeignschema.html "PostgreSQL devel - IMPORT FOREIGN SCHEMA")

Unsupported versions: [12](/docs/12/sql-importforeignschema.html "PostgreSQL
12 - IMPORT FOREIGN SCHEMA") / [11](/docs/11/sql-importforeignschema.html
"PostgreSQL 11 - IMPORT FOREIGN SCHEMA") / [10](/docs/10/sql-
importforeignschema.html "PostgreSQL 10 - IMPORT FOREIGN SCHEMA") /
[9.6](/docs/9.6/sql-importforeignschema.html "PostgreSQL 9.6 - IMPORT FOREIGN
SCHEMA") / [9.5](/docs/9.5/sql-importforeignschema.html "PostgreSQL 9.5 -
IMPORT FOREIGN SCHEMA")

__

IMPORT FOREIGN SCHEMA  
---  
[Prev](sql-grant.html "GRANT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-insert.html "INSERT")  
  
* * *

## IMPORT FOREIGN SCHEMA

IMPORT FOREIGN SCHEMA — import table definitions from a foreign server

## Synopsis

    
    
    IMPORT FOREIGN SCHEMA _remote_schema_
        [ { LIMIT TO | EXCEPT } ( _table_name_ [, ...] ) ]
        FROM SERVER _server_name_
        INTO _local_schema_
        [ OPTIONS ( _option_ '_value_ ' [, ... ] ) ]
    

## Description

`IMPORT FOREIGN SCHEMA` creates foreign tables that represent tables existing
on a foreign server. The new foreign tables will be owned by the user issuing
the command and are created with the correct column definitions and options to
match the remote tables.

By default, all tables and views existing in a particular schema on the
foreign server are imported. Optionally, the list of tables can be limited to
a specified subset, or specific tables can be excluded. The new foreign tables
are all created in the target schema, which must already exist.

To use `IMPORT FOREIGN SCHEMA`, the user must have `USAGE` privilege on the
foreign server, as well as `CREATE` privilege on the target schema.

## Parameters

_`remote_schema`_

    

The remote schema to import from. The specific meaning of a remote schema
depends on the foreign data wrapper in use.

`LIMIT TO ( _`table_name`_ [, ...] )`

    

Import only foreign tables matching one of the given table names. Other tables
existing in the foreign schema will be ignored.

`EXCEPT ( _`table_name`_ [, ...] )`

    

Exclude specified foreign tables from the import. All tables existing in the
foreign schema will be imported except the ones listed here.

_`server_name`_

    

The foreign server to import from.

_`local_schema`_

    

The schema in which the imported foreign tables will be created.

`OPTIONS ( _`option`_ '_`value`_ ' [, ...] )`

    

Options to be used during the import. The allowed option names and values are
specific to each foreign data wrapper.

## Examples

Import table definitions from a remote schema `foreign_films` on server
`film_server`, creating the foreign tables in local schema `films`:

    
    
    IMPORT FOREIGN SCHEMA foreign_films
        FROM SERVER film_server INTO films;
    

As above, but import only the two tables `actors` and `directors` (if they
exist):

    
    
    IMPORT FOREIGN SCHEMA foreign_films LIMIT TO (actors, directors)
        FROM SERVER film_server INTO films;
    

## Compatibility

The `IMPORT FOREIGN SCHEMA` command conforms to the SQL standard, except that
the `OPTIONS` clause is a PostgreSQL extension.

## See Also

[CREATE FOREIGN TABLE](sql-createforeigntable.html "CREATE FOREIGN TABLE"),
[CREATE SERVER](sql-createserver.html "CREATE SERVER")

* * *

[Prev](sql-grant.html "GRANT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-insert.html "INSERT")  
---|---|---  
GRANT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  INSERT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-importforeignschema.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

