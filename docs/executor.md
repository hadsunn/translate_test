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

Supported Versions: [Current](/docs/current/executor.html "PostgreSQL 17 -
52.6. Executor") ([17](/docs/17/executor.html "PostgreSQL 17 -
52.6. Executor")) / [16](/docs/16/executor.html "PostgreSQL 16 -
52.6. Executor") / [15](/docs/15/executor.html "PostgreSQL 15 -
52.6. Executor") / [14](/docs/14/executor.html "PostgreSQL 14 -
52.6. Executor") / [13](/docs/13/executor.html "PostgreSQL 13 -
52.6. Executor")

Development Versions: [18](/docs/18/executor.html "PostgreSQL 18 -
52.6. Executor") / [devel](/docs/devel/executor.html "PostgreSQL devel -
52.6. Executor")

Unsupported versions: [12](/docs/12/executor.html "PostgreSQL 12 -
52.6. Executor") / [11](/docs/11/executor.html "PostgreSQL 11 -
52.6. Executor") / [10](/docs/10/executor.html "PostgreSQL 10 -
52.6. Executor") / [9.6](/docs/9.6/executor.html "PostgreSQL 9.6 -
52.6. Executor") / [9.5](/docs/9.5/executor.html "PostgreSQL 9.5 -
52.6. Executor") / [9.4](/docs/9.4/executor.html "PostgreSQL 9.4 -
52.6. Executor") / [9.3](/docs/9.3/executor.html "PostgreSQL 9.3 -
52.6. Executor") / [9.2](/docs/9.2/executor.html "PostgreSQL 9.2 -
52.6. Executor") / [9.1](/docs/9.1/executor.html "PostgreSQL 9.1 -
52.6. Executor") / [9.0](/docs/9.0/executor.html "PostgreSQL 9.0 -
52.6. Executor") / [8.4](/docs/8.4/executor.html "PostgreSQL 8.4 -
52.6. Executor") / [8.3](/docs/8.3/executor.html "PostgreSQL 8.3 -
52.6. Executor") / [8.2](/docs/8.2/executor.html "PostgreSQL 8.2 -
52.6. Executor") / [8.1](/docs/8.1/executor.html "PostgreSQL 8.1 -
52.6. Executor") / [8.0](/docs/8.0/executor.html "PostgreSQL 8.0 -
52.6. Executor") / [7.4](/docs/7.4/executor.html "PostgreSQL 7.4 -
52.6. Executor") / [7.3](/docs/7.3/executor.html "PostgreSQL 7.3 -
52.6. Executor") / [7.2](/docs/7.2/executor.html "PostgreSQL 7.2 -
52.6. Executor") / [7.1](/docs/7.1/executor.html "PostgreSQL 7.1 -
52.6. Executor")

__

52.6. Executor  
---  
[Prev](planner-optimizer.html "52.5. Planner/Optimizer")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") | Chapter 52. Overview of PostgreSQL Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalogs.html "Chapter 53. System Catalogs")  
  
* * *

## 52.6. Executor #

The _executor_ takes the plan created by the planner/optimizer and recursively
processes it to extract the required set of rows. This is essentially a
demand-pull pipeline mechanism. Each time a plan node is called, it must
deliver one more row, or report that it is done delivering rows.

To provide a concrete example, assume that the top node is a `MergeJoin` node.
Before any merge can be done two rows have to be fetched (one from each
subplan). So the executor recursively calls itself to process the subplans (it
starts with the subplan attached to `lefttree`). The new top node (the top
node of the left subplan) is, let's say, a `Sort` node and again recursion is
needed to obtain an input row. The child node of the `Sort` might be a
`SeqScan` node, representing actual reading of a table. Execution of this node
causes the executor to fetch a row from the table and return it up to the
calling node. The `Sort` node will repeatedly call its child to obtain all the
rows to be sorted. When the input is exhausted (as indicated by the child node
returning a NULL instead of a row), the `Sort` code performs the sort, and
finally is able to return its first output row, namely the first one in sorted
order. It keeps the remaining rows stored so that it can deliver them in
sorted order in response to later demands.

The `MergeJoin` node similarly demands the first row from its right subplan.
Then it compares the two rows to see if they can be joined; if so, it returns
a join row to its caller. On the next call, or immediately if it cannot join
the current pair of inputs, it advances to the next row of one table or the
other (depending on how the comparison came out), and again checks for a
match. Eventually, one subplan or the other is exhausted, and the `MergeJoin`
node returns NULL to indicate that no more join rows can be formed.

Complex queries can involve many levels of plan nodes, but the general
approach is the same: each node computes and returns its next output row each
time it is called. Each node is also responsible for applying any selection or
projection expressions that were assigned to it by the planner.

The executor mechanism is used to evaluate all five basic SQL query types:
`SELECT`, `INSERT`, `UPDATE`, `DELETE`, and `MERGE`. For `SELECT`, the top-
level executor code only needs to send each row returned by the query plan
tree off to the client. `INSERT ... SELECT`, `UPDATE`, `DELETE`, and `MERGE`
are effectively `SELECT`s under a special top-level plan node called
`ModifyTable`.

`INSERT ... SELECT` feeds the rows up to `ModifyTable` for insertion. For
`UPDATE`, the planner arranges that each computed row includes all the updated
column values, plus the _TID_ (tuple ID, or row ID) of the original target
row; this data is fed up to the `ModifyTable` node, which uses the information
to create a new updated row and mark the old row deleted. For `DELETE`, the
only column that is actually returned by the plan is the TID, and the
`ModifyTable` node simply uses the TID to visit each target row and mark it
deleted. For `MERGE`, the planner joins the source and target relations, and
includes all column values required by any of the `WHEN` clauses, plus the TID
of the target row; this data is fed up to the `ModifyTable` node, which uses
the information to work out which `WHEN` clause to execute, and then inserts,
updates or deletes the target row, as required.

A simple `INSERT ... VALUES` command creates a trivial plan tree consisting of
a single `Result` node, which computes just one result row, feeding that up to
`ModifyTable` to perform the insertion.

* * *

[Prev](planner-optimizer.html "52.5. Planner/Optimizer")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") |  [Next](catalogs.html "Chapter 53. System Catalogs")  
---|---|---  
52.5. Planner/Optimizer  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 53. System Catalogs  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/executor.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

