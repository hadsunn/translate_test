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

Supported Versions: [Current](/docs/current/catalog-pg-replication-origin.html
"PostgreSQL 17 - 53.44. pg_replication_origin") ([17](/docs/17/catalog-pg-
replication-origin.html "PostgreSQL 17 - 53.44. pg_replication_origin")) /
[16](/docs/16/catalog-pg-replication-origin.html "PostgreSQL 16 -
53.44. pg_replication_origin") / [15](/docs/15/catalog-pg-replication-
origin.html "PostgreSQL 15 - 53.44. pg_replication_origin") /
[14](/docs/14/catalog-pg-replication-origin.html "PostgreSQL 14 -
53.44. pg_replication_origin") / [13](/docs/13/catalog-pg-replication-
origin.html "PostgreSQL 13 - 53.44. pg_replication_origin")

Development Versions: [18](/docs/18/catalog-pg-replication-origin.html
"PostgreSQL 18 - 53.44. pg_replication_origin") / [devel](/docs/devel/catalog-
pg-replication-origin.html "PostgreSQL devel - 53.44. pg_replication_origin")

Unsupported versions: [12](/docs/12/catalog-pg-replication-origin.html
"PostgreSQL 12 - 53.44. pg_replication_origin") / [11](/docs/11/catalog-pg-
replication-origin.html "PostgreSQL 11 - 53.44. pg_replication_origin") /
[10](/docs/10/catalog-pg-replication-origin.html "PostgreSQL 10 -
53.44. pg_replication_origin") / [9.6](/docs/9.6/catalog-pg-replication-
origin.html "PostgreSQL 9.6 - 53.44. pg_replication_origin") /
[9.5](/docs/9.5/catalog-pg-replication-origin.html "PostgreSQL 9.5 -
53.44. pg_replication_origin")

__

53.44. `pg_replication_origin`  
---  
[Prev](catalog-pg-range.html "53.43. pg_range")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-rewrite.html "53.45. pg_rewrite")  
  
* * *

## 53.44. `pg_replication_origin` #

The `pg_replication_origin` catalog contains all replication origins created.
For more on replication origins see [Chapter 50](replication-origins.html
"Chapter 50. Replication Progress Tracking").

Unlike most system catalogs, `pg_replication_origin` is shared across all
databases of a cluster: there is only one copy of `pg_replication_origin` per
cluster, not one per database.

**Table  53.44. `pg_replication_origin` Columns**

Column Type Description  
---  
`roident` `oid` A unique, cluster-wide identifier for the replication origin.
Should never leave the system.  
`roname` `text` The external, user defined, name of a replication origin.  
  
  

* * *

[Prev](catalog-pg-range.html "53.43. pg_range")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-rewrite.html "53.45. pg_rewrite")  
---|---|---  
53.43. `pg_range`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.45. `pg_rewrite`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-replication-
origin.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

