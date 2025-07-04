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

Supported Versions: [Current](/docs/current/trigger-definition.html
"PostgreSQL 17 - 39.1. Overview of Trigger Behavior") ([17](/docs/17/trigger-
definition.html "PostgreSQL 17 - 39.1. Overview of Trigger Behavior")) /
[16](/docs/16/trigger-definition.html "PostgreSQL 16 - 39.1. Overview of
Trigger Behavior") / [15](/docs/15/trigger-definition.html "PostgreSQL 15 -
39.1. Overview of Trigger Behavior") / [14](/docs/14/trigger-definition.html
"PostgreSQL 14 - 39.1. Overview of Trigger Behavior") / [13](/docs/13/trigger-
definition.html "PostgreSQL 13 - 39.1. Overview of Trigger Behavior")

Development Versions: [18](/docs/18/trigger-definition.html "PostgreSQL 18 -
39.1. Overview of Trigger Behavior") / [devel](/docs/devel/trigger-
definition.html "PostgreSQL devel - 39.1. Overview of Trigger Behavior")

Unsupported versions: [12](/docs/12/trigger-definition.html "PostgreSQL 12 -
39.1. Overview of Trigger Behavior") / [11](/docs/11/trigger-definition.html
"PostgreSQL 11 - 39.1. Overview of Trigger Behavior") / [10](/docs/10/trigger-
definition.html "PostgreSQL 10 - 39.1. Overview of Trigger Behavior") /
[9.6](/docs/9.6/trigger-definition.html "PostgreSQL 9.6 - 39.1. Overview of
Trigger Behavior") / [9.5](/docs/9.5/trigger-definition.html "PostgreSQL 9.5 -
39.1. Overview of Trigger Behavior") / [9.4](/docs/9.4/trigger-definition.html
"PostgreSQL 9.4 - 39.1. Overview of Trigger Behavior") /
[9.3](/docs/9.3/trigger-definition.html "PostgreSQL 9.3 - 39.1. Overview of
Trigger Behavior") / [9.2](/docs/9.2/trigger-definition.html "PostgreSQL 9.2 -
39.1. Overview of Trigger Behavior") / [9.1](/docs/9.1/trigger-definition.html
"PostgreSQL 9.1 - 39.1. Overview of Trigger Behavior") /
[9.0](/docs/9.0/trigger-definition.html "PostgreSQL 9.0 - 39.1. Overview of
Trigger Behavior") / [8.4](/docs/8.4/trigger-definition.html "PostgreSQL 8.4 -
39.1. Overview of Trigger Behavior") / [8.3](/docs/8.3/trigger-definition.html
"PostgreSQL 8.3 - 39.1. Overview of Trigger Behavior") /
[8.2](/docs/8.2/trigger-definition.html "PostgreSQL 8.2 - 39.1. Overview of
Trigger Behavior")

__

39.1. Overview of Trigger Behavior  
---  
[Prev](triggers.html "Chapter 39. Triggers")  | [Up](triggers.html "Chapter 39. Triggers") | Chapter 39. Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](trigger-datachanges.html "39.2. Visibility of Data Changes")  
  
* * *

## 39.1. Overview of Trigger Behavior #

A trigger is a specification that the database should automatically execute a
particular function whenever a certain type of operation is performed.
Triggers can be attached to tables (partitioned or not), views, and foreign
tables.

On tables and foreign tables, triggers can be defined to execute either before
or after any `INSERT`, `UPDATE`, or `DELETE` operation, either once per
modified row, or once per SQL statement. `UPDATE` triggers can moreover be set
to fire only if certain columns are mentioned in the `SET` clause of the
`UPDATE` statement. Triggers can also fire for `TRUNCATE` statements. If a
trigger event occurs, the trigger's function is called at the appropriate time
to handle the event.

On views, triggers can be defined to execute instead of `INSERT`, `UPDATE`, or
`DELETE` operations. Such `INSTEAD OF` triggers are fired once for each row
that needs to be modified in the view. It is the responsibility of the
trigger's function to perform the necessary modifications to the view's
underlying base table(s) and, where appropriate, return the modified row as it
will appear in the view. Triggers on views can also be defined to execute once
per SQL statement, before or after `INSERT`, `UPDATE`, or `DELETE` operations.
However, such triggers are fired only if there is also an `INSTEAD OF` trigger
on the view. Otherwise, any statement targeting the view must be rewritten
into a statement affecting its underlying base table(s), and then the triggers
that will be fired are the ones attached to the base table(s).

The trigger function must be defined before the trigger itself can be created.
The trigger function must be declared as a function taking no arguments and
returning type `trigger`. (The trigger function receives its input through a
specially-passed `TriggerData` structure, not in the form of ordinary function
arguments.)

Once a suitable trigger function has been created, the trigger is established
with [CREATE TRIGGER](sql-createtrigger.html "CREATE TRIGGER"). The same
trigger function can be used for multiple triggers.

PostgreSQL offers both _per-row_ triggers and _per-statement_ triggers. With a
per-row trigger, the trigger function is invoked once for each row that is
affected by the statement that fired the trigger. In contrast, a per-statement
trigger is invoked only once when an appropriate statement is executed,
regardless of the number of rows affected by that statement. In particular, a
statement that affects zero rows will still result in the execution of any
applicable per-statement triggers. These two types of triggers are sometimes
called _row-level_ triggers and _statement-level_ triggers, respectively.
Triggers on `TRUNCATE` may only be defined at statement level, not per-row.

Triggers are also classified according to whether they fire _before_ , _after_
, or _instead of_ the operation. These are referred to as `BEFORE` triggers,
`AFTER` triggers, and `INSTEAD OF` triggers respectively. Statement-level
`BEFORE` triggers naturally fire before the statement starts to do anything,
while statement-level `AFTER` triggers fire at the very end of the statement.
These types of triggers may be defined on tables, views, or foreign tables.
Row-level `BEFORE` triggers fire immediately before a particular row is
operated on, while row-level `AFTER` triggers fire at the end of the statement
(but before any statement-level `AFTER` triggers). These types of triggers may
only be defined on tables and foreign tables, not views. `INSTEAD OF` triggers
may only be defined on views, and only at row level; they fire immediately as
each row in the view is identified as needing to be operated on.

The execution of an `AFTER` trigger can be deferred to the end of the
transaction, rather than the end of the statement, if it was defined as a
_constraint trigger_. In all cases, a trigger is executed as part of the same
transaction as the statement that triggered it, so if either the statement or
the trigger causes an error, the effects of both will be rolled back.

A statement that targets a parent table in an inheritance or partitioning
hierarchy does not cause the statement-level triggers of affected child tables
to be fired; only the parent table's statement-level triggers are fired.
However, row-level triggers of any affected child tables will be fired.

If an `INSERT` contains an `ON CONFLICT DO UPDATE` clause, it is possible that
the effects of row-level `BEFORE` `INSERT` triggers and row-level `BEFORE`
`UPDATE` triggers can both be applied in a way that is apparent from the final
state of the updated row, if an `EXCLUDED` column is referenced. There need
not be an `EXCLUDED` column reference for both sets of row-level `BEFORE`
triggers to execute, though. The possibility of surprising outcomes should be
considered when there are both `BEFORE` `INSERT` and `BEFORE` `UPDATE` row-
level triggers that change a row being inserted/updated (this can be
problematic even if the modifications are more or less equivalent, if they're
not also idempotent). Note that statement-level `UPDATE` triggers are executed
when `ON CONFLICT DO UPDATE` is specified, regardless of whether or not any
rows were affected by the `UPDATE` (and regardless of whether the alternative
`UPDATE` path was ever taken). An `INSERT` with an `ON CONFLICT DO UPDATE`
clause will execute statement-level `BEFORE` `INSERT` triggers first, then
statement-level `BEFORE` `UPDATE` triggers, followed by statement-level
`AFTER` `UPDATE` triggers and finally statement-level `AFTER` `INSERT`
triggers.

If an `UPDATE` on a partitioned table causes a row to move to another
partition, it will be performed as a `DELETE` from the original partition
followed by an `INSERT` into the new partition. In this case, all row-level
`BEFORE` `UPDATE` triggers and all row-level `BEFORE` `DELETE` triggers are
fired on the original partition. Then all row-level `BEFORE` `INSERT` triggers
are fired on the destination partition. The possibility of surprising outcomes
should be considered when all these triggers affect the row being moved. As
far as `AFTER ROW` triggers are concerned, `AFTER` `DELETE` and `AFTER`
`INSERT` triggers are applied; but `AFTER` `UPDATE` triggers are not applied
because the `UPDATE` has been converted to a `DELETE` and an `INSERT`. As far
as statement-level triggers are concerned, none of the `DELETE` or `INSERT`
triggers are fired, even if row movement occurs; only the `UPDATE` triggers
defined on the target table used in the `UPDATE` statement will be fired.

No separate triggers are defined for `MERGE`. Instead, statement-level or row-
level `UPDATE`, `DELETE`, and `INSERT` triggers are fired depending on (for
statement-level triggers) what actions are specified in the `MERGE` query and
(for row-level triggers) what actions are performed.

While running a `MERGE` command, statement-level `BEFORE` and `AFTER` triggers
are fired for events specified in the actions of the `MERGE` command,
irrespective of whether or not the action is ultimately performed. This is the
same as an `UPDATE` statement that updates no rows, yet statement-level
triggers are fired. The row-level triggers are fired only when a row is
actually updated, inserted or deleted. So it's perfectly legal that while
statement-level triggers are fired for certain types of action, no row-level
triggers are fired for the same kind of action.

Trigger functions invoked by per-statement triggers should always return
`NULL`. Trigger functions invoked by per-row triggers can return a table row
(a value of type `HeapTuple`) to the calling executor, if they choose. A row-
level trigger fired before an operation has the following choices:

  * It can return `NULL` to skip the operation for the current row. This instructs the executor to not perform the row-level operation that invoked the trigger (the insertion, modification, or deletion of a particular table row).

  * For row-level `INSERT` and `UPDATE` triggers only, the returned row becomes the row that will be inserted or will replace the row being updated. This allows the trigger function to modify the row being inserted or updated.

A row-level `BEFORE` trigger that does not intend to cause either of these
behaviors must be careful to return as its result the same row that was passed
in (that is, the `NEW` row for `INSERT` and `UPDATE` triggers, the `OLD` row
for `DELETE` triggers).

A row-level `INSTEAD OF` trigger should either return `NULL` to indicate that
it did not modify any data from the view's underlying base tables, or it
should return the view row that was passed in (the `NEW` row for `INSERT` and
`UPDATE` operations, or the `OLD` row for `DELETE` operations). A nonnull
return value is used to signal that the trigger performed the necessary data
modifications in the view. This will cause the count of the number of rows
affected by the command to be incremented. For `INSERT` and `UPDATE`
operations only, the trigger may modify the `NEW` row before returning it.
This will change the data returned by `INSERT RETURNING` or `UPDATE
RETURNING`, and is useful when the view will not show exactly the same data
that was provided.

The return value is ignored for row-level triggers fired after an operation,
and so they can return `NULL`.

Some considerations apply for generated columns. Stored generated columns are
computed after `BEFORE` triggers and before `AFTER` triggers. Therefore, the
generated value can be inspected in `AFTER` triggers. In `BEFORE` triggers,
the `OLD` row contains the old generated value, as one would expect, but the
`NEW` row does not yet contain the new generated value and should not be
accessed. In the C language interface, the content of the column is undefined
at this point; a higher-level programming language should prevent access to a
stored generated column in the `NEW` row in a `BEFORE` trigger. Changes to the
value of a generated column in a `BEFORE` trigger are ignored and will be
overwritten.

If more than one trigger is defined for the same event on the same relation,
the triggers will be fired in alphabetical order by trigger name. In the case
of `BEFORE` and `INSTEAD OF` triggers, the possibly-modified row returned by
each trigger becomes the input to the next trigger. If any `BEFORE` or
`INSTEAD OF` trigger returns `NULL`, the operation is abandoned for that row
and subsequent triggers are not fired (for that row).

A trigger definition can also specify a Boolean `WHEN` condition, which will
be tested to see whether the trigger should be fired. In row-level triggers
the `WHEN` condition can examine the old and/or new values of columns of the
row. (Statement-level triggers can also have `WHEN` conditions, although the
feature is not so useful for them.) In a `BEFORE` trigger, the `WHEN`
condition is evaluated just before the function is or would be executed, so
using `WHEN` is not materially different from testing the same condition at
the beginning of the trigger function. However, in an `AFTER` trigger, the
`WHEN` condition is evaluated just after the row update occurs, and it
determines whether an event is queued to fire the trigger at the end of
statement. So when an `AFTER` trigger's `WHEN` condition does not return true,
it is not necessary to queue an event nor to re-fetch the row at end of
statement. This can result in significant speedups in statements that modify
many rows, if the trigger only needs to be fired for a few of the rows.
`INSTEAD OF` triggers do not support `WHEN` conditions.

Typically, row-level `BEFORE` triggers are used for checking or modifying the
data that will be inserted or updated. For example, a `BEFORE` trigger might
be used to insert the current time into a `timestamp` column, or to check that
two elements of the row are consistent. Row-level `AFTER` triggers are most
sensibly used to propagate the updates to other tables, or make consistency
checks against other tables. The reason for this division of labor is that an
`AFTER` trigger can be certain it is seeing the final value of the row, while
a `BEFORE` trigger cannot; there might be other `BEFORE` triggers firing after
it. If you have no specific reason to make a trigger `BEFORE` or `AFTER`, the
`BEFORE` case is more efficient, since the information about the operation
doesn't have to be saved until end of statement.

If a trigger function executes SQL commands then these commands might fire
triggers again. This is known as cascading triggers. There is no direct
limitation on the number of cascade levels. It is possible for cascades to
cause a recursive invocation of the same trigger; for example, an `INSERT`
trigger might execute a command that inserts an additional row into the same
table, causing the `INSERT` trigger to be fired again. It is the trigger
programmer's responsibility to avoid infinite recursion in such scenarios.

When a trigger is being defined, arguments can be specified for it. The
purpose of including arguments in the trigger definition is to allow different
triggers with similar requirements to call the same function. As an example,
there could be a generalized trigger function that takes as its arguments two
column names and puts the current user in one and the current time stamp in
the other. Properly written, this trigger function would be independent of the
specific table it is triggering on. So the same function could be used for
`INSERT` events on any table with suitable columns, to automatically track
creation of records in a transaction table for example. It could also be used
to track last-update events if defined as an `UPDATE` trigger.

Each programming language that supports triggers has its own method for making
the trigger input data available to the trigger function. This input data
includes the type of trigger event (e.g., `INSERT` or `UPDATE`) as well as any
arguments that were listed in `CREATE TRIGGER`. For a row-level trigger, the
input data also includes the `NEW` row for `INSERT` and `UPDATE` triggers,
and/or the `OLD` row for `UPDATE` and `DELETE` triggers.

By default, statement-level triggers do not have any way to examine the
individual row(s) modified by the statement. But an `AFTER STATEMENT` trigger
can request that _transition tables_ be created to make the sets of affected
rows available to the trigger. `AFTER ROW` triggers can also request
transition tables, so that they can see the total changes in the table as well
as the change in the individual row they are currently being fired for. The
method for examining the transition tables again depends on the programming
language that is being used, but the typical approach is to make the
transition tables act like read-only temporary tables that can be accessed by
SQL commands issued within the trigger function.

* * *

[Prev](triggers.html "Chapter 39. Triggers")  | [Up](triggers.html "Chapter 39. Triggers") |  [Next](trigger-datachanges.html "39.2. Visibility of Data Changes")  
---|---|---  
Chapter 39. Triggers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  39.2. Visibility of Data Changes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/trigger-definition.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

