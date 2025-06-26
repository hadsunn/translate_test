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

Supported Versions: [Current](/docs/current/when-can-parallel-query-be-
used.html "PostgreSQL 17 - 15.2. When Can Parallel Query Be Used?")
([17](/docs/17/when-can-parallel-query-be-used.html "PostgreSQL 17 -
15.2. When Can Parallel Query Be Used?")) / [16](/docs/16/when-can-parallel-
query-be-used.html "PostgreSQL 16 - 15.2. When Can Parallel Query Be Used?") /
[15](/docs/15/when-can-parallel-query-be-used.html "PostgreSQL 15 - 15.2. When
Can Parallel Query Be Used?") / [14](/docs/14/when-can-parallel-query-be-
used.html "PostgreSQL 14 - 15.2. When Can Parallel Query Be Used?") /
[13](/docs/13/when-can-parallel-query-be-used.html "PostgreSQL 13 - 15.2. When
Can Parallel Query Be Used?")

Development Versions: [18](/docs/18/when-can-parallel-query-be-used.html
"PostgreSQL 18 - 15.2. When Can Parallel Query Be Used?") /
[devel](/docs/devel/when-can-parallel-query-be-used.html "PostgreSQL devel -
15.2. When Can Parallel Query Be Used?")

Unsupported versions: [12](/docs/12/when-can-parallel-query-be-used.html
"PostgreSQL 12 - 15.2. When Can Parallel Query Be Used?") /
[11](/docs/11/when-can-parallel-query-be-used.html "PostgreSQL 11 - 15.2. When
Can Parallel Query Be Used?") / [10](/docs/10/when-can-parallel-query-be-
used.html "PostgreSQL 10 - 15.2. When Can Parallel Query Be Used?") /
[9.6](/docs/9.6/when-can-parallel-query-be-used.html "PostgreSQL 9.6 -
15.2. When Can Parallel Query Be Used?")

__

15.2. When Can Parallel Query Be Used?  
---  
[Prev](how-parallel-query-works.html "15.1. How Parallel Query Works")  | [Up](parallel-query.html "Chapter 15. Parallel Query") | Chapter 15. Parallel Query | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](parallel-plans.html "15.3. Parallel Plans")  
  
* * *

## 15.2. When Can Parallel Query Be Used? #

There are several settings that can cause the query planner not to generate a
parallel query plan under any circumstances. In order for any parallel query
plans whatsoever to be generated, the following settings must be configured as
indicated.

  * [max_parallel_workers_per_gather](runtime-config-resource.html#GUC-MAX-PARALLEL-WORKERS-PER-GATHER) must be set to a value that is greater than zero. This is a special case of the more general principle that no more workers should be used than the number configured via `max_parallel_workers_per_gather`.

In addition, the system must not be running in single-user mode. Since the
entire database system is running as a single process in this situation, no
background workers will be available.

Even when it is in general possible for parallel query plans to be generated,
the planner will not generate them for a given query if any of the following
are true:

  * The query writes any data or locks any database rows. If a query contains a data-modifying operation either at the top level or within a CTE, no parallel plans for that query will be generated. As an exception, the following commands, which create a new table and populate it, can use a parallel plan for the underlying `SELECT` part of the query:

    * `CREATE TABLE ... AS`

    * `SELECT INTO`

    * `CREATE MATERIALIZED VIEW`

    * `REFRESH MATERIALIZED VIEW`

  * The query might be suspended during execution. In any situation in which the system thinks that partial or incremental execution might occur, no parallel plan is generated. For example, a cursor created using [DECLARE CURSOR](sql-declare.html "DECLARE") will never use a parallel plan. Similarly, a PL/pgSQL loop of the form `FOR x IN query LOOP .. END LOOP` will never use a parallel plan, because the parallel query system is unable to verify that the code in the loop is safe to execute while parallel query is active.

  * The query uses any function marked `PARALLEL UNSAFE`. Most system-defined functions are `PARALLEL SAFE`, but user-defined functions are marked `PARALLEL UNSAFE` by default. See the discussion of [Section 15.4](parallel-safety.html "15.4. Parallel Safety").

  * The query is running inside of another query that is already parallel. For example, if a function called by a parallel query issues an SQL query itself, that query will never use a parallel plan. This is a limitation of the current implementation, but it may not be desirable to remove this limitation, since it could result in a single query using a very large number of processes.

Even when a parallel query plan is generated for a particular query, there are
several circumstances under which it will be impossible to execute that plan
in parallel at execution time. If this occurs, the leader will execute the
portion of the plan below the `Gather` node entirely by itself, almost as if
the `Gather` node were not present. This will happen if any of the following
conditions are met:

  * No background workers can be obtained because of the limitation that the total number of background workers cannot exceed [max_worker_processes](runtime-config-resource.html#GUC-MAX-WORKER-PROCESSES).

  * No background workers can be obtained because of the limitation that the total number of background workers launched for purposes of parallel query cannot exceed [max_parallel_workers](runtime-config-resource.html#GUC-MAX-PARALLEL-WORKERS).

  * The client sends an Execute message with a non-zero fetch count. See the discussion of the [extended query protocol](protocol-flow.html#PROTOCOL-FLOW-EXT-QUERY "55.2.3. Extended Query"). Since [libpq](libpq.html "Chapter 34. libpq — C Library") currently provides no way to send such a message, this can only occur when using a client that does not rely on libpq. If this is a frequent occurrence, it may be a good idea to set [max_parallel_workers_per_gather](runtime-config-resource.html#GUC-MAX-PARALLEL-WORKERS-PER-GATHER) to zero in sessions where it is likely, so as to avoid generating query plans that may be suboptimal when run serially.

* * *

[Prev](how-parallel-query-works.html "15.1. How Parallel Query Works")  | [Up](parallel-query.html "Chapter 15. Parallel Query") |  [Next](parallel-plans.html "15.3. Parallel Plans")  
---|---|---  
15.1. How Parallel Query Works  | [Home](index.html "PostgreSQL 16.9 Documentation") |  15.3. Parallel Plans  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/when-can-parallel-query-be-
used.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

