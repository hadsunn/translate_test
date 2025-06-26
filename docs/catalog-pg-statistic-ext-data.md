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

Supported Versions: [Current](/docs/current/catalog-pg-statistic-ext-data.html
"PostgreSQL 17 - 53.53. pg_statistic_ext_data") ([17](/docs/17/catalog-pg-
statistic-ext-data.html "PostgreSQL 17 - 53.53. pg_statistic_ext_data")) /
[16](/docs/16/catalog-pg-statistic-ext-data.html "PostgreSQL 16 -
53.53. pg_statistic_ext_data") / [15](/docs/15/catalog-pg-statistic-ext-
data.html "PostgreSQL 15 - 53.53. pg_statistic_ext_data") /
[14](/docs/14/catalog-pg-statistic-ext-data.html "PostgreSQL 14 -
53.53. pg_statistic_ext_data") / [13](/docs/13/catalog-pg-statistic-ext-
data.html "PostgreSQL 13 - 53.53. pg_statistic_ext_data")

Development Versions: [18](/docs/18/catalog-pg-statistic-ext-data.html
"PostgreSQL 18 - 53.53. pg_statistic_ext_data") / [devel](/docs/devel/catalog-
pg-statistic-ext-data.html "PostgreSQL devel - 53.53. pg_statistic_ext_data")

Unsupported versions: [12](/docs/12/catalog-pg-statistic-ext-data.html
"PostgreSQL 12 - 53.53. pg_statistic_ext_data")

__

53.53. `pg_statistic_ext_data`  
---  
[Prev](catalog-pg-statistic-ext.html "53.52. pg_statistic_ext")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-subscription.html "53.54. pg_subscription")  
  
* * *

## 53.53. `pg_statistic_ext_data` #

The catalog `pg_statistic_ext_data` holds data for extended planner statistics
defined in [`pg_statistic_ext`](catalog-pg-statistic-ext.html
"53.52. pg_statistic_ext"). Each row in this catalog corresponds to a
_statistics object_ created with [`CREATE STATISTICS`](sql-
createstatistics.html "CREATE STATISTICS").

Normally there is one entry, with `stxdinherit` = `false`, for each statistics
object that has been analyzed. If the table has inheritance children or
partitions, a second entry with `stxdinherit` = `true` is also created. This
row represents the statistics object over the inheritance tree, i.e.,
statistics for the data you'd see with `SELECT * FROM _`table`_ *`, whereas
the `stxdinherit` = `false` row represents the results of `SELECT * FROM ONLY
_`table`_`.

Like [`pg_statistic`](catalog-pg-statistic.html "53.51. pg_statistic"),
`pg_statistic_ext_data` should not be readable by the public, since the
contents might be considered sensitive. (Example: most common combinations of
values in columns might be quite interesting.) [`pg_stats_ext`](view-pg-stats-
ext.html "54.28. pg_stats_ext") is a publicly readable view on
`pg_statistic_ext_data` (after joining with [`pg_statistic_ext`](catalog-pg-
statistic-ext.html "53.52. pg_statistic_ext")) that only exposes information
about tables the current user owns.

**Table  53.53. `pg_statistic_ext_data` Columns**

Column Type Description  
---  
`stxoid` `oid` (references [`pg_statistic_ext`](catalog-pg-statistic-ext.html
"53.52. pg_statistic_ext").`oid`) Extended statistics object containing the
definition for this data  
`stxdinherit` `bool` If true, the stats include values from child tables, not
just the values in the specified relation  
`stxdndistinct` `pg_ndistinct` N-distinct counts, serialized as `pg_ndistinct`
type  
`stxddependencies` `pg_dependencies` Functional dependency statistics,
serialized as `pg_dependencies` type  
`stxdmcv` `pg_mcv_list` MCV (most-common values) list statistics, serialized
as `pg_mcv_list` type  
`stxdexpr` `pg_statistic[]` Per-expression statistics, serialized as an array
of `pg_statistic` type  
  
  

* * *

[Prev](catalog-pg-statistic-ext.html "53.52. pg_statistic_ext")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-subscription.html "53.54. pg_subscription")  
---|---|---  
53.52. `pg_statistic_ext`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.54. `pg_subscription`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-statistic-ext-
data.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

