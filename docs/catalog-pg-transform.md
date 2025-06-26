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

Supported Versions: [Current](/docs/current/catalog-pg-transform.html
"PostgreSQL 17 - 53.57. pg_transform") ([17](/docs/17/catalog-pg-
transform.html "PostgreSQL 17 - 53.57. pg_transform")) /
[16](/docs/16/catalog-pg-transform.html "PostgreSQL 16 - 53.57. pg_transform")
/ [15](/docs/15/catalog-pg-transform.html "PostgreSQL 15 -
53.57. pg_transform") / [14](/docs/14/catalog-pg-transform.html "PostgreSQL 14
- 53.57. pg_transform") / [13](/docs/13/catalog-pg-transform.html "PostgreSQL
13 - 53.57. pg_transform")

Development Versions: [18](/docs/18/catalog-pg-transform.html "PostgreSQL 18 -
53.57. pg_transform") / [devel](/docs/devel/catalog-pg-transform.html
"PostgreSQL devel - 53.57. pg_transform")

Unsupported versions: [12](/docs/12/catalog-pg-transform.html "PostgreSQL 12 -
53.57. pg_transform") / [11](/docs/11/catalog-pg-transform.html "PostgreSQL 11
- 53.57. pg_transform") / [10](/docs/10/catalog-pg-transform.html "PostgreSQL
10 - 53.57. pg_transform") / [9.6](/docs/9.6/catalog-pg-transform.html
"PostgreSQL 9.6 - 53.57. pg_transform") / [9.5](/docs/9.5/catalog-pg-
transform.html "PostgreSQL 9.5 - 53.57. pg_transform")

__

53.57. `pg_transform`  
---  
[Prev](catalog-pg-tablespace.html "53.56. pg_tablespace")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-trigger.html "53.58. pg_trigger")  
  
* * *

## 53.57. `pg_transform` #

The catalog `pg_transform` stores information about transforms, which are a
mechanism to adapt data types to procedural languages. See [CREATE
TRANSFORM](sql-createtransform.html "CREATE TRANSFORM") for more information.

**Table  53.57. `pg_transform` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`trftype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) OID of the data type this transform is for  
`trflang` `oid` (references [`pg_language`](catalog-pg-language.html
"53.29. pg_language").`oid`) OID of the language this transform is for  
`trffromsql` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) The OID of the function to use when converting the
data type for input to the procedural language (e.g., function parameters).
Zero is stored if the default behavior should be used.  
`trftosql` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) The OID of the function to use when converting output
from the procedural language (e.g., return values) to the data type. Zero is
stored if the default behavior should be used.  
  
  

* * *

[Prev](catalog-pg-tablespace.html "53.56. pg_tablespace")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-trigger.html "53.58. pg_trigger")  
---|---|---  
53.56. `pg_tablespace`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.58. `pg_trigger`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-transform.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

