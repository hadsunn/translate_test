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

Supported Versions: [Current](/docs/current/sql-creatematerializedview.html
"PostgreSQL 17 - CREATE MATERIALIZED VIEW") ([17](/docs/17/sql-
creatematerializedview.html "PostgreSQL 17 - CREATE MATERIALIZED VIEW")) /
[16](/docs/16/sql-creatematerializedview.html "PostgreSQL 16 - CREATE
MATERIALIZED VIEW") / [15](/docs/15/sql-creatematerializedview.html
"PostgreSQL 15 - CREATE MATERIALIZED VIEW") / [14](/docs/14/sql-
creatematerializedview.html "PostgreSQL 14 - CREATE MATERIALIZED VIEW") /
[13](/docs/13/sql-creatematerializedview.html "PostgreSQL 13 - CREATE
MATERIALIZED VIEW")

Development Versions: [18](/docs/18/sql-creatematerializedview.html
"PostgreSQL 18 - CREATE MATERIALIZED VIEW") / [devel](/docs/devel/sql-
creatematerializedview.html "PostgreSQL devel - CREATE MATERIALIZED VIEW")

Unsupported versions: [12](/docs/12/sql-creatematerializedview.html
"PostgreSQL 12 - CREATE MATERIALIZED VIEW") / [11](/docs/11/sql-
creatematerializedview.html "PostgreSQL 11 - CREATE MATERIALIZED VIEW") /
[10](/docs/10/sql-creatematerializedview.html "PostgreSQL 10 - CREATE
MATERIALIZED VIEW") / [9.6](/docs/9.6/sql-creatematerializedview.html
"PostgreSQL 9.6 - CREATE MATERIALIZED VIEW") / [9.5](/docs/9.5/sql-
creatematerializedview.html "PostgreSQL 9.5 - CREATE MATERIALIZED VIEW") /
[9.4](/docs/9.4/sql-creatematerializedview.html "PostgreSQL 9.4 - CREATE
MATERIALIZED VIEW") / [9.3](/docs/9.3/sql-creatematerializedview.html
"PostgreSQL 9.3 - CREATE MATERIALIZED VIEW")

__

CREATE MATERIALIZED VIEW  
---  
[Prev](sql-createlanguage.html "CREATE LANGUAGE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createoperator.html "CREATE OPERATOR")  
  
* * *

## CREATE MATERIALIZED VIEW

CREATE MATERIALIZED VIEW — define a new materialized view

## Synopsis

    
    
    CREATE MATERIALIZED VIEW [ IF NOT EXISTS ] _table_name_
        [ (_column_name_ [, ...] ) ]
        [ USING _method_ ]
        [ WITH ( _storage_parameter_ [= _value_] [, ... ] ) ]
        [ TABLESPACE _tablespace_name_ ]
        AS _query_
        [ WITH [ NO ] DATA ]
    

## Description

`CREATE MATERIALIZED VIEW` defines a materialized view of a query. The query
is executed and used to populate the view at the time the command is issued
(unless `WITH NO DATA` is used) and may be refreshed later using `REFRESH
MATERIALIZED VIEW`.

`CREATE MATERIALIZED VIEW` is similar to `CREATE TABLE AS`, except that it
also remembers the query used to initialize the view, so that it can be
refreshed later upon demand. A materialized view has many of the same
properties as a table, but there is no support for temporary materialized
views.

`CREATE MATERIALIZED VIEW` requires `CREATE` privilege on the schema used for
the materialized view.

## Parameters

`IF NOT EXISTS`

    

Do not throw an error if a materialized view with the same name already
exists. A notice is issued in this case. Note that there is no guarantee that
the existing materialized view is anything like the one that would have been
created.

_`table_name`_

    

The name (optionally schema-qualified) of the materialized view to be created.
The name must be distinct from the name of any other relation (table,
sequence, index, view, materialized view, or foreign table) in the same
schema.

_`column_name`_

    

The name of a column in the new materialized view. If column names are not
provided, they are taken from the output column names of the query.

`USING _`method`_`

    

This optional clause specifies the table access method to use to store the
contents for the new materialized view; the method needs be an access method
of type `TABLE`. See [Chapter 63](tableam.html "Chapter 63. Table Access
Method Interface Definition") for more information. If this option is not
specified, the default table access method is chosen for the new materialized
view. See [default_table_access_method](runtime-config-client.html#GUC-
DEFAULT-TABLE-ACCESS-METHOD) for more information.

`WITH ( _`storage_parameter`_ [= _`value`_] [, ... ] )`

    

This clause specifies optional storage parameters for the new materialized
view; see [Storage Parameters](sql-createtable.html#SQL-CREATETABLE-STORAGE-
PARAMETERS "Storage Parameters") in the [CREATE TABLE](sql-createtable.html
"CREATE TABLE") documentation for more information. All parameters supported
for `CREATE TABLE` are also supported for `CREATE MATERIALIZED VIEW`. See
[CREATE TABLE](sql-createtable.html "CREATE TABLE") for more information.

`TABLESPACE _`tablespace_name`_`

    

The _`tablespace_name`_ is the name of the tablespace in which the new
materialized view is to be created. If not specified,
[default_tablespace](runtime-config-client.html#GUC-DEFAULT-TABLESPACE) is
consulted.

_`query`_

    

A [`SELECT`](sql-select.html "SELECT"), [`TABLE`](sql-select.html#SQL-TABLE
"TABLE Command"), or [`VALUES`](sql-values.html "VALUES") command. This query
will run within a security-restricted operation; in particular, calls to
functions that themselves create temporary tables will fail.

`WITH [ NO ] DATA`

    

This clause specifies whether or not the materialized view should be populated
at creation time. If not, the materialized view will be flagged as unscannable
and cannot be queried until `REFRESH MATERIALIZED VIEW` is used.

## Compatibility

`CREATE MATERIALIZED VIEW` is a PostgreSQL extension.

## See Also

[ALTER MATERIALIZED VIEW](sql-altermaterializedview.html "ALTER MATERIALIZED
VIEW"), [CREATE TABLE AS](sql-createtableas.html "CREATE TABLE AS"), [CREATE
VIEW](sql-createview.html "CREATE VIEW"), [DROP MATERIALIZED VIEW](sql-
dropmaterializedview.html "DROP MATERIALIZED VIEW"), [REFRESH MATERIALIZED
VIEW](sql-refreshmaterializedview.html "REFRESH MATERIALIZED VIEW")

* * *

[Prev](sql-createlanguage.html "CREATE LANGUAGE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createoperator.html "CREATE OPERATOR")  
---|---|---  
CREATE LANGUAGE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE OPERATOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
creatematerializedview.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

