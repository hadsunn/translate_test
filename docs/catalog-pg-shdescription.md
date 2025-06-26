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

Supported Versions: [Current](/docs/current/catalog-pg-shdescription.html
"PostgreSQL 17 - 53.49. pg_shdescription") ([17](/docs/17/catalog-pg-
shdescription.html "PostgreSQL 17 - 53.49. pg_shdescription")) /
[16](/docs/16/catalog-pg-shdescription.html "PostgreSQL 16 -
53.49. pg_shdescription") / [15](/docs/15/catalog-pg-shdescription.html
"PostgreSQL 15 - 53.49. pg_shdescription") / [14](/docs/14/catalog-pg-
shdescription.html "PostgreSQL 14 - 53.49. pg_shdescription") /
[13](/docs/13/catalog-pg-shdescription.html "PostgreSQL 13 -
53.49. pg_shdescription")

Development Versions: [18](/docs/18/catalog-pg-shdescription.html "PostgreSQL
18 - 53.49. pg_shdescription") / [devel](/docs/devel/catalog-pg-
shdescription.html "PostgreSQL devel - 53.49. pg_shdescription")

Unsupported versions: [12](/docs/12/catalog-pg-shdescription.html "PostgreSQL
12 - 53.49. pg_shdescription") / [11](/docs/11/catalog-pg-shdescription.html
"PostgreSQL 11 - 53.49. pg_shdescription") / [10](/docs/10/catalog-pg-
shdescription.html "PostgreSQL 10 - 53.49. pg_shdescription") /
[9.6](/docs/9.6/catalog-pg-shdescription.html "PostgreSQL 9.6 -
53.49. pg_shdescription") / [9.5](/docs/9.5/catalog-pg-shdescription.html
"PostgreSQL 9.5 - 53.49. pg_shdescription") / [9.4](/docs/9.4/catalog-pg-
shdescription.html "PostgreSQL 9.4 - 53.49. pg_shdescription") /
[9.3](/docs/9.3/catalog-pg-shdescription.html "PostgreSQL 9.3 -
53.49. pg_shdescription") / [9.2](/docs/9.2/catalog-pg-shdescription.html
"PostgreSQL 9.2 - 53.49. pg_shdescription") / [9.1](/docs/9.1/catalog-pg-
shdescription.html "PostgreSQL 9.1 - 53.49. pg_shdescription") /
[9.0](/docs/9.0/catalog-pg-shdescription.html "PostgreSQL 9.0 -
53.49. pg_shdescription") / [8.4](/docs/8.4/catalog-pg-shdescription.html
"PostgreSQL 8.4 - 53.49. pg_shdescription") / [8.3](/docs/8.3/catalog-pg-
shdescription.html "PostgreSQL 8.3 - 53.49. pg_shdescription") /
[8.2](/docs/8.2/catalog-pg-shdescription.html "PostgreSQL 8.2 -
53.49. pg_shdescription")

__

53.49. `pg_shdescription`  
---  
[Prev](catalog-pg-shdepend.html "53.48. pg_shdepend")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-shseclabel.html "53.50. pg_shseclabel")  
  
* * *

## 53.49. `pg_shdescription` #

The catalog `pg_shdescription` stores optional descriptions (comments) for
shared database objects. Descriptions can be manipulated with the
[`COMMENT`](sql-comment.html "COMMENT") command and viewed with psql's `\d`
commands.

See also [`pg_description`](catalog-pg-description.html
"53.19. pg_description"), which performs a similar function for descriptions
involving objects within a single database.

Unlike most system catalogs, `pg_shdescription` is shared across all databases
of a cluster: there is only one copy of `pg_shdescription` per cluster, not
one per database.

**Table  53.49. `pg_shdescription` Columns**

Column Type Description  
---  
`objoid` `oid` (references any OID column) The OID of the object this
description pertains to  
`classoid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog this object appears in  
`description` `text` Arbitrary text that serves as the description of this
object  
  
  

* * *

[Prev](catalog-pg-shdepend.html "53.48. pg_shdepend")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-shseclabel.html "53.50. pg_shseclabel")  
---|---|---  
53.48. `pg_shdepend`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.50. `pg_shseclabel`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-
shdescription.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

