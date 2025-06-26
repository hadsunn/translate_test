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

Supported Versions: [Current](/docs/current/catalog-pg-publication-
namespace.html "PostgreSQL 17 - 53.41. pg_publication_namespace")
([17](/docs/17/catalog-pg-publication-namespace.html "PostgreSQL 17 -
53.41. pg_publication_namespace")) / [16](/docs/16/catalog-pg-publication-
namespace.html "PostgreSQL 16 - 53.41. pg_publication_namespace") /
[15](/docs/15/catalog-pg-publication-namespace.html "PostgreSQL 15 -
53.41. pg_publication_namespace")

Development Versions: [18](/docs/18/catalog-pg-publication-namespace.html
"PostgreSQL 18 - 53.41. pg_publication_namespace") /
[devel](/docs/devel/catalog-pg-publication-namespace.html "PostgreSQL devel -
53.41. pg_publication_namespace")

__

53.41. `pg_publication_namespace`  
---  
[Prev](catalog-pg-publication.html "53.40. pg_publication")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-publication-rel.html "53.42. pg_publication_rel")  
  
* * *

## 53.41. `pg_publication_namespace` #

The catalog `pg_publication_namespace` contains the mapping between schemas
and publications in the database. This is a many-to-many mapping.

**Table  53.41. `pg_publication_namespace` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`pnpubid` `oid` (references [`pg_publication`](catalog-pg-publication.html
"53.40. pg_publication").`oid`) Reference to publication  
`pnnspid` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) Reference to schema  
  
  

* * *

[Prev](catalog-pg-publication.html "53.40. pg_publication")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-publication-rel.html "53.42. pg_publication_rel")  
---|---|---  
53.40. `pg_publication`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.42. `pg_publication_rel`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-publication-
namespace.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

