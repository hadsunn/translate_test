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

Supported Versions: [Current](/docs/current/view-pg-matviews.html "PostgreSQL
17 - 54.13. pg_matviews") ([17](/docs/17/view-pg-matviews.html "PostgreSQL 17
- 54.13. pg_matviews")) / [16](/docs/16/view-pg-matviews.html "PostgreSQL 16 -
54.13. pg_matviews") / [15](/docs/15/view-pg-matviews.html "PostgreSQL 15 -
54.13. pg_matviews") / [14](/docs/14/view-pg-matviews.html "PostgreSQL 14 -
54.13. pg_matviews") / [13](/docs/13/view-pg-matviews.html "PostgreSQL 13 -
54.13. pg_matviews")

Development Versions: [18](/docs/18/view-pg-matviews.html "PostgreSQL 18 -
54.13. pg_matviews") / [devel](/docs/devel/view-pg-matviews.html "PostgreSQL
devel - 54.13. pg_matviews")

Unsupported versions: [12](/docs/12/view-pg-matviews.html "PostgreSQL 12 -
54.13. pg_matviews") / [11](/docs/11/view-pg-matviews.html "PostgreSQL 11 -
54.13. pg_matviews") / [10](/docs/10/view-pg-matviews.html "PostgreSQL 10 -
54.13. pg_matviews") / [9.6](/docs/9.6/view-pg-matviews.html "PostgreSQL 9.6 -
54.13. pg_matviews") / [9.5](/docs/9.5/view-pg-matviews.html "PostgreSQL 9.5 -
54.13. pg_matviews") / [9.4](/docs/9.4/view-pg-matviews.html "PostgreSQL 9.4 -
54.13. pg_matviews") / [9.3](/docs/9.3/view-pg-matviews.html "PostgreSQL 9.3 -
54.13. pg_matviews")

__

54.13. `pg_matviews`  
---  
[Prev](view-pg-locks.html "54.12. pg_locks")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-policies.html "54.14. pg_policies")  
  
* * *

## 54.13. `pg_matviews` #

The view `pg_matviews` provides access to useful information about each
materialized view in the database.

**Table  54.13. `pg_matviews` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing materialized view  
`matviewname` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of materialized view  
`matviewowner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Name of materialized view's owner  
`tablespace` `name` (references [`pg_tablespace`](catalog-pg-tablespace.html
"53.56. pg_tablespace").`spcname`) Name of tablespace containing materialized
view (null if default for database)  
`hasindexes` `bool` True if materialized view has (or recently had) any
indexes  
`ispopulated` `bool` True if materialized view is currently populated  
`definition` `text` Materialized view definition (a reconstructed
[SELECT](sql-select.html "SELECT") query)  
  
  

* * *

[Prev](view-pg-locks.html "54.12. pg_locks")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-policies.html "54.14. pg_policies")  
---|---|---  
54.12. `pg_locks`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.14. `pg_policies`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-matviews.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

