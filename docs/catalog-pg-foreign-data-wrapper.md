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

Supported Versions: [Current](/docs/current/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 17 - 53.23. pg_foreign_data_wrapper")
([17](/docs/17/catalog-pg-foreign-data-wrapper.html "PostgreSQL 17 -
53.23. pg_foreign_data_wrapper")) / [16](/docs/16/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 16 - 53.23. pg_foreign_data_wrapper") /
[15](/docs/15/catalog-pg-foreign-data-wrapper.html "PostgreSQL 15 -
53.23. pg_foreign_data_wrapper") / [14](/docs/14/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 14 - 53.23. pg_foreign_data_wrapper") /
[13](/docs/13/catalog-pg-foreign-data-wrapper.html "PostgreSQL 13 -
53.23. pg_foreign_data_wrapper")

Development Versions: [18](/docs/18/catalog-pg-foreign-data-wrapper.html
"PostgreSQL 18 - 53.23. pg_foreign_data_wrapper") /
[devel](/docs/devel/catalog-pg-foreign-data-wrapper.html "PostgreSQL devel -
53.23. pg_foreign_data_wrapper")

Unsupported versions: [12](/docs/12/catalog-pg-foreign-data-wrapper.html
"PostgreSQL 12 - 53.23. pg_foreign_data_wrapper") / [11](/docs/11/catalog-pg-
foreign-data-wrapper.html "PostgreSQL 11 - 53.23. pg_foreign_data_wrapper") /
[10](/docs/10/catalog-pg-foreign-data-wrapper.html "PostgreSQL 10 -
53.23. pg_foreign_data_wrapper") / [9.6](/docs/9.6/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 9.6 - 53.23. pg_foreign_data_wrapper") /
[9.5](/docs/9.5/catalog-pg-foreign-data-wrapper.html "PostgreSQL 9.5 -
53.23. pg_foreign_data_wrapper") / [9.4](/docs/9.4/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 9.4 - 53.23. pg_foreign_data_wrapper") /
[9.3](/docs/9.3/catalog-pg-foreign-data-wrapper.html "PostgreSQL 9.3 -
53.23. pg_foreign_data_wrapper") / [9.2](/docs/9.2/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 9.2 - 53.23. pg_foreign_data_wrapper") /
[9.1](/docs/9.1/catalog-pg-foreign-data-wrapper.html "PostgreSQL 9.1 -
53.23. pg_foreign_data_wrapper") / [9.0](/docs/9.0/catalog-pg-foreign-data-
wrapper.html "PostgreSQL 9.0 - 53.23. pg_foreign_data_wrapper") /
[8.4](/docs/8.4/catalog-pg-foreign-data-wrapper.html "PostgreSQL 8.4 -
53.23. pg_foreign_data_wrapper")

__

53.23. `pg_foreign_data_wrapper`  
---  
[Prev](catalog-pg-extension.html "53.22. pg_extension")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-foreign-server.html "53.24. pg_foreign_server")  
  
* * *

## 53.23. `pg_foreign_data_wrapper` #

The catalog `pg_foreign_data_wrapper` stores foreign-data wrapper definitions.
A foreign-data wrapper is the mechanism by which external data, residing on
foreign servers, is accessed.

**Table  53.23. `pg_foreign_data_wrapper` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`fdwname` `name` Name of the foreign-data wrapper  
`fdwowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the foreign-data wrapper  
`fdwhandler` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) References a handler function that is responsible for
supplying execution routines for the foreign-data wrapper. Zero if no handler
is provided  
`fdwvalidator` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) References a validator function that is responsible
for checking the validity of the options given to the foreign-data wrapper, as
well as options for foreign servers and user mappings using the foreign-data
wrapper. Zero if no validator is provided  
`fdwacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
`fdwoptions` `text[]` Foreign-data wrapper specific options, as
“keyword=value” strings  
  
  

* * *

[Prev](catalog-pg-extension.html "53.22. pg_extension")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-foreign-server.html "53.24. pg_foreign_server")  
---|---|---  
53.22. `pg_extension`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.24. `pg_foreign_server`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-foreign-data-
wrapper.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

