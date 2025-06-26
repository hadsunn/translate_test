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

Supported Versions: [Current](/docs/current/indexes.html "PostgreSQL 17 -
Chapter 11. Indexes") ([17](/docs/17/indexes.html "PostgreSQL 17 -
Chapter 11. Indexes")) / [16](/docs/16/indexes.html "PostgreSQL 16 -
Chapter 11. Indexes") / [15](/docs/15/indexes.html "PostgreSQL 15 -
Chapter 11. Indexes") / [14](/docs/14/indexes.html "PostgreSQL 14 -
Chapter 11. Indexes") / [13](/docs/13/indexes.html "PostgreSQL 13 -
Chapter 11. Indexes")

Development Versions: [18](/docs/18/indexes.html "PostgreSQL 18 -
Chapter 11. Indexes") / [devel](/docs/devel/indexes.html "PostgreSQL devel -
Chapter 11. Indexes")

Unsupported versions: [12](/docs/12/indexes.html "PostgreSQL 12 -
Chapter 11. Indexes") / [11](/docs/11/indexes.html "PostgreSQL 11 -
Chapter 11. Indexes") / [10](/docs/10/indexes.html "PostgreSQL 10 -
Chapter 11. Indexes") / [9.6](/docs/9.6/indexes.html "PostgreSQL 9.6 -
Chapter 11. Indexes") / [9.5](/docs/9.5/indexes.html "PostgreSQL 9.5 -
Chapter 11. Indexes") / [9.4](/docs/9.4/indexes.html "PostgreSQL 9.4 -
Chapter 11. Indexes") / [9.3](/docs/9.3/indexes.html "PostgreSQL 9.3 -
Chapter 11. Indexes") / [9.2](/docs/9.2/indexes.html "PostgreSQL 9.2 -
Chapter 11. Indexes") / [9.1](/docs/9.1/indexes.html "PostgreSQL 9.1 -
Chapter 11. Indexes") / [9.0](/docs/9.0/indexes.html "PostgreSQL 9.0 -
Chapter 11. Indexes") / [8.4](/docs/8.4/indexes.html "PostgreSQL 8.4 -
Chapter 11. Indexes") / [8.3](/docs/8.3/indexes.html "PostgreSQL 8.3 -
Chapter 11. Indexes") / [8.2](/docs/8.2/indexes.html "PostgreSQL 8.2 -
Chapter 11. Indexes") / [8.1](/docs/8.1/indexes.html "PostgreSQL 8.1 -
Chapter 11. Indexes") / [8.0](/docs/8.0/indexes.html "PostgreSQL 8.0 -
Chapter 11. Indexes") / [7.4](/docs/7.4/indexes.html "PostgreSQL 7.4 -
Chapter 11. Indexes") / [7.3](/docs/7.3/indexes.html "PostgreSQL 7.3 -
Chapter 11. Indexes") / [7.2](/docs/7.2/indexes.html "PostgreSQL 7.2 -
Chapter 11. Indexes")

__

Chapter 11. Indexes  
---  
[Prev](typeconv-select.html "10.6. SELECT Output Columns")  | [Up](sql.html "Part II. The SQL Language") | Part II. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-intro.html "11.1. Introduction")  
  
* * *

## Chapter 11. Indexes

**Table of Contents**

[11.1. Introduction](indexes-intro.html)

[11.2. Index Types](indexes-types.html)

    

[11.2.1. B-Tree](indexes-types.html#INDEXES-TYPES-BTREE)

[11.2.2. Hash](indexes-types.html#INDEXES-TYPES-HASH)

[11.2.3. GiST](indexes-types.html#INDEXES-TYPE-GIST)

[11.2.4. SP-GiST](indexes-types.html#INDEXES-TYPE-SPGIST)

[11.2.5. GIN](indexes-types.html#INDEXES-TYPES-GIN)

[11.2.6. BRIN](indexes-types.html#INDEXES-TYPES-BRIN)

[11.3. Multicolumn Indexes](indexes-multicolumn.html)

[11.4. Indexes and `ORDER BY`](indexes-ordering.html)

[11.5. Combining Multiple Indexes](indexes-bitmap-scans.html)

[11.6. Unique Indexes](indexes-unique.html)

[11.7. Indexes on Expressions](indexes-expressional.html)

[11.8. Partial Indexes](indexes-partial.html)

[11.9. Index-Only Scans and Covering Indexes](indexes-index-only-scans.html)

[11.10. Operator Classes and Operator Families](indexes-opclass.html)

[11.11. Indexes and Collations](indexes-collations.html)

[11.12. Examining Index Usage](indexes-examine.html)

Indexes are a common way to enhance database performance. An index allows the
database server to find and retrieve specific rows much faster than it could
do without an index. But indexes also add overhead to the database system as a
whole, so they should be used sensibly.

* * *

[Prev](typeconv-select.html "10.6. SELECT Output Columns")  | [Up](sql.html "Part II. The SQL Language") |  [Next](indexes-intro.html "11.1. Introduction")  
---|---|---  
10.6. `SELECT` Output Columns  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.1. Introduction  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

