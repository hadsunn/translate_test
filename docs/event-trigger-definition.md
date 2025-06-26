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

Supported Versions: [Current](/docs/current/event-trigger-definition.html
"PostgreSQL 17 - 40.1. Overview of Event Trigger Behavior")
([17](/docs/17/event-trigger-definition.html "PostgreSQL 17 - 40.1. Overview
of Event Trigger Behavior")) / [16](/docs/16/event-trigger-definition.html
"PostgreSQL 16 - 40.1. Overview of Event Trigger Behavior") /
[15](/docs/15/event-trigger-definition.html "PostgreSQL 15 - 40.1. Overview of
Event Trigger Behavior") / [14](/docs/14/event-trigger-definition.html
"PostgreSQL 14 - 40.1. Overview of Event Trigger Behavior") /
[13](/docs/13/event-trigger-definition.html "PostgreSQL 13 - 40.1. Overview of
Event Trigger Behavior")

Development Versions: [18](/docs/18/event-trigger-definition.html "PostgreSQL
18 - 40.1. Overview of Event Trigger Behavior") / [devel](/docs/devel/event-
trigger-definition.html "PostgreSQL devel - 40.1. Overview of Event Trigger
Behavior")

Unsupported versions: [12](/docs/12/event-trigger-definition.html "PostgreSQL
12 - 40.1. Overview of Event Trigger Behavior") / [11](/docs/11/event-trigger-
definition.html "PostgreSQL 11 - 40.1. Overview of Event Trigger Behavior") /
[10](/docs/10/event-trigger-definition.html "PostgreSQL 10 - 40.1. Overview of
Event Trigger Behavior") / [9.6](/docs/9.6/event-trigger-definition.html
"PostgreSQL 9.6 - 40.1. Overview of Event Trigger Behavior") /
[9.5](/docs/9.5/event-trigger-definition.html "PostgreSQL 9.5 - 40.1. Overview
of Event Trigger Behavior") / [9.4](/docs/9.4/event-trigger-definition.html
"PostgreSQL 9.4 - 40.1. Overview of Event Trigger Behavior") /
[9.3](/docs/9.3/event-trigger-definition.html "PostgreSQL 9.3 - 40.1. Overview
of Event Trigger Behavior")

__

40.1. Overview of Event Trigger Behavior  
---  
[Prev](event-triggers.html "Chapter 40. Event Triggers")  | [Up](event-triggers.html "Chapter 40. Event Triggers") | Chapter 40. Event Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-trigger-matrix.html "40.2. Event Trigger Firing Matrix")  
  
* * *

## 40.1. Overview of Event Trigger Behavior #

An event trigger fires whenever the event with which it is associated occurs
in the database in which it is defined. Currently, the only supported events
are `ddl_command_start`, `ddl_command_end`, `table_rewrite` and `sql_drop`.
Support for additional events may be added in future releases.

The `ddl_command_start` event occurs just before the execution of a `CREATE`,
`ALTER`, `DROP`, `SECURITY LABEL`, `COMMENT`, `GRANT` or `REVOKE` command. No
check whether the affected object exists or doesn't exist is performed before
the event trigger fires. As an exception, however, this event does not occur
for DDL commands targeting shared objects — databases, roles, and tablespaces
— or for commands targeting event triggers themselves. The event trigger
mechanism does not support these object types. `ddl_command_start` also occurs
just before the execution of a `SELECT INTO` command, since this is equivalent
to `CREATE TABLE AS`.

The `ddl_command_end` event occurs just after the execution of this same set
of commands. To obtain more details on the DDL operations that took place, use
the set-returning function `pg_event_trigger_ddl_commands()` from the
`ddl_command_end` event trigger code (see [Section 9.29](functions-event-
triggers.html "9.29. Event Trigger Functions")). Note that the trigger fires
after the actions have taken place (but before the transaction commits), and
thus the system catalogs can be read as already changed.

The `sql_drop` event occurs just before the `ddl_command_end` event trigger
for any operation that drops database objects. To list the objects that have
been dropped, use the set-returning function
`pg_event_trigger_dropped_objects()` from the `sql_drop` event trigger code
(see [Section 9.29](functions-event-triggers.html "9.29. Event Trigger
Functions")). Note that the trigger is executed after the objects have been
deleted from the system catalogs, so it's not possible to look them up
anymore.

The `table_rewrite` event occurs just before a table is rewritten by some
actions of the commands `ALTER TABLE` and `ALTER TYPE`. While other control
statements are available to rewrite a table, like `CLUSTER` and `VACUUM`, the
`table_rewrite` event is not triggered by them. To find the OID of the table
that was rewritten, use the function `pg_event_trigger_table_rewrite_oid()`
(see [Section 9.29](functions-event-triggers.html "9.29. Event Trigger
Functions")). To discover the reason(s) for the rewrite, use the function
`pg_event_trigger_table_rewrite_reason()`.

Event triggers (like other functions) cannot be executed in an aborted
transaction. Thus, if a DDL command fails with an error, any associated
`ddl_command_end` triggers will not be executed. Conversely, if a
`ddl_command_start` trigger fails with an error, no further event triggers
will fire, and no attempt will be made to execute the command itself.
Similarly, if a `ddl_command_end` trigger fails with an error, the effects of
the DDL statement will be rolled back, just as they would be in any other case
where the containing transaction aborts.

For a complete list of commands supported by the event trigger mechanism, see
[Section 40.2](event-trigger-matrix.html "40.2. Event Trigger Firing Matrix").

Event triggers are created using the command [CREATE EVENT TRIGGER](sql-
createeventtrigger.html "CREATE EVENT TRIGGER"). In order to create an event
trigger, you must first create a function with the special return type
`event_trigger`. This function need not (and may not) return a value; the
return type serves merely as a signal that the function is to be invoked as an
event trigger.

If more than one event trigger is defined for a particular event, they will
fire in alphabetical order by trigger name.

A trigger definition can also specify a `WHEN` condition so that, for example,
a `ddl_command_start` trigger can be fired only for particular commands which
the user wishes to intercept. A common use of such triggers is to restrict the
range of DDL operations which users may perform.

* * *

[Prev](event-triggers.html "Chapter 40. Event Triggers")  | [Up](event-triggers.html "Chapter 40. Event Triggers") |  [Next](event-trigger-matrix.html "40.2. Event Trigger Firing Matrix")  
---|---|---  
Chapter 40. Event Triggers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  40.2. Event Trigger Firing Matrix  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-trigger-
definition.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

