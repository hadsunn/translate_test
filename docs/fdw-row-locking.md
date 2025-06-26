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

Supported Versions: [Current](/docs/current/fdw-row-locking.html "PostgreSQL
17 - 59.5. Row Locking in Foreign Data Wrappers") ([17](/docs/17/fdw-row-
locking.html "PostgreSQL 17 - 59.5. Row Locking in Foreign Data Wrappers")) /
[16](/docs/16/fdw-row-locking.html "PostgreSQL 16 - 59.5. Row Locking in
Foreign Data Wrappers") / [15](/docs/15/fdw-row-locking.html "PostgreSQL 15 -
59.5. Row Locking in Foreign Data Wrappers") / [14](/docs/14/fdw-row-
locking.html "PostgreSQL 14 - 59.5. Row Locking in Foreign Data Wrappers") /
[13](/docs/13/fdw-row-locking.html "PostgreSQL 13 - 59.5. Row Locking in
Foreign Data Wrappers")

Development Versions: [18](/docs/18/fdw-row-locking.html "PostgreSQL 18 -
59.5. Row Locking in Foreign Data Wrappers") / [devel](/docs/devel/fdw-row-
locking.html "PostgreSQL devel - 59.5. Row Locking in Foreign Data Wrappers")

Unsupported versions: [12](/docs/12/fdw-row-locking.html "PostgreSQL 12 -
59.5. Row Locking in Foreign Data Wrappers") / [11](/docs/11/fdw-row-
locking.html "PostgreSQL 11 - 59.5. Row Locking in Foreign Data Wrappers") /
[10](/docs/10/fdw-row-locking.html "PostgreSQL 10 - 59.5. Row Locking in
Foreign Data Wrappers") / [9.6](/docs/9.6/fdw-row-locking.html "PostgreSQL 9.6
- 59.5. Row Locking in Foreign Data Wrappers") / [9.5](/docs/9.5/fdw-row-
locking.html "PostgreSQL 9.5 - 59.5. Row Locking in Foreign Data Wrappers")

__

59.5. Row Locking in Foreign Data Wrappers  
---  
[Prev](fdw-planning.html "59.4. Foreign Data Wrapper Query Planning")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") | Chapter 59. Writing a Foreign Data Wrapper | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tablesample-method.html "Chapter 60. Writing a Table Sampling Method")  
  
* * *

## 59.5. Row Locking in Foreign Data Wrappers #

If an FDW's underlying storage mechanism has a concept of locking individual
rows to prevent concurrent updates of those rows, it is usually worthwhile for
the FDW to perform row-level locking with as close an approximation as
practical to the semantics used in ordinary PostgreSQL tables. There are
multiple considerations involved in this.

One key decision to be made is whether to perform _early locking_ or _late
locking_. In early locking, a row is locked when it is first retrieved from
the underlying store, while in late locking, the row is locked only when it is
known that it needs to be locked. (The difference arises because some rows may
be discarded by locally-checked restriction or join conditions.) Early locking
is much simpler and avoids extra round trips to a remote store, but it can
cause locking of rows that need not have been locked, resulting in reduced
concurrency or even unexpected deadlocks. Also, late locking is only possible
if the row to be locked can be uniquely re-identified later. Preferably the
row identifier should identify a specific version of the row, as PostgreSQL
TIDs do.

By default, PostgreSQL ignores locking considerations when interfacing to
FDWs, but an FDW can perform early locking without any explicit support from
the core code. The API functions described in [Section 59.2.6](fdw-
callbacks.html#FDW-CALLBACKS-ROW-LOCKING "59.2.6. FDW Routines for Row
Locking"), which were added in PostgreSQL 9.5, allow an FDW to use late
locking if it wishes.

An additional consideration is that in `READ COMMITTED` isolation mode,
PostgreSQL may need to re-check restriction and join conditions against an
updated version of some target tuple. Rechecking join conditions requires re-
obtaining copies of the non-target rows that were previously joined to the
target tuple. When working with standard PostgreSQL tables, this is done by
including the TIDs of the non-target tables in the column list projected
through the join, and then re-fetching non-target rows when required. This
approach keeps the join data set compact, but it requires inexpensive re-fetch
capability, as well as a TID that can uniquely identify the row version to be
re-fetched. By default, therefore, the approach used with foreign tables is to
include a copy of the entire row fetched from a foreign table in the column
list projected through the join. This puts no special demands on the FDW but
can result in reduced performance of merge and hash joins. An FDW that is
capable of meeting the re-fetch requirements can choose to do it the first
way.

For an `UPDATE` or `DELETE` on a foreign table, it is recommended that the
`ForeignScan` operation on the target table perform early locking on the rows
that it fetches, perhaps via the equivalent of `SELECT FOR UPDATE`. An FDW can
detect whether a table is an `UPDATE`/`DELETE` target at plan time by
comparing its relid to `root->parse->resultRelation`, or at execution time by
using `ExecRelationIsTargetRelation()`. An alternative possibility is to
perform late locking within the `ExecForeignUpdate` or `ExecForeignDelete`
callback, but no special support is provided for this.

For foreign tables that are specified to be locked by a `SELECT FOR
UPDATE/SHARE` command, the `ForeignScan` operation can again perform early
locking by fetching tuples with the equivalent of `SELECT FOR UPDATE/SHARE`.
To perform late locking instead, provide the callback functions defined in
[Section 59.2.6](fdw-callbacks.html#FDW-CALLBACKS-ROW-LOCKING "59.2.6. FDW
Routines for Row Locking"). In `GetForeignRowMarkType`, select rowmark option
`ROW_MARK_EXCLUSIVE`, `ROW_MARK_NOKEYEXCLUSIVE`, `ROW_MARK_SHARE`, or
`ROW_MARK_KEYSHARE` depending on the requested lock strength. (The core code
will act the same regardless of which of these four options you choose.)
Elsewhere, you can detect whether a foreign table was specified to be locked
by this type of command by using `get_plan_rowmark` at plan time, or
`ExecFindRowMark` at execution time; you must check not only whether a non-
null rowmark struct is returned, but that its `strength` field is not
`LCS_NONE`.

Lastly, for foreign tables that are used in an `UPDATE`, `DELETE` or `SELECT
FOR UPDATE/SHARE` command but are not specified to be row-locked, you can
override the default choice to copy entire rows by having
`GetForeignRowMarkType` select option `ROW_MARK_REFERENCE` when it sees lock
strength `LCS_NONE`. This will cause `RefetchForeignRow` to be called with
that value for `markType`; it should then re-fetch the row without acquiring
any new lock. (If you have a `GetForeignRowMarkType` function but don't wish
to re-fetch unlocked rows, select option `ROW_MARK_COPY` for `LCS_NONE`.)

See `src/include/nodes/lockoptions.h`, the comments for `RowMarkType` and
`PlanRowMark` in `src/include/nodes/plannodes.h`, and the comments for
`ExecRowMark` in `src/include/nodes/execnodes.h` for additional information.

* * *

[Prev](fdw-planning.html "59.4. Foreign Data Wrapper Query Planning")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") |  [Next](tablesample-method.html "Chapter 60. Writing a Table Sampling Method")  
---|---|---  
59.4. Foreign Data Wrapper Query Planning  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 60. Writing a Table Sampling Method  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/fdw-row-locking.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

