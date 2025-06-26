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

Supported Versions: [Current](/docs/current/sql-createforeigntable.html
"PostgreSQL 17 - CREATE FOREIGN TABLE") ([17](/docs/17/sql-
createforeigntable.html "PostgreSQL 17 - CREATE FOREIGN TABLE")) /
[16](/docs/16/sql-createforeigntable.html "PostgreSQL 16 - CREATE FOREIGN
TABLE") / [15](/docs/15/sql-createforeigntable.html "PostgreSQL 15 - CREATE
FOREIGN TABLE") / [14](/docs/14/sql-createforeigntable.html "PostgreSQL 14 -
CREATE FOREIGN TABLE") / [13](/docs/13/sql-createforeigntable.html "PostgreSQL
13 - CREATE FOREIGN TABLE")

Development Versions: [18](/docs/18/sql-createforeigntable.html "PostgreSQL 18
- CREATE FOREIGN TABLE") / [devel](/docs/devel/sql-createforeigntable.html
"PostgreSQL devel - CREATE FOREIGN TABLE")

Unsupported versions: [12](/docs/12/sql-createforeigntable.html "PostgreSQL 12
- CREATE FOREIGN TABLE") / [11](/docs/11/sql-createforeigntable.html
"PostgreSQL 11 - CREATE FOREIGN TABLE") / [10](/docs/10/sql-
createforeigntable.html "PostgreSQL 10 - CREATE FOREIGN TABLE") /
[9.6](/docs/9.6/sql-createforeigntable.html "PostgreSQL 9.6 - CREATE FOREIGN
TABLE") / [9.5](/docs/9.5/sql-createforeigntable.html "PostgreSQL 9.5 - CREATE
FOREIGN TABLE") / [9.4](/docs/9.4/sql-createforeigntable.html "PostgreSQL 9.4
- CREATE FOREIGN TABLE") / [9.3](/docs/9.3/sql-createforeigntable.html
"PostgreSQL 9.3 - CREATE FOREIGN TABLE") / [9.2](/docs/9.2/sql-
createforeigntable.html "PostgreSQL 9.2 - CREATE FOREIGN TABLE") /
[9.1](/docs/9.1/sql-createforeigntable.html "PostgreSQL 9.1 - CREATE FOREIGN
TABLE")

__

CREATE FOREIGN TABLE  
---  
[Prev](sql-createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createfunction.html "CREATE FUNCTION")  
  
* * *

## CREATE FOREIGN TABLE

CREATE FOREIGN TABLE — define a new foreign table

## Synopsis

    
    
    CREATE FOREIGN TABLE [ IF NOT EXISTS ] _table_name_ ( [
      { _column_name_ _data_type_ [ OPTIONS ( _option_ '_value_ ' [, ... ] ) ] [ COLLATE _collation_ ] [ _column_constraint_ [ ... ] ]
        | _table_constraint_ }
        [, ... ]
    ] )
    [ INHERITS ( _parent_table_ [, ... ] ) ]
      SERVER _server_name_
    [ OPTIONS ( _option_ '_value_ ' [, ... ] ) ]
    
    CREATE FOREIGN TABLE [ IF NOT EXISTS ] _table_name_
      PARTITION OF _parent_table_ [ (
      { _column_name_ [ WITH OPTIONS ] [ _column_constraint_ [ ... ] ]
        | _table_constraint_ }
        [, ... ]
    ) ]
    { FOR VALUES _partition_bound_spec_ | DEFAULT }
      SERVER _server_name_
    [ OPTIONS ( _option_ '_value_ ' [, ... ] ) ]
    
    where _column_constraint_ is:
    
    [ CONSTRAINT _constraint_name_ ]
    { NOT NULL |
      NULL |
      CHECK ( _expression_ ) [ NO INHERIT ] |
      DEFAULT _default_expr_ |
      GENERATED ALWAYS AS ( _generation_expr_ ) STORED }
    
    and _table_constraint_ is:
    
    [ CONSTRAINT _constraint_name_ ]
    CHECK ( _expression_ ) [ NO INHERIT ]
    
    and _partition_bound_spec_ is:
    
    IN ( _partition_bound_expr_ [, ...] ) |
    FROM ( { _partition_bound_expr_ | MINVALUE | MAXVALUE } [, ...] )
      TO ( { _partition_bound_expr_ | MINVALUE | MAXVALUE } [, ...] ) |
    WITH ( MODULUS _numeric_literal_ , REMAINDER _numeric_literal_ )
    

## Description

`CREATE FOREIGN TABLE` creates a new foreign table in the current database.
The table will be owned by the user issuing the command.

If a schema name is given (for example, `CREATE FOREIGN TABLE myschema.mytable
...`) then the table is created in the specified schema. Otherwise it is
created in the current schema. The name of the foreign table must be distinct
from the name of any other relation (table, sequence, index, view,
materialized view, or foreign table) in the same schema.

`CREATE FOREIGN TABLE` also automatically creates a data type that represents
the composite type corresponding to one row of the foreign table. Therefore,
foreign tables cannot have the same name as any existing data type in the same
schema.

If `PARTITION OF` clause is specified then the table is created as a partition
of `parent_table` with specified bounds.

To be able to create a foreign table, you must have `USAGE` privilege on the
foreign server, as well as `USAGE` privilege on all column types used in the
table.

## Parameters

`IF NOT EXISTS`

    

Do not throw an error if a relation with the same name already exists. A
notice is issued in this case. Note that there is no guarantee that the
existing relation is anything like the one that would have been created.

_`table_name`_

    

The name (optionally schema-qualified) of the table to be created.

_`column_name`_

    

The name of a column to be created in the new table.

_`data_type`_

    

The data type of the column. This can include array specifiers. For more
information on the data types supported by PostgreSQL, refer to [Chapter
8](datatype.html "Chapter 8. Data Types").

`COLLATE _`collation`_`

    

The `COLLATE` clause assigns a collation to the column (which must be of a
collatable data type). If not specified, the column data type's default
collation is used.

`INHERITS ( _`parent_table`_ [, ... ] )`

    

The optional `INHERITS` clause specifies a list of tables from which the new
foreign table automatically inherits all columns. Parent tables can be plain
tables or foreign tables. See the similar form of [`CREATE TABLE`](sql-
createtable.html "CREATE TABLE") for more details.

`PARTITION OF _`parent_table`_ { FOR VALUES _`partition_bound_spec`_ | DEFAULT }`
    

This form can be used to create the foreign table as partition of the given
parent table with specified partition bound values. See the similar form of
[`CREATE TABLE`](sql-createtable.html "CREATE TABLE") for more details. Note
that it is currently not allowed to create the foreign table as a partition of
the parent table if there are `UNIQUE` indexes on the parent table. (See also
[`ALTER TABLE ATTACH PARTITION`](sql-altertable.html "ALTER TABLE").)

`CONSTRAINT _`constraint_name`_`

    

An optional name for a column or table constraint. If the constraint is
violated, the constraint name is present in error messages, so constraint
names like `col must be positive` can be used to communicate helpful
constraint information to client applications. (Double-quotes are needed to
specify constraint names that contain spaces.) If a constraint name is not
specified, the system generates a name.

`NOT NULL`

    

The column is not allowed to contain null values.

`NULL`

    

The column is allowed to contain null values. This is the default.

This clause is only provided for compatibility with non-standard SQL
databases. Its use is discouraged in new applications.

`CHECK ( _`expression`_ ) [ NO INHERIT ]`

    

The `CHECK` clause specifies an expression producing a Boolean result which
each row in the foreign table is expected to satisfy; that is, the expression
should produce TRUE or UNKNOWN, never FALSE, for all rows in the foreign
table. A check constraint specified as a column constraint should reference
that column's value only, while an expression appearing in a table constraint
can reference multiple columns.

Currently, `CHECK` expressions cannot contain subqueries nor refer to
variables other than columns of the current row. The system column `tableoid`
may be referenced, but not any other system column.

A constraint marked with `NO INHERIT` will not propagate to child tables.

`DEFAULT _`default_expr`_`

    

The `DEFAULT` clause assigns a default data value for the column whose column
definition it appears within. The value is any variable-free expression
(subqueries and cross-references to other columns in the current table are not
allowed). The data type of the default expression must match the data type of
the column.

The default expression will be used in any insert operation that does not
specify a value for the column. If there is no default for a column, then the
default is null.

`GENERATED ALWAYS AS ( _`generation_expr`_ ) STORED`

    

This clause creates the column as a _generated column_. The column cannot be
written to, and when read the result of the specified expression will be
returned.

The keyword `STORED` is required to signify that the column will be computed
on write. (The computed value will be presented to the foreign-data wrapper
for storage and must be returned on reading.)

The generation expression can refer to other columns in the table, but not
other generated columns. Any functions and operators used must be immutable.
References to other tables are not allowed.

_`server_name`_

    

The name of an existing foreign server to use for the foreign table. For
details on defining a server, see [CREATE SERVER](sql-createserver.html
"CREATE SERVER").

`OPTIONS ( _`option`_ '_`value`_ ' [, ...] )`

    

Options to be associated with the new foreign table or one of its columns. The
allowed option names and values are specific to each foreign data wrapper and
are validated using the foreign-data wrapper's validator function. Duplicate
option names are not allowed (although it's OK for a table option and a column
option to have the same name).

## Notes

Constraints on foreign tables (such as `CHECK` or `NOT NULL` clauses) are not
enforced by the core PostgreSQL system, and most foreign data wrappers do not
attempt to enforce them either; that is, the constraint is simply assumed to
hold true. There would be little point in such enforcement since it would only
apply to rows inserted or updated via the foreign table, and not to rows
modified by other means, such as directly on the remote server. Instead, a
constraint attached to a foreign table should represent a constraint that is
being enforced by the remote server.

Some special-purpose foreign data wrappers might be the only access mechanism
for the data they access, and in that case it might be appropriate for the
foreign data wrapper itself to perform constraint enforcement. But you should
not assume that a wrapper does that unless its documentation says so.

Although PostgreSQL does not attempt to enforce constraints on foreign tables,
it does assume that they are correct for purposes of query optimization. If
there are rows visible in the foreign table that do not satisfy a declared
constraint, queries on the table might produce errors or incorrect answers. It
is the user's responsibility to ensure that the constraint definition matches
reality.

### Caution

When a foreign table is used as a partition of a partitioned table, there is
an implicit constraint that its contents must satisfy the partitioning rule.
Again, it is the user's responsibility to ensure that that is true, which is
best done by installing a matching constraint on the remote server.

Within a partitioned table containing foreign-table partitions, an `UPDATE`
that changes the partition key value can cause a row to be moved from a local
partition to a foreign-table partition, provided the foreign data wrapper
supports tuple routing. However, it is not currently possible to move a row
from a foreign-table partition to another partition. An `UPDATE` that would
require doing that will fail due to the partitioning constraint, assuming that
that is properly enforced by the remote server.

Similar considerations apply to generated columns. Stored generated columns
are computed on insert or update on the local PostgreSQL server and handed to
the foreign-data wrapper for writing out to the foreign data store, but it is
not enforced that a query of the foreign table returns values for stored
generated columns that are consistent with the generation expression. Again,
this might result in incorrect query results.

## Examples

Create foreign table `films`, which will be accessed through the server
`film_server`:

    
    
    CREATE FOREIGN TABLE films (
        code        char(5) NOT NULL,
        title       varchar(40) NOT NULL,
        did         integer NOT NULL,
        date_prod   date,
        kind        varchar(10),
        len         interval hour to minute
    )
    SERVER film_server;
    

Create foreign table `measurement_y2016m07`, which will be accessed through
the server `server_07`, as a partition of the range partitioned table
`measurement`:

    
    
    CREATE FOREIGN TABLE measurement_y2016m07
        PARTITION OF measurement FOR VALUES FROM ('2016-07-01') TO ('2016-08-01')
        SERVER server_07;
    

## Compatibility

The `CREATE FOREIGN TABLE` command largely conforms to the SQL standard;
however, much as with [`CREATE TABLE`](sql-createtable.html "CREATE TABLE"),
`NULL` constraints and zero-column foreign tables are permitted. The ability
to specify column default values is also a PostgreSQL extension. Table
inheritance, in the form defined by PostgreSQL, is nonstandard.

## See Also

[ALTER FOREIGN TABLE](sql-alterforeigntable.html "ALTER FOREIGN TABLE"), [DROP
FOREIGN TABLE](sql-dropforeigntable.html "DROP FOREIGN TABLE"), [CREATE
TABLE](sql-createtable.html "CREATE TABLE"), [CREATE SERVER](sql-
createserver.html "CREATE SERVER"), [IMPORT FOREIGN SCHEMA](sql-
importforeignschema.html "IMPORT FOREIGN SCHEMA")

* * *

[Prev](sql-createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createfunction.html "CREATE FUNCTION")  
---|---|---  
CREATE FOREIGN DATA WRAPPER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE FUNCTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createforeigntable.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

