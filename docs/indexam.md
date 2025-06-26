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

Supported Versions: [Current](/docs/current/indexam.html "PostgreSQL 17 -
Chapter 64. Index Access Method Interface Definition")
([17](/docs/17/indexam.html "PostgreSQL 17 - Chapter 64. Index Access Method
Interface Definition")) / [16](/docs/16/indexam.html "PostgreSQL 16 -
Chapter 64. Index Access Method Interface Definition") /
[15](/docs/15/indexam.html "PostgreSQL 15 - Chapter 64. Index Access Method
Interface Definition") / [14](/docs/14/indexam.html "PostgreSQL 14 -
Chapter 64. Index Access Method Interface Definition") /
[13](/docs/13/indexam.html "PostgreSQL 13 - Chapter 64. Index Access Method
Interface Definition")

Development Versions: [18](/docs/18/indexam.html "PostgreSQL 18 -
Chapter 64. Index Access Method Interface Definition") /
[devel](/docs/devel/indexam.html "PostgreSQL devel - Chapter 64. Index Access
Method Interface Definition")

Unsupported versions: [12](/docs/12/indexam.html "PostgreSQL 12 -
Chapter 64. Index Access Method Interface Definition") /
[11](/docs/11/indexam.html "PostgreSQL 11 - Chapter 64. Index Access Method
Interface Definition") / [10](/docs/10/indexam.html "PostgreSQL 10 -
Chapter 64. Index Access Method Interface Definition") /
[9.6](/docs/9.6/indexam.html "PostgreSQL 9.6 - Chapter 64. Index Access Method
Interface Definition") / [9.5](/docs/9.5/indexam.html "PostgreSQL 9.5 -
Chapter 64. Index Access Method Interface Definition") /
[9.4](/docs/9.4/indexam.html "PostgreSQL 9.4 - Chapter 64. Index Access Method
Interface Definition") / [9.3](/docs/9.3/indexam.html "PostgreSQL 9.3 -
Chapter 64. Index Access Method Interface Definition") /
[9.2](/docs/9.2/indexam.html "PostgreSQL 9.2 - Chapter 64. Index Access Method
Interface Definition") / [9.1](/docs/9.1/indexam.html "PostgreSQL 9.1 -
Chapter 64. Index Access Method Interface Definition") /
[9.0](/docs/9.0/indexam.html "PostgreSQL 9.0 - Chapter 64. Index Access Method
Interface Definition") / [8.4](/docs/8.4/indexam.html "PostgreSQL 8.4 -
Chapter 64. Index Access Method Interface Definition") /
[8.3](/docs/8.3/indexam.html "PostgreSQL 8.3 - Chapter 64. Index Access Method
Interface Definition") / [8.2](/docs/8.2/indexam.html "PostgreSQL 8.2 -
Chapter 64. Index Access Method Interface Definition") /
[8.1](/docs/8.1/indexam.html "PostgreSQL 8.1 - Chapter 64. Index Access Method
Interface Definition")

__

Chapter 64. Index Access Method Interface Definition  
---  
[Prev](tableam.html "Chapter 63. Table Access Method Interface Definition")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](index-api.html "64.1. Basic API Structure for Indexes")  
  
* * *

## Chapter 64. Index Access Method Interface Definition

**Table of Contents**

[64.1. Basic API Structure for Indexes](index-api.html)

[64.2. Index Access Method Functions](index-functions.html)

[64.3. Index Scanning](index-scanning.html)

[64.4. Index Locking Considerations](index-locking.html)

[64.5. Index Uniqueness Checks](index-unique-checks.html)

[64.6. Index Cost Estimation Functions](index-cost-estimation.html)

This chapter defines the interface between the core PostgreSQL system and
_index access methods_ , which manage individual index types. The core system
knows nothing about indexes beyond what is specified here, so it is possible
to develop entirely new index types by writing add-on code.

All indexes in PostgreSQL are what are known technically as _secondary
indexes_ ; that is, the index is physically separate from the table file that
it describes. Each index is stored as its own physical _relation_ and so is
described by an entry in the `pg_class` catalog. The contents of an index are
entirely under the control of its index access method. In practice, all index
access methods divide indexes into standard-size pages so that they can use
the regular storage manager and buffer manager to access the index contents.
(All the existing index access methods furthermore use the standard page
layout described in [Section 73.6](storage-page-layout.html "73.6. Database
Page Layout"), and most use the same format for index tuple headers; but these
decisions are not forced on an access method.)

An index is effectively a mapping from some data key values to _tuple
identifiers_ , or TIDs, of row versions (tuples) in the index's parent table.
A TID consists of a block number and an item number within that block (see
[Section 73.6](storage-page-layout.html "73.6. Database Page Layout")). This
is sufficient information to fetch a particular row version from the table.
Indexes are not directly aware that under MVCC, there might be multiple extant
versions of the same logical row; to an index, each tuple is an independent
object that needs its own index entry. Thus, an update of a row always creates
all-new index entries for the row, even if the key values did not change.
([HOT tuples](storage-hot.html "73.7. Heap-Only Tuples \(HOT\)") are an
exception to this statement; but indexes do not deal with those, either.)
Index entries for dead tuples are reclaimed (by vacuuming) when the dead
tuples themselves are reclaimed.

* * *

[Prev](tableam.html "Chapter 63. Table Access Method Interface Definition")  | [Up](internals.html "Part VII. Internals") |  [Next](index-api.html "64.1. Basic API Structure for Indexes")  
---|---|---  
Chapter 63. Table Access Method Interface Definition  | [Home](index.html "PostgreSQL 16.9 Documentation") |  64.1. Basic API Structure for Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexam.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

