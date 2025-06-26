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

Supported Versions: [Current](/docs/current/catalog-pg-db-role-setting.html
"PostgreSQL 17 - 53.16. pg_db_role_setting") ([17](/docs/17/catalog-pg-db-
role-setting.html "PostgreSQL 17 - 53.16. pg_db_role_setting")) /
[16](/docs/16/catalog-pg-db-role-setting.html "PostgreSQL 16 -
53.16. pg_db_role_setting") / [15](/docs/15/catalog-pg-db-role-setting.html
"PostgreSQL 15 - 53.16. pg_db_role_setting") / [14](/docs/14/catalog-pg-db-
role-setting.html "PostgreSQL 14 - 53.16. pg_db_role_setting") /
[13](/docs/13/catalog-pg-db-role-setting.html "PostgreSQL 13 -
53.16. pg_db_role_setting")

Development Versions: [18](/docs/18/catalog-pg-db-role-setting.html
"PostgreSQL 18 - 53.16. pg_db_role_setting") / [devel](/docs/devel/catalog-pg-
db-role-setting.html "PostgreSQL devel - 53.16. pg_db_role_setting")

Unsupported versions: [12](/docs/12/catalog-pg-db-role-setting.html
"PostgreSQL 12 - 53.16. pg_db_role_setting") / [11](/docs/11/catalog-pg-db-
role-setting.html "PostgreSQL 11 - 53.16. pg_db_role_setting") /
[10](/docs/10/catalog-pg-db-role-setting.html "PostgreSQL 10 -
53.16. pg_db_role_setting") / [9.6](/docs/9.6/catalog-pg-db-role-setting.html
"PostgreSQL 9.6 - 53.16. pg_db_role_setting") / [9.5](/docs/9.5/catalog-pg-db-
role-setting.html "PostgreSQL 9.5 - 53.16. pg_db_role_setting") /
[9.4](/docs/9.4/catalog-pg-db-role-setting.html "PostgreSQL 9.4 -
53.16. pg_db_role_setting") / [9.3](/docs/9.3/catalog-pg-db-role-setting.html
"PostgreSQL 9.3 - 53.16. pg_db_role_setting") / [9.2](/docs/9.2/catalog-pg-db-
role-setting.html "PostgreSQL 9.2 - 53.16. pg_db_role_setting") /
[9.1](/docs/9.1/catalog-pg-db-role-setting.html "PostgreSQL 9.1 -
53.16. pg_db_role_setting") / [9.0](/docs/9.0/catalog-pg-db-role-setting.html
"PostgreSQL 9.0 - 53.16. pg_db_role_setting")

__

53.16. `pg_db_role_setting`  
---  
[Prev](catalog-pg-database.html "53.15. pg_database")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-default-acl.html "53.17. pg_default_acl")  
  
* * *

## 53.16. `pg_db_role_setting` #

The catalog `pg_db_role_setting` records the default values that have been set
for run-time configuration variables, for each role and database combination.

Unlike most system catalogs, `pg_db_role_setting` is shared across all
databases of a cluster: there is only one copy of `pg_db_role_setting` per
cluster, not one per database.

**Table  53.16. `pg_db_role_setting` Columns**

Column Type Description  
---  
`setdatabase` `oid` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`oid`) The OID of the database the setting is applicable
to, or zero if not database-specific  
`setrole` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) The OID of the role the setting is applicable to, or
zero if not role-specific  
`setconfig` `text[]` Defaults for run-time configuration variables  
  
  

* * *

[Prev](catalog-pg-database.html "53.15. pg_database")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-default-acl.html "53.17. pg_default_acl")  
---|---|---  
53.15. `pg_database`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.17. `pg_default_acl`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-db-role-
setting.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

