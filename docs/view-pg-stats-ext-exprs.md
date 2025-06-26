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

Supported Versions: [Current](/docs/current/view-pg-stats-ext-exprs.html
"PostgreSQL 17 - 54.29. pg_stats_ext_exprs") ([17](/docs/17/view-pg-stats-ext-
exprs.html "PostgreSQL 17 - 54.29. pg_stats_ext_exprs")) / [16](/docs/16/view-
pg-stats-ext-exprs.html "PostgreSQL 16 - 54.29. pg_stats_ext_exprs") /
[15](/docs/15/view-pg-stats-ext-exprs.html "PostgreSQL 15 -
54.29. pg_stats_ext_exprs") / [14](/docs/14/view-pg-stats-ext-exprs.html
"PostgreSQL 14 - 54.29. pg_stats_ext_exprs")

Development Versions: [18](/docs/18/view-pg-stats-ext-exprs.html "PostgreSQL
18 - 54.29. pg_stats_ext_exprs") / [devel](/docs/devel/view-pg-stats-ext-
exprs.html "PostgreSQL devel - 54.29. pg_stats_ext_exprs")

__

54.29. `pg_stats_ext_exprs`  
---  
[Prev](view-pg-stats-ext.html "54.28. pg_stats_ext")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-tables.html "54.30. pg_tables")  
  
* * *

## 54.29. `pg_stats_ext_exprs` #

The view `pg_stats_ext_exprs` provides access to information about all
expressions included in extended statistics objects, combining information
stored in the [`pg_statistic_ext`](catalog-pg-statistic-ext.html
"53.52. pg_statistic_ext") and [`pg_statistic_ext_data`](catalog-pg-statistic-
ext-data.html "53.53. pg_statistic_ext_data") catalogs. This view allows
access only to rows of [`pg_statistic_ext`](catalog-pg-statistic-ext.html
"53.52. pg_statistic_ext") and [`pg_statistic_ext_data`](catalog-pg-statistic-
ext-data.html "53.53. pg_statistic_ext_data") that correspond to tables the
user owns, and therefore it is safe to allow public read access to this view.

`pg_stats_ext_exprs` is also designed to present the information in a more
readable format than the underlying catalogs — at the cost that its schema
must be extended whenever the structure of statistics in `pg_statistic_ext`
changes.

**Table  54.29. `pg_stats_ext_exprs` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table the statistics object is defined
on  
`statistics_schemaname` `name` (references [`pg_namespace`](catalog-pg-
namespace.html "53.32. pg_namespace").`nspname`) Name of schema containing
extended statistics object  
`statistics_name` `name` (references [`pg_statistic_ext`](catalog-pg-
statistic-ext.html "53.52. pg_statistic_ext").`stxname`) Name of extended
statistics object  
`statistics_owner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Owner of the extended statistics object  
`expr` `text` Expression included in the extended statistics object  
`inherited` `bool` (references [`pg_statistic_ext_data`](catalog-pg-statistic-
ext-data.html "53.53. pg_statistic_ext_data").`stxdinherit`) If true, the
stats include values from child tables, not just the values in the specified
relation  
`null_frac` `float4` Fraction of expression entries that are null  
`avg_width` `int4` Average width in bytes of expression's entries  
`n_distinct` `float4` If greater than zero, the estimated number of distinct
values in the expression. If less than zero, the negative of the number of
distinct values divided by the number of rows. (The negated form is used when
`ANALYZE` believes that the number of distinct values is likely to increase as
the table grows; the positive form is used when the expression seems to have a
fixed number of possible values.) For example, -1 indicates a unique
expression in which the number of distinct values is the same as the number of
rows.  
`most_common_vals` `anyarray` A list of the most common values in the
expression. (Null if no values seem to be more common than any others.)  
`most_common_freqs` `float4[]` A list of the frequencies of the most common
values, i.e., number of occurrences of each divided by total number of rows.
(Null when `most_common_vals` is.)  
`histogram_bounds` `anyarray` A list of values that divide the expression's
values into groups of approximately equal population. The values in
`most_common_vals`, if present, are omitted from this histogram calculation.
(This expression is null if the expression data type does not have a `<`
operator or if the `most_common_vals` list accounts for the entire
population.)  
`correlation` `float4` Statistical correlation between physical row ordering
and logical ordering of the expression values. This ranges from -1 to +1. When
the value is near -1 or +1, an index scan on the expression will be estimated
to be cheaper than when it is near zero, due to reduction of random access to
the disk. (This expression is null if the expression's data type does not have
a `<` operator.)  
`most_common_elems` `anyarray` A list of non-null element values most often
appearing within values of the expression. (Null for scalar types.)  
`most_common_elem_freqs` `float4[]` A list of the frequencies of the most
common element values, i.e., the fraction of rows containing at least one
instance of the given value. Two or three additional values follow the per-
element frequencies; these are the minimum and maximum of the preceding per-
element frequencies, and optionally the frequency of null elements. (Null when
`most_common_elems` is.)  
`elem_count_histogram` `float4[]` A histogram of the counts of distinct non-
null element values within the values of the expression, followed by the
average number of distinct non-null elements. (Null for scalar types.)  
  
  

The maximum number of entries in the array fields can be controlled on a
column-by-column basis using the [`ALTER TABLE SET STATISTICS`](sql-
altertable.html "ALTER TABLE") command, or globally by setting the
[default_statistics_target](runtime-config-query.html#GUC-DEFAULT-STATISTICS-
TARGET) run-time parameter.

* * *

[Prev](view-pg-stats-ext.html "54.28. pg_stats_ext")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-tables.html "54.30. pg_tables")  
---|---|---  
54.28. `pg_stats_ext`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.30. `pg_tables`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-stats-ext-exprs.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

