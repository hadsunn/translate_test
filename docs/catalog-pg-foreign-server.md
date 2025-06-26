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

Supported Versions: [Current](/docs/current/catalog-pg-foreign-server.html
"PostgreSQL 17 - 53.24. pg_foreign_server") ([17](/docs/17/catalog-pg-foreign-
server.html "PostgreSQL 17 - 53.24. pg_foreign_server")) /
[16](/docs/16/catalog-pg-foreign-server.html "PostgreSQL 16 -
53.24. pg_foreign_server") / [15](/docs/15/catalog-pg-foreign-server.html
"PostgreSQL 15 - 53.24. pg_foreign_server") / [14](/docs/14/catalog-pg-
foreign-server.html "PostgreSQL 14 - 53.24. pg_foreign_server") /
[13](/docs/13/catalog-pg-foreign-server.html "PostgreSQL 13 -
53.24. pg_foreign_server")

Development Versions: [18](/docs/18/catalog-pg-foreign-server.html "PostgreSQL
18 - 53.24. pg_foreign_server") / [devel](/docs/devel/catalog-pg-foreign-
server.html "PostgreSQL devel - 53.24. pg_foreign_server")

Unsupported versions: [12](/docs/12/catalog-pg-foreign-server.html "PostgreSQL
12 - 53.24. pg_foreign_server") / [11](/docs/11/catalog-pg-foreign-server.html
"PostgreSQL 11 - 53.24. pg_foreign_server") / [10](/docs/10/catalog-pg-
foreign-server.html "PostgreSQL 10 - 53.24. pg_foreign_server") /
[9.6](/docs/9.6/catalog-pg-foreign-server.html "PostgreSQL 9.6 -
53.24. pg_foreign_server") / [9.5](/docs/9.5/catalog-pg-foreign-server.html
"PostgreSQL 9.5 - 53.24. pg_foreign_server") / [9.4](/docs/9.4/catalog-pg-
foreign-server.html "PostgreSQL 9.4 - 53.24. pg_foreign_server") /
[9.3](/docs/9.3/catalog-pg-foreign-server.html "PostgreSQL 9.3 -
53.24. pg_foreign_server") / [9.2](/docs/9.2/catalog-pg-foreign-server.html
"PostgreSQL 9.2 - 53.24. pg_foreign_server") / [9.1](/docs/9.1/catalog-pg-
foreign-server.html "PostgreSQL 9.1 - 53.24. pg_foreign_server") /
[9.0](/docs/9.0/catalog-pg-foreign-server.html "PostgreSQL 9.0 -
53.24. pg_foreign_server") / [8.4](/docs/8.4/catalog-pg-foreign-server.html
"PostgreSQL 8.4 - 53.24. pg_foreign_server")

__

53.24. `pg_foreign_server`  
---  
[Prev](catalog-pg-foreign-data-wrapper.html "53.23. pg_foreign_data_wrapper")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-foreign-table.html "53.25. pg_foreign_table")  
  
* * *

## 53.24. `pg_foreign_server` #

The catalog `pg_foreign_server` stores foreign server definitions. A foreign
server describes a source of external data, such as a remote server. Foreign
servers are accessed via foreign-data wrappers.

**Table  53.24. `pg_foreign_server` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`srvname` `name` Name of the foreign server  
`srvowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the foreign server  
`srvfdw` `oid` (references [`pg_foreign_data_wrapper`](catalog-pg-foreign-
data-wrapper.html "53.23. pg_foreign_data_wrapper").`oid`) OID of the foreign-
data wrapper of this foreign server  
`srvtype` `text` Type of the server (optional)  
`srvversion` `text` Version of the server (optional)  
`srvacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
`srvoptions` `text[]` Foreign server specific options, as “keyword=value”
strings  
  
  

* * *

[Prev](catalog-pg-foreign-data-wrapper.html "53.23. pg_foreign_data_wrapper")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-foreign-table.html "53.25. pg_foreign_table")  
---|---|---  
53.23. `pg_foreign_data_wrapper`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.25. `pg_foreign_table`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-foreign-
server.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

