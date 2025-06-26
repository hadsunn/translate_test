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

Supported Versions: [Current](/docs/current/sql-droptrigger.html "PostgreSQL
17 - DROP TRIGGER") ([17](/docs/17/sql-droptrigger.html "PostgreSQL 17 - DROP
TRIGGER")) / [16](/docs/16/sql-droptrigger.html "PostgreSQL 16 - DROP
TRIGGER") / [15](/docs/15/sql-droptrigger.html "PostgreSQL 15 - DROP TRIGGER")
/ [14](/docs/14/sql-droptrigger.html "PostgreSQL 14 - DROP TRIGGER") /
[13](/docs/13/sql-droptrigger.html "PostgreSQL 13 - DROP TRIGGER")

Development Versions: [18](/docs/18/sql-droptrigger.html "PostgreSQL 18 - DROP
TRIGGER") / [devel](/docs/devel/sql-droptrigger.html "PostgreSQL devel - DROP
TRIGGER")

Unsupported versions: [12](/docs/12/sql-droptrigger.html "PostgreSQL 12 - DROP
TRIGGER") / [11](/docs/11/sql-droptrigger.html "PostgreSQL 11 - DROP TRIGGER")
/ [10](/docs/10/sql-droptrigger.html "PostgreSQL 10 - DROP TRIGGER") /
[9.6](/docs/9.6/sql-droptrigger.html "PostgreSQL 9.6 - DROP TRIGGER") /
[9.5](/docs/9.5/sql-droptrigger.html "PostgreSQL 9.5 - DROP TRIGGER") /
[9.4](/docs/9.4/sql-droptrigger.html "PostgreSQL 9.4 - DROP TRIGGER") /
[9.3](/docs/9.3/sql-droptrigger.html "PostgreSQL 9.3 - DROP TRIGGER") /
[9.2](/docs/9.2/sql-droptrigger.html "PostgreSQL 9.2 - DROP TRIGGER") /
[9.1](/docs/9.1/sql-droptrigger.html "PostgreSQL 9.1 - DROP TRIGGER") /
[9.0](/docs/9.0/sql-droptrigger.html "PostgreSQL 9.0 - DROP TRIGGER") /
[8.4](/docs/8.4/sql-droptrigger.html "PostgreSQL 8.4 - DROP TRIGGER") /
[8.3](/docs/8.3/sql-droptrigger.html "PostgreSQL 8.3 - DROP TRIGGER") /
[8.2](/docs/8.2/sql-droptrigger.html "PostgreSQL 8.2 - DROP TRIGGER") /
[8.1](/docs/8.1/sql-droptrigger.html "PostgreSQL 8.1 - DROP TRIGGER") /
[8.0](/docs/8.0/sql-droptrigger.html "PostgreSQL 8.0 - DROP TRIGGER") /
[7.4](/docs/7.4/sql-droptrigger.html "PostgreSQL 7.4 - DROP TRIGGER") /
[7.3](/docs/7.3/sql-droptrigger.html "PostgreSQL 7.3 - DROP TRIGGER") /
[7.2](/docs/7.2/sql-droptrigger.html "PostgreSQL 7.2 - DROP TRIGGER") /
[7.1](/docs/7.1/sql-droptrigger.html "PostgreSQL 7.1 - DROP TRIGGER")

__

DROP TRIGGER  
---  
[Prev](sql-droptransform.html "DROP TRANSFORM")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droptype.html "DROP TYPE")  
  
* * *

## DROP TRIGGER

DROP TRIGGER — remove a trigger

## Synopsis

    
    
    DROP TRIGGER [ IF EXISTS ] _name_ ON _table_name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP TRIGGER` removes an existing trigger definition. To execute this
command, the current user must be the owner of the table for which the trigger
is defined.

## Parameters

`IF EXISTS`

    

Do not throw an error if the trigger does not exist. A notice is issued in
this case.

_`name`_

    

The name of the trigger to remove.

_`table_name`_

    

The name (optionally schema-qualified) of the table for which the trigger is
defined.

`CASCADE`

    

Automatically drop objects that depend on the trigger, and in turn all objects
that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the trigger if any objects depend on it. This is the default.

## Examples

Destroy the trigger `if_dist_exists` on the table `films`:

    
    
    DROP TRIGGER if_dist_exists ON films;
    

## Compatibility

The `DROP TRIGGER` statement in PostgreSQL is incompatible with the SQL
standard. In the SQL standard, trigger names are not local to tables, so the
command is simply `DROP TRIGGER _`name`_`.

## See Also

[CREATE TRIGGER](sql-createtrigger.html "CREATE TRIGGER")

* * *

[Prev](sql-droptransform.html "DROP TRANSFORM")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droptype.html "DROP TYPE")  
---|---|---  
DROP TRANSFORM  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP TYPE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droptrigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

