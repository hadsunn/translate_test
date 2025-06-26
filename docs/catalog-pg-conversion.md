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

Supported Versions: [Current](/docs/current/catalog-pg-conversion.html
"PostgreSQL 17 - 53.14. pg_conversion") ([17](/docs/17/catalog-pg-
conversion.html "PostgreSQL 17 - 53.14. pg_conversion")) /
[16](/docs/16/catalog-pg-conversion.html "PostgreSQL 16 -
53.14. pg_conversion") / [15](/docs/15/catalog-pg-conversion.html "PostgreSQL
15 - 53.14. pg_conversion") / [14](/docs/14/catalog-pg-conversion.html
"PostgreSQL 14 - 53.14. pg_conversion") / [13](/docs/13/catalog-pg-
conversion.html "PostgreSQL 13 - 53.14. pg_conversion")

Development Versions: [18](/docs/18/catalog-pg-conversion.html "PostgreSQL 18
- 53.14. pg_conversion") / [devel](/docs/devel/catalog-pg-conversion.html
"PostgreSQL devel - 53.14. pg_conversion")

Unsupported versions: [12](/docs/12/catalog-pg-conversion.html "PostgreSQL 12
- 53.14. pg_conversion") / [11](/docs/11/catalog-pg-conversion.html
"PostgreSQL 11 - 53.14. pg_conversion") / [10](/docs/10/catalog-pg-
conversion.html "PostgreSQL 10 - 53.14. pg_conversion") /
[9.6](/docs/9.6/catalog-pg-conversion.html "PostgreSQL 9.6 -
53.14. pg_conversion") / [9.5](/docs/9.5/catalog-pg-conversion.html
"PostgreSQL 9.5 - 53.14. pg_conversion") / [9.4](/docs/9.4/catalog-pg-
conversion.html "PostgreSQL 9.4 - 53.14. pg_conversion") /
[9.3](/docs/9.3/catalog-pg-conversion.html "PostgreSQL 9.3 -
53.14. pg_conversion") / [9.2](/docs/9.2/catalog-pg-conversion.html
"PostgreSQL 9.2 - 53.14. pg_conversion") / [9.1](/docs/9.1/catalog-pg-
conversion.html "PostgreSQL 9.1 - 53.14. pg_conversion") /
[9.0](/docs/9.0/catalog-pg-conversion.html "PostgreSQL 9.0 -
53.14. pg_conversion") / [8.4](/docs/8.4/catalog-pg-conversion.html
"PostgreSQL 8.4 - 53.14. pg_conversion") / [8.3](/docs/8.3/catalog-pg-
conversion.html "PostgreSQL 8.3 - 53.14. pg_conversion") /
[8.2](/docs/8.2/catalog-pg-conversion.html "PostgreSQL 8.2 -
53.14. pg_conversion") / [8.1](/docs/8.1/catalog-pg-conversion.html
"PostgreSQL 8.1 - 53.14. pg_conversion") / [8.0](/docs/8.0/catalog-pg-
conversion.html "PostgreSQL 8.0 - 53.14. pg_conversion") /
[7.4](/docs/7.4/catalog-pg-conversion.html "PostgreSQL 7.4 -
53.14. pg_conversion") / [7.3](/docs/7.3/catalog-pg-conversion.html
"PostgreSQL 7.3 - 53.14. pg_conversion")

__

53.14. `pg_conversion`  
---  
[Prev](catalog-pg-constraint.html "53.13. pg_constraint")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-database.html "53.15. pg_database")  
  
* * *

## 53.14. `pg_conversion` #

The catalog `pg_conversion` describes encoding conversion functions. See
[CREATE CONVERSION](sql-createconversion.html "CREATE CONVERSION") for more
information.

**Table  53.14. `pg_conversion` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`conname` `name` Conversion name (unique within a namespace)  
`connamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
conversion  
`conowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the conversion  
`conforencoding` `int4` Source encoding ID
([`pg_encoding_to_char()`](functions-info.html#PG-ENCODING-TO-CHAR) can
translate this number to the encoding name)  
`contoencoding` `int4` Destination encoding ID
([`pg_encoding_to_char()`](functions-info.html#PG-ENCODING-TO-CHAR) can
translate this number to the encoding name)  
`conproc` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Conversion function  
`condefault` `bool` True if this is the default conversion  
  
  

* * *

[Prev](catalog-pg-constraint.html "53.13. pg_constraint")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-database.html "53.15. pg_database")  
---|---|---  
53.13. `pg_constraint`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.15. `pg_database`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-conversion.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

