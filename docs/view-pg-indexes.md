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

Supported Versions: [Current](/docs/current/view-pg-indexes.html "PostgreSQL
17 - 54.11. pg_indexes") ([17](/docs/17/view-pg-indexes.html "PostgreSQL 17 -
54.11. pg_indexes")) / [16](/docs/16/view-pg-indexes.html "PostgreSQL 16 -
54.11. pg_indexes") / [15](/docs/15/view-pg-indexes.html "PostgreSQL 15 -
54.11. pg_indexes") / [14](/docs/14/view-pg-indexes.html "PostgreSQL 14 -
54.11. pg_indexes") / [13](/docs/13/view-pg-indexes.html "PostgreSQL 13 -
54.11. pg_indexes")

Development Versions: [18](/docs/18/view-pg-indexes.html "PostgreSQL 18 -
54.11. pg_indexes") / [devel](/docs/devel/view-pg-indexes.html "PostgreSQL
devel - 54.11. pg_indexes")

Unsupported versions: [12](/docs/12/view-pg-indexes.html "PostgreSQL 12 -
54.11. pg_indexes") / [11](/docs/11/view-pg-indexes.html "PostgreSQL 11 -
54.11. pg_indexes") / [10](/docs/10/view-pg-indexes.html "PostgreSQL 10 -
54.11. pg_indexes") / [9.6](/docs/9.6/view-pg-indexes.html "PostgreSQL 9.6 -
54.11. pg_indexes") / [9.5](/docs/9.5/view-pg-indexes.html "PostgreSQL 9.5 -
54.11. pg_indexes") / [9.4](/docs/9.4/view-pg-indexes.html "PostgreSQL 9.4 -
54.11. pg_indexes") / [9.3](/docs/9.3/view-pg-indexes.html "PostgreSQL 9.3 -
54.11. pg_indexes") / [9.2](/docs/9.2/view-pg-indexes.html "PostgreSQL 9.2 -
54.11. pg_indexes") / [9.1](/docs/9.1/view-pg-indexes.html "PostgreSQL 9.1 -
54.11. pg_indexes") / [9.0](/docs/9.0/view-pg-indexes.html "PostgreSQL 9.0 -
54.11. pg_indexes") / [8.4](/docs/8.4/view-pg-indexes.html "PostgreSQL 8.4 -
54.11. pg_indexes") / [8.3](/docs/8.3/view-pg-indexes.html "PostgreSQL 8.3 -
54.11. pg_indexes") / [8.2](/docs/8.2/view-pg-indexes.html "PostgreSQL 8.2 -
54.11. pg_indexes") / [8.1](/docs/8.1/view-pg-indexes.html "PostgreSQL 8.1 -
54.11. pg_indexes") / [8.0](/docs/8.0/view-pg-indexes.html "PostgreSQL 8.0 -
54.11. pg_indexes") / [7.4](/docs/7.4/view-pg-indexes.html "PostgreSQL 7.4 -
54.11. pg_indexes")

__

54.11. `pg_indexes`  
---  
[Prev](view-pg-ident-file-mappings.html "54.10. pg_ident_file_mappings")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-locks.html "54.12. pg_locks")  
  
* * *

## 54.11. `pg_indexes` #

The view `pg_indexes` provides access to useful information about each index
in the database.

**Table  54.11. `pg_indexes` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table and index  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table the index is for  
`indexname` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of index  
`tablespace` `name` (references [`pg_tablespace`](catalog-pg-tablespace.html
"53.56. pg_tablespace").`spcname`) Name of tablespace containing index (null
if default for database)  
`indexdef` `text` Index definition (a reconstructed [CREATE INDEX](sql-
createindex.html "CREATE INDEX") command)  
  
  

* * *

[Prev](view-pg-ident-file-mappings.html "54.10. pg_ident_file_mappings")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-locks.html "54.12. pg_locks")  
---|---|---  
54.10. `pg_ident_file_mappings`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.12. `pg_locks`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-indexes.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

