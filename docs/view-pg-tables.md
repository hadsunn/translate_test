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

Supported Versions: [Current](/docs/current/view-pg-tables.html "PostgreSQL 17
- 54.30. pg_tables") ([17](/docs/17/view-pg-tables.html "PostgreSQL 17 -
54.30. pg_tables")) / [16](/docs/16/view-pg-tables.html "PostgreSQL 16 -
54.30. pg_tables") / [15](/docs/15/view-pg-tables.html "PostgreSQL 15 -
54.30. pg_tables") / [14](/docs/14/view-pg-tables.html "PostgreSQL 14 -
54.30. pg_tables") / [13](/docs/13/view-pg-tables.html "PostgreSQL 13 -
54.30. pg_tables")

Development Versions: [18](/docs/18/view-pg-tables.html "PostgreSQL 18 -
54.30. pg_tables") / [devel](/docs/devel/view-pg-tables.html "PostgreSQL devel
- 54.30. pg_tables")

Unsupported versions: [12](/docs/12/view-pg-tables.html "PostgreSQL 12 -
54.30. pg_tables") / [11](/docs/11/view-pg-tables.html "PostgreSQL 11 -
54.30. pg_tables") / [10](/docs/10/view-pg-tables.html "PostgreSQL 10 -
54.30. pg_tables") / [9.6](/docs/9.6/view-pg-tables.html "PostgreSQL 9.6 -
54.30. pg_tables") / [9.5](/docs/9.5/view-pg-tables.html "PostgreSQL 9.5 -
54.30. pg_tables") / [9.4](/docs/9.4/view-pg-tables.html "PostgreSQL 9.4 -
54.30. pg_tables") / [9.3](/docs/9.3/view-pg-tables.html "PostgreSQL 9.3 -
54.30. pg_tables") / [9.2](/docs/9.2/view-pg-tables.html "PostgreSQL 9.2 -
54.30. pg_tables") / [9.1](/docs/9.1/view-pg-tables.html "PostgreSQL 9.1 -
54.30. pg_tables") / [9.0](/docs/9.0/view-pg-tables.html "PostgreSQL 9.0 -
54.30. pg_tables") / [8.4](/docs/8.4/view-pg-tables.html "PostgreSQL 8.4 -
54.30. pg_tables") / [8.3](/docs/8.3/view-pg-tables.html "PostgreSQL 8.3 -
54.30. pg_tables") / [8.2](/docs/8.2/view-pg-tables.html "PostgreSQL 8.2 -
54.30. pg_tables") / [8.1](/docs/8.1/view-pg-tables.html "PostgreSQL 8.1 -
54.30. pg_tables") / [8.0](/docs/8.0/view-pg-tables.html "PostgreSQL 8.0 -
54.30. pg_tables") / [7.4](/docs/7.4/view-pg-tables.html "PostgreSQL 7.4 -
54.30. pg_tables")

__

54.30. `pg_tables`  
---  
[Prev](view-pg-stats-ext-exprs.html "54.29. pg_stats_ext_exprs")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-timezone-abbrevs.html "54.31. pg_timezone_abbrevs")  
  
* * *

## 54.30. `pg_tables` #

The view `pg_tables` provides access to useful information about each table in
the database.

**Table  54.30. `pg_tables` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table  
`tableowner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Name of table's owner  
`tablespace` `name` (references [`pg_tablespace`](catalog-pg-tablespace.html
"53.56. pg_tablespace").`spcname`) Name of tablespace containing table (null
if default for database)  
`hasindexes` `bool` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relhasindex`) True if table has (or recently had) any
indexes  
`hasrules` `bool` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relhasrules`) True if table has (or once had) rules  
`hastriggers` `bool` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relhastriggers`) True if table has (or once had) triggers  
`rowsecurity` `bool` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relrowsecurity`) True if row security is enabled on the
table  
  
  

* * *

[Prev](view-pg-stats-ext-exprs.html "54.29. pg_stats_ext_exprs")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-timezone-abbrevs.html "54.31. pg_timezone_abbrevs")  
---|---|---  
54.29. `pg_stats_ext_exprs`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.31. `pg_timezone_abbrevs`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-tables.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

