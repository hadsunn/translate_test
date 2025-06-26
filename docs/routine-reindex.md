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

Supported Versions: [Current](/docs/current/routine-reindex.html "PostgreSQL
17 - 25.2. Routine Reindexing") ([17](/docs/17/routine-reindex.html
"PostgreSQL 17 - 25.2. Routine Reindexing")) / [16](/docs/16/routine-
reindex.html "PostgreSQL 16 - 25.2. Routine Reindexing") /
[15](/docs/15/routine-reindex.html "PostgreSQL 15 - 25.2. Routine Reindexing")
/ [14](/docs/14/routine-reindex.html "PostgreSQL 14 - 25.2. Routine
Reindexing") / [13](/docs/13/routine-reindex.html "PostgreSQL 13 -
25.2. Routine Reindexing")

Development Versions: [18](/docs/18/routine-reindex.html "PostgreSQL 18 -
25.2. Routine Reindexing") / [devel](/docs/devel/routine-reindex.html
"PostgreSQL devel - 25.2. Routine Reindexing")

Unsupported versions: [12](/docs/12/routine-reindex.html "PostgreSQL 12 -
25.2. Routine Reindexing") / [11](/docs/11/routine-reindex.html "PostgreSQL 11
- 25.2. Routine Reindexing") / [10](/docs/10/routine-reindex.html "PostgreSQL
10 - 25.2. Routine Reindexing") / [9.6](/docs/9.6/routine-reindex.html
"PostgreSQL 9.6 - 25.2. Routine Reindexing") / [9.5](/docs/9.5/routine-
reindex.html "PostgreSQL 9.5 - 25.2. Routine Reindexing") /
[9.4](/docs/9.4/routine-reindex.html "PostgreSQL 9.4 - 25.2. Routine
Reindexing") / [9.3](/docs/9.3/routine-reindex.html "PostgreSQL 9.3 -
25.2. Routine Reindexing") / [9.2](/docs/9.2/routine-reindex.html "PostgreSQL
9.2 - 25.2. Routine Reindexing") / [9.1](/docs/9.1/routine-reindex.html
"PostgreSQL 9.1 - 25.2. Routine Reindexing") / [9.0](/docs/9.0/routine-
reindex.html "PostgreSQL 9.0 - 25.2. Routine Reindexing") /
[8.4](/docs/8.4/routine-reindex.html "PostgreSQL 8.4 - 25.2. Routine
Reindexing") / [8.3](/docs/8.3/routine-reindex.html "PostgreSQL 8.3 -
25.2. Routine Reindexing") / [8.2](/docs/8.2/routine-reindex.html "PostgreSQL
8.2 - 25.2. Routine Reindexing") / [8.1](/docs/8.1/routine-reindex.html
"PostgreSQL 8.1 - 25.2. Routine Reindexing") / [8.0](/docs/8.0/routine-
reindex.html "PostgreSQL 8.0 - 25.2. Routine Reindexing") /
[7.4](/docs/7.4/routine-reindex.html "PostgreSQL 7.4 - 25.2. Routine
Reindexing") / [7.3](/docs/7.3/routine-reindex.html "PostgreSQL 7.3 -
25.2. Routine Reindexing")

__

25.2. Routine Reindexing  
---  
[Prev](routine-vacuuming.html "25.1. Routine Vacuuming")  | [Up](maintenance.html "Chapter 25. Routine Database Maintenance Tasks") | Chapter 25. Routine Database Maintenance Tasks | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logfile-maintenance.html "25.3. Log File Maintenance")  
  
* * *

## 25.2. Routine Reindexing #

In some situations it is worthwhile to rebuild indexes periodically with the
[REINDEX](sql-reindex.html "REINDEX") command or a series of individual
rebuilding steps.

B-tree index pages that have become completely empty are reclaimed for re-use.
However, there is still a possibility of inefficient use of space: if all but
a few index keys on a page have been deleted, the page remains allocated.
Therefore, a usage pattern in which most, but not all, keys in each range are
eventually deleted will see poor use of space. For such usage patterns,
periodic reindexing is recommended.

The potential for bloat in non-B-tree indexes has not been well researched. It
is a good idea to periodically monitor the index's physical size when using
any non-B-tree index type.

Also, for B-tree indexes, a freshly-constructed index is slightly faster to
access than one that has been updated many times because logically adjacent
pages are usually also physically adjacent in a newly built index. (This
consideration does not apply to non-B-tree indexes.) It might be worthwhile to
reindex periodically just to improve access speed.

[REINDEX](sql-reindex.html "REINDEX") can be used safely and easily in all
cases. This command requires an `ACCESS EXCLUSIVE` lock by default, hence it
is often preferable to execute it with its `CONCURRENTLY` option, which
requires only a `SHARE UPDATE EXCLUSIVE` lock.

* * *

[Prev](routine-vacuuming.html "25.1. Routine Vacuuming")  | [Up](maintenance.html "Chapter 25. Routine Database Maintenance Tasks") |  [Next](logfile-maintenance.html "25.3. Log File Maintenance")  
---|---|---  
25.1. Routine Vacuuming  | [Home](index.html "PostgreSQL 16.9 Documentation") |  25.3. Log File Maintenance  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/routine-reindex.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

