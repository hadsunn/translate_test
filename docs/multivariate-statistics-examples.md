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

Supported Versions: [Current](/docs/current/multivariate-statistics-
examples.html "PostgreSQL 17 - 76.2. Multivariate Statistics Examples")
([17](/docs/17/multivariate-statistics-examples.html "PostgreSQL 17 -
76.2. Multivariate Statistics Examples")) / [16](/docs/16/multivariate-
statistics-examples.html "PostgreSQL 16 - 76.2. Multivariate Statistics
Examples") / [15](/docs/15/multivariate-statistics-examples.html "PostgreSQL
15 - 76.2. Multivariate Statistics Examples") / [14](/docs/14/multivariate-
statistics-examples.html "PostgreSQL 14 - 76.2. Multivariate Statistics
Examples") / [13](/docs/13/multivariate-statistics-examples.html "PostgreSQL
13 - 76.2. Multivariate Statistics Examples")

Development Versions: [18](/docs/18/multivariate-statistics-examples.html
"PostgreSQL 18 - 76.2. Multivariate Statistics Examples") /
[devel](/docs/devel/multivariate-statistics-examples.html "PostgreSQL devel -
76.2. Multivariate Statistics Examples")

Unsupported versions: [12](/docs/12/multivariate-statistics-examples.html
"PostgreSQL 12 - 76.2. Multivariate Statistics Examples") /
[11](/docs/11/multivariate-statistics-examples.html "PostgreSQL 11 -
76.2. Multivariate Statistics Examples") / [10](/docs/10/multivariate-
statistics-examples.html "PostgreSQL 10 - 76.2. Multivariate Statistics
Examples")

__

76.2. Multivariate Statistics Examples  
---  
[Prev](row-estimation-examples.html "76.1. Row Estimation Examples")  | [Up](planner-stats-details.html "Chapter 76. How the Planner Uses Statistics") | Chapter 76. How the Planner Uses Statistics | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](planner-stats-security.html "76.3. Planner Statistics and Security")  
  
* * *

## 76.2. Multivariate Statistics Examples #

[76.2.1. Functional Dependencies](multivariate-statistics-
examples.html#FUNCTIONAL-DEPENDENCIES)

[76.2.2. Multivariate N-Distinct Counts](multivariate-statistics-
examples.html#MULTIVARIATE-NDISTINCT-COUNTS)

[76.2.3. MCV Lists](multivariate-statistics-examples.html#MCV-LISTS)

### 76.2.1. Functional Dependencies #

Multivariate correlation can be demonstrated with a very simple data set — a
table with two columns, both containing the same values:

    
    
    CREATE TABLE t (a INT, b INT);
    INSERT INTO t SELECT i % 100, i % 100 FROM generate_series(1, 10000) s(i);
    ANALYZE t;
    

As explained in [Section 14.2](planner-stats.html "14.2. Statistics Used by
the Planner"), the planner can determine cardinality of `t` using the number
of pages and rows obtained from `pg_class`:

    
    
    SELECT relpages, reltuples FROM pg_class WHERE relname = 't';
    
     relpages | reltuples
    ----------+-----------
           45 |     10000
    

The data distribution is very simple; there are only 100 distinct values in
each column, uniformly distributed.

The following example shows the result of estimating a `WHERE` condition on
the `a` column:

    
    
    EXPLAIN (ANALYZE, TIMING OFF) SELECT * FROM t WHERE a = 1;
                                     QUERY PLAN
    -------------------------------------------------------------------​------------
     Seq Scan on t  (cost=0.00..170.00 rows=100 width=8) (actual rows=100 loops=1)
       Filter: (a = 1)
       Rows Removed by Filter: 9900
    

The planner examines the condition and determines the selectivity of this
clause to be 1%. By comparing this estimate and the actual number of rows, we
see that the estimate is very accurate (in fact exact, as the table is very
small). Changing the `WHERE` condition to use the `b` column, an identical
plan is generated. But observe what happens if we apply the same condition on
both columns, combining them with `AND`:

    
    
    EXPLAIN (ANALYZE, TIMING OFF) SELECT * FROM t WHERE a = 1 AND b = 1;
                                     QUERY PLAN
    -------------------------------------------------------------------​----------
     Seq Scan on t  (cost=0.00..195.00 rows=1 width=8) (actual rows=100 loops=1)
       Filter: ((a = 1) AND (b = 1))
       Rows Removed by Filter: 9900
    

The planner estimates the selectivity for each condition individually,
arriving at the same 1% estimates as above. Then it assumes that the
conditions are independent, and so it multiplies their selectivities,
producing a final selectivity estimate of just 0.01%. This is a significant
underestimate, as the actual number of rows matching the conditions (100) is
two orders of magnitude higher.

This problem can be fixed by creating a statistics object that directs
`ANALYZE` to calculate functional-dependency multivariate statistics on the
two columns:

    
    
    CREATE STATISTICS stts (dependencies) ON a, b FROM t;
    ANALYZE t;
    EXPLAIN (ANALYZE, TIMING OFF) SELECT * FROM t WHERE a = 1 AND b = 1;
                                      QUERY PLAN
    -------------------------------------------------------------------​------------
     Seq Scan on t  (cost=0.00..195.00 rows=100 width=8) (actual rows=100 loops=1)
       Filter: ((a = 1) AND (b = 1))
       Rows Removed by Filter: 9900
    

### 76.2.2. Multivariate N-Distinct Counts #

A similar problem occurs with estimation of the cardinality of sets of
multiple columns, such as the number of groups that would be generated by a
`GROUP BY` clause. When `GROUP BY` lists a single column, the n-distinct
estimate (which is visible as the estimated number of rows returned by the
HashAggregate node) is very accurate:

    
    
    EXPLAIN (ANALYZE, TIMING OFF) SELECT COUNT(*) FROM t GROUP BY a;
                                           QUERY PLAN
    -------------------------------------------------------------------​----------------------
     HashAggregate  (cost=195.00..196.00 rows=100 width=12) (actual rows=100 loops=1)
       Group Key: a
       ->  Seq Scan on t  (cost=0.00..145.00 rows=10000 width=4) (actual rows=10000 loops=1)
    

But without multivariate statistics, the estimate for the number of groups in
a query with two columns in `GROUP BY`, as in the following example, is off by
an order of magnitude:

    
    
    EXPLAIN (ANALYZE, TIMING OFF) SELECT COUNT(*) FROM t GROUP BY a, b;
                                           QUERY PLAN
    -------------------------------------------------------------------​-------------------------
     HashAggregate  (cost=220.00..230.00 rows=1000 width=16) (actual rows=100 loops=1)
       Group Key: a, b
       ->  Seq Scan on t  (cost=0.00..145.00 rows=10000 width=8) (actual rows=10000 loops=1)
    

By redefining the statistics object to include n-distinct counts for the two
columns, the estimate is much improved:

    
    
    DROP STATISTICS stts;
    CREATE STATISTICS stts (dependencies, ndistinct) ON a, b FROM t;
    ANALYZE t;
    EXPLAIN (ANALYZE, TIMING OFF) SELECT COUNT(*) FROM t GROUP BY a, b;
                                           QUERY PLAN
    -------------------------------------------------------------------​-------------------------
     HashAggregate  (cost=220.00..221.00 rows=100 width=16) (actual rows=100 loops=1)
       Group Key: a, b
       ->  Seq Scan on t  (cost=0.00..145.00 rows=10000 width=8) (actual rows=10000 loops=1)
    

### 76.2.3. MCV Lists #

As explained in [Section 76.2.1](multivariate-statistics-
examples.html#FUNCTIONAL-DEPENDENCIES "76.2.1. Functional Dependencies"),
functional dependencies are very cheap and efficient type of statistics, but
their main limitation is their global nature (only tracking dependencies at
the column level, not between individual column values).

This section introduces multivariate variant of MCV (most-common values)
lists, a straightforward extension of the per-column statistics described in
[Section 76.1](row-estimation-examples.html "76.1. Row Estimation Examples").
These statistics address the limitation by storing individual values, but it
is naturally more expensive, both in terms of building the statistics in
`ANALYZE`, storage and planning time.

Let's look at the query from [Section 76.2.1](multivariate-statistics-
examples.html#FUNCTIONAL-DEPENDENCIES "76.2.1. Functional Dependencies")
again, but this time with a MCV list created on the same set of columns (be
sure to drop the functional dependencies, to make sure the planner uses the
newly created statistics).

    
    
    DROP STATISTICS stts;
    CREATE STATISTICS stts2 (mcv) ON a, b FROM t;
    ANALYZE t;
    EXPLAIN (ANALYZE, TIMING OFF) SELECT * FROM t WHERE a = 1 AND b = 1;
                                       QUERY PLAN
    -------------------------------------------------------------------​------------
     Seq Scan on t  (cost=0.00..195.00 rows=100 width=8) (actual rows=100 loops=1)
       Filter: ((a = 1) AND (b = 1))
       Rows Removed by Filter: 9900
    

The estimate is as accurate as with the functional dependencies, mostly thanks
to the table being fairly small and having a simple distribution with a low
number of distinct values. Before looking at the second query, which was not
handled by functional dependencies particularly well, let's inspect the MCV
list a bit.

Inspecting the MCV list is possible using `pg_mcv_list_items` set-returning
function.

    
    
    SELECT m.* FROM pg_statistic_ext join pg_statistic_ext_data on (oid = stxoid),
                    pg_mcv_list_items(stxdmcv) m WHERE stxname = 'stts2';
     index |  values  | nulls | frequency | base_frequency
    -------+----------+-------+-----------+----------------
         0 | {0, 0}   | {f,f} |      0.01 |         0.0001
         1 | {1, 1}   | {f,f} |      0.01 |         0.0001
       ...
        49 | {49, 49} | {f,f} |      0.01 |         0.0001
        50 | {50, 50} | {f,f} |      0.01 |         0.0001
       ...
        97 | {97, 97} | {f,f} |      0.01 |         0.0001
        98 | {98, 98} | {f,f} |      0.01 |         0.0001
        99 | {99, 99} | {f,f} |      0.01 |         0.0001
    (100 rows)
    

This confirms there are 100 distinct combinations in the two columns, and all
of them are about equally likely (1% frequency for each one). The base
frequency is the frequency computed from per-column statistics, as if there
were no multi-column statistics. Had there been any null values in either of
the columns, this would be identified in the `nulls` column.

When estimating the selectivity, the planner applies all the conditions on
items in the MCV list, and then sums the frequencies of the matching ones. See
`mcv_clauselist_selectivity` in `src/backend/statistics/mcv.c` for details.

Compared to functional dependencies, MCV lists have two major advantages.
Firstly, the list stores actual values, making it possible to decide which
combinations are compatible.

    
    
    EXPLAIN (ANALYZE, TIMING OFF) SELECT * FROM t WHERE a = 1 AND b = 10;
                                     QUERY PLAN
    -------------------------------------------------------------------​--------
     Seq Scan on t  (cost=0.00..195.00 rows=1 width=8) (actual rows=0 loops=1)
       Filter: ((a = 1) AND (b = 10))
       Rows Removed by Filter: 10000
    

Secondly, MCV lists handle a wider range of clause types, not just equality
clauses like functional dependencies. For example, consider the following
range query for the same table:

    
    
    EXPLAIN (ANALYZE, TIMING OFF) SELECT * FROM t WHERE a <= 49 AND b > 49;
                                    QUERY PLAN
    -------------------------------------------------------------------​--------
     Seq Scan on t  (cost=0.00..195.00 rows=1 width=8) (actual rows=0 loops=1)
       Filter: ((a <= 49) AND (b > 49))
       Rows Removed by Filter: 10000
    

* * *

[Prev](row-estimation-examples.html "76.1. Row Estimation Examples")  | [Up](planner-stats-details.html "Chapter 76. How the Planner Uses Statistics") |  [Next](planner-stats-security.html "76.3. Planner Statistics and Security")  
---|---|---  
76.1. Row Estimation Examples  | [Home](index.html "PostgreSQL 16.9 Documentation") |  76.3. Planner Statistics and Security  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/multivariate-statistics-
examples.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

