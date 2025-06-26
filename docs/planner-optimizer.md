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

Supported Versions: [Current](/docs/current/planner-optimizer.html "PostgreSQL
17 - 52.5. Planner/Optimizer") ([17](/docs/17/planner-optimizer.html
"PostgreSQL 17 - 52.5. Planner/Optimizer")) / [16](/docs/16/planner-
optimizer.html "PostgreSQL 16 - 52.5. Planner/Optimizer") /
[15](/docs/15/planner-optimizer.html "PostgreSQL 15 -
52.5. Planner/Optimizer") / [14](/docs/14/planner-optimizer.html "PostgreSQL
14 - 52.5. Planner/Optimizer") / [13](/docs/13/planner-optimizer.html
"PostgreSQL 13 - 52.5. Planner/Optimizer")

Development Versions: [18](/docs/18/planner-optimizer.html "PostgreSQL 18 -
52.5. Planner/Optimizer") / [devel](/docs/devel/planner-optimizer.html
"PostgreSQL devel - 52.5. Planner/Optimizer")

Unsupported versions: [12](/docs/12/planner-optimizer.html "PostgreSQL 12 -
52.5. Planner/Optimizer") / [11](/docs/11/planner-optimizer.html "PostgreSQL
11 - 52.5. Planner/Optimizer") / [10](/docs/10/planner-optimizer.html
"PostgreSQL 10 - 52.5. Planner/Optimizer") / [9.6](/docs/9.6/planner-
optimizer.html "PostgreSQL 9.6 - 52.5. Planner/Optimizer") /
[9.5](/docs/9.5/planner-optimizer.html "PostgreSQL 9.5 -
52.5. Planner/Optimizer") / [9.4](/docs/9.4/planner-optimizer.html "PostgreSQL
9.4 - 52.5. Planner/Optimizer") / [9.3](/docs/9.3/planner-optimizer.html
"PostgreSQL 9.3 - 52.5. Planner/Optimizer") / [9.2](/docs/9.2/planner-
optimizer.html "PostgreSQL 9.2 - 52.5. Planner/Optimizer") /
[9.1](/docs/9.1/planner-optimizer.html "PostgreSQL 9.1 -
52.5. Planner/Optimizer") / [9.0](/docs/9.0/planner-optimizer.html "PostgreSQL
9.0 - 52.5. Planner/Optimizer") / [8.4](/docs/8.4/planner-optimizer.html
"PostgreSQL 8.4 - 52.5. Planner/Optimizer") / [8.3](/docs/8.3/planner-
optimizer.html "PostgreSQL 8.3 - 52.5. Planner/Optimizer") /
[8.2](/docs/8.2/planner-optimizer.html "PostgreSQL 8.2 -
52.5. Planner/Optimizer") / [8.1](/docs/8.1/planner-optimizer.html "PostgreSQL
8.1 - 52.5. Planner/Optimizer") / [8.0](/docs/8.0/planner-optimizer.html
"PostgreSQL 8.0 - 52.5. Planner/Optimizer") / [7.4](/docs/7.4/planner-
optimizer.html "PostgreSQL 7.4 - 52.5. Planner/Optimizer") /
[7.3](/docs/7.3/planner-optimizer.html "PostgreSQL 7.3 -
52.5. Planner/Optimizer") / [7.2](/docs/7.2/planner-optimizer.html "PostgreSQL
7.2 - 52.5. Planner/Optimizer") / [7.1](/docs/7.1/planner-optimizer.html
"PostgreSQL 7.1 - 52.5. Planner/Optimizer")

__

52.5. Planner/Optimizer  
---  
[Prev](rule-system.html "52.4. The PostgreSQL Rule System")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") | Chapter 52. Overview of PostgreSQL Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](executor.html "52.6. Executor")  
  
* * *

## 52.5. Planner/Optimizer #

[52.5.1. Generating Possible Plans](planner-optimizer.html#PLANNER-OPTIMIZER-
GENERATING-POSSIBLE-PLANS)

The task of the _planner/optimizer_ is to create an optimal execution plan. A
given SQL query (and hence, a query tree) can be actually executed in a wide
variety of different ways, each of which will produce the same set of results.
If it is computationally feasible, the query optimizer will examine each of
these possible execution plans, ultimately selecting the execution plan that
is expected to run the fastest.

### Note

In some situations, examining each possible way in which a query can be
executed would take an excessive amount of time and memory. In particular,
this occurs when executing queries involving large numbers of join operations.
In order to determine a reasonable (not necessarily optimal) query plan in a
reasonable amount of time, PostgreSQL uses a _Genetic Query Optimizer_ (see
[Chapter 62](geqo.html "Chapter 62. Genetic Query Optimizer")) when the number
of joins exceeds a threshold (see [geqo_threshold](runtime-config-
query.html#GUC-GEQO-THRESHOLD)).

The planner's search procedure actually works with data structures called
_paths_ , which are simply cut-down representations of plans containing only
as much information as the planner needs to make its decisions. After the
cheapest path is determined, a full-fledged _plan tree_ is built to pass to
the executor. This represents the desired execution plan in sufficient detail
for the executor to run it. In the rest of this section we'll ignore the
distinction between paths and plans.

### 52.5.1. Generating Possible Plans #

The planner/optimizer starts by generating plans for scanning each individual
relation (table) used in the query. The possible plans are determined by the
available indexes on each relation. There is always the possibility of
performing a sequential scan on a relation, so a sequential scan plan is
always created. Assume an index is defined on a relation (for example a B-tree
index) and a query contains the restriction `relation.attribute OPR constant`.
If `relation.attribute` happens to match the key of the B-tree index and `OPR`
is one of the operators listed in the index's _operator class_ , another plan
is created using the B-tree index to scan the relation. If there are further
indexes present and the restrictions in the query happen to match a key of an
index, further plans will be considered. Index scan plans are also generated
for indexes that have a sort ordering that can match the query's `ORDER BY`
clause (if any), or a sort ordering that might be useful for merge joining
(see below).

If the query requires joining two or more relations, plans for joining
relations are considered after all feasible plans have been found for scanning
single relations. The three available join strategies are:

  * _nested loop join_ : The right relation is scanned once for every row found in the left relation. This strategy is easy to implement but can be very time consuming. (However, if the right relation can be scanned with an index scan, this can be a good strategy. It is possible to use values from the current row of the left relation as keys for the index scan of the right.)

  * _merge join_ : Each relation is sorted on the join attributes before the join starts. Then the two relations are scanned in parallel, and matching rows are combined to form join rows. This kind of join is attractive because each relation has to be scanned only once. The required sorting might be achieved either by an explicit sort step, or by scanning the relation in the proper order using an index on the join key.

  * _hash join_ : the right relation is first scanned and loaded into a hash table, using its join attributes as hash keys. Next the left relation is scanned and the appropriate values of every row found are used as hash keys to locate the matching rows in the table.

When the query involves more than two relations, the final result must be
built up by a tree of join steps, each with two inputs. The planner examines
different possible join sequences to find the cheapest one.

If the query uses fewer than [geqo_threshold](runtime-config-query.html#GUC-
GEQO-THRESHOLD) relations, a near-exhaustive search is conducted to find the
best join sequence. The planner preferentially considers joins between any two
relations for which there exists a corresponding join clause in the `WHERE`
qualification (i.e., for which a restriction like `where
rel1.attr1=rel2.attr2` exists). Join pairs with no join clause are considered
only when there is no other choice, that is, a particular relation has no
available join clauses to any other relation. All possible plans are generated
for every join pair considered by the planner, and the one that is (estimated
to be) the cheapest is chosen.

When `geqo_threshold` is exceeded, the join sequences considered are
determined by heuristics, as described in [Chapter 62](geqo.html
"Chapter 62. Genetic Query Optimizer"). Otherwise the process is the same.

The finished plan tree consists of sequential or index scans of the base
relations, plus nested-loop, merge, or hash join nodes as needed, plus any
auxiliary steps needed, such as sort nodes or aggregate-function calculation
nodes. Most of these plan node types have the additional ability to do
_selection_ (discarding rows that do not meet a specified Boolean condition)
and _projection_ (computation of a derived column set based on given column
values, that is, evaluation of scalar expressions where needed). One of the
responsibilities of the planner is to attach selection conditions from the
`WHERE` clause and computation of required output expressions to the most
appropriate nodes of the plan tree.

* * *

[Prev](rule-system.html "52.4. The PostgreSQL Rule System")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") |  [Next](executor.html "52.6. Executor")  
---|---|---  
52.4. The PostgreSQL Rule System  | [Home](index.html "PostgreSQL 16.9 Documentation") |  52.6. Executor  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/planner-optimizer.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

