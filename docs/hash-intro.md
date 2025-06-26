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

Supported Versions: [16](/docs/16/hash-intro.html "PostgreSQL 16 -
72.1. Overview") / [15](/docs/15/hash-intro.html "PostgreSQL 15 -
72.1. Overview") / [14](/docs/14/hash-intro.html "PostgreSQL 14 -
72.1. Overview") / [13](/docs/13/hash-intro.html "PostgreSQL 13 -
72.1. Overview")

Unsupported versions: [12](/docs/12/hash-intro.html "PostgreSQL 12 -
72.1. Overview") / [11](/docs/11/hash-intro.html "PostgreSQL 11 -
72.1. Overview") / [10](/docs/10/hash-intro.html "PostgreSQL 10 -
72.1. Overview")

__

72.1. Overview  
---  
[Prev](hash-index.html "Chapter 72. Hash Indexes")  | [Up](hash-index.html "Chapter 72. Hash Indexes") | Chapter 72. Hash Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](hash-implementation.html "72.2. Implementation")  
  
* * *

## 72.1. Overview #

PostgreSQL includes an implementation of persistent on-disk hash indexes,
which are fully crash recoverable. Any data type can be indexed by a hash
index, including data types that do not have a well-defined linear ordering.
Hash indexes store only the hash value of the data being indexed, thus there
are no restrictions on the size of the data column being indexed.

Hash indexes support only single-column indexes and do not allow uniqueness
checking.

Hash indexes support only the `=` operator, so WHERE clauses that specify
range operations will not be able to take advantage of hash indexes.

Each hash index tuple stores just the 4-byte hash value, not the actual column
value. As a result, hash indexes may be much smaller than B-trees when
indexing longer data items such as UUIDs, URLs, etc. The absence of the column
value also makes all hash index scans lossy. Hash indexes may take part in
bitmap index scans and backward scans.

Hash indexes are best optimized for SELECT and UPDATE-heavy workloads that use
equality scans on larger tables. In a B-tree index, searches must descend
through the tree until the leaf page is found. In tables with millions of
rows, this descent can increase access time to data. The equivalent of a leaf
page in a hash index is referred to as a bucket page. In contrast, a hash
index allows accessing the bucket pages directly, thereby potentially reducing
index access time in larger tables. This reduction in "logical I/O" becomes
even more pronounced on indexes/data larger than shared_buffers/RAM.

Hash indexes have been designed to cope with uneven distributions of hash
values. Direct access to the bucket pages works well if the hash values are
evenly distributed. When inserts mean that the bucket page becomes full,
additional overflow pages are chained to that specific bucket page, locally
expanding the storage for index tuples that match that hash value. When
scanning a hash bucket during queries, we need to scan through all of the
overflow pages. Thus an unbalanced hash index might actually be worse than a
B-tree in terms of number of block accesses required, for some data.

As a result of the overflow cases, we can say that hash indexes are most
suitable for unique, nearly unique data or data with a low number of rows per
hash bucket. One possible way to avoid problems is to exclude highly non-
unique values from the index using a partial index condition, but this may not
be suitable in many cases.

Like B-Trees, hash indexes perform simple index tuple deletion. This is a
deferred maintenance operation that deletes index tuples that are known to be
safe to delete (those whose item identifier's LP_DEAD bit is already set). If
an insert finds no space is available on a page we try to avoid creating a new
overflow page by attempting to remove dead index tuples. Removal cannot occur
if the page is pinned at that time. Deletion of dead index pointers also
occurs during VACUUM.

If it can, VACUUM will also try to squeeze the index tuples onto as few
overflow pages as possible, minimizing the overflow chain. If an overflow page
becomes empty, overflow pages can be recycled for reuse in other buckets,
though we never return them to the operating system. There is currently no
provision to shrink a hash index, other than by rebuilding it with REINDEX.
There is no provision for reducing the number of buckets, either.

Hash indexes may expand the number of bucket pages as the number of rows
indexed grows. The hash key-to-bucket-number mapping is chosen so that the
index can be incrementally expanded. When a new bucket is to be added to the
index, exactly one existing bucket will need to be "split", with some of its
tuples being transferred to the new bucket according to the updated key-to-
bucket-number mapping.

The expansion occurs in the foreground, which could increase execution time
for user inserts. Thus, hash indexes may not be suitable for tables with
rapidly increasing number of rows.

* * *

[Prev](hash-index.html "Chapter 72. Hash Indexes")  | [Up](hash-index.html "Chapter 72. Hash Indexes") |  [Next](hash-implementation.html "72.2. Implementation")  
---|---|---  
Chapter 72. Hash Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  72.2. Implementation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/hash-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

