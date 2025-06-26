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

Supported Versions: [Current](/docs/current/sql-createeventtrigger.html
"PostgreSQL 17 - CREATE EVENT TRIGGER") ([17](/docs/17/sql-
createeventtrigger.html "PostgreSQL 17 - CREATE EVENT TRIGGER")) /
[16](/docs/16/sql-createeventtrigger.html "PostgreSQL 16 - CREATE EVENT
TRIGGER") / [15](/docs/15/sql-createeventtrigger.html "PostgreSQL 15 - CREATE
EVENT TRIGGER") / [14](/docs/14/sql-createeventtrigger.html "PostgreSQL 14 -
CREATE EVENT TRIGGER") / [13](/docs/13/sql-createeventtrigger.html "PostgreSQL
13 - CREATE EVENT TRIGGER")

Development Versions: [18](/docs/18/sql-createeventtrigger.html "PostgreSQL 18
- CREATE EVENT TRIGGER") / [devel](/docs/devel/sql-createeventtrigger.html
"PostgreSQL devel - CREATE EVENT TRIGGER")

Unsupported versions: [12](/docs/12/sql-createeventtrigger.html "PostgreSQL 12
- CREATE EVENT TRIGGER") / [11](/docs/11/sql-createeventtrigger.html
"PostgreSQL 11 - CREATE EVENT TRIGGER") / [10](/docs/10/sql-
createeventtrigger.html "PostgreSQL 10 - CREATE EVENT TRIGGER") /
[9.6](/docs/9.6/sql-createeventtrigger.html "PostgreSQL 9.6 - CREATE EVENT
TRIGGER") / [9.5](/docs/9.5/sql-createeventtrigger.html "PostgreSQL 9.5 -
CREATE EVENT TRIGGER") / [9.4](/docs/9.4/sql-createeventtrigger.html
"PostgreSQL 9.4 - CREATE EVENT TRIGGER") / [9.3](/docs/9.3/sql-
createeventtrigger.html "PostgreSQL 9.3 - CREATE EVENT TRIGGER")

__

CREATE EVENT TRIGGER  
---  
[Prev](sql-createdomain.html "CREATE DOMAIN")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createextension.html "CREATE EXTENSION")  
  
* * *

## CREATE EVENT TRIGGER

CREATE EVENT TRIGGER — define a new event trigger

## Synopsis

    
    
    CREATE EVENT TRIGGER _name_
        ON _event_
        [ WHEN _filter_variable_ IN (_filter_value_ [, ... ]) [ AND ... ] ]
        EXECUTE { FUNCTION | PROCEDURE } _function_name_()
    

## Description

`CREATE EVENT TRIGGER` creates a new event trigger. Whenever the designated
event occurs and the `WHEN` condition associated with the trigger, if any, is
satisfied, the trigger function will be executed. For a general introduction
to event triggers, see [Chapter 40](event-triggers.html "Chapter 40. Event
Triggers"). The user who creates an event trigger becomes its owner.

## Parameters

_`name`_

    

The name to give the new trigger. This name must be unique within the
database.

_`event`_

    

The name of the event that triggers a call to the given function. See [Section
40.1](event-trigger-definition.html "40.1. Overview of Event Trigger
Behavior") for more information on event names.

_`filter_variable`_

    

The name of a variable used to filter events. This makes it possible to
restrict the firing of the trigger to a subset of the cases in which it is
supported. Currently the only supported _`filter_variable`_ is `TAG`.

_`filter_value`_

    

A list of values for the associated _`filter_variable`_ for which the trigger
should fire. For `TAG`, this means a list of command tags (e.g., `'DROP
FUNCTION'`).

_`function_name`_

    

A user-supplied function that is declared as taking no argument and returning
type `event_trigger`.

In the syntax of `CREATE EVENT TRIGGER`, the keywords `FUNCTION` and
`PROCEDURE` are equivalent, but the referenced function must in any case be a
function, not a procedure. The use of the keyword `PROCEDURE` here is
historical and deprecated.

## Notes

Only superusers can create event triggers.

Event triggers are disabled in single-user mode (see [postgres](app-
postgres.html "postgres")). If an erroneous event trigger disables the
database so much that you can't even drop the trigger, restart in single-user
mode and you'll be able to do that.

## Examples

Forbid the execution of any [DDL](ddl.html "Chapter 5. Data Definition")
command:

    
    
    CREATE OR REPLACE FUNCTION abort_any_command()
      RETURNS event_trigger
     LANGUAGE plpgsql
      AS $$
    BEGIN
      RAISE EXCEPTION 'command % is disabled', tg_tag;
    END;
    $$;
    
    CREATE EVENT TRIGGER abort_ddl ON ddl_command_start
       EXECUTE FUNCTION abort_any_command();
    

## Compatibility

There is no `CREATE EVENT TRIGGER` statement in the SQL standard.

## See Also

[ALTER EVENT TRIGGER](sql-altereventtrigger.html "ALTER EVENT TRIGGER"), [DROP
EVENT TRIGGER](sql-dropeventtrigger.html "DROP EVENT TRIGGER"), [CREATE
FUNCTION](sql-createfunction.html "CREATE FUNCTION")

* * *

[Prev](sql-createdomain.html "CREATE DOMAIN")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createextension.html "CREATE EXTENSION")  
---|---|---  
CREATE DOMAIN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE EXTENSION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createeventtrigger.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

