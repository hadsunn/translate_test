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

Supported Versions: [Current](/docs/current/catalog-pg-tablespace.html
"PostgreSQL 17 - 53.56. pg_tablespace") ([17](/docs/17/catalog-pg-
tablespace.html "PostgreSQL 17 - 53.56. pg_tablespace")) /
[16](/docs/16/catalog-pg-tablespace.html "PostgreSQL 16 -
53.56. pg_tablespace") / [15](/docs/15/catalog-pg-tablespace.html "PostgreSQL
15 - 53.56. pg_tablespace") / [14](/docs/14/catalog-pg-tablespace.html
"PostgreSQL 14 - 53.56. pg_tablespace") / [13](/docs/13/catalog-pg-
tablespace.html "PostgreSQL 13 - 53.56. pg_tablespace")

Development Versions: [18](/docs/18/catalog-pg-tablespace.html "PostgreSQL 18
- 53.56. pg_tablespace") / [devel](/docs/devel/catalog-pg-tablespace.html
"PostgreSQL devel - 53.56. pg_tablespace")

Unsupported versions: [12](/docs/12/catalog-pg-tablespace.html "PostgreSQL 12
- 53.56. pg_tablespace") / [11](/docs/11/catalog-pg-tablespace.html
"PostgreSQL 11 - 53.56. pg_tablespace") / [10](/docs/10/catalog-pg-
tablespace.html "PostgreSQL 10 - 53.56. pg_tablespace") /
[9.6](/docs/9.6/catalog-pg-tablespace.html "PostgreSQL 9.6 -
53.56. pg_tablespace") / [9.5](/docs/9.5/catalog-pg-tablespace.html
"PostgreSQL 9.5 - 53.56. pg_tablespace") / [9.4](/docs/9.4/catalog-pg-
tablespace.html "PostgreSQL 9.4 - 53.56. pg_tablespace") /
[9.3](/docs/9.3/catalog-pg-tablespace.html "PostgreSQL 9.3 -
53.56. pg_tablespace") / [9.2](/docs/9.2/catalog-pg-tablespace.html
"PostgreSQL 9.2 - 53.56. pg_tablespace") / [9.1](/docs/9.1/catalog-pg-
tablespace.html "PostgreSQL 9.1 - 53.56. pg_tablespace") /
[9.0](/docs/9.0/catalog-pg-tablespace.html "PostgreSQL 9.0 -
53.56. pg_tablespace") / [8.4](/docs/8.4/catalog-pg-tablespace.html
"PostgreSQL 8.4 - 53.56. pg_tablespace") / [8.3](/docs/8.3/catalog-pg-
tablespace.html "PostgreSQL 8.3 - 53.56. pg_tablespace") /
[8.2](/docs/8.2/catalog-pg-tablespace.html "PostgreSQL 8.2 -
53.56. pg_tablespace") / [8.1](/docs/8.1/catalog-pg-tablespace.html
"PostgreSQL 8.1 - 53.56. pg_tablespace") / [8.0](/docs/8.0/catalog-pg-
tablespace.html "PostgreSQL 8.0 - 53.56. pg_tablespace")

__

53.56. `pg_tablespace`  
---  
[Prev](catalog-pg-subscription-rel.html "53.55. pg_subscription_rel")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-transform.html "53.57. pg_transform")  
  
* * *

## 53.56. `pg_tablespace` #

The catalog `pg_tablespace` stores information about the available
tablespaces. Tables can be placed in particular tablespaces to aid
administration of disk layout.

Unlike most system catalogs, `pg_tablespace` is shared across all databases of
a cluster: there is only one copy of `pg_tablespace` per cluster, not one per
database.

**Table  53.56. `pg_tablespace` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`spcname` `name` Tablespace name  
`spcowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the tablespace, usually the user who
created it  
`spcacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
`spcoptions` `text[]` Tablespace-level options, as “keyword=value” strings  
  
  

* * *

[Prev](catalog-pg-subscription-rel.html "53.55. pg_subscription_rel")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-transform.html "53.57. pg_transform")  
---|---|---  
53.55. `pg_subscription_rel`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.57. `pg_transform`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-tablespace.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

