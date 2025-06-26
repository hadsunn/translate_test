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

Supported Versions: [Current](/docs/current/sql-refreshmaterializedview.html
"PostgreSQL 17 - REFRESH MATERIALIZED VIEW") ([17](/docs/17/sql-
refreshmaterializedview.html "PostgreSQL 17 - REFRESH MATERIALIZED VIEW")) /
[16](/docs/16/sql-refreshmaterializedview.html "PostgreSQL 16 - REFRESH
MATERIALIZED VIEW") / [15](/docs/15/sql-refreshmaterializedview.html
"PostgreSQL 15 - REFRESH MATERIALIZED VIEW") / [14](/docs/14/sql-
refreshmaterializedview.html "PostgreSQL 14 - REFRESH MATERIALIZED VIEW") /
[13](/docs/13/sql-refreshmaterializedview.html "PostgreSQL 13 - REFRESH
MATERIALIZED VIEW")

Development Versions: [18](/docs/18/sql-refreshmaterializedview.html
"PostgreSQL 18 - REFRESH MATERIALIZED VIEW") / [devel](/docs/devel/sql-
refreshmaterializedview.html "PostgreSQL devel - REFRESH MATERIALIZED VIEW")

Unsupported versions: [12](/docs/12/sql-refreshmaterializedview.html
"PostgreSQL 12 - REFRESH MATERIALIZED VIEW") / [11](/docs/11/sql-
refreshmaterializedview.html "PostgreSQL 11 - REFRESH MATERIALIZED VIEW") /
[10](/docs/10/sql-refreshmaterializedview.html "PostgreSQL 10 - REFRESH
MATERIALIZED VIEW") / [9.6](/docs/9.6/sql-refreshmaterializedview.html
"PostgreSQL 9.6 - REFRESH MATERIALIZED VIEW") / [9.5](/docs/9.5/sql-
refreshmaterializedview.html "PostgreSQL 9.5 - REFRESH MATERIALIZED VIEW") /
[9.4](/docs/9.4/sql-refreshmaterializedview.html "PostgreSQL 9.4 - REFRESH
MATERIALIZED VIEW") / [9.3](/docs/9.3/sql-refreshmaterializedview.html
"PostgreSQL 9.3 - REFRESH MATERIALIZED VIEW")

__

REFRESH MATERIALIZED VIEW  
---  
[Prev](sql-reassign-owned.html "REASSIGN OWNED")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-reindex.html "REINDEX")  
  
* * *

## REFRESH MATERIALIZED VIEW

REFRESH MATERIALIZED VIEW — replace the contents of a materialized view

## Synopsis

    
    
    REFRESH MATERIALIZED VIEW [ CONCURRENTLY ] _name_
        [ WITH [ NO ] DATA ]
    

## Description

`REFRESH MATERIALIZED VIEW` completely replaces the contents of a materialized
view. To execute this command you must be the owner of the materialized view.
The old contents are discarded. If `WITH DATA` is specified (or defaults) the
backing query is executed to provide the new data, and the materialized view
is left in a scannable state. If `WITH NO DATA` is specified no new data is
generated and the materialized view is left in an unscannable state.

`CONCURRENTLY` and `WITH NO DATA` may not be specified together.

## Parameters

`CONCURRENTLY`

    

Refresh the materialized view without locking out concurrent selects on the
materialized view. Without this option a refresh which affects a lot of rows
will tend to use fewer resources and complete more quickly, but could block
other connections which are trying to read from the materialized view. This
option may be faster in cases where a small number of rows are affected.

This option is only allowed if there is at least one `UNIQUE` index on the
materialized view which uses only column names and includes all rows; that is,
it must not be an expression index or include a `WHERE` clause.

This option may not be used when the materialized view is not already
populated.

Even with this option only one `REFRESH` at a time may run against any one
materialized view.

_`name`_

    

The name (optionally schema-qualified) of the materialized view to refresh.

## Notes

If there is an `ORDER BY` clause in the materialized view's defining query,
the original contents of the materialized view will be ordered that way; but
`REFRESH MATERIALIZED VIEW` does not guarantee to preserve that ordering.

## Examples

This command will replace the contents of the materialized view called
`order_summary` using the query from the materialized view's definition, and
leave it in a scannable state:

    
    
    REFRESH MATERIALIZED VIEW order_summary;
    

This command will free storage associated with the materialized view
`annual_statistics_basis` and leave it in an unscannable state:

    
    
    REFRESH MATERIALIZED VIEW annual_statistics_basis WITH NO DATA;
    

## Compatibility

`REFRESH MATERIALIZED VIEW` is a PostgreSQL extension.

## See Also

[CREATE MATERIALIZED VIEW](sql-creatematerializedview.html "CREATE
MATERIALIZED VIEW"), [ALTER MATERIALIZED VIEW](sql-altermaterializedview.html
"ALTER MATERIALIZED VIEW"), [DROP MATERIALIZED VIEW](sql-
dropmaterializedview.html "DROP MATERIALIZED VIEW")

* * *

[Prev](sql-reassign-owned.html "REASSIGN OWNED")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-reindex.html "REINDEX")  
---|---|---  
REASSIGN OWNED  | [Home](index.html "PostgreSQL 16.9 Documentation") |  REINDEX  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
refreshmaterializedview.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

