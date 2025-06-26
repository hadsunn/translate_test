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

Supported Versions: [Current](/docs/current/parallel-safety.html "PostgreSQL
17 - 15.4. Parallel Safety") ([17](/docs/17/parallel-safety.html "PostgreSQL
17 - 15.4. Parallel Safety")) / [16](/docs/16/parallel-safety.html "PostgreSQL
16 - 15.4. Parallel Safety") / [15](/docs/15/parallel-safety.html "PostgreSQL
15 - 15.4. Parallel Safety") / [14](/docs/14/parallel-safety.html "PostgreSQL
14 - 15.4. Parallel Safety") / [13](/docs/13/parallel-safety.html "PostgreSQL
13 - 15.4. Parallel Safety")

Development Versions: [18](/docs/18/parallel-safety.html "PostgreSQL 18 -
15.4. Parallel Safety") / [devel](/docs/devel/parallel-safety.html "PostgreSQL
devel - 15.4. Parallel Safety")

Unsupported versions: [12](/docs/12/parallel-safety.html "PostgreSQL 12 -
15.4. Parallel Safety") / [11](/docs/11/parallel-safety.html "PostgreSQL 11 -
15.4. Parallel Safety") / [10](/docs/10/parallel-safety.html "PostgreSQL 10 -
15.4. Parallel Safety") / [9.6](/docs/9.6/parallel-safety.html "PostgreSQL 9.6
- 15.4. Parallel Safety")

__

15.4. Parallel Safety  
---  
[Prev](parallel-plans.html "15.3. Parallel Plans")  | [Up](parallel-query.html "Chapter 15. Parallel Query") | Chapter 15. Parallel Query | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](admin.html "Part III. Server Administration")  
  
* * *

## 15.4. Parallel Safety #

[15.4.1. Parallel Labeling for Functions and Aggregates](parallel-
safety.html#PARALLEL-LABELING)

The planner classifies operations involved in a query as either _parallel
safe_ , _parallel restricted_ , or _parallel unsafe_. A parallel safe
operation is one that does not conflict with the use of parallel query. A
parallel restricted operation is one that cannot be performed in a parallel
worker, but that can be performed in the leader while parallel query is in
use. Therefore, parallel restricted operations can never occur below a
`Gather` or `Gather Merge` node, but can occur elsewhere in a plan that
contains such a node. A parallel unsafe operation is one that cannot be
performed while parallel query is in use, not even in the leader. When a query
contains anything that is parallel unsafe, parallel query is completely
disabled for that query.

The following operations are always parallel restricted:

  * Scans of common table expressions (CTEs).

  * Scans of temporary tables.

  * Scans of foreign tables, unless the foreign data wrapper has an `IsForeignScanParallelSafe` API that indicates otherwise.

  * Plan nodes to which an `InitPlan` is attached.

  * Plan nodes that reference a correlated `SubPlan`.

### 15.4.1. Parallel Labeling for Functions and Aggregates #

The planner cannot automatically determine whether a user-defined function or
aggregate is parallel safe, parallel restricted, or parallel unsafe, because
this would require predicting every operation that the function could possibly
perform. In general, this is equivalent to the Halting Problem and therefore
impossible. Even for simple functions where it could conceivably be done, we
do not try, since this would be expensive and error-prone. Instead, all user-
defined functions are assumed to be parallel unsafe unless otherwise marked.
When using [CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION") or
[ALTER FUNCTION](sql-alterfunction.html "ALTER FUNCTION"), markings can be set
by specifying `PARALLEL SAFE`, `PARALLEL RESTRICTED`, or `PARALLEL UNSAFE` as
appropriate. When using [CREATE AGGREGATE](sql-createaggregate.html "CREATE
AGGREGATE"), the `PARALLEL` option can be specified with `SAFE`, `RESTRICTED`,
or `UNSAFE` as the corresponding value.

Functions and aggregates must be marked `PARALLEL UNSAFE` if they write to the
database, access sequences, change the transaction state even temporarily
(e.g., a PL/pgSQL function that establishes an `EXCEPTION` block to catch
errors), or make persistent changes to settings. Similarly, functions must be
marked `PARALLEL RESTRICTED` if they access temporary tables, client
connection state, cursors, prepared statements, or miscellaneous backend-local
state that the system cannot synchronize across workers. For example,
`setseed` and `random` are parallel restricted for this last reason.

In general, if a function is labeled as being safe when it is restricted or
unsafe, or if it is labeled as being restricted when it is in fact unsafe, it
may throw errors or produce wrong answers when used in a parallel query.
C-language functions could in theory exhibit totally undefined behavior if
mislabeled, since there is no way for the system to protect itself against
arbitrary C code, but in most likely cases the result will be no worse than
for any other function. If in doubt, it is probably best to label functions as
`UNSAFE`.

If a function executed within a parallel worker acquires locks that are not
held by the leader, for example by querying a table not referenced in the
query, those locks will be released at worker exit, not end of transaction. If
you write a function that does this, and this behavior difference is important
to you, mark such functions as `PARALLEL RESTRICTED` to ensure that they
execute only in the leader.

Note that the query planner does not consider deferring the evaluation of
parallel-restricted functions or aggregates involved in the query in order to
obtain a superior plan. So, for example, if a `WHERE` clause applied to a
particular table is parallel restricted, the query planner will not consider
performing a scan of that table in the parallel portion of a plan. In some
cases, it would be possible (and perhaps even efficient) to include the scan
of that table in the parallel portion of the query and defer the evaluation of
the `WHERE` clause so that it happens above the `Gather` node. However, the
planner does not do this.

* * *

[Prev](parallel-plans.html "15.3. Parallel Plans")  | [Up](parallel-query.html "Chapter 15. Parallel Query") |  [Next](admin.html "Part III. Server Administration")  
---|---|---  
15.3. Parallel Plans  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Part III. Server Administration  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/parallel-safety.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

