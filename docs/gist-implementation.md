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

Supported Versions: [16](/docs/16/gist-implementation.html "PostgreSQL 16 -
68.4. Implementation") / [15](/docs/15/gist-implementation.html "PostgreSQL 15
- 68.4. Implementation") / [14](/docs/14/gist-implementation.html "PostgreSQL
14 - 68.4. Implementation") / [13](/docs/13/gist-implementation.html
"PostgreSQL 13 - 68.4. Implementation")

Unsupported versions: [12](/docs/12/gist-implementation.html "PostgreSQL 12 -
68.4. Implementation") / [11](/docs/11/gist-implementation.html "PostgreSQL 11
- 68.4. Implementation") / [10](/docs/10/gist-implementation.html "PostgreSQL
10 - 68.4. Implementation") / [9.6](/docs/9.6/gist-implementation.html
"PostgreSQL 9.6 - 68.4. Implementation") / [9.5](/docs/9.5/gist-
implementation.html "PostgreSQL 9.5 - 68.4. Implementation") /
[9.4](/docs/9.4/gist-implementation.html "PostgreSQL 9.4 -
68.4. Implementation") / [9.3](/docs/9.3/gist-implementation.html "PostgreSQL
9.3 - 68.4. Implementation") / [9.2](/docs/9.2/gist-implementation.html
"PostgreSQL 9.2 - 68.4. Implementation") / [9.1](/docs/9.1/gist-
implementation.html "PostgreSQL 9.1 - 68.4. Implementation") /
[9.0](/docs/9.0/gist-implementation.html "PostgreSQL 9.0 -
68.4. Implementation") / [8.4](/docs/8.4/gist-implementation.html "PostgreSQL
8.4 - 68.4. Implementation") / [8.3](/docs/8.3/gist-implementation.html
"PostgreSQL 8.3 - 68.4. Implementation") / [8.2](/docs/8.2/gist-
implementation.html "PostgreSQL 8.2 - 68.4. Implementation") /
[8.1](/docs/8.1/gist-implementation.html "PostgreSQL 8.1 -
68.4. Implementation")

__

68.4. Implementation  
---  
[Prev](gist-extensibility.html "68.3. Extensibility")  | [Up](gist.html "Chapter 68. GiST Indexes") | Chapter 68. GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gist-examples.html "68.5. Examples")  
  
* * *

## 68.4. Implementation #

[68.4.1. GiST Index Build Methods](gist-implementation.html#GIST-BUFFERING-
BUILD)

### 68.4.1. GiST Index Build Methods #

The simplest way to build a GiST index is just to insert all the entries, one
by one. This tends to be slow for large indexes, because if the index tuples
are scattered across the index and the index is large enough to not fit in
cache, a lot of random I/O will be needed. PostgreSQL supports two alternative
methods for initial build of a GiST index: _sorted_ and _buffered_ modes.

The sorted method is only available if each of the opclasses used by the index
provides a `sortsupport` function, as described in [Section 68.3](gist-
extensibility.html "68.3. Extensibility"). If they do, this method is usually
the best, so it is used by default.

The buffered method works by not inserting tuples directly into the index
right away. It can dramatically reduce the amount of random I/O needed for
non-ordered data sets. For well-ordered data sets the benefit is smaller or
non-existent, because only a small number of pages receive new tuples at a
time, and those pages fit in cache even if the index as a whole does not.

The buffered method needs to call the `penalty` function more often than the
simple method does, which consumes some extra CPU resources. Also, the buffers
need temporary disk space, up to the size of the resulting index. Buffering
can also influence the quality of the resulting index, in both positive and
negative directions. That influence depends on various factors, like the
distribution of the input data and the operator class implementation.

If sorting is not possible, then by default a GiST index build switches to the
buffering method when the index size reaches [effective_cache_size](runtime-
config-query.html#GUC-EFFECTIVE-CACHE-SIZE). Buffering can be manually forced
or prevented by the `buffering` parameter to the CREATE INDEX command. The
default behavior is good for most cases, but turning buffering off might speed
up the build somewhat if the input data is ordered.

* * *

[Prev](gist-extensibility.html "68.3. Extensibility")  | [Up](gist.html "Chapter 68. GiST Indexes") |  [Next](gist-examples.html "68.5. Examples")  
---|---|---  
68.3. Extensibility  | [Home](index.html "PostgreSQL 16.9 Documentation") |  68.5. Examples  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gist-implementation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

