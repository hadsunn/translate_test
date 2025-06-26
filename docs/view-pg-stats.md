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

Supported Versions: [Current](/docs/current/view-pg-stats.html "PostgreSQL 17
- 54.27. pg_stats") ([17](/docs/17/view-pg-stats.html "PostgreSQL 17 -
54.27. pg_stats")) / [16](/docs/16/view-pg-stats.html "PostgreSQL 16 -
54.27. pg_stats") / [15](/docs/15/view-pg-stats.html "PostgreSQL 15 -
54.27. pg_stats") / [14](/docs/14/view-pg-stats.html "PostgreSQL 14 -
54.27. pg_stats") / [13](/docs/13/view-pg-stats.html "PostgreSQL 13 -
54.27. pg_stats")

Development Versions: [18](/docs/18/view-pg-stats.html "PostgreSQL 18 -
54.27. pg_stats") / [devel](/docs/devel/view-pg-stats.html "PostgreSQL devel -
54.27. pg_stats")

Unsupported versions: [12](/docs/12/view-pg-stats.html "PostgreSQL 12 -
54.27. pg_stats") / [11](/docs/11/view-pg-stats.html "PostgreSQL 11 -
54.27. pg_stats") / [10](/docs/10/view-pg-stats.html "PostgreSQL 10 -
54.27. pg_stats") / [9.6](/docs/9.6/view-pg-stats.html "PostgreSQL 9.6 -
54.27. pg_stats") / [9.5](/docs/9.5/view-pg-stats.html "PostgreSQL 9.5 -
54.27. pg_stats") / [9.4](/docs/9.4/view-pg-stats.html "PostgreSQL 9.4 -
54.27. pg_stats") / [9.3](/docs/9.3/view-pg-stats.html "PostgreSQL 9.3 -
54.27. pg_stats") / [9.2](/docs/9.2/view-pg-stats.html "PostgreSQL 9.2 -
54.27. pg_stats") / [9.1](/docs/9.1/view-pg-stats.html "PostgreSQL 9.1 -
54.27. pg_stats") / [9.0](/docs/9.0/view-pg-stats.html "PostgreSQL 9.0 -
54.27. pg_stats") / [8.4](/docs/8.4/view-pg-stats.html "PostgreSQL 8.4 -
54.27. pg_stats") / [8.3](/docs/8.3/view-pg-stats.html "PostgreSQL 8.3 -
54.27. pg_stats") / [8.2](/docs/8.2/view-pg-stats.html "PostgreSQL 8.2 -
54.27. pg_stats") / [8.1](/docs/8.1/view-pg-stats.html "PostgreSQL 8.1 -
54.27. pg_stats") / [8.0](/docs/8.0/view-pg-stats.html "PostgreSQL 8.0 -
54.27. pg_stats") / [7.4](/docs/7.4/view-pg-stats.html "PostgreSQL 7.4 -
54.27. pg_stats")

__

54.27. `pg_stats`  
---  
[Prev](view-pg-shmem-allocations.html "54.26. pg_shmem_allocations")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-stats-ext.html "54.28. pg_stats_ext")  
  
* * *

## 54.27. `pg_stats` #

The view `pg_stats` provides access to the information stored in the
[`pg_statistic`](catalog-pg-statistic.html "53.51. pg_statistic") catalog.
This view allows access only to rows of [`pg_statistic`](catalog-pg-
statistic.html "53.51. pg_statistic") that correspond to tables the user has
permission to read, and therefore it is safe to allow public read access to
this view.

`pg_stats` is also designed to present the information in a more readable
format than the underlying catalog — at the cost that its schema must be
extended whenever new slot types are defined for [`pg_statistic`](catalog-pg-
statistic.html "53.51. pg_statistic").

**Table  54.27. `pg_stats` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table  
`attname` `name` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attname`) Name of column described by this row  
`inherited` `bool` If true, this row includes values from child tables, not
just the values in the specified table  
`null_frac` `float4` Fraction of column entries that are null  
`avg_width` `int4` Average width in bytes of column's entries  
`n_distinct` `float4` If greater than zero, the estimated number of distinct
values in the column. If less than zero, the negative of the number of
distinct values divided by the number of rows. (The negated form is used when
`ANALYZE` believes that the number of distinct values is likely to increase as
the table grows; the positive form is used when the column seems to have a
fixed number of possible values.) For example, -1 indicates a unique column in
which the number of distinct values is the same as the number of rows.  
`most_common_vals` `anyarray` A list of the most common values in the column.
(Null if no values seem to be more common than any others.)  
`most_common_freqs` `float4[]` A list of the frequencies of the most common
values, i.e., number of occurrences of each divided by total number of rows.
(Null when `most_common_vals` is.)  
`histogram_bounds` `anyarray` A list of values that divide the column's values
into groups of approximately equal population. The values in
`most_common_vals`, if present, are omitted from this histogram calculation.
(This column is null if the column data type does not have a `<` operator or
if the `most_common_vals` list accounts for the entire population.)  
`correlation` `float4` Statistical correlation between physical row ordering
and logical ordering of the column values. This ranges from -1 to +1. When the
value is near -1 or +1, an index scan on the column will be estimated to be
cheaper than when it is near zero, due to reduction of random access to the
disk. (This column is null if the column data type does not have a `<`
operator.)  
`most_common_elems` `anyarray` A list of non-null element values most often
appearing within values of the column. (Null for scalar types.)  
`most_common_elem_freqs` `float4[]` A list of the frequencies of the most
common element values, i.e., the fraction of rows containing at least one
instance of the given value. Two or three additional values follow the per-
element frequencies; these are the minimum and maximum of the preceding per-
element frequencies, and optionally the frequency of null elements. (Null when
`most_common_elems` is.)  
`elem_count_histogram` `float4[]` A histogram of the counts of distinct non-
null element values within the values of the column, followed by the average
number of distinct non-null elements. (Null for scalar types.)  
  
  

The maximum number of entries in the array fields can be controlled on a
column-by-column basis using the [`ALTER TABLE SET STATISTICS`](sql-
altertable.html "ALTER TABLE") command, or globally by setting the
[default_statistics_target](runtime-config-query.html#GUC-DEFAULT-STATISTICS-
TARGET) run-time parameter.

* * *

[Prev](view-pg-shmem-allocations.html "54.26. pg_shmem_allocations")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-stats-ext.html "54.28. pg_stats_ext")  
---|---|---  
54.26. `pg_shmem_allocations`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.28. `pg_stats_ext`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-stats.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

