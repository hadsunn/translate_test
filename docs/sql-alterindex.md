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

Supported Versions: [Current](/docs/current/sql-alterindex.html "PostgreSQL 17
- ALTER INDEX") ([17](/docs/17/sql-alterindex.html "PostgreSQL 17 - ALTER
INDEX")) / [16](/docs/16/sql-alterindex.html "PostgreSQL 16 - ALTER INDEX") /
[15](/docs/15/sql-alterindex.html "PostgreSQL 15 - ALTER INDEX") /
[14](/docs/14/sql-alterindex.html "PostgreSQL 14 - ALTER INDEX") /
[13](/docs/13/sql-alterindex.html "PostgreSQL 13 - ALTER INDEX")

Development Versions: [18](/docs/18/sql-alterindex.html "PostgreSQL 18 - ALTER
INDEX") / [devel](/docs/devel/sql-alterindex.html "PostgreSQL devel - ALTER
INDEX")

Unsupported versions: [12](/docs/12/sql-alterindex.html "PostgreSQL 12 - ALTER
INDEX") / [11](/docs/11/sql-alterindex.html "PostgreSQL 11 - ALTER INDEX") /
[10](/docs/10/sql-alterindex.html "PostgreSQL 10 - ALTER INDEX") /
[9.6](/docs/9.6/sql-alterindex.html "PostgreSQL 9.6 - ALTER INDEX") /
[9.5](/docs/9.5/sql-alterindex.html "PostgreSQL 9.5 - ALTER INDEX") /
[9.4](/docs/9.4/sql-alterindex.html "PostgreSQL 9.4 - ALTER INDEX") /
[9.3](/docs/9.3/sql-alterindex.html "PostgreSQL 9.3 - ALTER INDEX") /
[9.2](/docs/9.2/sql-alterindex.html "PostgreSQL 9.2 - ALTER INDEX") /
[9.1](/docs/9.1/sql-alterindex.html "PostgreSQL 9.1 - ALTER INDEX") /
[9.0](/docs/9.0/sql-alterindex.html "PostgreSQL 9.0 - ALTER INDEX") /
[8.4](/docs/8.4/sql-alterindex.html "PostgreSQL 8.4 - ALTER INDEX") /
[8.3](/docs/8.3/sql-alterindex.html "PostgreSQL 8.3 - ALTER INDEX") /
[8.2](/docs/8.2/sql-alterindex.html "PostgreSQL 8.2 - ALTER INDEX") /
[8.1](/docs/8.1/sql-alterindex.html "PostgreSQL 8.1 - ALTER INDEX") /
[8.0](/docs/8.0/sql-alterindex.html "PostgreSQL 8.0 - ALTER INDEX")

__

ALTER INDEX  
---  
[Prev](sql-altergroup.html "ALTER GROUP")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterlanguage.html "ALTER LANGUAGE")  
  
* * *

## ALTER INDEX

ALTER INDEX — change the definition of an index

## Synopsis

    
    
    ALTER INDEX [ IF EXISTS ] _name_ RENAME TO _new_name_
    ALTER INDEX [ IF EXISTS ] _name_ SET TABLESPACE _tablespace_name_
    ALTER INDEX _name_ ATTACH PARTITION _index_name_
    ALTER INDEX _name_ [ NO ] DEPENDS ON EXTENSION _extension_name_
    ALTER INDEX [ IF EXISTS ] _name_ SET ( _storage_parameter_ [= _value_] [, ... ] )
    ALTER INDEX [ IF EXISTS ] _name_ RESET ( _storage_parameter_ [, ... ] )
    ALTER INDEX [ IF EXISTS ] _name_ ALTER [ COLUMN ] _column_number_
        SET STATISTICS _integer_
    ALTER INDEX ALL IN TABLESPACE _name_ [ OWNED BY _role_name_ [, ... ] ]
        SET TABLESPACE _new_tablespace_ [ NOWAIT ]
    

## Description

`ALTER INDEX` changes the definition of an existing index. There are several
subforms described below. Note that the lock level required may differ for
each subform. An `ACCESS EXCLUSIVE` lock is held unless explicitly noted. When
multiple subcommands are listed, the lock held will be the strictest one
required from any subcommand.

`RENAME`

    

The `RENAME` form changes the name of the index. If the index is associated
with a table constraint (either `UNIQUE`, `PRIMARY KEY`, or `EXCLUDE`), the
constraint is renamed as well. There is no effect on the stored data.

Renaming an index acquires a `SHARE UPDATE EXCLUSIVE` lock.

`SET TABLESPACE`

    

This form changes the index's tablespace to the specified tablespace and moves
the data file(s) associated with the index to the new tablespace. To change
the tablespace of an index, you must own the index and have `CREATE` privilege
on the new tablespace. All indexes in the current database in a tablespace can
be moved by using the `ALL IN TABLESPACE` form, which will lock all indexes to
be moved and then move each one. This form also supports `OWNED BY`, which
will only move indexes owned by the roles specified. If the `NOWAIT` option is
specified then the command will fail if it is unable to acquire all of the
locks required immediately. Note that system catalogs will not be moved by
this command, use `ALTER DATABASE` or explicit `ALTER INDEX` invocations
instead if desired. See also [`CREATE TABLESPACE`](sql-createtablespace.html
"CREATE TABLESPACE").

`ATTACH PARTITION _`index_name`_`

    

Causes the named index (possibly schema-qualified) to become attached to the
altered index. The named index must be on a partition of the table containing
the index being altered, and have an equivalent definition. An attached index
cannot be dropped by itself, and will automatically be dropped if its parent
index is dropped.

`DEPENDS ON EXTENSION _`extension_name`_`  
`NO DEPENDS ON EXTENSION _`extension_name`_`

    

This form marks the index as dependent on the extension, or no longer
dependent on that extension if `NO` is specified. An index that's marked as
dependent on an extension is automatically dropped when the extension is
dropped.

`SET ( _`storage_parameter`_ [= _`value`_] [, ... ] )`

    

This form changes one or more index-method-specific storage parameters for the
index. See [`CREATE INDEX`](sql-createindex.html "CREATE INDEX") for details
on the available parameters. Note that the index contents will not be modified
immediately by this command; depending on the parameter you might need to
rebuild the index with [`REINDEX`](sql-reindex.html "REINDEX") to get the
desired effects.

`RESET ( _`storage_parameter`_ [, ... ] )`

    

This form resets one or more index-method-specific storage parameters to their
defaults. As with `SET`, a `REINDEX` might be needed to update the index
entirely.

`ALTER [ COLUMN ] _`column_number`_ SET STATISTICS _`integer`_`

    

This form sets the per-column statistics-gathering target for subsequent
[`ANALYZE`](sql-analyze.html "ANALYZE") operations, though can be used only on
index columns that are defined as an expression. Since expressions lack a
unique name, we refer to them using the ordinal number of the index column.
The target can be set in the range 0 to 10000; alternatively, set it to -1 to
revert to using the system default statistics target
([default_statistics_target](runtime-config-query.html#GUC-DEFAULT-STATISTICS-
TARGET)). For more information on the use of statistics by the PostgreSQL
query planner, refer to [Section 14.2](planner-stats.html "14.2. Statistics
Used by the Planner").

## Parameters

`IF EXISTS`

    

Do not throw an error if the index does not exist. A notice is issued in this
case.

_`column_number`_

    

The ordinal number refers to the ordinal (left-to-right) position of the index
column.

_`name`_

    

The name (possibly schema-qualified) of an existing index to alter.

_`new_name`_

    

The new name for the index.

_`tablespace_name`_

    

The tablespace to which the index will be moved.

_`extension_name`_

    

The name of the extension that the index is to depend on.

_`storage_parameter`_

    

The name of an index-method-specific storage parameter.

_`value`_

    

The new value for an index-method-specific storage parameter. This might be a
number or a word depending on the parameter.

## Notes

These operations are also possible using [`ALTER TABLE`](sql-altertable.html
"ALTER TABLE"). `ALTER INDEX` is in fact just an alias for the forms of `ALTER
TABLE` that apply to indexes.

There was formerly an `ALTER INDEX OWNER` variant, but this is now ignored
(with a warning). An index cannot have an owner different from its table's
owner. Changing the table's owner automatically changes the index as well.

Changing any part of a system catalog index is not permitted.

## Examples

To rename an existing index:

    
    
    ALTER INDEX distributors RENAME TO suppliers;
    

To move an index to a different tablespace:

    
    
    ALTER INDEX distributors SET TABLESPACE fasttablespace;
    

To change an index's fill factor (assuming that the index method supports it):

    
    
    ALTER INDEX distributors SET (fillfactor = 75);
    REINDEX INDEX distributors;
    

Set the statistics-gathering target for an expression index:

    
    
    CREATE INDEX coord_idx ON measured (x, y, (z + t));
    ALTER INDEX coord_idx ALTER COLUMN 3 SET STATISTICS 1000;
    

## Compatibility

`ALTER INDEX` is a PostgreSQL extension.

## See Also

[CREATE INDEX](sql-createindex.html "CREATE INDEX"), [REINDEX](sql-
reindex.html "REINDEX")

* * *

[Prev](sql-altergroup.html "ALTER GROUP")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterlanguage.html "ALTER LANGUAGE")  
---|---|---  
ALTER GROUP  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER LANGUAGE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterindex.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

