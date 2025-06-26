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

Supported Versions: [Current](/docs/current/catalog-pg-namespace.html
"PostgreSQL 17 - 53.32. pg_namespace") ([17](/docs/17/catalog-pg-
namespace.html "PostgreSQL 17 - 53.32. pg_namespace")) /
[16](/docs/16/catalog-pg-namespace.html "PostgreSQL 16 - 53.32. pg_namespace")
/ [15](/docs/15/catalog-pg-namespace.html "PostgreSQL 15 -
53.32. pg_namespace") / [14](/docs/14/catalog-pg-namespace.html "PostgreSQL 14
- 53.32. pg_namespace") / [13](/docs/13/catalog-pg-namespace.html "PostgreSQL
13 - 53.32. pg_namespace")

Development Versions: [18](/docs/18/catalog-pg-namespace.html "PostgreSQL 18 -
53.32. pg_namespace") / [devel](/docs/devel/catalog-pg-namespace.html
"PostgreSQL devel - 53.32. pg_namespace")

Unsupported versions: [12](/docs/12/catalog-pg-namespace.html "PostgreSQL 12 -
53.32. pg_namespace") / [11](/docs/11/catalog-pg-namespace.html "PostgreSQL 11
- 53.32. pg_namespace") / [10](/docs/10/catalog-pg-namespace.html "PostgreSQL
10 - 53.32. pg_namespace") / [9.6](/docs/9.6/catalog-pg-namespace.html
"PostgreSQL 9.6 - 53.32. pg_namespace") / [9.5](/docs/9.5/catalog-pg-
namespace.html "PostgreSQL 9.5 - 53.32. pg_namespace") /
[9.4](/docs/9.4/catalog-pg-namespace.html "PostgreSQL 9.4 -
53.32. pg_namespace") / [9.3](/docs/9.3/catalog-pg-namespace.html "PostgreSQL
9.3 - 53.32. pg_namespace") / [9.2](/docs/9.2/catalog-pg-namespace.html
"PostgreSQL 9.2 - 53.32. pg_namespace") / [9.1](/docs/9.1/catalog-pg-
namespace.html "PostgreSQL 9.1 - 53.32. pg_namespace") /
[9.0](/docs/9.0/catalog-pg-namespace.html "PostgreSQL 9.0 -
53.32. pg_namespace") / [8.4](/docs/8.4/catalog-pg-namespace.html "PostgreSQL
8.4 - 53.32. pg_namespace") / [8.3](/docs/8.3/catalog-pg-namespace.html
"PostgreSQL 8.3 - 53.32. pg_namespace") / [8.2](/docs/8.2/catalog-pg-
namespace.html "PostgreSQL 8.2 - 53.32. pg_namespace") /
[8.1](/docs/8.1/catalog-pg-namespace.html "PostgreSQL 8.1 -
53.32. pg_namespace") / [8.0](/docs/8.0/catalog-pg-namespace.html "PostgreSQL
8.0 - 53.32. pg_namespace") / [7.4](/docs/7.4/catalog-pg-namespace.html
"PostgreSQL 7.4 - 53.32. pg_namespace") / [7.3](/docs/7.3/catalog-pg-
namespace.html "PostgreSQL 7.3 - 53.32. pg_namespace")

__

53.32. `pg_namespace`  
---  
[Prev](catalog-pg-largeobject-metadata.html "53.31. pg_largeobject_metadata")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-opclass.html "53.33. pg_opclass")  
  
* * *

## 53.32. `pg_namespace` #

The catalog `pg_namespace` stores namespaces. A namespace is the structure
underlying SQL schemas: each namespace can have a separate collection of
relations, types, etc. without name conflicts.

**Table  53.32. `pg_namespace` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`nspname` `name` Name of the namespace  
`nspowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the namespace  
`nspacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

* * *

[Prev](catalog-pg-largeobject-metadata.html "53.31. pg_largeobject_metadata")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-opclass.html "53.33. pg_opclass")  
---|---|---  
53.31. `pg_largeobject_metadata`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.33. `pg_opclass`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-namespace.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

