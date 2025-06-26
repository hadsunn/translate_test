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

Supported Versions: [Current](/docs/current/how-parallel-query-works.html
"PostgreSQL 17 - 15.1. How Parallel Query Works") ([17](/docs/17/how-parallel-
query-works.html "PostgreSQL 17 - 15.1. How Parallel Query Works")) /
[16](/docs/16/how-parallel-query-works.html "PostgreSQL 16 - 15.1. How
Parallel Query Works") / [15](/docs/15/how-parallel-query-works.html
"PostgreSQL 15 - 15.1. How Parallel Query Works") / [14](/docs/14/how-
parallel-query-works.html "PostgreSQL 14 - 15.1. How Parallel Query Works") /
[13](/docs/13/how-parallel-query-works.html "PostgreSQL 13 - 15.1. How
Parallel Query Works")

Development Versions: [18](/docs/18/how-parallel-query-works.html "PostgreSQL
18 - 15.1. How Parallel Query Works") / [devel](/docs/devel/how-parallel-
query-works.html "PostgreSQL devel - 15.1. How Parallel Query Works")

Unsupported versions: [12](/docs/12/how-parallel-query-works.html "PostgreSQL
12 - 15.1. How Parallel Query Works") / [11](/docs/11/how-parallel-query-
works.html "PostgreSQL 11 - 15.1. How Parallel Query Works") /
[10](/docs/10/how-parallel-query-works.html "PostgreSQL 10 - 15.1. How
Parallel Query Works") / [9.6](/docs/9.6/how-parallel-query-works.html
"PostgreSQL 9.6 - 15.1. How Parallel Query Works")

__

15.1. How Parallel Query Works  
---  
[Prev](parallel-query.html "Chapter 15. Parallel Query")  | [Up](parallel-query.html "Chapter 15. Parallel Query") | Chapter 15. Parallel Query | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](when-can-parallel-query-be-used.html "15.2. When Can Parallel Query Be Used?")  
  
* * *

## 15.1. How Parallel Query Works #

When the optimizer determines that parallel query is the fastest execution
strategy for a particular query, it will create a query plan that includes a
_Gather_ or _Gather Merge_ node. Here is a simple example:

    
    
    EXPLAIN SELECT * FROM pgbench_accounts WHERE filler LIKE '%x%';
                                         QUERY PLAN
    -------------------------------------------------------------------​------------------
     Gather  (cost=1000.00..217018.43 rows=1 width=97)
       Workers Planned: 2
       ->  Parallel Seq Scan on pgbench_accounts  (cost=0.00..216018.33 rows=1 width=97)
             Filter: (filler ~~ '%x%'::text)
    (4 rows)
    

In all cases, the `Gather` or `Gather Merge` node will have exactly one child
plan, which is the portion of the plan that will be executed in parallel. If
the `Gather` or `Gather Merge` node is at the very top of the plan tree, then
the entire query will execute in parallel. If it is somewhere else in the plan
tree, then only the portion of the plan below it will run in parallel. In the
example above, the query accesses only one table, so there is only one plan
node other than the `Gather` node itself; since that plan node is a child of
the `Gather` node, it will run in parallel.

[Using EXPLAIN](using-explain.html "14.1. Using EXPLAIN"), you can see the
number of workers chosen by the planner. When the `Gather` node is reached
during query execution, the process that is implementing the user's session
will request a number of [background worker processes](bgworker.html
"Chapter 48. Background Worker Processes") equal to the number of workers
chosen by the planner. The number of background workers that the planner will
consider using is limited to at most
[max_parallel_workers_per_gather](runtime-config-resource.html#GUC-MAX-
PARALLEL-WORKERS-PER-GATHER). The total number of background workers that can
exist at any one time is limited by both [max_worker_processes](runtime-
config-resource.html#GUC-MAX-WORKER-PROCESSES) and
[max_parallel_workers](runtime-config-resource.html#GUC-MAX-PARALLEL-WORKERS).
Therefore, it is possible for a parallel query to run with fewer workers than
planned, or even with no workers at all. The optimal plan may depend on the
number of workers that are available, so this can result in poor query
performance. If this occurrence is frequent, consider increasing
`max_worker_processes` and `max_parallel_workers` so that more workers can be
run simultaneously or alternatively reducing `max_parallel_workers_per_gather`
so that the planner requests fewer workers.

Every background worker process that is successfully started for a given
parallel query will execute the parallel portion of the plan. The leader will
also execute that portion of the plan, but it has an additional
responsibility: it must also read all of the tuples generated by the workers.
When the parallel portion of the plan generates only a small number of tuples,
the leader will often behave very much like an additional worker, speeding up
query execution. Conversely, when the parallel portion of the plan generates a
large number of tuples, the leader may be almost entirely occupied with
reading the tuples generated by the workers and performing any further
processing steps that are required by plan nodes above the level of the
`Gather` node or `Gather Merge` node. In such cases, the leader will do very
little of the work of executing the parallel portion of the plan.

When the node at the top of the parallel portion of the plan is `Gather Merge`
rather than `Gather`, it indicates that each process executing the parallel
portion of the plan is producing tuples in sorted order, and that the leader
is performing an order-preserving merge. In contrast, `Gather` reads tuples
from the workers in whatever order is convenient, destroying any sort order
that may have existed.

* * *

[Prev](parallel-query.html "Chapter 15. Parallel Query")  | [Up](parallel-query.html "Chapter 15. Parallel Query") |  [Next](when-can-parallel-query-be-used.html "15.2. When Can Parallel Query Be Used?")  
---|---|---  
Chapter 15. Parallel Query  | [Home](index.html "PostgreSQL 16.9 Documentation") |  15.2. When Can Parallel Query Be Used?  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/how-parallel-query-
works.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

