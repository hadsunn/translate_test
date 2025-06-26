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

Supported Versions: [Current](/docs/current/catalog-pg-statistic.html
"PostgreSQL 17 - 53.51. pg_statistic") ([17](/docs/17/catalog-pg-
statistic.html "PostgreSQL 17 - 53.51. pg_statistic")) /
[16](/docs/16/catalog-pg-statistic.html "PostgreSQL 16 - 53.51. pg_statistic")
/ [15](/docs/15/catalog-pg-statistic.html "PostgreSQL 15 -
53.51. pg_statistic") / [14](/docs/14/catalog-pg-statistic.html "PostgreSQL 14
- 53.51. pg_statistic") / [13](/docs/13/catalog-pg-statistic.html "PostgreSQL
13 - 53.51. pg_statistic")

Development Versions: [18](/docs/18/catalog-pg-statistic.html "PostgreSQL 18 -
53.51. pg_statistic") / [devel](/docs/devel/catalog-pg-statistic.html
"PostgreSQL devel - 53.51. pg_statistic")

Unsupported versions: [12](/docs/12/catalog-pg-statistic.html "PostgreSQL 12 -
53.51. pg_statistic") / [11](/docs/11/catalog-pg-statistic.html "PostgreSQL 11
- 53.51. pg_statistic") / [10](/docs/10/catalog-pg-statistic.html "PostgreSQL
10 - 53.51. pg_statistic") / [9.6](/docs/9.6/catalog-pg-statistic.html
"PostgreSQL 9.6 - 53.51. pg_statistic") / [9.5](/docs/9.5/catalog-pg-
statistic.html "PostgreSQL 9.5 - 53.51. pg_statistic") /
[9.4](/docs/9.4/catalog-pg-statistic.html "PostgreSQL 9.4 -
53.51. pg_statistic") / [9.3](/docs/9.3/catalog-pg-statistic.html "PostgreSQL
9.3 - 53.51. pg_statistic") / [9.2](/docs/9.2/catalog-pg-statistic.html
"PostgreSQL 9.2 - 53.51. pg_statistic") / [9.1](/docs/9.1/catalog-pg-
statistic.html "PostgreSQL 9.1 - 53.51. pg_statistic") /
[9.0](/docs/9.0/catalog-pg-statistic.html "PostgreSQL 9.0 -
53.51. pg_statistic") / [8.4](/docs/8.4/catalog-pg-statistic.html "PostgreSQL
8.4 - 53.51. pg_statistic") / [8.3](/docs/8.3/catalog-pg-statistic.html
"PostgreSQL 8.3 - 53.51. pg_statistic") / [8.2](/docs/8.2/catalog-pg-
statistic.html "PostgreSQL 8.2 - 53.51. pg_statistic") /
[8.1](/docs/8.1/catalog-pg-statistic.html "PostgreSQL 8.1 -
53.51. pg_statistic") / [8.0](/docs/8.0/catalog-pg-statistic.html "PostgreSQL
8.0 - 53.51. pg_statistic") / [7.4](/docs/7.4/catalog-pg-statistic.html
"PostgreSQL 7.4 - 53.51. pg_statistic") / [7.3](/docs/7.3/catalog-pg-
statistic.html "PostgreSQL 7.3 - 53.51. pg_statistic") /
[7.2](/docs/7.2/catalog-pg-statistic.html "PostgreSQL 7.2 -
53.51. pg_statistic")

__

53.51. `pg_statistic`  
---  
[Prev](catalog-pg-shseclabel.html "53.50. pg_shseclabel")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-statistic-ext.html "53.52. pg_statistic_ext")  
  
* * *

## 53.51. `pg_statistic` #

The catalog `pg_statistic` stores statistical data about the contents of the
database. Entries are created by [`ANALYZE`](sql-analyze.html "ANALYZE") and
subsequently used by the query planner. Note that all the statistical data is
inherently approximate, even assuming that it is up-to-date.

Normally there is one entry, with `stainherit` = `false`, for each table
column that has been analyzed. If the table has inheritance children or
partitions, a second entry with `stainherit` = `true` is also created. This
row represents the column's statistics over the inheritance tree, i.e.,
statistics for the data you'd see with `SELECT _`column`_ FROM _`table`_ *`,
whereas the `stainherit` = `false` row represents the results of `SELECT
_`column`_ FROM ONLY _`table`_`.

`pg_statistic` also stores statistical data about the values of index
expressions. These are described as if they were actual data columns; in
particular, `starelid` references the index. No entry is made for an ordinary
non-expression index column, however, since it would be redundant with the
entry for the underlying table column. Currently, entries for index
expressions always have `stainherit` = `false`.

Since different kinds of statistics might be appropriate for different kinds
of data, `pg_statistic` is designed not to assume very much about what sort of
statistics it stores. Only extremely general statistics (such as nullness) are
given dedicated columns in `pg_statistic`. Everything else is stored in
“slots”, which are groups of associated columns whose content is identified by
a code number in one of the slot's columns. For more information see
`src/include/catalog/pg_statistic.h`.

`pg_statistic` should not be readable by the public, since even statistical
information about a table's contents might be considered sensitive. (Example:
minimum and maximum values of a salary column might be quite interesting.)
[`pg_stats`](view-pg-stats.html "54.27. pg_stats") is a publicly readable view
on `pg_statistic` that only exposes information about those tables that are
readable by the current user.

**Table  53.51. `pg_statistic` Columns**

Column Type Description  
---  
`starelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table or index that the described column belongs
to  
`staattnum` `int2` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attnum`) The number of the described column  
`stainherit` `bool` If true, the stats include values from child tables, not
just the values in the specified relation  
`stanullfrac` `float4` The fraction of the column's entries that are null  
`stawidth` `int4` The average stored width, in bytes, of nonnull entries  
`stadistinct` `float4` The number of distinct nonnull data values in the
column. A value greater than zero is the actual number of distinct values. A
value less than zero is the negative of a multiplier for the number of rows in
the table; for example, a column in which about 80% of the values are nonnull
and each nonnull value appears about twice on average could be represented by
`stadistinct` = -0.4. A zero value means the number of distinct values is
unknown.  
`stakind _`N`_` `int2` A code number indicating the kind of statistics stored
in the _`N`_ th “slot” of the `pg_statistic` row.  
`staop _`N`_` `oid` (references [`pg_operator`](catalog-pg-operator.html
"53.34. pg_operator").`oid`) An operator used to derive the statistics stored
in the _`N`_ th “slot”. For example, a histogram slot would show the `<`
operator that defines the sort order of the data. Zero if the statistics kind
does not require an operator.  
`stacoll _`N`_` `oid` (references [`pg_collation`](catalog-pg-collation.html
"53.12. pg_collation").`oid`) The collation used to derive the statistics
stored in the _`N`_ th “slot”. For example, a histogram slot for a collatable
column would show the collation that defines the sort order of the data. Zero
for noncollatable data.  
`stanumbers _`N`_` `float4[]` Numerical statistics of the appropriate kind for
the _`N`_ th “slot”, or null if the slot kind does not involve numerical
values  
`stavalues _`N`_` `anyarray` Column data values of the appropriate kind for
the _`N`_ th “slot”, or null if the slot kind does not store any data values.
Each array's element values are actually of the specific column's data type,
or a related type such as an array's element type, so there is no way to
define these columns' type more specifically than `anyarray`.  
  
  

* * *

[Prev](catalog-pg-shseclabel.html "53.50. pg_shseclabel")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-statistic-ext.html "53.52. pg_statistic_ext")  
---|---|---  
53.50. `pg_shseclabel`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.52. `pg_statistic_ext`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-statistic.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

