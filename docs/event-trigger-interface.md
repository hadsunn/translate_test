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

Supported Versions: [Current](/docs/current/event-trigger-interface.html
"PostgreSQL 17 - 40.3. Writing Event Trigger Functions in C")
([17](/docs/17/event-trigger-interface.html "PostgreSQL 17 - 40.3. Writing
Event Trigger Functions in C")) / [16](/docs/16/event-trigger-interface.html
"PostgreSQL 16 - 40.3. Writing Event Trigger Functions in C") /
[15](/docs/15/event-trigger-interface.html "PostgreSQL 15 - 40.3. Writing
Event Trigger Functions in C") / [14](/docs/14/event-trigger-interface.html
"PostgreSQL 14 - 40.3. Writing Event Trigger Functions in C") /
[13](/docs/13/event-trigger-interface.html "PostgreSQL 13 - 40.3. Writing
Event Trigger Functions in C")

Development Versions: [18](/docs/18/event-trigger-interface.html "PostgreSQL
18 - 40.3. Writing Event Trigger Functions in C") / [devel](/docs/devel/event-
trigger-interface.html "PostgreSQL devel - 40.3. Writing Event Trigger
Functions in C")

Unsupported versions: [12](/docs/12/event-trigger-interface.html "PostgreSQL
12 - 40.3. Writing Event Trigger Functions in C") / [11](/docs/11/event-
trigger-interface.html "PostgreSQL 11 - 40.3. Writing Event Trigger Functions
in C") / [10](/docs/10/event-trigger-interface.html "PostgreSQL 10 -
40.3. Writing Event Trigger Functions in C") / [9.6](/docs/9.6/event-trigger-
interface.html "PostgreSQL 9.6 - 40.3. Writing Event Trigger Functions in C")
/ [9.5](/docs/9.5/event-trigger-interface.html "PostgreSQL 9.5 - 40.3. Writing
Event Trigger Functions in C") / [9.4](/docs/9.4/event-trigger-interface.html
"PostgreSQL 9.4 - 40.3. Writing Event Trigger Functions in C") /
[9.3](/docs/9.3/event-trigger-interface.html "PostgreSQL 9.3 - 40.3. Writing
Event Trigger Functions in C")

__

40.3. Writing Event Trigger Functions in C  
---  
[Prev](event-trigger-matrix.html "40.2. Event Trigger Firing Matrix")  | [Up](event-triggers.html "Chapter 40. Event Triggers") | Chapter 40. Event Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-trigger-example.html "40.4. A Complete Event Trigger Example")  
  
* * *

## 40.3. Writing Event Trigger Functions in C #

This section describes the low-level details of the interface to an event
trigger function. This information is only needed when writing event trigger
functions in C. If you are using a higher-level language then these details
are handled for you. In most cases you should consider using a procedural
language before writing your event triggers in C. The documentation of each
procedural language explains how to write an event trigger in that language.

Event trigger functions must use the “version 1” function manager interface.

When a function is called by the event trigger manager, it is not passed any
normal arguments, but it is passed a “context” pointer pointing to a
`EventTriggerData` structure. C functions can check whether they were called
from the event trigger manager or not by executing the macro:

    
    
    CALLED_AS_EVENT_TRIGGER(fcinfo)
    

which expands to:

    
    
    ((fcinfo)->context != NULL && IsA((fcinfo)->context, EventTriggerData))
    

If this returns true, then it is safe to cast `fcinfo->context` to type
`EventTriggerData *` and make use of the pointed-to `EventTriggerData`
structure. The function must _not_ alter the `EventTriggerData` structure or
any of the data it points to.

`struct EventTriggerData` is defined in `commands/event_trigger.h`:

    
    
    typedef struct EventTriggerData
    {
        NodeTag     type;
        const char *event;      /* event name */
        Node       *parsetree;  /* parse tree */
        CommandTag  tag;        /* command tag */
    } EventTriggerData;
    

where the members are defined as follows:

`type`

    

Always `T_EventTriggerData`.

`event`

    

Describes the event for which the function is called, one of
`"ddl_command_start"`, `"ddl_command_end"`, `"sql_drop"`, `"table_rewrite"`.
See [Section 40.1](event-trigger-definition.html "40.1. Overview of Event
Trigger Behavior") for the meaning of these events.

`parsetree`

    

A pointer to the parse tree of the command. Check the PostgreSQL source code
for details. The parse tree structure is subject to change without notice.

`tag`

    

The command tag associated with the event for which the event trigger is run,
for example `"CREATE FUNCTION"`.

An event trigger function must return a `NULL` pointer (_not_ an SQL null
value, that is, do not set _`isNull`_ true).

* * *

[Prev](event-trigger-matrix.html "40.2. Event Trigger Firing Matrix")  | [Up](event-triggers.html "Chapter 40. Event Triggers") |  [Next](event-trigger-example.html "40.4. A Complete Event Trigger Example")  
---|---|---  
40.2. Event Trigger Firing Matrix  | [Home](index.html "PostgreSQL 16.9 Documentation") |  40.4. A Complete Event Trigger Example  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-trigger-interface.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

