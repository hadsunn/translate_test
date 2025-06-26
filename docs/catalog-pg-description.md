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

Supported Versions: [Current](/docs/current/catalog-pg-description.html
"PostgreSQL 17 - 53.19. pg_description") ([17](/docs/17/catalog-pg-
description.html "PostgreSQL 17 - 53.19. pg_description")) /
[16](/docs/16/catalog-pg-description.html "PostgreSQL 16 -
53.19. pg_description") / [15](/docs/15/catalog-pg-description.html
"PostgreSQL 15 - 53.19. pg_description") / [14](/docs/14/catalog-pg-
description.html "PostgreSQL 14 - 53.19. pg_description") /
[13](/docs/13/catalog-pg-description.html "PostgreSQL 13 -
53.19. pg_description")

Development Versions: [18](/docs/18/catalog-pg-description.html "PostgreSQL 18
- 53.19. pg_description") / [devel](/docs/devel/catalog-pg-description.html
"PostgreSQL devel - 53.19. pg_description")

Unsupported versions: [12](/docs/12/catalog-pg-description.html "PostgreSQL 12
- 53.19. pg_description") / [11](/docs/11/catalog-pg-description.html
"PostgreSQL 11 - 53.19. pg_description") / [10](/docs/10/catalog-pg-
description.html "PostgreSQL 10 - 53.19. pg_description") /
[9.6](/docs/9.6/catalog-pg-description.html "PostgreSQL 9.6 -
53.19. pg_description") / [9.5](/docs/9.5/catalog-pg-description.html
"PostgreSQL 9.5 - 53.19. pg_description") / [9.4](/docs/9.4/catalog-pg-
description.html "PostgreSQL 9.4 - 53.19. pg_description") /
[9.3](/docs/9.3/catalog-pg-description.html "PostgreSQL 9.3 -
53.19. pg_description") / [9.2](/docs/9.2/catalog-pg-description.html
"PostgreSQL 9.2 - 53.19. pg_description") / [9.1](/docs/9.1/catalog-pg-
description.html "PostgreSQL 9.1 - 53.19. pg_description") /
[9.0](/docs/9.0/catalog-pg-description.html "PostgreSQL 9.0 -
53.19. pg_description") / [8.4](/docs/8.4/catalog-pg-description.html
"PostgreSQL 8.4 - 53.19. pg_description") / [8.3](/docs/8.3/catalog-pg-
description.html "PostgreSQL 8.3 - 53.19. pg_description") /
[8.2](/docs/8.2/catalog-pg-description.html "PostgreSQL 8.2 -
53.19. pg_description") / [8.1](/docs/8.1/catalog-pg-description.html
"PostgreSQL 8.1 - 53.19. pg_description") / [8.0](/docs/8.0/catalog-pg-
description.html "PostgreSQL 8.0 - 53.19. pg_description") /
[7.4](/docs/7.4/catalog-pg-description.html "PostgreSQL 7.4 -
53.19. pg_description") / [7.3](/docs/7.3/catalog-pg-description.html
"PostgreSQL 7.3 - 53.19. pg_description") / [7.2](/docs/7.2/catalog-pg-
description.html "PostgreSQL 7.2 - 53.19. pg_description") /
[7.1](/docs/7.1/catalog-pg-description.html "PostgreSQL 7.1 -
53.19. pg_description")

__

53.19. `pg_description`  
---  
[Prev](catalog-pg-depend.html "53.18. pg_depend")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-enum.html "53.20. pg_enum")  
  
* * *

## 53.19. `pg_description` #

The catalog `pg_description` stores optional descriptions (comments) for each
database object. Descriptions can be manipulated with the [`COMMENT`](sql-
comment.html "COMMENT") command and viewed with psql's `\d` commands.
Descriptions of many built-in system objects are provided in the initial
contents of `pg_description`.

See also [`pg_shdescription`](catalog-pg-shdescription.html
"53.49. pg_shdescription"), which performs a similar function for descriptions
involving objects that are shared across a database cluster.

**Table  53.19. `pg_description` Columns**

Column Type Description  
---  
`objoid` `oid` (references any OID column) The OID of the object this
description pertains to  
`classoid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog this object appears in  
`objsubid` `int4` For a comment on a table column, this is the column number
(the `objoid` and `classoid` refer to the table itself). For all other object
types, this column is zero.  
`description` `text` Arbitrary text that serves as the description of this
object  
  
  

* * *

[Prev](catalog-pg-depend.html "53.18. pg_depend")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-enum.html "53.20. pg_enum")  
---|---|---  
53.18. `pg_depend`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.20. `pg_enum`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-description.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

