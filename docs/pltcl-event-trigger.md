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

Supported Versions: [Current](/docs/current/pltcl-event-trigger.html
"PostgreSQL 17 - 44.7. Event Trigger Functions in PL/Tcl")
([17](/docs/17/pltcl-event-trigger.html "PostgreSQL 17 - 44.7. Event Trigger
Functions in PL/Tcl")) / [16](/docs/16/pltcl-event-trigger.html "PostgreSQL 16
- 44.7. Event Trigger Functions in PL/Tcl") / [15](/docs/15/pltcl-event-
trigger.html "PostgreSQL 15 - 44.7. Event Trigger Functions in PL/Tcl") /
[14](/docs/14/pltcl-event-trigger.html "PostgreSQL 14 - 44.7. Event Trigger
Functions in PL/Tcl") / [13](/docs/13/pltcl-event-trigger.html "PostgreSQL 13
- 44.7. Event Trigger Functions in PL/Tcl")

Development Versions: [18](/docs/18/pltcl-event-trigger.html "PostgreSQL 18 -
44.7. Event Trigger Functions in PL/Tcl") / [devel](/docs/devel/pltcl-event-
trigger.html "PostgreSQL devel - 44.7. Event Trigger Functions in PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-event-trigger.html "PostgreSQL 12 -
44.7. Event Trigger Functions in PL/Tcl") / [11](/docs/11/pltcl-event-
trigger.html "PostgreSQL 11 - 44.7. Event Trigger Functions in PL/Tcl") /
[10](/docs/10/pltcl-event-trigger.html "PostgreSQL 10 - 44.7. Event Trigger
Functions in PL/Tcl") / [9.6](/docs/9.6/pltcl-event-trigger.html "PostgreSQL
9.6 - 44.7. Event Trigger Functions in PL/Tcl") / [9.5](/docs/9.5/pltcl-event-
trigger.html "PostgreSQL 9.5 - 44.7. Event Trigger Functions in PL/Tcl") /
[9.4](/docs/9.4/pltcl-event-trigger.html "PostgreSQL 9.4 - 44.7. Event Trigger
Functions in PL/Tcl")

__

44.7. Event Trigger Functions in PL/Tcl  
---  
[Prev](pltcl-trigger.html "44.6. Trigger Functions in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-error-handling.html "44.8. Error Handling in PL/Tcl")  
  
* * *

## 44.7. Event Trigger Functions in PL/Tcl #

Event trigger functions can be written in PL/Tcl. PostgreSQL requires that a
function that is to be called as an event trigger must be declared as a
function with no arguments and a return type of `event_trigger`.

The information from the trigger manager is passed to the function body in the
following variables:

`$TG_event`

    

The name of the event the trigger is fired for.

`$TG_tag`

    

The command tag for which the trigger is fired.

The return value of the trigger function is ignored.

Here's a little example event trigger function that simply raises a `NOTICE`
message each time a supported command is executed:

    
    
    CREATE OR REPLACE FUNCTION tclsnitch() RETURNS event_trigger AS $$
      elog NOTICE "tclsnitch: $TG_event $TG_tag"
    $$ LANGUAGE pltcl;
    
    CREATE EVENT TRIGGER tcl_a_snitch ON ddl_command_start EXECUTE FUNCTION tclsnitch();
    

* * *

[Prev](pltcl-trigger.html "44.6. Trigger Functions in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-error-handling.html "44.8. Error Handling in PL/Tcl")  
---|---|---  
44.6. Trigger Functions in PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.8. Error Handling in PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-event-trigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

