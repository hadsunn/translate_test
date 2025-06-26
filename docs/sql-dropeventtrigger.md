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

Supported Versions: [Current](/docs/current/sql-dropeventtrigger.html
"PostgreSQL 17 - DROP EVENT TRIGGER") ([17](/docs/17/sql-dropeventtrigger.html
"PostgreSQL 17 - DROP EVENT TRIGGER")) / [16](/docs/16/sql-
dropeventtrigger.html "PostgreSQL 16 - DROP EVENT TRIGGER") /
[15](/docs/15/sql-dropeventtrigger.html "PostgreSQL 15 - DROP EVENT TRIGGER")
/ [14](/docs/14/sql-dropeventtrigger.html "PostgreSQL 14 - DROP EVENT
TRIGGER") / [13](/docs/13/sql-dropeventtrigger.html "PostgreSQL 13 - DROP
EVENT TRIGGER")

Development Versions: [18](/docs/18/sql-dropeventtrigger.html "PostgreSQL 18 -
DROP EVENT TRIGGER") / [devel](/docs/devel/sql-dropeventtrigger.html
"PostgreSQL devel - DROP EVENT TRIGGER")

Unsupported versions: [12](/docs/12/sql-dropeventtrigger.html "PostgreSQL 12 -
DROP EVENT TRIGGER") / [11](/docs/11/sql-dropeventtrigger.html "PostgreSQL 11
- DROP EVENT TRIGGER") / [10](/docs/10/sql-dropeventtrigger.html "PostgreSQL
10 - DROP EVENT TRIGGER") / [9.6](/docs/9.6/sql-dropeventtrigger.html
"PostgreSQL 9.6 - DROP EVENT TRIGGER") / [9.5](/docs/9.5/sql-
dropeventtrigger.html "PostgreSQL 9.5 - DROP EVENT TRIGGER") /
[9.4](/docs/9.4/sql-dropeventtrigger.html "PostgreSQL 9.4 - DROP EVENT
TRIGGER") / [9.3](/docs/9.3/sql-dropeventtrigger.html "PostgreSQL 9.3 - DROP
EVENT TRIGGER")

__

DROP EVENT TRIGGER  
---  
[Prev](sql-dropdomain.html "DROP DOMAIN")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropextension.html "DROP EXTENSION")  
  
* * *

## DROP EVENT TRIGGER

DROP EVENT TRIGGER — remove an event trigger

## Synopsis

    
    
    DROP EVENT TRIGGER [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP EVENT TRIGGER` removes an existing event trigger. To execute this
command, the current user must be the owner of the event trigger.

## Parameters

`IF EXISTS`

    

Do not throw an error if the event trigger does not exist. A notice is issued
in this case.

_`name`_

    

The name of the event trigger to remove.

`CASCADE`

    

Automatically drop objects that depend on the trigger, and in turn all objects
that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the trigger if any objects depend on it. This is the default.

## Examples

Destroy the trigger `snitch`:

    
    
    DROP EVENT TRIGGER snitch;
    

## Compatibility

There is no `DROP EVENT TRIGGER` statement in the SQL standard.

## See Also

[CREATE EVENT TRIGGER](sql-createeventtrigger.html "CREATE EVENT TRIGGER"),
[ALTER EVENT TRIGGER](sql-altereventtrigger.html "ALTER EVENT TRIGGER")

* * *

[Prev](sql-dropdomain.html "DROP DOMAIN")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropextension.html "DROP EXTENSION")  
---|---|---  
DROP DOMAIN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP EXTENSION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropeventtrigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

