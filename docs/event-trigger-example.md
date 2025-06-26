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

Supported Versions: [Current](/docs/current/event-trigger-example.html
"PostgreSQL 17 - 40.4. A Complete Event Trigger Example")
([17](/docs/17/event-trigger-example.html "PostgreSQL 17 - 40.4. A Complete
Event Trigger Example")) / [16](/docs/16/event-trigger-example.html
"PostgreSQL 16 - 40.4. A Complete Event Trigger Example") /
[15](/docs/15/event-trigger-example.html "PostgreSQL 15 - 40.4. A Complete
Event Trigger Example") / [14](/docs/14/event-trigger-example.html "PostgreSQL
14 - 40.4. A Complete Event Trigger Example") / [13](/docs/13/event-trigger-
example.html "PostgreSQL 13 - 40.4. A Complete Event Trigger Example")

Development Versions: [18](/docs/18/event-trigger-example.html "PostgreSQL 18
- 40.4. A Complete Event Trigger Example") / [devel](/docs/devel/event-
trigger-example.html "PostgreSQL devel - 40.4. A Complete Event Trigger
Example")

Unsupported versions: [12](/docs/12/event-trigger-example.html "PostgreSQL 12
- 40.4. A Complete Event Trigger Example") / [11](/docs/11/event-trigger-
example.html "PostgreSQL 11 - 40.4. A Complete Event Trigger Example") /
[10](/docs/10/event-trigger-example.html "PostgreSQL 10 - 40.4. A Complete
Event Trigger Example") / [9.6](/docs/9.6/event-trigger-example.html
"PostgreSQL 9.6 - 40.4. A Complete Event Trigger Example") /
[9.5](/docs/9.5/event-trigger-example.html "PostgreSQL 9.5 - 40.4. A Complete
Event Trigger Example") / [9.4](/docs/9.4/event-trigger-example.html
"PostgreSQL 9.4 - 40.4. A Complete Event Trigger Example") /
[9.3](/docs/9.3/event-trigger-example.html "PostgreSQL 9.3 - 40.4. A Complete
Event Trigger Example")

__

40.4. A Complete Event Trigger Example  
---  
[Prev](event-trigger-interface.html "40.3. Writing Event Trigger Functions in C")  | [Up](event-triggers.html "Chapter 40. Event Triggers") | Chapter 40. Event Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-trigger-table-rewrite-example.html "40.5. A Table Rewrite Event Trigger Example")  
  
* * *

## 40.4. A Complete Event Trigger Example #

Here is a very simple example of an event trigger function written in C.
(Examples of triggers written in procedural languages can be found in the
documentation of the procedural languages.)

The function `noddl` raises an exception each time it is called. The event
trigger definition associated the function with the `ddl_command_start` event.
The effect is that all DDL commands (with the exceptions mentioned in [Section
40.1](event-trigger-definition.html "40.1. Overview of Event Trigger
Behavior")) are prevented from running.

This is the source code of the trigger function:

    
    
    #include "postgres.h"
    #include "commands/event_trigger.h"
    
    
    PG_MODULE_MAGIC;
    
    PG_FUNCTION_INFO_V1(noddl);
    
    Datum
    noddl(PG_FUNCTION_ARGS)
    {
        EventTriggerData *trigdata;
    
        if (!CALLED_AS_EVENT_TRIGGER(fcinfo))  /* internal error */
            elog(ERROR, "not fired by event trigger manager");
    
        trigdata = (EventTriggerData *) fcinfo->context;
    
        ereport(ERROR,
                (errcode(ERRCODE_INSUFFICIENT_PRIVILEGE),
                 errmsg("command \"%s\" denied",
                        GetCommandTagName(trigdata->tag))));
    
        PG_RETURN_NULL();
    }
    

After you have compiled the source code (see [Section
38.10.5](xfunc-c.html#DFUNC "38.10.5. Compiling and Linking Dynamically-Loaded
Functions")), declare the function and the triggers:

    
    
    CREATE FUNCTION noddl() RETURNS event_trigger
        AS 'noddl' LANGUAGE C;
    
    CREATE EVENT TRIGGER noddl ON ddl_command_start
        EXECUTE FUNCTION noddl();
    

Now you can test the operation of the trigger:

    
    
    =# \dy
                         List of event triggers
     Name  |       Event       | Owner | Enabled | Function | Tags
    -------+-------------------+-------+---------+----------+------
     noddl | ddl_command_start | dim   | enabled | noddl    |
    (1 row)
    
    =# CREATE TABLE foo(id serial);
    ERROR:  command "CREATE TABLE" denied
    

In this situation, in order to be able to run some DDL commands when you need
to do so, you have to either drop the event trigger or disable it. It can be
convenient to disable the trigger for only the duration of a transaction:

    
    
    BEGIN;
    ALTER EVENT TRIGGER noddl DISABLE;
    CREATE TABLE foo (id serial);
    ALTER EVENT TRIGGER noddl ENABLE;
    COMMIT;
    

(Recall that DDL commands on event triggers themselves are not affected by
event triggers.)

* * *

[Prev](event-trigger-interface.html "40.3. Writing Event Trigger Functions in C")  | [Up](event-triggers.html "Chapter 40. Event Triggers") |  [Next](event-trigger-table-rewrite-example.html "40.5. A Table Rewrite Event Trigger Example")  
---|---|---  
40.3. Writing Event Trigger Functions in C  | [Home](index.html "PostgreSQL 16.9 Documentation") |  40.5. A Table Rewrite Event Trigger Example  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-trigger-example.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

