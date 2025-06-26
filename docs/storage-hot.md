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

Supported Versions: [Current](/docs/current/storage-hot.html "PostgreSQL 17 -
73.7. Heap-Only Tuples \(HOT\)") ([17](/docs/17/storage-hot.html "PostgreSQL
17 - 73.7. Heap-Only Tuples \(HOT\)")) / [16](/docs/16/storage-hot.html
"PostgreSQL 16 - 73.7. Heap-Only Tuples \(HOT\)") / [15](/docs/15/storage-
hot.html "PostgreSQL 15 - 73.7. Heap-Only Tuples \(HOT\)") /
[14](/docs/14/storage-hot.html "PostgreSQL 14 - 73.7. Heap-Only Tuples
\(HOT\)") / [13](/docs/13/storage-hot.html "PostgreSQL 13 - 73.7. Heap-Only
Tuples \(HOT\)")

Development Versions: [18](/docs/18/storage-hot.html "PostgreSQL 18 -
73.7. Heap-Only Tuples \(HOT\)") / [devel](/docs/devel/storage-hot.html
"PostgreSQL devel - 73.7. Heap-Only Tuples \(HOT\)")

Unsupported versions: [12](/docs/12/storage-hot.html "PostgreSQL 12 -
73.7. Heap-Only Tuples \(HOT\)") / [11](/docs/11/storage-hot.html "PostgreSQL
11 - 73.7. Heap-Only Tuples \(HOT\)")

__

73.7. Heap-Only Tuples (HOT)  
---  
[Prev](storage-page-layout.html "73.6. Database Page Layout")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](transactions.html "Chapter 74. Transaction Processing")  
  
* * *

## 73.7. Heap-Only Tuples (HOT) #

To allow for high concurrency, PostgreSQL uses [multiversion concurrency
control](mvcc-intro.html "13.1. Introduction") (MVCC) to store rows. However,
MVCC has some downsides for update queries. Specifically, updates require new
versions of rows to be added to tables. This can also require new index
entries for each updated row, and removal of old versions of rows and their
index entries can be expensive.

To help reduce the overhead of updates, PostgreSQL has an optimization called
heap-only tuples (HOT). This optimization is possible when:

  * The update does not modify any columns referenced by the table's indexes, not including summarizing indexes. The only summarizing index method in the core PostgreSQL distribution is [BRIN](brin.html "Chapter 71. BRIN Indexes").

  * There is sufficient free space on the page containing the old row for the updated row.

In such cases, heap-only tuples provide two optimizations:

  * New index entries are not needed to represent updated rows, however, summary indexes may still need to be updated.

  * Old versions of updated rows can be completely removed during normal operation, including `SELECT`s, instead of requiring periodic vacuum operations. (This is possible because indexes do not reference their [page item identifiers](storage-page-layout.html "73.6. Database Page Layout").)

You can increase the likelihood of sufficient page space for HOT updates by
decreasing a table's [`fillfactor`](sql-createtable.html#RELOPTION-
FILLFACTOR). If you don't, HOT updates will still happen because new rows will
naturally migrate to new pages and existing pages with sufficient free space
for new row versions. The system view [pg_stat_all_tables](monitoring-
stats.html#MONITORING-PG-STAT-ALL-TABLES-VIEW "28.2.18. pg_stat_all_tables")
allows monitoring of the occurrence of HOT and non-HOT updates.

* * *

[Prev](storage-page-layout.html "73.6. Database Page Layout")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](transactions.html "Chapter 74. Transaction Processing")  
---|---|---  
73.6. Database Page Layout  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 74. Transaction Processing  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-hot.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

