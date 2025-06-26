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

Supported Versions: [Current](/docs/current/catalog-pg-statistic-ext.html
"PostgreSQL 17 - 53.52. pg_statistic_ext") ([17](/docs/17/catalog-pg-
statistic-ext.html "PostgreSQL 17 - 53.52. pg_statistic_ext")) /
[16](/docs/16/catalog-pg-statistic-ext.html "PostgreSQL 16 -
53.52. pg_statistic_ext") / [15](/docs/15/catalog-pg-statistic-ext.html
"PostgreSQL 15 - 53.52. pg_statistic_ext") / [14](/docs/14/catalog-pg-
statistic-ext.html "PostgreSQL 14 - 53.52. pg_statistic_ext") /
[13](/docs/13/catalog-pg-statistic-ext.html "PostgreSQL 13 -
53.52. pg_statistic_ext")

Development Versions: [18](/docs/18/catalog-pg-statistic-ext.html "PostgreSQL
18 - 53.52. pg_statistic_ext") / [devel](/docs/devel/catalog-pg-statistic-
ext.html "PostgreSQL devel - 53.52. pg_statistic_ext")

Unsupported versions: [12](/docs/12/catalog-pg-statistic-ext.html "PostgreSQL
12 - 53.52. pg_statistic_ext") / [11](/docs/11/catalog-pg-statistic-ext.html
"PostgreSQL 11 - 53.52. pg_statistic_ext") / [10](/docs/10/catalog-pg-
statistic-ext.html "PostgreSQL 10 - 53.52. pg_statistic_ext")

__

53.52. `pg_statistic_ext`  
---  
[Prev](catalog-pg-statistic.html "53.51. pg_statistic")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-statistic-ext-data.html "53.53. pg_statistic_ext_data")  
  
* * *

## 53.52. `pg_statistic_ext` #

The catalog `pg_statistic_ext` holds definitions of extended planner
statistics. Each row in this catalog corresponds to a _statistics object_
created with [`CREATE STATISTICS`](sql-createstatistics.html "CREATE
STATISTICS").

**Table  53.52. `pg_statistic_ext` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`stxrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) Table containing the columns described by this
object  
`stxname` `name` Name of the statistics object  
`stxnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
statistics object  
`stxowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the statistics object  
`stxstattarget` `int4` `stxstattarget` controls the level of detail of
statistics accumulated for this statistics object by [`ANALYZE`](sql-
analyze.html "ANALYZE"). A zero value indicates that no statistics should be
collected. A negative value says to use the maximum of the statistics targets
of the referenced columns, if set, or the system default statistics target.
Positive values of `stxstattarget` determine the target number of “most common
values” to collect.  
`stxkeys` `int2vector` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attnum`) An array of attribute numbers, indicating
which table columns are covered by this statistics object; for example a value
of `1 3` would mean that the first and the third table columns are covered  
`stxkind` `char[]` An array containing codes for the enabled statistics kinds;
valid values are: `d` for n-distinct statistics, `f` for functional dependency
statistics, `m` for most common values (MCV) list statistics, and `e` for
expression statistics  
`stxexprs` `pg_node_tree` Expression trees (in `nodeToString()`
representation) for statistics object attributes that are not simple column
references. This is a list with one element per expression. Null if all
statistics object attributes are simple references.  
  
  

The `pg_statistic_ext` entry is filled in completely during [`CREATE
STATISTICS`](sql-createstatistics.html "CREATE STATISTICS"), but the actual
statistical values are not computed then. Subsequent [`ANALYZE`](sql-
analyze.html "ANALYZE") commands compute the desired values and populate an
entry in the [`pg_statistic_ext_data`](catalog-pg-statistic-ext-data.html
"53.53. pg_statistic_ext_data") catalog.

* * *

[Prev](catalog-pg-statistic.html "53.51. pg_statistic")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-statistic-ext-data.html "53.53. pg_statistic_ext_data")  
---|---|---  
53.51. `pg_statistic`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.53. `pg_statistic_ext_data`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-statistic-
ext.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

