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

Supported Versions: [Current](/docs/current/locking-indexes.html "PostgreSQL
17 - 13.7. Locking and Indexes") ([17](/docs/17/locking-indexes.html
"PostgreSQL 17 - 13.7. Locking and Indexes")) / [16](/docs/16/locking-
indexes.html "PostgreSQL 16 - 13.7. Locking and Indexes") /
[15](/docs/15/locking-indexes.html "PostgreSQL 15 - 13.7. Locking and
Indexes") / [14](/docs/14/locking-indexes.html "PostgreSQL 14 - 13.7. Locking
and Indexes") / [13](/docs/13/locking-indexes.html "PostgreSQL 13 -
13.7. Locking and Indexes")

Development Versions: [18](/docs/18/locking-indexes.html "PostgreSQL 18 -
13.7. Locking and Indexes") / [devel](/docs/devel/locking-indexes.html
"PostgreSQL devel - 13.7. Locking and Indexes")

Unsupported versions: [12](/docs/12/locking-indexes.html "PostgreSQL 12 -
13.7. Locking and Indexes") / [11](/docs/11/locking-indexes.html "PostgreSQL
11 - 13.7. Locking and Indexes") / [10](/docs/10/locking-indexes.html
"PostgreSQL 10 - 13.7. Locking and Indexes") / [9.6](/docs/9.6/locking-
indexes.html "PostgreSQL 9.6 - 13.7. Locking and Indexes") /
[9.5](/docs/9.5/locking-indexes.html "PostgreSQL 9.5 - 13.7. Locking and
Indexes") / [9.4](/docs/9.4/locking-indexes.html "PostgreSQL 9.4 -
13.7. Locking and Indexes") / [9.3](/docs/9.3/locking-indexes.html "PostgreSQL
9.3 - 13.7. Locking and Indexes") / [9.2](/docs/9.2/locking-indexes.html
"PostgreSQL 9.2 - 13.7. Locking and Indexes") / [9.1](/docs/9.1/locking-
indexes.html "PostgreSQL 9.1 - 13.7. Locking and Indexes") /
[9.0](/docs/9.0/locking-indexes.html "PostgreSQL 9.0 - 13.7. Locking and
Indexes") / [8.4](/docs/8.4/locking-indexes.html "PostgreSQL 8.4 -
13.7. Locking and Indexes") / [8.3](/docs/8.3/locking-indexes.html "PostgreSQL
8.3 - 13.7. Locking and Indexes") / [8.2](/docs/8.2/locking-indexes.html
"PostgreSQL 8.2 - 13.7. Locking and Indexes") / [8.1](/docs/8.1/locking-
indexes.html "PostgreSQL 8.1 - 13.7. Locking and Indexes") /
[8.0](/docs/8.0/locking-indexes.html "PostgreSQL 8.0 - 13.7. Locking and
Indexes") / [7.4](/docs/7.4/locking-indexes.html "PostgreSQL 7.4 -
13.7. Locking and Indexes") / [7.3](/docs/7.3/locking-indexes.html "PostgreSQL
7.3 - 13.7. Locking and Indexes") / [7.2](/docs/7.2/locking-indexes.html
"PostgreSQL 7.2 - 13.7. Locking and Indexes")

__

13.7. Locking and Indexes  
---  
[Prev](mvcc-caveats.html "13.6. Caveats")  | [Up](mvcc.html "Chapter 13. Concurrency Control") | Chapter 13. Concurrency Control | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](performance-tips.html "Chapter 14. Performance Tips")  
  
* * *

## 13.7. Locking and Indexes #

Though PostgreSQL provides nonblocking read/write access to table data,
nonblocking read/write access is not currently offered for every index access
method implemented in PostgreSQL. The various index types are handled as
follows:

B-tree, GiST and SP-GiST indexes

    

Short-term share/exclusive page-level locks are used for read/write access.
Locks are released immediately after each index row is fetched or inserted.
These index types provide the highest concurrency without deadlock conditions.

Hash indexes

    

Share/exclusive hash-bucket-level locks are used for read/write access. Locks
are released after the whole bucket is processed. Bucket-level locks provide
better concurrency than index-level ones, but deadlock is possible since the
locks are held longer than one index operation.

GIN indexes

    

Short-term share/exclusive page-level locks are used for read/write access.
Locks are released immediately after each index row is fetched or inserted.
But note that insertion of a GIN-indexed value usually produces several index
key insertions per row, so GIN might do substantial work for a single value's
insertion.

Currently, B-tree indexes offer the best performance for concurrent
applications; since they also have more features than hash indexes, they are
the recommended index type for concurrent applications that need to index
scalar data. When dealing with non-scalar data, B-trees are not useful, and
GiST, SP-GiST or GIN indexes should be used instead.

* * *

[Prev](mvcc-caveats.html "13.6. Caveats")  | [Up](mvcc.html "Chapter 13. Concurrency Control") |  [Next](performance-tips.html "Chapter 14. Performance Tips")  
---|---|---  
13.6. Caveats  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 14. Performance Tips  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/locking-indexes.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

