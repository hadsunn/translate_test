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

Supported Versions: [Current](/docs/current/indexes-bitmap-scans.html
"PostgreSQL 17 - 11.5. Combining Multiple Indexes") ([17](/docs/17/indexes-
bitmap-scans.html "PostgreSQL 17 - 11.5. Combining Multiple Indexes")) /
[16](/docs/16/indexes-bitmap-scans.html "PostgreSQL 16 - 11.5. Combining
Multiple Indexes") / [15](/docs/15/indexes-bitmap-scans.html "PostgreSQL 15 -
11.5. Combining Multiple Indexes") / [14](/docs/14/indexes-bitmap-scans.html
"PostgreSQL 14 - 11.5. Combining Multiple Indexes") / [13](/docs/13/indexes-
bitmap-scans.html "PostgreSQL 13 - 11.5. Combining Multiple Indexes")

Development Versions: [18](/docs/18/indexes-bitmap-scans.html "PostgreSQL 18 -
11.5. Combining Multiple Indexes") / [devel](/docs/devel/indexes-bitmap-
scans.html "PostgreSQL devel - 11.5. Combining Multiple Indexes")

Unsupported versions: [12](/docs/12/indexes-bitmap-scans.html "PostgreSQL 12 -
11.5. Combining Multiple Indexes") / [11](/docs/11/indexes-bitmap-scans.html
"PostgreSQL 11 - 11.5. Combining Multiple Indexes") / [10](/docs/10/indexes-
bitmap-scans.html "PostgreSQL 10 - 11.5. Combining Multiple Indexes") /
[9.6](/docs/9.6/indexes-bitmap-scans.html "PostgreSQL 9.6 - 11.5. Combining
Multiple Indexes") / [9.5](/docs/9.5/indexes-bitmap-scans.html "PostgreSQL 9.5
- 11.5. Combining Multiple Indexes") / [9.4](/docs/9.4/indexes-bitmap-
scans.html "PostgreSQL 9.4 - 11.5. Combining Multiple Indexes") /
[9.3](/docs/9.3/indexes-bitmap-scans.html "PostgreSQL 9.3 - 11.5. Combining
Multiple Indexes") / [9.2](/docs/9.2/indexes-bitmap-scans.html "PostgreSQL 9.2
- 11.5. Combining Multiple Indexes") / [9.1](/docs/9.1/indexes-bitmap-
scans.html "PostgreSQL 9.1 - 11.5. Combining Multiple Indexes") /
[9.0](/docs/9.0/indexes-bitmap-scans.html "PostgreSQL 9.0 - 11.5. Combining
Multiple Indexes") / [8.4](/docs/8.4/indexes-bitmap-scans.html "PostgreSQL 8.4
- 11.5. Combining Multiple Indexes") / [8.3](/docs/8.3/indexes-bitmap-
scans.html "PostgreSQL 8.3 - 11.5. Combining Multiple Indexes") /
[8.2](/docs/8.2/indexes-bitmap-scans.html "PostgreSQL 8.2 - 11.5. Combining
Multiple Indexes") / [8.1](/docs/8.1/indexes-bitmap-scans.html "PostgreSQL 8.1
- 11.5. Combining Multiple Indexes")

__

11.5. Combining Multiple Indexes  
---  
[Prev](indexes-ordering.html "11.4. Indexes and ORDER BY")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-unique.html "11.6. Unique Indexes")  
  
* * *

## 11.5. Combining Multiple Indexes #

A single index scan can only use query clauses that use the index's columns
with operators of its operator class and are joined with `AND`. For example,
given an index on `(a, b)` a query condition like `WHERE a = 5 AND b = 6`
could use the index, but a query like `WHERE a = 5 OR b = 6` could not
directly use the index.

Fortunately, PostgreSQL has the ability to combine multiple indexes (including
multiple uses of the same index) to handle cases that cannot be implemented by
single index scans. The system can form `AND` and `OR` conditions across
several index scans. For example, a query like `WHERE x = 42 OR x = 47 OR x =
53 OR x = 99` could be broken down into four separate scans of an index on
`x`, each scan using one of the query clauses. The results of these scans are
then ORed together to produce the result. Another example is that if we have
separate indexes on `x` and `y`, one possible implementation of a query like
`WHERE x = 5 AND y = 6` is to use each index with the appropriate query clause
and then AND together the index results to identify the result rows.

To combine multiple indexes, the system scans each needed index and prepares a
_bitmap_ in memory giving the locations of table rows that are reported as
matching that index's conditions. The bitmaps are then ANDed and ORed together
as needed by the query. Finally, the actual table rows are visited and
returned. The table rows are visited in physical order, because that is how
the bitmap is laid out; this means that any ordering of the original indexes
is lost, and so a separate sort step will be needed if the query has an `ORDER
BY` clause. For this reason, and because each additional index scan adds extra
time, the planner will sometimes choose to use a simple index scan even though
additional indexes are available that could have been used as well.

In all but the simplest applications, there are various combinations of
indexes that might be useful, and the database developer must make trade-offs
to decide which indexes to provide. Sometimes multicolumn indexes are best,
but sometimes it's better to create separate indexes and rely on the index-
combination feature. For example, if your workload includes a mix of queries
that sometimes involve only column `x`, sometimes only column `y`, and
sometimes both columns, you might choose to create two separate indexes on `x`
and `y`, relying on index combination to process the queries that use both
columns. You could also create a multicolumn index on `(x, y)`. This index
would typically be more efficient than index combination for queries involving
both columns, but as discussed in [Section 11.3](indexes-multicolumn.html
"11.3. Multicolumn Indexes"), it would be almost useless for queries involving
only `y`, so it should not be the only index. A combination of the multicolumn
index and a separate index on `y` would serve reasonably well. For queries
involving only `x`, the multicolumn index could be used, though it would be
larger and hence slower than an index on `x` alone. The last alternative is to
create all three indexes, but this is probably only reasonable if the table is
searched much more often than it is updated and all three types of query are
common. If one of the types of query is much less common than the others,
you'd probably settle for creating just the two indexes that best match the
common types.

* * *

[Prev](indexes-ordering.html "11.4. Indexes and ORDER BY")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-unique.html "11.6. Unique Indexes")  
---|---|---  
11.4. Indexes and `ORDER BY`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.6. Unique Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-bitmap-scans.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

