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

Supported Versions: [Current](/docs/current/fdw-planning.html "PostgreSQL 17 -
59.4. Foreign Data Wrapper Query Planning") ([17](/docs/17/fdw-planning.html
"PostgreSQL 17 - 59.4. Foreign Data Wrapper Query Planning")) /
[16](/docs/16/fdw-planning.html "PostgreSQL 16 - 59.4. Foreign Data Wrapper
Query Planning") / [15](/docs/15/fdw-planning.html "PostgreSQL 15 -
59.4. Foreign Data Wrapper Query Planning") / [14](/docs/14/fdw-planning.html
"PostgreSQL 14 - 59.4. Foreign Data Wrapper Query Planning") /
[13](/docs/13/fdw-planning.html "PostgreSQL 13 - 59.4. Foreign Data Wrapper
Query Planning")

Development Versions: [18](/docs/18/fdw-planning.html "PostgreSQL 18 -
59.4. Foreign Data Wrapper Query Planning") / [devel](/docs/devel/fdw-
planning.html "PostgreSQL devel - 59.4. Foreign Data Wrapper Query Planning")

Unsupported versions: [12](/docs/12/fdw-planning.html "PostgreSQL 12 -
59.4. Foreign Data Wrapper Query Planning") / [11](/docs/11/fdw-planning.html
"PostgreSQL 11 - 59.4. Foreign Data Wrapper Query Planning") /
[10](/docs/10/fdw-planning.html "PostgreSQL 10 - 59.4. Foreign Data Wrapper
Query Planning") / [9.6](/docs/9.6/fdw-planning.html "PostgreSQL 9.6 -
59.4. Foreign Data Wrapper Query Planning") / [9.5](/docs/9.5/fdw-
planning.html "PostgreSQL 9.5 - 59.4. Foreign Data Wrapper Query Planning") /
[9.4](/docs/9.4/fdw-planning.html "PostgreSQL 9.4 - 59.4. Foreign Data Wrapper
Query Planning") / [9.3](/docs/9.3/fdw-planning.html "PostgreSQL 9.3 -
59.4. Foreign Data Wrapper Query Planning") / [9.2](/docs/9.2/fdw-
planning.html "PostgreSQL 9.2 - 59.4. Foreign Data Wrapper Query Planning")

__

59.4. Foreign Data Wrapper Query Planning  
---  
[Prev](fdw-helpers.html "59.3. Foreign Data Wrapper Helper Functions")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") | Chapter 59. Writing a Foreign Data Wrapper | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](fdw-row-locking.html "59.5. Row Locking in Foreign Data Wrappers")  
  
* * *

## 59.4. Foreign Data Wrapper Query Planning #

The FDW callback functions `GetForeignRelSize`, `GetForeignPaths`,
`GetForeignPlan`, `PlanForeignModify`, `GetForeignJoinPaths`,
`GetForeignUpperPaths`, and `PlanDirectModify` must fit into the workings of
the PostgreSQL planner. Here are some notes about what they must do.

The information in `root` and `baserel` can be used to reduce the amount of
information that has to be fetched from the foreign table (and therefore
reduce the cost). `baserel->baserestrictinfo` is particularly interesting, as
it contains restriction quals (`WHERE` clauses) that should be used to filter
the rows to be fetched. (The FDW itself is not required to enforce these
quals, as the core executor can check them instead.)
`baserel->reltarget->exprs` can be used to determine which columns need to be
fetched; but note that it only lists columns that have to be emitted by the
`ForeignScan` plan node, not columns that are used in qual evaluation but not
output by the query.

Various private fields are available for the FDW planning functions to keep
information in. Generally, whatever you store in FDW private fields should be
palloc'd, so that it will be reclaimed at the end of planning.

`baserel->fdw_private` is a `void` pointer that is available for FDW planning
functions to store information relevant to the particular foreign table. The
core planner does not touch it except to initialize it to NULL when the
`RelOptInfo` node is created. It is useful for passing information forward
from `GetForeignRelSize` to `GetForeignPaths` and/or `GetForeignPaths` to
`GetForeignPlan`, thereby avoiding recalculation.

`GetForeignPaths` can identify the meaning of different access paths by
storing private information in the `fdw_private` field of `ForeignPath` nodes.
`fdw_private` is declared as a `List` pointer, but could actually contain
anything since the core planner does not touch it. However, best practice is
to use a representation that's dumpable by `nodeToString`, for use with
debugging support available in the backend.

`GetForeignPlan` can examine the `fdw_private` field of the selected
`ForeignPath` node, and can generate `fdw_exprs` and `fdw_private` lists to be
placed in the `ForeignScan` plan node, where they will be available at
execution time. Both of these lists must be represented in a form that
`copyObject` knows how to copy. The `fdw_private` list has no other
restrictions and is not interpreted by the core backend in any way. The
`fdw_exprs` list, if not NIL, is expected to contain expression trees that are
intended to be executed at run time. These trees will undergo post-processing
by the planner to make them fully executable.

In `GetForeignPlan`, generally the passed-in target list can be copied into
the plan node as-is. The passed `scan_clauses` list contains the same clauses
as `baserel->baserestrictinfo`, but may be re-ordered for better execution
efficiency. In simple cases the FDW can just strip `RestrictInfo` nodes from
the `scan_clauses` list (using `extract_actual_clauses`) and put all the
clauses into the plan node's qual list, which means that all the clauses will
be checked by the executor at run time. More complex FDWs may be able to check
some of the clauses internally, in which case those clauses can be removed
from the plan node's qual list so that the executor doesn't waste time
rechecking them.

As an example, the FDW might identify some restriction clauses of the form
_`foreign_variable`_ `=` _`sub_expression`_ , which it determines can be
executed on the remote server given the locally-evaluated value of the
_`sub_expression`_. The actual identification of such a clause should happen
during `GetForeignPaths`, since it would affect the cost estimate for the
path. The path's `fdw_private` field would probably include a pointer to the
identified clause's `RestrictInfo` node. Then `GetForeignPlan` would remove
that clause from `scan_clauses`, but add the _`sub_expression`_ to `fdw_exprs`
to ensure that it gets massaged into executable form. It would probably also
put control information into the plan node's `fdw_private` field to tell the
execution functions what to do at run time. The query transmitted to the
remote server would involve something like `WHERE _`foreign_variable`_ = $1`,
with the parameter value obtained at run time from evaluation of the
`fdw_exprs` expression tree.

Any clauses removed from the plan node's qual list must instead be added to
`fdw_recheck_quals` or rechecked by `RecheckForeignScan` in order to ensure
correct behavior at the `READ COMMITTED` isolation level. When a concurrent
update occurs for some other table involved in the query, the executor may
need to verify that all of the original quals are still satisfied for the
tuple, possibly against a different set of parameter values. Using
`fdw_recheck_quals` is typically easier than implementing checks inside
`RecheckForeignScan`, but this method will be insufficient when outer joins
have been pushed down, since the join tuples in that case might have some
fields go to NULL without rejecting the tuple entirely.

Another `ForeignScan` field that can be filled by FDWs is `fdw_scan_tlist`,
which describes the tuples returned by the FDW for this plan node. For simple
foreign table scans this can be set to `NIL`, implying that the returned
tuples have the row type declared for the foreign table. A non-`NIL` value
must be a target list (list of `TargetEntry`s) containing Vars and/or
expressions representing the returned columns. This might be used, for
example, to show that the FDW has omitted some columns that it noticed won't
be needed for the query. Also, if the FDW can compute expressions used by the
query more cheaply than can be done locally, it could add those expressions to
`fdw_scan_tlist`. Note that join plans (created from paths made by
`GetForeignJoinPaths`) must always supply `fdw_scan_tlist` to describe the set
of columns they will return.

The FDW should always construct at least one path that depends only on the
table's restriction clauses. In join queries, it might also choose to
construct path(s) that depend on join clauses, for example
_`foreign_variable`_ `=` _`local_variable`_. Such clauses will not be found in
`baserel->baserestrictinfo` but must be sought in the relation's join lists. A
path using such a clause is called a “parameterized path”. It must identify
the other relations used in the selected join clause(s) with a suitable value
of `param_info`; use `get_baserel_parampathinfo` to compute that value. In
`GetForeignPlan`, the _`local_variable`_ portion of the join clause would be
added to `fdw_exprs`, and then at run time the case works the same as for an
ordinary restriction clause.

If an FDW supports remote joins, `GetForeignJoinPaths` should produce
`ForeignPath`s for potential remote joins in much the same way as
`GetForeignPaths` works for base tables. Information about the intended join
can be passed forward to `GetForeignPlan` in the same ways described above.
However, `baserestrictinfo` is not relevant for join relations; instead, the
relevant join clauses for a particular join are passed to
`GetForeignJoinPaths` as a separate parameter (`extra->restrictlist`).

An FDW might additionally support direct execution of some plan actions that
are above the level of scans and joins, such as grouping or aggregation. To
offer such options, the FDW should generate paths and insert them into the
appropriate _upper relation_. For example, a path representing remote
aggregation should be inserted into the `UPPERREL_GROUP_AGG` relation, using
`add_path`. This path will be compared on a cost basis with local aggregation
performed by reading a simple scan path for the foreign relation (note that
such a path must also be supplied, else there will be an error at plan time).
If the remote-aggregation path wins, which it usually would, it will be
converted into a plan in the usual way, by calling `GetForeignPlan`. The
recommended place to generate such paths is in the `GetForeignUpperPaths`
callback function, which is called for each upper relation (i.e., each post-
scan/join processing step), if all the base relations of the query come from
the same FDW.

`PlanForeignModify` and the other callbacks described in [Section 59.2.4](fdw-
callbacks.html#FDW-CALLBACKS-UPDATE "59.2.4. FDW Routines for Updating Foreign
Tables") are designed around the assumption that the foreign relation will be
scanned in the usual way and then individual row updates will be driven by a
local `ModifyTable` plan node. This approach is necessary for the general case
where an update requires reading local tables as well as foreign tables.
However, if the operation could be executed entirely by the foreign server,
the FDW could generate a path representing that and insert it into the
`UPPERREL_FINAL` upper relation, where it would compete against the
`ModifyTable` approach. This approach could also be used to implement remote
`SELECT FOR UPDATE`, rather than using the row locking callbacks described in
[Section 59.2.6](fdw-callbacks.html#FDW-CALLBACKS-ROW-LOCKING "59.2.6. FDW
Routines for Row Locking"). Keep in mind that a path inserted into
`UPPERREL_FINAL` is responsible for implementing _all_ behavior of the query.

When planning an `UPDATE` or `DELETE`, `PlanForeignModify` and
`PlanDirectModify` can look up the `RelOptInfo` struct for the foreign table
and make use of the `baserel->fdw_private` data previously created by the
scan-planning functions. However, in `INSERT` the target table is not scanned
so there is no `RelOptInfo` for it. The `List` returned by `PlanForeignModify`
has the same restrictions as the `fdw_private` list of a `ForeignScan` plan
node, that is it must contain only structures that `copyObject` knows how to
copy.

`INSERT` with an `ON CONFLICT` clause does not support specifying the conflict
target, as unique constraints or exclusion constraints on remote tables are
not locally known. This in turn implies that `ON CONFLICT DO UPDATE` is not
supported, since the specification is mandatory there.

* * *

[Prev](fdw-helpers.html "59.3. Foreign Data Wrapper Helper Functions")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") |  [Next](fdw-row-locking.html "59.5. Row Locking in Foreign Data Wrappers")  
---|---|---  
59.3. Foreign Data Wrapper Helper Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  59.5. Row Locking in Foreign Data Wrappers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/fdw-planning.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

