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

Supported Versions: [16](/docs/16/hash-implementation.html "PostgreSQL 16 -
72.2. Implementation") / [15](/docs/15/hash-implementation.html "PostgreSQL 15
- 72.2. Implementation") / [14](/docs/14/hash-implementation.html "PostgreSQL
14 - 72.2. Implementation") / [13](/docs/13/hash-implementation.html
"PostgreSQL 13 - 72.2. Implementation")

Unsupported versions: [12](/docs/12/hash-implementation.html "PostgreSQL 12 -
72.2. Implementation") / [11](/docs/11/hash-implementation.html "PostgreSQL 11
- 72.2. Implementation") / [10](/docs/10/hash-implementation.html "PostgreSQL
10 - 72.2. Implementation")

__

72.2. Implementation  
---  
[Prev](hash-intro.html "72.1. Overview")  | [Up](hash-index.html "Chapter 72. Hash Indexes") | Chapter 72. Hash Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage.html "Chapter 73. Database Physical Storage")  
  
* * *

## 72.2. Implementation #

There are four kinds of pages in a hash index: the meta page (page zero),
which contains statically allocated control information; primary bucket pages;
overflow pages; and bitmap pages, which keep track of overflow pages that have
been freed and are available for re-use. For addressing purposes, bitmap pages
are regarded as a subset of the overflow pages.

Both scanning the index and inserting tuples require locating the bucket where
a given tuple ought to be located. To do this, we need the bucket count,
highmask, and lowmask from the metapage; however, it's undesirable for
performance reasons to have to have to lock and pin the metapage for every
such operation. Instead, we retain a cached copy of the metapage in each
backend's relcache entry. This will produce the correct bucket mapping as long
as the target bucket hasn't been split since the last cache refresh.

Primary bucket pages and overflow pages are allocated independently since any
given index might need more or fewer overflow pages relative to its number of
buckets. The hash code uses an interesting set of addressing rules to support
a variable number of overflow pages while not having to move primary bucket
pages around after they are created.

Each row in the table indexed is represented by a single index tuple in the
hash index. Hash index tuples are stored in bucket pages, and if they exist,
overflow pages. We speed up searches by keeping the index entries in any one
index page sorted by hash code, thus allowing binary search to be used within
an index page. Note however that there is *no* assumption about the relative
ordering of hash codes across different index pages of a bucket.

The bucket splitting algorithms to expand the hash index are too complex to be
worthy of mention here, though are described in more detail in
`src/backend/access/hash/README`. The split algorithm is crash safe and can be
restarted if not completed successfully.

* * *

[Prev](hash-intro.html "72.1. Overview")  | [Up](hash-index.html "Chapter 72. Hash Indexes") |  [Next](storage.html "Chapter 73. Database Physical Storage")  
---|---|---  
72.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 73. Database Physical Storage  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/hash-implementation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

