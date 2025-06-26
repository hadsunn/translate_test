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

Supported Versions: [Current](/docs/current/catalog-pg-range.html "PostgreSQL
17 - 53.43. pg_range") ([17](/docs/17/catalog-pg-range.html "PostgreSQL 17 -
53.43. pg_range")) / [16](/docs/16/catalog-pg-range.html "PostgreSQL 16 -
53.43. pg_range") / [15](/docs/15/catalog-pg-range.html "PostgreSQL 15 -
53.43. pg_range") / [14](/docs/14/catalog-pg-range.html "PostgreSQL 14 -
53.43. pg_range") / [13](/docs/13/catalog-pg-range.html "PostgreSQL 13 -
53.43. pg_range")

Development Versions: [18](/docs/18/catalog-pg-range.html "PostgreSQL 18 -
53.43. pg_range") / [devel](/docs/devel/catalog-pg-range.html "PostgreSQL
devel - 53.43. pg_range")

Unsupported versions: [12](/docs/12/catalog-pg-range.html "PostgreSQL 12 -
53.43. pg_range") / [11](/docs/11/catalog-pg-range.html "PostgreSQL 11 -
53.43. pg_range") / [10](/docs/10/catalog-pg-range.html "PostgreSQL 10 -
53.43. pg_range") / [9.6](/docs/9.6/catalog-pg-range.html "PostgreSQL 9.6 -
53.43. pg_range") / [9.5](/docs/9.5/catalog-pg-range.html "PostgreSQL 9.5 -
53.43. pg_range") / [9.4](/docs/9.4/catalog-pg-range.html "PostgreSQL 9.4 -
53.43. pg_range") / [9.3](/docs/9.3/catalog-pg-range.html "PostgreSQL 9.3 -
53.43. pg_range") / [9.2](/docs/9.2/catalog-pg-range.html "PostgreSQL 9.2 -
53.43. pg_range")

__

53.43. `pg_range`  
---  
[Prev](catalog-pg-publication-rel.html "53.42. pg_publication_rel")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-replication-origin.html "53.44. pg_replication_origin")  
  
* * *

## 53.43. `pg_range` #

The catalog `pg_range` stores information about range types. This is in
addition to the types' entries in [`pg_type`](catalog-pg-type.html
"53.64. pg_type").

**Table  53.43. `pg_range` Columns**

Column Type Description  
---  
`rngtypid` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) OID of the range type  
`rngsubtype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) OID of the element type (subtype) of this range type  
`rngmultitypid` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) OID of the multirange type for this range type  
`rngcollation` `oid` (references [`pg_collation`](catalog-pg-collation.html
"53.12. pg_collation").`oid`) OID of the collation used for range comparisons,
or zero if none  
`rngsubopc` `oid` (references [`pg_opclass`](catalog-pg-opclass.html
"53.33. pg_opclass").`oid`) OID of the subtype's operator class used for range
comparisons  
`rngcanonical` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) OID of the function to convert a range value into
canonical form, or zero if none  
`rngsubdiff` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) OID of the function to return the difference between
two element values as `double precision`, or zero if none  
  
  

`rngsubopc` (plus `rngcollation`, if the element type is collatable)
determines the sort ordering used by the range type. `rngcanonical` is used
when the element type is discrete. `rngsubdiff` is optional but should be
supplied to improve performance of GiST indexes on the range type.

* * *

[Prev](catalog-pg-publication-rel.html "53.42. pg_publication_rel")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-replication-origin.html "53.44. pg_replication_origin")  
---|---|---  
53.42. `pg_publication_rel`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.44. `pg_replication_origin`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-range.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

