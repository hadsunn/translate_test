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

Supported Versions: [Current](/docs/current/lo-intro.html "PostgreSQL 17 -
35.1. Introduction") ([17](/docs/17/lo-intro.html "PostgreSQL 17 -
35.1. Introduction")) / [16](/docs/16/lo-intro.html "PostgreSQL 16 -
35.1. Introduction") / [15](/docs/15/lo-intro.html "PostgreSQL 15 -
35.1. Introduction") / [14](/docs/14/lo-intro.html "PostgreSQL 14 -
35.1. Introduction") / [13](/docs/13/lo-intro.html "PostgreSQL 13 -
35.1. Introduction")

Development Versions: [18](/docs/18/lo-intro.html "PostgreSQL 18 -
35.1. Introduction") / [devel](/docs/devel/lo-intro.html "PostgreSQL devel -
35.1. Introduction")

Unsupported versions: [12](/docs/12/lo-intro.html "PostgreSQL 12 -
35.1. Introduction") / [11](/docs/11/lo-intro.html "PostgreSQL 11 -
35.1. Introduction") / [10](/docs/10/lo-intro.html "PostgreSQL 10 -
35.1. Introduction") / [9.6](/docs/9.6/lo-intro.html "PostgreSQL 9.6 -
35.1. Introduction") / [9.5](/docs/9.5/lo-intro.html "PostgreSQL 9.5 -
35.1. Introduction") / [9.4](/docs/9.4/lo-intro.html "PostgreSQL 9.4 -
35.1. Introduction") / [9.3](/docs/9.3/lo-intro.html "PostgreSQL 9.3 -
35.1. Introduction") / [9.2](/docs/9.2/lo-intro.html "PostgreSQL 9.2 -
35.1. Introduction") / [9.1](/docs/9.1/lo-intro.html "PostgreSQL 9.1 -
35.1. Introduction") / [9.0](/docs/9.0/lo-intro.html "PostgreSQL 9.0 -
35.1. Introduction") / [8.4](/docs/8.4/lo-intro.html "PostgreSQL 8.4 -
35.1. Introduction") / [8.3](/docs/8.3/lo-intro.html "PostgreSQL 8.3 -
35.1. Introduction") / [8.2](/docs/8.2/lo-intro.html "PostgreSQL 8.2 -
35.1. Introduction")

__

35.1. Introduction  
---  
[Prev](largeobjects.html "Chapter 35. Large Objects")  | [Up](largeobjects.html "Chapter 35. Large Objects") | Chapter 35. Large Objects | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](lo-implementation.html "35.2. Implementation Features")  
  
* * *

## 35.1. Introduction #

All large objects are stored in a single system table named
[`pg_largeobject`](catalog-pg-largeobject.html "53.30. pg_largeobject"). Each
large object also has an entry in the system table
[`pg_largeobject_metadata`](catalog-pg-largeobject-metadata.html
"53.31. pg_largeobject_metadata"). Large objects can be created, modified, and
deleted using a read/write API that is similar to standard operations on
files.

PostgreSQL also supports a storage system called [“TOAST”](storage-toast.html
"73.2. TOAST"), which automatically stores values larger than a single
database page into a secondary storage area per table. This makes the large
object facility partially obsolete. One remaining advantage of the large
object facility is that it allows values up to 4 TB in size, whereas TOASTed
fields can be at most 1 GB. Also, reading and updating portions of a large
object can be done efficiently, while most operations on a TOASTed field will
read or write the whole value as a unit.

* * *

[Prev](largeobjects.html "Chapter 35. Large Objects")  | [Up](largeobjects.html "Chapter 35. Large Objects") |  [Next](lo-implementation.html "35.2. Implementation Features")  
---|---|---  
Chapter 35. Large Objects  | [Home](index.html "PostgreSQL 16.9 Documentation") |  35.2. Implementation Features  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/lo-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

