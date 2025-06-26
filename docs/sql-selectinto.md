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

Supported Versions: [Current](/docs/current/sql-selectinto.html "PostgreSQL 17
- SELECT INTO") ([17](/docs/17/sql-selectinto.html "PostgreSQL 17 - SELECT
INTO")) / [16](/docs/16/sql-selectinto.html "PostgreSQL 16 - SELECT INTO") /
[15](/docs/15/sql-selectinto.html "PostgreSQL 15 - SELECT INTO") /
[14](/docs/14/sql-selectinto.html "PostgreSQL 14 - SELECT INTO") /
[13](/docs/13/sql-selectinto.html "PostgreSQL 13 - SELECT INTO")

Development Versions: [18](/docs/18/sql-selectinto.html "PostgreSQL 18 -
SELECT INTO") / [devel](/docs/devel/sql-selectinto.html "PostgreSQL devel -
SELECT INTO")

Unsupported versions: [12](/docs/12/sql-selectinto.html "PostgreSQL 12 -
SELECT INTO") / [11](/docs/11/sql-selectinto.html "PostgreSQL 11 - SELECT
INTO") / [10](/docs/10/sql-selectinto.html "PostgreSQL 10 - SELECT INTO") /
[9.6](/docs/9.6/sql-selectinto.html "PostgreSQL 9.6 - SELECT INTO") /
[9.5](/docs/9.5/sql-selectinto.html "PostgreSQL 9.5 - SELECT INTO") /
[9.4](/docs/9.4/sql-selectinto.html "PostgreSQL 9.4 - SELECT INTO") /
[9.3](/docs/9.3/sql-selectinto.html "PostgreSQL 9.3 - SELECT INTO") /
[9.2](/docs/9.2/sql-selectinto.html "PostgreSQL 9.2 - SELECT INTO") /
[9.1](/docs/9.1/sql-selectinto.html "PostgreSQL 9.1 - SELECT INTO") /
[9.0](/docs/9.0/sql-selectinto.html "PostgreSQL 9.0 - SELECT INTO") /
[8.4](/docs/8.4/sql-selectinto.html "PostgreSQL 8.4 - SELECT INTO") /
[8.3](/docs/8.3/sql-selectinto.html "PostgreSQL 8.3 - SELECT INTO") /
[8.2](/docs/8.2/sql-selectinto.html "PostgreSQL 8.2 - SELECT INTO") /
[8.1](/docs/8.1/sql-selectinto.html "PostgreSQL 8.1 - SELECT INTO") /
[8.0](/docs/8.0/sql-selectinto.html "PostgreSQL 8.0 - SELECT INTO") /
[7.4](/docs/7.4/sql-selectinto.html "PostgreSQL 7.4 - SELECT INTO") /
[7.3](/docs/7.3/sql-selectinto.html "PostgreSQL 7.3 - SELECT INTO") /
[7.2](/docs/7.2/sql-selectinto.html "PostgreSQL 7.2 - SELECT INTO") /
[7.1](/docs/7.1/sql-selectinto.html "PostgreSQL 7.1 - SELECT INTO")

__

SELECT INTO  
---  
[Prev](sql-select.html "SELECT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-set.html "SET")  
  
* * *

## SELECT INTO

SELECT INTO — define a new table from the results of a query

## Synopsis

    
    
    [ WITH [ RECURSIVE ] _with_query_ [, ...] ]
    SELECT [ ALL | DISTINCT [ ON ( _expression_ [, ...] ) ] ]
        [ { * | _expression_ [ [ AS ] _output_name_ ] } [, ...] ]
        INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] _new_table_
        [ FROM _from_item_ [, ...] ]
        [ WHERE _condition_ ]
        [ GROUP BY _expression_ [, ...] ]
        [ HAVING _condition_ ]
        [ WINDOW _window_name_ AS ( _window_definition_ ) [, ...] ]
        [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] _select_ ]
        [ ORDER BY _expression_ [ ASC | DESC | USING _operator_ ] [ NULLS { FIRST | LAST } ] [, ...] ]
        [ LIMIT { _count_ | ALL } ]
        [ OFFSET _start_ [ ROW | ROWS ] ]
        [ FETCH { FIRST | NEXT } [ _count_ ] { ROW | ROWS } ONLY ]
        [ FOR { UPDATE | SHARE } [ OF _table_name_ [, ...] ] [ NOWAIT ] [...] ]
    

## Description

`SELECT INTO` creates a new table and fills it with data computed by a query.
The data is not returned to the client, as it is with a normal `SELECT`. The
new table's columns have the names and data types associated with the output
columns of the `SELECT`.

## Parameters

`TEMPORARY` or `TEMP`

    

If specified, the table is created as a temporary table. Refer to [CREATE
TABLE](sql-createtable.html "CREATE TABLE") for details.

`UNLOGGED`

    

If specified, the table is created as an unlogged table. Refer to [CREATE
TABLE](sql-createtable.html "CREATE TABLE") for details.

_`new_table`_

    

The name (optionally schema-qualified) of the table to be created.

All other parameters are described in detail under [SELECT](sql-select.html
"SELECT").

## Notes

[`CREATE TABLE AS`](sql-createtableas.html "CREATE TABLE AS") is functionally
similar to `SELECT INTO`. `CREATE TABLE AS` is the recommended syntax, since
this form of `SELECT INTO` is not available in ECPG or PL/pgSQL, because they
interpret the `INTO` clause differently. Furthermore, `CREATE TABLE AS` offers
a superset of the functionality provided by `SELECT INTO`.

In contrast to `CREATE TABLE AS`, `SELECT INTO` does not allow specifying
properties like a table's access method with [`USING _`method`_`](sql-
createtable.html#SQL-CREATETABLE-METHOD) or the table's tablespace with
[`TABLESPACE _`tablespace_name`_`](sql-createtable.html#SQL-CREATETABLE-
TABLESPACE). Use `CREATE TABLE AS` if necessary. Therefore, the default table
access method is chosen for the new table. See
[default_table_access_method](runtime-config-client.html#GUC-DEFAULT-TABLE-
ACCESS-METHOD) for more information.

## Examples

Create a new table `films_recent` consisting of only recent entries from the
table `films`:

    
    
    SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
    

## Compatibility

The SQL standard uses `SELECT INTO` to represent selecting values into scalar
variables of a host program, rather than creating a new table. This indeed is
the usage found in ECPG (see [Chapter 36](ecpg.html "Chapter 36. ECPG —
Embedded SQL in C")) and PL/pgSQL (see [Chapter 43](plpgsql.html
"Chapter 43. PL/pgSQL — SQL Procedural Language")). The PostgreSQL usage of
`SELECT INTO` to represent table creation is historical. Some other SQL
implementations also use `SELECT INTO` in this way (but most SQL
implementations support `CREATE TABLE AS` instead). Apart from such
compatibility considerations, it is best to use `CREATE TABLE AS` for this
purpose in new code.

## See Also

[CREATE TABLE AS](sql-createtableas.html "CREATE TABLE AS")

* * *

[Prev](sql-select.html "SELECT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-set.html "SET")  
---|---|---  
SELECT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-selectinto.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

