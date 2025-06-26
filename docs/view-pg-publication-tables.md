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

Supported Versions: [Current](/docs/current/view-pg-publication-tables.html
"PostgreSQL 17 - 54.17. pg_publication_tables") ([17](/docs/17/view-pg-
publication-tables.html "PostgreSQL 17 - 54.17. pg_publication_tables")) /
[16](/docs/16/view-pg-publication-tables.html "PostgreSQL 16 -
54.17. pg_publication_tables") / [15](/docs/15/view-pg-publication-tables.html
"PostgreSQL 15 - 54.17. pg_publication_tables") / [14](/docs/14/view-pg-
publication-tables.html "PostgreSQL 14 - 54.17. pg_publication_tables") /
[13](/docs/13/view-pg-publication-tables.html "PostgreSQL 13 -
54.17. pg_publication_tables")

Development Versions: [18](/docs/18/view-pg-publication-tables.html
"PostgreSQL 18 - 54.17. pg_publication_tables") / [devel](/docs/devel/view-pg-
publication-tables.html "PostgreSQL devel - 54.17. pg_publication_tables")

Unsupported versions: [12](/docs/12/view-pg-publication-tables.html
"PostgreSQL 12 - 54.17. pg_publication_tables") / [11](/docs/11/view-pg-
publication-tables.html "PostgreSQL 11 - 54.17. pg_publication_tables") /
[10](/docs/10/view-pg-publication-tables.html "PostgreSQL 10 -
54.17. pg_publication_tables")

__

54.17. `pg_publication_tables`  
---  
[Prev](view-pg-prepared-xacts.html "54.16. pg_prepared_xacts")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-replication-origin-status.html "54.18. pg_replication_origin_status")  
  
* * *

## 54.17. `pg_publication_tables` #

The view `pg_publication_tables` provides information about the mapping
between publications and information of tables they contain. Unlike the
underlying catalog [`pg_publication_rel`](catalog-pg-publication-rel.html
"53.42. pg_publication_rel"), this view expands publications defined as [`FOR
ALL TABLES`](sql-createpublication.html#SQL-CREATEPUBLICATION-FOR-ALL-TABLES)
and [`FOR TABLES IN SCHEMA`](sql-createpublication.html#SQL-CREATEPUBLICATION-
FOR-TABLES-IN-SCHEMA), so for such publications there will be a row for each
eligible table.

**Table  54.17. `pg_publication_tables` Columns**

Column Type Description  
---  
`pubname` `name` (references [`pg_publication`](catalog-pg-publication.html
"53.40. pg_publication").`pubname`) Name of publication  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table  
`attnames` `name[]` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attname`) Names of table columns included in the
publication. This contains all the columns of the table when the user didn't
specify the column list for the table.  
`rowfilter` `text` Expression for the table's publication qualifying condition  
  
  

* * *

[Prev](view-pg-prepared-xacts.html "54.16. pg_prepared_xacts")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-replication-origin-status.html "54.18. pg_replication_origin_status")  
---|---|---  
54.16. `pg_prepared_xacts`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.18. `pg_replication_origin_status`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-publication-
tables.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

