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

Supported Versions: [Current](/docs/current/sql-createtableas.html "PostgreSQL
17 - CREATE TABLE AS") ([17](/docs/17/sql-createtableas.html "PostgreSQL 17 -
CREATE TABLE AS")) / [16](/docs/16/sql-createtableas.html "PostgreSQL 16 -
CREATE TABLE AS") / [15](/docs/15/sql-createtableas.html "PostgreSQL 15 -
CREATE TABLE AS") / [14](/docs/14/sql-createtableas.html "PostgreSQL 14 -
CREATE TABLE AS") / [13](/docs/13/sql-createtableas.html "PostgreSQL 13 -
CREATE TABLE AS")

Development Versions: [18](/docs/18/sql-createtableas.html "PostgreSQL 18 -
CREATE TABLE AS") / [devel](/docs/devel/sql-createtableas.html "PostgreSQL
devel - CREATE TABLE AS")

Unsupported versions: [12](/docs/12/sql-createtableas.html "PostgreSQL 12 -
CREATE TABLE AS") / [11](/docs/11/sql-createtableas.html "PostgreSQL 11 -
CREATE TABLE AS") / [10](/docs/10/sql-createtableas.html "PostgreSQL 10 -
CREATE TABLE AS") / [9.6](/docs/9.6/sql-createtableas.html "PostgreSQL 9.6 -
CREATE TABLE AS") / [9.5](/docs/9.5/sql-createtableas.html "PostgreSQL 9.5 -
CREATE TABLE AS") / [9.4](/docs/9.4/sql-createtableas.html "PostgreSQL 9.4 -
CREATE TABLE AS") / [9.3](/docs/9.3/sql-createtableas.html "PostgreSQL 9.3 -
CREATE TABLE AS") / [9.2](/docs/9.2/sql-createtableas.html "PostgreSQL 9.2 -
CREATE TABLE AS") / [9.1](/docs/9.1/sql-createtableas.html "PostgreSQL 9.1 -
CREATE TABLE AS") / [9.0](/docs/9.0/sql-createtableas.html "PostgreSQL 9.0 -
CREATE TABLE AS") / [8.4](/docs/8.4/sql-createtableas.html "PostgreSQL 8.4 -
CREATE TABLE AS") / [8.3](/docs/8.3/sql-createtableas.html "PostgreSQL 8.3 -
CREATE TABLE AS") / [8.2](/docs/8.2/sql-createtableas.html "PostgreSQL 8.2 -
CREATE TABLE AS") / [8.1](/docs/8.1/sql-createtableas.html "PostgreSQL 8.1 -
CREATE TABLE AS") / [8.0](/docs/8.0/sql-createtableas.html "PostgreSQL 8.0 -
CREATE TABLE AS") / [7.4](/docs/7.4/sql-createtableas.html "PostgreSQL 7.4 -
CREATE TABLE AS") / [7.3](/docs/7.3/sql-createtableas.html "PostgreSQL 7.3 -
CREATE TABLE AS") / [7.2](/docs/7.2/sql-createtableas.html "PostgreSQL 7.2 -
CREATE TABLE AS") / [7.1](/docs/7.1/sql-createtableas.html "PostgreSQL 7.1 -
CREATE TABLE AS")

__

CREATE TABLE AS  
---  
[Prev](sql-createtable.html "CREATE TABLE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtablespace.html "CREATE TABLESPACE")  
  
* * *

## CREATE TABLE AS

CREATE TABLE AS — define a new table from the results of a query

## Synopsis

    
    
    CREATE [ [ GLOBAL | LOCAL ] { TEMPORARY | TEMP } | UNLOGGED ] TABLE [ IF NOT EXISTS ] _table_name_
        [ (_column_name_ [, ...] ) ]
        [ USING _method_ ]
        [ WITH ( _storage_parameter_ [= _value_] [, ... ] ) | WITHOUT OIDS ]
        [ ON COMMIT { PRESERVE ROWS | DELETE ROWS | DROP } ]
        [ TABLESPACE _tablespace_name_ ]
        AS _query_
        [ WITH [ NO ] DATA ]
    

## Description

`CREATE TABLE AS` creates a table and fills it with data computed by a
`SELECT` command. The table columns have the names and data types associated
with the output columns of the `SELECT` (except that you can override the
column names by giving an explicit list of new column names).

`CREATE TABLE AS` bears some resemblance to creating a view, but it is really
quite different: it creates a new table and evaluates the query just once to
fill the new table initially. The new table will not track subsequent changes
to the source tables of the query. In contrast, a view re-evaluates its
defining `SELECT` statement whenever it is queried.

`CREATE TABLE AS` requires `CREATE` privilege on the schema used for the
table.

## Parameters

`GLOBAL` or `LOCAL`

    

Ignored for compatibility. Use of these keywords is deprecated; refer to
[CREATE TABLE](sql-createtable.html "CREATE TABLE") for details.

`TEMPORARY` or `TEMP`

    

If specified, the table is created as a temporary table. Refer to [CREATE
TABLE](sql-createtable.html "CREATE TABLE") for details.

`UNLOGGED`

    

If specified, the table is created as an unlogged table. Refer to [CREATE
TABLE](sql-createtable.html "CREATE TABLE") for details.

`IF NOT EXISTS`

    

Do not throw an error if a relation with the same name already exists; simply
issue a notice and leave the table unmodified.

_`table_name`_

    

The name (optionally schema-qualified) of the table to be created.

_`column_name`_

    

The name of a column in the new table. If column names are not provided, they
are taken from the output column names of the query.

`USING _`method`_`

    

This optional clause specifies the table access method to use to store the
contents for the new table; the method needs be an access method of type
`TABLE`. See [Chapter 63](tableam.html "Chapter 63. Table Access Method
Interface Definition") for more information. If this option is not specified,
the default table access method is chosen for the new table. See
[default_table_access_method](runtime-config-client.html#GUC-DEFAULT-TABLE-
ACCESS-METHOD) for more information.

`WITH ( _`storage_parameter`_ [= _`value`_] [, ... ] )`

    

This clause specifies optional storage parameters for the new table; see
[Storage Parameters](sql-createtable.html#SQL-CREATETABLE-STORAGE-PARAMETERS
"Storage Parameters") in the [CREATE TABLE](sql-createtable.html "CREATE
TABLE") documentation for more information. For backward-compatibility the
`WITH` clause for a table can also include `OIDS=FALSE` to specify that rows
of the new table should contain no OIDs (object identifiers), `OIDS=TRUE` is
not supported anymore.

`WITHOUT OIDS`

    

This is backward-compatible syntax for declaring a table `WITHOUT OIDS`,
creating a table `WITH OIDS` is not supported anymore.

`ON COMMIT`

    

The behavior of temporary tables at the end of a transaction block can be
controlled using `ON COMMIT`. The three options are:

`PRESERVE ROWS`

    

No special action is taken at the ends of transactions. This is the default
behavior.

`DELETE ROWS`

    

All rows in the temporary table will be deleted at the end of each transaction
block. Essentially, an automatic [`TRUNCATE`](sql-truncate.html "TRUNCATE") is
done at each commit.

`DROP`

    

The temporary table will be dropped at the end of the current transaction
block.

`TABLESPACE _`tablespace_name`_`

    

The _`tablespace_name`_ is the name of the tablespace in which the new table
is to be created. If not specified, [default_tablespace](runtime-config-
client.html#GUC-DEFAULT-TABLESPACE) is consulted, or
[temp_tablespaces](runtime-config-client.html#GUC-TEMP-TABLESPACES) if the
table is temporary.

_`query`_

    

A [`SELECT`](sql-select.html "SELECT"), [`TABLE`](sql-select.html#SQL-TABLE
"TABLE Command"), or [`VALUES`](sql-values.html "VALUES") command, or an
[`EXECUTE`](sql-execute.html "EXECUTE") command that runs a prepared `SELECT`,
`TABLE`, or `VALUES` query.

`WITH [ NO ] DATA`

    

This clause specifies whether or not the data produced by the query should be
copied into the new table. If not, only the table structure is copied. The
default is to copy the data.

## Notes

This command is functionally similar to [SELECT INTO](sql-selectinto.html
"SELECT INTO"), but it is preferred since it is less likely to be confused
with other uses of the `SELECT INTO` syntax. Furthermore, `CREATE TABLE AS`
offers a superset of the functionality offered by `SELECT INTO`.

## Examples

Create a new table `films_recent` consisting of only recent entries from the
table `films`:

    
    
    CREATE TABLE films_recent AS
      SELECT * FROM films WHERE date_prod >= '2002-01-01';
    

To copy a table completely, the short form using the `TABLE` command can also
be used:

    
    
    CREATE TABLE films2 AS
      TABLE films;
    

Create a new temporary table `films_recent`, consisting of only recent entries
from the table `films`, using a prepared statement. The new table will be
dropped at commit:

    
    
    PREPARE recentfilms(date) AS
      SELECT * FROM films WHERE date_prod > $1;
    CREATE TEMP TABLE films_recent ON COMMIT DROP AS
      EXECUTE recentfilms('2002-01-01');
    

## Compatibility

`CREATE TABLE AS` conforms to the SQL standard. The following are nonstandard
extensions:

  * The standard requires parentheses around the subquery clause; in PostgreSQL, these parentheses are optional.

  * In the standard, the `WITH [ NO ] DATA` clause is required; in PostgreSQL it is optional.

  * PostgreSQL handles temporary tables in a way rather different from the standard; see [CREATE TABLE](sql-createtable.html "CREATE TABLE") for details.

  * The `WITH` clause is a PostgreSQL extension; storage parameters are not in the standard.

  * The PostgreSQL concept of tablespaces is not part of the standard. Hence, the clause `TABLESPACE` is an extension.

## See Also

[CREATE MATERIALIZED VIEW](sql-creatematerializedview.html "CREATE
MATERIALIZED VIEW"), [CREATE TABLE](sql-createtable.html "CREATE TABLE"),
[EXECUTE](sql-execute.html "EXECUTE"), [SELECT](sql-select.html "SELECT"),
[SELECT INTO](sql-selectinto.html "SELECT INTO"), [VALUES](sql-values.html
"VALUES")

* * *

[Prev](sql-createtable.html "CREATE TABLE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtablespace.html "CREATE TABLESPACE")  
---|---|---  
CREATE TABLE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TABLESPACE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtableas.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

