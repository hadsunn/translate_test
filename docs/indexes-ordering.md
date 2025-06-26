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

Supported Versions: [Current](/docs/current/indexes-ordering.html "PostgreSQL
17 - 11.4. Indexes and ORDER BY") ([17](/docs/17/indexes-ordering.html
"PostgreSQL 17 - 11.4. Indexes and ORDER BY")) / [16](/docs/16/indexes-
ordering.html "PostgreSQL 16 - 11.4. Indexes and ORDER BY") /
[15](/docs/15/indexes-ordering.html "PostgreSQL 15 - 11.4. Indexes and ORDER
BY") / [14](/docs/14/indexes-ordering.html "PostgreSQL 14 - 11.4. Indexes and
ORDER BY") / [13](/docs/13/indexes-ordering.html "PostgreSQL 13 -
11.4. Indexes and ORDER BY")

Development Versions: [18](/docs/18/indexes-ordering.html "PostgreSQL 18 -
11.4. Indexes and ORDER BY") / [devel](/docs/devel/indexes-ordering.html
"PostgreSQL devel - 11.4. Indexes and ORDER BY")

Unsupported versions: [12](/docs/12/indexes-ordering.html "PostgreSQL 12 -
11.4. Indexes and ORDER BY") / [11](/docs/11/indexes-ordering.html "PostgreSQL
11 - 11.4. Indexes and ORDER BY") / [10](/docs/10/indexes-ordering.html
"PostgreSQL 10 - 11.4. Indexes and ORDER BY") / [9.6](/docs/9.6/indexes-
ordering.html "PostgreSQL 9.6 - 11.4. Indexes and ORDER BY") /
[9.5](/docs/9.5/indexes-ordering.html "PostgreSQL 9.5 - 11.4. Indexes and
ORDER BY") / [9.4](/docs/9.4/indexes-ordering.html "PostgreSQL 9.4 -
11.4. Indexes and ORDER BY") / [9.3](/docs/9.3/indexes-ordering.html
"PostgreSQL 9.3 - 11.4. Indexes and ORDER BY") / [9.2](/docs/9.2/indexes-
ordering.html "PostgreSQL 9.2 - 11.4. Indexes and ORDER BY") /
[9.1](/docs/9.1/indexes-ordering.html "PostgreSQL 9.1 - 11.4. Indexes and
ORDER BY") / [9.0](/docs/9.0/indexes-ordering.html "PostgreSQL 9.0 -
11.4. Indexes and ORDER BY") / [8.4](/docs/8.4/indexes-ordering.html
"PostgreSQL 8.4 - 11.4. Indexes and ORDER BY") / [8.3](/docs/8.3/indexes-
ordering.html "PostgreSQL 8.3 - 11.4. Indexes and ORDER BY")

__

11.4. Indexes and `ORDER BY`  
---  
[Prev](indexes-multicolumn.html "11.3. Multicolumn Indexes")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-bitmap-scans.html "11.5. Combining Multiple Indexes")  
  
* * *

## 11.4. Indexes and `ORDER BY` #

In addition to simply finding the rows to be returned by a query, an index may
be able to deliver them in a specific sorted order. This allows a query's
`ORDER BY` specification to be honored without a separate sorting step. Of the
index types currently supported by PostgreSQL, only B-tree can produce sorted
output — the other index types return matching rows in an unspecified,
implementation-dependent order.

The planner will consider satisfying an `ORDER BY` specification either by
scanning an available index that matches the specification, or by scanning the
table in physical order and doing an explicit sort. For a query that requires
scanning a large fraction of the table, an explicit sort is likely to be
faster than using an index because it requires less disk I/O due to following
a sequential access pattern. Indexes are more useful when only a few rows need
be fetched. An important special case is `ORDER BY` in combination with
`LIMIT` _`n`_ : an explicit sort will have to process all the data to identify
the first _`n`_ rows, but if there is an index matching the `ORDER BY`, the
first _`n`_ rows can be retrieved directly, without scanning the remainder at
all.

By default, B-tree indexes store their entries in ascending order with nulls
last (table TID is treated as a tiebreaker column among otherwise equal
entries). This means that a forward scan of an index on column `x` produces
output satisfying `ORDER BY x` (or more verbosely, `ORDER BY x ASC NULLS
LAST`). The index can also be scanned backward, producing output satisfying
`ORDER BY x DESC` (or more verbosely, `ORDER BY x DESC NULLS FIRST`, since
`NULLS FIRST` is the default for `ORDER BY DESC`).

You can adjust the ordering of a B-tree index by including the options `ASC`,
`DESC`, `NULLS FIRST`, and/or `NULLS LAST` when creating the index; for
example:

    
    
    CREATE INDEX test2_info_nulls_low ON test2 (info NULLS FIRST);
    CREATE INDEX test3_desc_index ON test3 (id DESC NULLS LAST);
    

An index stored in ascending order with nulls first can satisfy either `ORDER
BY x ASC NULLS FIRST` or `ORDER BY x DESC NULLS LAST` depending on which
direction it is scanned in.

You might wonder why bother providing all four options, when two options
together with the possibility of backward scan would cover all the variants of
`ORDER BY`. In single-column indexes the options are indeed redundant, but in
multicolumn indexes they can be useful. Consider a two-column index on `(x,
y)`: this can satisfy `ORDER BY x, y` if we scan forward, or `ORDER BY x DESC,
y DESC` if we scan backward. But it might be that the application frequently
needs to use `ORDER BY x ASC, y DESC`. There is no way to get that ordering
from a plain index, but it is possible if the index is defined as `(x ASC, y
DESC)` or `(x DESC, y ASC)`.

Obviously, indexes with non-default sort orderings are a fairly specialized
feature, but sometimes they can produce tremendous speedups for certain
queries. Whether it's worth maintaining such an index depends on how often you
use queries that require a special sort ordering.

* * *

[Prev](indexes-multicolumn.html "11.3. Multicolumn Indexes")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-bitmap-scans.html "11.5. Combining Multiple Indexes")  
---|---|---  
11.3. Multicolumn Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.5. Combining Multiple Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-ordering.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

