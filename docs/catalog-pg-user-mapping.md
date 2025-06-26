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

Supported Versions: [Current](/docs/current/catalog-pg-user-mapping.html
"PostgreSQL 17 - 53.65. pg_user_mapping") ([17](/docs/17/catalog-pg-user-
mapping.html "PostgreSQL 17 - 53.65. pg_user_mapping")) /
[16](/docs/16/catalog-pg-user-mapping.html "PostgreSQL 16 -
53.65. pg_user_mapping") / [15](/docs/15/catalog-pg-user-mapping.html
"PostgreSQL 15 - 53.65. pg_user_mapping") / [14](/docs/14/catalog-pg-user-
mapping.html "PostgreSQL 14 - 53.65. pg_user_mapping") /
[13](/docs/13/catalog-pg-user-mapping.html "PostgreSQL 13 -
53.65. pg_user_mapping")

Development Versions: [18](/docs/18/catalog-pg-user-mapping.html "PostgreSQL
18 - 53.65. pg_user_mapping") / [devel](/docs/devel/catalog-pg-user-
mapping.html "PostgreSQL devel - 53.65. pg_user_mapping")

Unsupported versions: [12](/docs/12/catalog-pg-user-mapping.html "PostgreSQL
12 - 53.65. pg_user_mapping") / [11](/docs/11/catalog-pg-user-mapping.html
"PostgreSQL 11 - 53.65. pg_user_mapping") / [10](/docs/10/catalog-pg-user-
mapping.html "PostgreSQL 10 - 53.65. pg_user_mapping") /
[9.6](/docs/9.6/catalog-pg-user-mapping.html "PostgreSQL 9.6 -
53.65. pg_user_mapping") / [9.5](/docs/9.5/catalog-pg-user-mapping.html
"PostgreSQL 9.5 - 53.65. pg_user_mapping") / [9.4](/docs/9.4/catalog-pg-user-
mapping.html "PostgreSQL 9.4 - 53.65. pg_user_mapping") /
[9.3](/docs/9.3/catalog-pg-user-mapping.html "PostgreSQL 9.3 -
53.65. pg_user_mapping") / [9.2](/docs/9.2/catalog-pg-user-mapping.html
"PostgreSQL 9.2 - 53.65. pg_user_mapping") / [9.1](/docs/9.1/catalog-pg-user-
mapping.html "PostgreSQL 9.1 - 53.65. pg_user_mapping") /
[9.0](/docs/9.0/catalog-pg-user-mapping.html "PostgreSQL 9.0 -
53.65. pg_user_mapping") / [8.4](/docs/8.4/catalog-pg-user-mapping.html
"PostgreSQL 8.4 - 53.65. pg_user_mapping")

__

53.65. `pg_user_mapping`  
---  
[Prev](catalog-pg-type.html "53.64. pg_type")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](views.html "Chapter 54. System Views")  
  
* * *

## 53.65. `pg_user_mapping` #

The catalog `pg_user_mapping` stores the mappings from local user to remote.
Access to this catalog is restricted from normal users, use the view
[`pg_user_mappings`](view-pg-user-mappings.html "54.34. pg_user_mappings")
instead.

**Table  53.66. `pg_user_mapping` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`umuser` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) OID of the local role being mapped, or zero if the
user mapping is public  
`umserver` `oid` (references [`pg_foreign_server`](catalog-pg-foreign-
server.html "53.24. pg_foreign_server").`oid`) The OID of the foreign server
that contains this mapping  
`umoptions` `text[]` User mapping specific options, as “keyword=value” strings  
  
  

* * *

[Prev](catalog-pg-type.html "53.64. pg_type")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](views.html "Chapter 54. System Views")  
---|---|---  
53.64. `pg_type`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 54. System Views  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-user-mapping.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

