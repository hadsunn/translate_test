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

Supported Versions: [Current](/docs/current/indexes-examine.html "PostgreSQL
17 - 11.12. Examining Index Usage") ([17](/docs/17/indexes-examine.html
"PostgreSQL 17 - 11.12. Examining Index Usage")) / [16](/docs/16/indexes-
examine.html "PostgreSQL 16 - 11.12. Examining Index Usage") /
[15](/docs/15/indexes-examine.html "PostgreSQL 15 - 11.12. Examining Index
Usage") / [14](/docs/14/indexes-examine.html "PostgreSQL 14 - 11.12. Examining
Index Usage") / [13](/docs/13/indexes-examine.html "PostgreSQL 13 -
11.12. Examining Index Usage")

Development Versions: [18](/docs/18/indexes-examine.html "PostgreSQL 18 -
11.12. Examining Index Usage") / [devel](/docs/devel/indexes-examine.html
"PostgreSQL devel - 11.12. Examining Index Usage")

Unsupported versions: [12](/docs/12/indexes-examine.html "PostgreSQL 12 -
11.12. Examining Index Usage") / [11](/docs/11/indexes-examine.html
"PostgreSQL 11 - 11.12. Examining Index Usage") / [10](/docs/10/indexes-
examine.html "PostgreSQL 10 - 11.12. Examining Index Usage") /
[9.6](/docs/9.6/indexes-examine.html "PostgreSQL 9.6 - 11.12. Examining Index
Usage") / [9.5](/docs/9.5/indexes-examine.html "PostgreSQL 9.5 -
11.12. Examining Index Usage") / [9.4](/docs/9.4/indexes-examine.html
"PostgreSQL 9.4 - 11.12. Examining Index Usage") / [9.3](/docs/9.3/indexes-
examine.html "PostgreSQL 9.3 - 11.12. Examining Index Usage") /
[9.2](/docs/9.2/indexes-examine.html "PostgreSQL 9.2 - 11.12. Examining Index
Usage") / [9.1](/docs/9.1/indexes-examine.html "PostgreSQL 9.1 -
11.12. Examining Index Usage") / [9.0](/docs/9.0/indexes-examine.html
"PostgreSQL 9.0 - 11.12. Examining Index Usage") / [8.4](/docs/8.4/indexes-
examine.html "PostgreSQL 8.4 - 11.12. Examining Index Usage") /
[8.3](/docs/8.3/indexes-examine.html "PostgreSQL 8.3 - 11.12. Examining Index
Usage") / [8.2](/docs/8.2/indexes-examine.html "PostgreSQL 8.2 -
11.12. Examining Index Usage") / [8.1](/docs/8.1/indexes-examine.html
"PostgreSQL 8.1 - 11.12. Examining Index Usage") / [8.0](/docs/8.0/indexes-
examine.html "PostgreSQL 8.0 - 11.12. Examining Index Usage") /
[7.4](/docs/7.4/indexes-examine.html "PostgreSQL 7.4 - 11.12. Examining Index
Usage") / [7.3](/docs/7.3/indexes-examine.html "PostgreSQL 7.3 -
11.12. Examining Index Usage") / [7.2](/docs/7.2/indexes-examine.html
"PostgreSQL 7.2 - 11.12. Examining Index Usage")

__

11.12. Examining Index Usage  
---  
[Prev](indexes-collations.html "11.11. Indexes and Collations")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch.html "Chapter 12. Full Text Search")  
  
* * *

## 11.12. Examining Index Usage #

Although indexes in PostgreSQL do not need maintenance or tuning, it is still
important to check which indexes are actually used by the real-life query
workload. Examining index usage for an individual query is done with the
[EXPLAIN](sql-explain.html "EXPLAIN") command; its application for this
purpose is illustrated in [Section 14.1](using-explain.html "14.1. Using
EXPLAIN"). It is also possible to gather overall statistics about index usage
in a running server, as described in [Section 28.2](monitoring-stats.html
"28.2. The Cumulative Statistics System").

It is difficult to formulate a general procedure for determining which indexes
to create. There are a number of typical cases that have been shown in the
examples throughout the previous sections. A good deal of experimentation is
often necessary. The rest of this section gives some tips for that:

  * Always run [ANALYZE](sql-analyze.html "ANALYZE") first. This command collects statistics about the distribution of the values in the table. This information is required to estimate the number of rows returned by a query, which is needed by the planner to assign realistic costs to each possible query plan. In absence of any real statistics, some default values are assumed, which are almost certain to be inaccurate. Examining an application's index usage without having run `ANALYZE` is therefore a lost cause. See [Section 25.1.3](routine-vacuuming.html#VACUUM-FOR-STATISTICS "25.1.3. Updating Planner Statistics") and [Section 25.1.6](routine-vacuuming.html#AUTOVACUUM "25.1.6. The Autovacuum Daemon") for more information.

  * Use real data for experimentation. Using test data for setting up indexes will tell you what indexes you need for the test data, but that is all.

It is especially fatal to use very small test data sets. While selecting 1000
out of 100000 rows could be a candidate for an index, selecting 1 out of 100
rows will hardly be, because the 100 rows probably fit within a single disk
page, and there is no plan that can beat sequentially fetching 1 disk page.

Also be careful when making up test data, which is often unavoidable when the
application is not yet in production. Values that are very similar, completely
random, or inserted in sorted order will skew the statistics away from the
distribution that real data would have.

  * When indexes are not used, it can be useful for testing to force their use. There are run-time parameters that can turn off various plan types (see [Section 20.7.1](runtime-config-query.html#RUNTIME-CONFIG-QUERY-ENABLE "20.7.1. Planner Method Configuration")). For instance, turning off sequential scans (`enable_seqscan`) and nested-loop joins (`enable_nestloop`), which are the most basic plans, will force the system to use a different plan. If the system still chooses a sequential scan or nested-loop join then there is probably a more fundamental reason why the index is not being used; for example, the query condition does not match the index. (What kind of query can use what kind of index is explained in the previous sections.)

  * If forcing index usage does use the index, then there are two possibilities: Either the system is right and using the index is indeed not appropriate, or the cost estimates of the query plans are not reflecting reality. So you should time your query with and without indexes. The `EXPLAIN ANALYZE` command can be useful here.

  * If it turns out that the cost estimates are wrong, there are, again, two possibilities. The total cost is computed from the per-row costs of each plan node times the selectivity estimate of the plan node. The costs estimated for the plan nodes can be adjusted via run-time parameters (described in [Section 20.7.2](runtime-config-query.html#RUNTIME-CONFIG-QUERY-CONSTANTS "20.7.2. Planner Cost Constants")). An inaccurate selectivity estimate is due to insufficient statistics. It might be possible to improve this by tuning the statistics-gathering parameters (see [ALTER TABLE](sql-altertable.html "ALTER TABLE")).

If you do not succeed in adjusting the costs to be more appropriate, then you
might have to resort to forcing index usage explicitly. You might also want to
contact the PostgreSQL developers to examine the issue.

* * *

[Prev](indexes-collations.html "11.11. Indexes and Collations")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](textsearch.html "Chapter 12. Full Text Search")  
---|---|---  
11.11. Indexes and Collations  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 12. Full Text Search  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-examine.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

