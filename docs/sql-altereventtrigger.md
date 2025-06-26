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

Supported Versions: [Current](/docs/current/sql-altereventtrigger.html
"PostgreSQL 17 - ALTER EVENT TRIGGER") ([17](/docs/17/sql-
altereventtrigger.html "PostgreSQL 17 - ALTER EVENT TRIGGER")) /
[16](/docs/16/sql-altereventtrigger.html "PostgreSQL 16 - ALTER EVENT
TRIGGER") / [15](/docs/15/sql-altereventtrigger.html "PostgreSQL 15 - ALTER
EVENT TRIGGER") / [14](/docs/14/sql-altereventtrigger.html "PostgreSQL 14 -
ALTER EVENT TRIGGER") / [13](/docs/13/sql-altereventtrigger.html "PostgreSQL
13 - ALTER EVENT TRIGGER")

Development Versions: [18](/docs/18/sql-altereventtrigger.html "PostgreSQL 18
- ALTER EVENT TRIGGER") / [devel](/docs/devel/sql-altereventtrigger.html
"PostgreSQL devel - ALTER EVENT TRIGGER")

Unsupported versions: [12](/docs/12/sql-altereventtrigger.html "PostgreSQL 12
- ALTER EVENT TRIGGER") / [11](/docs/11/sql-altereventtrigger.html "PostgreSQL
11 - ALTER EVENT TRIGGER") / [10](/docs/10/sql-altereventtrigger.html
"PostgreSQL 10 - ALTER EVENT TRIGGER") / [9.6](/docs/9.6/sql-
altereventtrigger.html "PostgreSQL 9.6 - ALTER EVENT TRIGGER") /
[9.5](/docs/9.5/sql-altereventtrigger.html "PostgreSQL 9.5 - ALTER EVENT
TRIGGER") / [9.4](/docs/9.4/sql-altereventtrigger.html "PostgreSQL 9.4 - ALTER
EVENT TRIGGER") / [9.3](/docs/9.3/sql-altereventtrigger.html "PostgreSQL 9.3 -
ALTER EVENT TRIGGER")

__

ALTER EVENT TRIGGER  
---  
[Prev](sql-alterdomain.html "ALTER DOMAIN")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterextension.html "ALTER EXTENSION")  
  
* * *

## ALTER EVENT TRIGGER

ALTER EVENT TRIGGER — change the definition of an event trigger

## Synopsis

    
    
    ALTER EVENT TRIGGER _name_ DISABLE
    ALTER EVENT TRIGGER _name_ ENABLE [ REPLICA | ALWAYS ]
    ALTER EVENT TRIGGER _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER EVENT TRIGGER _name_ RENAME TO _new_name_
    

## Description

`ALTER EVENT TRIGGER` changes properties of an existing event trigger.

You must be superuser to alter an event trigger.

## Parameters

_`name`_

    

The name of an existing trigger to alter.

_`new_owner`_

    

The user name of the new owner of the event trigger.

_`new_name`_

    

The new name of the event trigger.

`DISABLE`/`ENABLE [ REPLICA | ALWAYS ]`
    

These forms configure the firing of event triggers. A disabled trigger is
still known to the system, but is not executed when its triggering event
occurs. See also [session_replication_role](runtime-config-client.html#GUC-
SESSION-REPLICATION-ROLE).

## Compatibility

There is no `ALTER EVENT TRIGGER` statement in the SQL standard.

## See Also

[CREATE EVENT TRIGGER](sql-createeventtrigger.html "CREATE EVENT TRIGGER"),
[DROP EVENT TRIGGER](sql-dropeventtrigger.html "DROP EVENT TRIGGER")

* * *

[Prev](sql-alterdomain.html "ALTER DOMAIN")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterextension.html "ALTER EXTENSION")  
---|---|---  
ALTER DOMAIN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER EXTENSION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altereventtrigger.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

