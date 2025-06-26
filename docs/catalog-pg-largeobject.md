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

Supported Versions: [Current](/docs/current/catalog-pg-largeobject.html
"PostgreSQL 17 - 53.30. pg_largeobject") ([17](/docs/17/catalog-pg-
largeobject.html "PostgreSQL 17 - 53.30. pg_largeobject")) /
[16](/docs/16/catalog-pg-largeobject.html "PostgreSQL 16 -
53.30. pg_largeobject") / [15](/docs/15/catalog-pg-largeobject.html
"PostgreSQL 15 - 53.30. pg_largeobject") / [14](/docs/14/catalog-pg-
largeobject.html "PostgreSQL 14 - 53.30. pg_largeobject") /
[13](/docs/13/catalog-pg-largeobject.html "PostgreSQL 13 -
53.30. pg_largeobject")

Development Versions: [18](/docs/18/catalog-pg-largeobject.html "PostgreSQL 18
- 53.30. pg_largeobject") / [devel](/docs/devel/catalog-pg-largeobject.html
"PostgreSQL devel - 53.30. pg_largeobject")

Unsupported versions: [12](/docs/12/catalog-pg-largeobject.html "PostgreSQL 12
- 53.30. pg_largeobject") / [11](/docs/11/catalog-pg-largeobject.html
"PostgreSQL 11 - 53.30. pg_largeobject") / [10](/docs/10/catalog-pg-
largeobject.html "PostgreSQL 10 - 53.30. pg_largeobject") /
[9.6](/docs/9.6/catalog-pg-largeobject.html "PostgreSQL 9.6 -
53.30. pg_largeobject") / [9.5](/docs/9.5/catalog-pg-largeobject.html
"PostgreSQL 9.5 - 53.30. pg_largeobject") / [9.4](/docs/9.4/catalog-pg-
largeobject.html "PostgreSQL 9.4 - 53.30. pg_largeobject") /
[9.3](/docs/9.3/catalog-pg-largeobject.html "PostgreSQL 9.3 -
53.30. pg_largeobject") / [9.2](/docs/9.2/catalog-pg-largeobject.html
"PostgreSQL 9.2 - 53.30. pg_largeobject") / [9.1](/docs/9.1/catalog-pg-
largeobject.html "PostgreSQL 9.1 - 53.30. pg_largeobject") /
[9.0](/docs/9.0/catalog-pg-largeobject.html "PostgreSQL 9.0 -
53.30. pg_largeobject") / [8.4](/docs/8.4/catalog-pg-largeobject.html
"PostgreSQL 8.4 - 53.30. pg_largeobject") / [8.3](/docs/8.3/catalog-pg-
largeobject.html "PostgreSQL 8.3 - 53.30. pg_largeobject") /
[8.2](/docs/8.2/catalog-pg-largeobject.html "PostgreSQL 8.2 -
53.30. pg_largeobject") / [8.1](/docs/8.1/catalog-pg-largeobject.html
"PostgreSQL 8.1 - 53.30. pg_largeobject") / [8.0](/docs/8.0/catalog-pg-
largeobject.html "PostgreSQL 8.0 - 53.30. pg_largeobject") /
[7.4](/docs/7.4/catalog-pg-largeobject.html "PostgreSQL 7.4 -
53.30. pg_largeobject") / [7.3](/docs/7.3/catalog-pg-largeobject.html
"PostgreSQL 7.3 - 53.30. pg_largeobject") / [7.2](/docs/7.2/catalog-pg-
largeobject.html "PostgreSQL 7.2 - 53.30. pg_largeobject")

__

53.30. `pg_largeobject`  
---  
[Prev](catalog-pg-language.html "53.29. pg_language")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-largeobject-metadata.html "53.31. pg_largeobject_metadata")  
  
* * *

## 53.30. `pg_largeobject` #

The catalog `pg_largeobject` holds the data making up “large objects”. A large
object is identified by an OID assigned when it is created. Each large object
is broken into segments or “pages” small enough to be conveniently stored as
rows in `pg_largeobject`. The amount of data per page is defined to be
`LOBLKSIZE` (which is currently `BLCKSZ/4`, or typically 2 kB).

Prior to PostgreSQL 9.0, there was no permission structure associated with
large objects. As a result, `pg_largeobject` was publicly readable and could
be used to obtain the OIDs (and contents) of all large objects in the system.
This is no longer the case; use [`pg_largeobject_metadata`](catalog-pg-
largeobject-metadata.html "53.31. pg_largeobject_metadata") to obtain a list
of large object OIDs.

**Table  53.30. `pg_largeobject` Columns**

Column Type Description  
---  
`loid` `oid` (references [`pg_largeobject_metadata`](catalog-pg-largeobject-
metadata.html "53.31. pg_largeobject_metadata").`oid`) Identifier of the large
object that includes this page  
`pageno` `int4` Page number of this page within its large object (counting
from zero)  
`data` `bytea` Actual data stored in the large object. This will never be more
than `LOBLKSIZE` bytes and might be less.  
  
  

Each row of `pg_largeobject` holds data for one page of a large object,
beginning at byte offset (`pageno * LOBLKSIZE`) within the object. The
implementation allows sparse storage: pages might be missing, and might be
shorter than `LOBLKSIZE` bytes even if they are not the last page of the
object. Missing regions within a large object read as zeroes.

* * *

[Prev](catalog-pg-language.html "53.29. pg_language")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-largeobject-metadata.html "53.31. pg_largeobject_metadata")  
---|---|---  
53.29. `pg_language`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.31. `pg_largeobject_metadata`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-largeobject.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

