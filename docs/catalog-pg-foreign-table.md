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

Supported Versions: [Current](/docs/current/catalog-pg-foreign-table.html
"PostgreSQL 17 - 53.25. pg_foreign_table") ([17](/docs/17/catalog-pg-foreign-
table.html "PostgreSQL 17 - 53.25. pg_foreign_table")) /
[16](/docs/16/catalog-pg-foreign-table.html "PostgreSQL 16 -
53.25. pg_foreign_table") / [15](/docs/15/catalog-pg-foreign-table.html
"PostgreSQL 15 - 53.25. pg_foreign_table") / [14](/docs/14/catalog-pg-foreign-
table.html "PostgreSQL 14 - 53.25. pg_foreign_table") / [13](/docs/13/catalog-
pg-foreign-table.html "PostgreSQL 13 - 53.25. pg_foreign_table")

Development Versions: [18](/docs/18/catalog-pg-foreign-table.html "PostgreSQL
18 - 53.25. pg_foreign_table") / [devel](/docs/devel/catalog-pg-foreign-
table.html "PostgreSQL devel - 53.25. pg_foreign_table")

Unsupported versions: [12](/docs/12/catalog-pg-foreign-table.html "PostgreSQL
12 - 53.25. pg_foreign_table") / [11](/docs/11/catalog-pg-foreign-table.html
"PostgreSQL 11 - 53.25. pg_foreign_table") / [10](/docs/10/catalog-pg-foreign-
table.html "PostgreSQL 10 - 53.25. pg_foreign_table") /
[9.6](/docs/9.6/catalog-pg-foreign-table.html "PostgreSQL 9.6 -
53.25. pg_foreign_table") / [9.5](/docs/9.5/catalog-pg-foreign-table.html
"PostgreSQL 9.5 - 53.25. pg_foreign_table") / [9.4](/docs/9.4/catalog-pg-
foreign-table.html "PostgreSQL 9.4 - 53.25. pg_foreign_table") /
[9.3](/docs/9.3/catalog-pg-foreign-table.html "PostgreSQL 9.3 -
53.25. pg_foreign_table") / [9.2](/docs/9.2/catalog-pg-foreign-table.html
"PostgreSQL 9.2 - 53.25. pg_foreign_table") / [9.1](/docs/9.1/catalog-pg-
foreign-table.html "PostgreSQL 9.1 - 53.25. pg_foreign_table")

__

53.25. `pg_foreign_table`  
---  
[Prev](catalog-pg-foreign-server.html "53.24. pg_foreign_server")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-index.html "53.26. pg_index")  
  
* * *

## 53.25. `pg_foreign_table` #

The catalog `pg_foreign_table` contains auxiliary information about foreign
tables. A foreign table is primarily represented by a [`pg_class`](catalog-pg-
class.html "53.11. pg_class") entry, just like a regular table. Its
`pg_foreign_table` entry contains the information that is pertinent only to
foreign tables and not any other kind of relation.

**Table  53.25. `pg_foreign_table` Columns**

Column Type Description  
---  
`ftrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry for this foreign table  
`ftserver` `oid` (references [`pg_foreign_server`](catalog-pg-foreign-
server.html "53.24. pg_foreign_server").`oid`) OID of the foreign server for
this foreign table  
`ftoptions` `text[]` Foreign table options, as “keyword=value” strings  
  
  

* * *

[Prev](catalog-pg-foreign-server.html "53.24. pg_foreign_server")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-index.html "53.26. pg_index")  
---|---|---  
53.24. `pg_foreign_server`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.26. `pg_index`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-foreign-
table.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

