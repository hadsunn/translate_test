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

Supported Versions: [Current](/docs/current/catalog-pg-largeobject-
metadata.html "PostgreSQL 17 - 53.31. pg_largeobject_metadata")
([17](/docs/17/catalog-pg-largeobject-metadata.html "PostgreSQL 17 -
53.31. pg_largeobject_metadata")) / [16](/docs/16/catalog-pg-largeobject-
metadata.html "PostgreSQL 16 - 53.31. pg_largeobject_metadata") /
[15](/docs/15/catalog-pg-largeobject-metadata.html "PostgreSQL 15 -
53.31. pg_largeobject_metadata") / [14](/docs/14/catalog-pg-largeobject-
metadata.html "PostgreSQL 14 - 53.31. pg_largeobject_metadata") /
[13](/docs/13/catalog-pg-largeobject-metadata.html "PostgreSQL 13 -
53.31. pg_largeobject_metadata")

Development Versions: [18](/docs/18/catalog-pg-largeobject-metadata.html
"PostgreSQL 18 - 53.31. pg_largeobject_metadata") /
[devel](/docs/devel/catalog-pg-largeobject-metadata.html "PostgreSQL devel -
53.31. pg_largeobject_metadata")

Unsupported versions: [12](/docs/12/catalog-pg-largeobject-metadata.html
"PostgreSQL 12 - 53.31. pg_largeobject_metadata") / [11](/docs/11/catalog-pg-
largeobject-metadata.html "PostgreSQL 11 - 53.31. pg_largeobject_metadata") /
[10](/docs/10/catalog-pg-largeobject-metadata.html "PostgreSQL 10 -
53.31. pg_largeobject_metadata") / [9.6](/docs/9.6/catalog-pg-largeobject-
metadata.html "PostgreSQL 9.6 - 53.31. pg_largeobject_metadata") /
[9.5](/docs/9.5/catalog-pg-largeobject-metadata.html "PostgreSQL 9.5 -
53.31. pg_largeobject_metadata") / [9.4](/docs/9.4/catalog-pg-largeobject-
metadata.html "PostgreSQL 9.4 - 53.31. pg_largeobject_metadata") /
[9.3](/docs/9.3/catalog-pg-largeobject-metadata.html "PostgreSQL 9.3 -
53.31. pg_largeobject_metadata") / [9.2](/docs/9.2/catalog-pg-largeobject-
metadata.html "PostgreSQL 9.2 - 53.31. pg_largeobject_metadata") /
[9.1](/docs/9.1/catalog-pg-largeobject-metadata.html "PostgreSQL 9.1 -
53.31. pg_largeobject_metadata") / [9.0](/docs/9.0/catalog-pg-largeobject-
metadata.html "PostgreSQL 9.0 - 53.31. pg_largeobject_metadata")

__

53.31. `pg_largeobject_metadata`  
---  
[Prev](catalog-pg-largeobject.html "53.30. pg_largeobject")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-namespace.html "53.32. pg_namespace")  
  
* * *

## 53.31. `pg_largeobject_metadata` #

The catalog `pg_largeobject_metadata` holds metadata associated with large
objects. The actual large object data is stored in [`pg_largeobject`](catalog-
pg-largeobject.html "53.30. pg_largeobject").

**Table  53.31. `pg_largeobject_metadata` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`lomowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the large object  
`lomacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

* * *

[Prev](catalog-pg-largeobject.html "53.30. pg_largeobject")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-namespace.html "53.32. pg_namespace")  
---|---|---  
53.30. `pg_largeobject`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.32. `pg_namespace`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-largeobject-
metadata.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

