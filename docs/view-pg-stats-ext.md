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

Supported Versions: [Current](/docs/current/view-pg-stats-ext.html "PostgreSQL
17 - 54.28. pg_stats_ext") ([17](/docs/17/view-pg-stats-ext.html "PostgreSQL
17 - 54.28. pg_stats_ext")) / [16](/docs/16/view-pg-stats-ext.html "PostgreSQL
16 - 54.28. pg_stats_ext") / [15](/docs/15/view-pg-stats-ext.html "PostgreSQL
15 - 54.28. pg_stats_ext") / [14](/docs/14/view-pg-stats-ext.html "PostgreSQL
14 - 54.28. pg_stats_ext") / [13](/docs/13/view-pg-stats-ext.html "PostgreSQL
13 - 54.28. pg_stats_ext")

Development Versions: [18](/docs/18/view-pg-stats-ext.html "PostgreSQL 18 -
54.28. pg_stats_ext") / [devel](/docs/devel/view-pg-stats-ext.html "PostgreSQL
devel - 54.28. pg_stats_ext")

Unsupported versions: [12](/docs/12/view-pg-stats-ext.html "PostgreSQL 12 -
54.28. pg_stats_ext")

__

54.28. `pg_stats_ext`  
---  
[Prev](view-pg-stats.html "54.27. pg_stats")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-stats-ext-exprs.html "54.29. pg_stats_ext_exprs")  
  
* * *

## 54.28. `pg_stats_ext` #

The view `pg_stats_ext` provides access to information about each extended
statistics object in the database, combining information stored in the
[`pg_statistic_ext`](catalog-pg-statistic-ext.html "53.52. pg_statistic_ext")
and [`pg_statistic_ext_data`](catalog-pg-statistic-ext-data.html
"53.53. pg_statistic_ext_data") catalogs. This view allows access only to rows
of [`pg_statistic_ext`](catalog-pg-statistic-ext.html
"53.52. pg_statistic_ext") and [`pg_statistic_ext_data`](catalog-pg-statistic-
ext-data.html "53.53. pg_statistic_ext_data") that correspond to tables the
user owns, and therefore it is safe to allow public read access to this view.

`pg_stats_ext` is also designed to present the information in a more readable
format than the underlying catalogs — at the cost that its schema must be
extended whenever new types of extended statistics are added to
[`pg_statistic_ext`](catalog-pg-statistic-ext.html "53.52. pg_statistic_ext").

**Table  54.28. `pg_stats_ext` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table  
`statistics_schemaname` `name` (references [`pg_namespace`](catalog-pg-
namespace.html "53.32. pg_namespace").`nspname`) Name of schema containing
extended statistics object  
`statistics_name` `name` (references [`pg_statistic_ext`](catalog-pg-
statistic-ext.html "53.52. pg_statistic_ext").`stxname`) Name of extended
statistics object  
`statistics_owner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Owner of the extended statistics object  
`attnames` `name[]` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attname`) Names of the columns included in the extended
statistics object  
`exprs` `text[]` Expressions included in the extended statistics object  
`kinds` `char[]` Types of extended statistics object enabled for this record  
`inherited` `bool` (references [`pg_statistic_ext_data`](catalog-pg-statistic-
ext-data.html "53.53. pg_statistic_ext_data").`stxdinherit`) If true, the
stats include values from child tables, not just the values in the specified
relation  
`n_distinct` `pg_ndistinct` N-distinct counts for combinations of column
values. If greater than zero, the estimated number of distinct values in the
combination. If less than zero, the negative of the number of distinct values
divided by the number of rows. (The negated form is used when `ANALYZE`
believes that the number of distinct values is likely to increase as the table
grows; the positive form is used when the column seems to have a fixed number
of possible values.) For example, -1 indicates a unique combination of columns
in which the number of distinct combinations is the same as the number of
rows.  
`dependencies` `pg_dependencies` Functional dependency statistics  
`most_common_vals` `text[]` A list of the most common combinations of values
in the columns. (Null if no combinations seem to be more common than any
others.)  
`most_common_val_nulls` `bool[]` A list of NULL flags for the most common
combinations of values. (Null when `most_common_vals` is.)  
`most_common_freqs` `float8[]` A list of the frequencies of the most common
combinations, i.e., number of occurrences of each divided by total number of
rows. (Null when `most_common_vals` is.)  
`most_common_base_freqs` `float8[]` A list of the base frequencies of the most
common combinations, i.e., product of per-value frequencies. (Null when
`most_common_vals` is.)  
  
  

The maximum number of entries in the array fields can be controlled on a
column-by-column basis using the [`ALTER TABLE SET STATISTICS`](sql-
altertable.html "ALTER TABLE") command, or globally by setting the
[default_statistics_target](runtime-config-query.html#GUC-DEFAULT-STATISTICS-
TARGET) run-time parameter.

* * *

[Prev](view-pg-stats.html "54.27. pg_stats")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-stats-ext-exprs.html "54.29. pg_stats_ext_exprs")  
---|---|---  
54.27. `pg_stats`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.29. `pg_stats_ext_exprs`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-stats-ext.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

