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

Supported Versions: [Current](/docs/current/sql-dropstatistics.html
"PostgreSQL 17 - DROP STATISTICS") ([17](/docs/17/sql-dropstatistics.html
"PostgreSQL 17 - DROP STATISTICS")) / [16](/docs/16/sql-dropstatistics.html
"PostgreSQL 16 - DROP STATISTICS") / [15](/docs/15/sql-dropstatistics.html
"PostgreSQL 15 - DROP STATISTICS") / [14](/docs/14/sql-dropstatistics.html
"PostgreSQL 14 - DROP STATISTICS") / [13](/docs/13/sql-dropstatistics.html
"PostgreSQL 13 - DROP STATISTICS")

Development Versions: [18](/docs/18/sql-dropstatistics.html "PostgreSQL 18 -
DROP STATISTICS") / [devel](/docs/devel/sql-dropstatistics.html "PostgreSQL
devel - DROP STATISTICS")

Unsupported versions: [12](/docs/12/sql-dropstatistics.html "PostgreSQL 12 -
DROP STATISTICS") / [11](/docs/11/sql-dropstatistics.html "PostgreSQL 11 -
DROP STATISTICS") / [10](/docs/10/sql-dropstatistics.html "PostgreSQL 10 -
DROP STATISTICS")

__

DROP STATISTICS  
---  
[Prev](sql-dropserver.html "DROP SERVER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropsubscription.html "DROP SUBSCRIPTION")  
  
* * *

## DROP STATISTICS

DROP STATISTICS — remove extended statistics

## Synopsis

    
    
    DROP STATISTICS [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP STATISTICS` removes statistics object(s) from the database. Only the
statistics object's owner, the schema owner, or a superuser can drop a
statistics object.

## Parameters

`IF EXISTS`

    

Do not throw an error if the statistics object does not exist. A notice is
issued in this case.

_`name`_

    

The name (optionally schema-qualified) of the statistics object to drop.

`CASCADE`  
`RESTRICT`

    

These key words do not have any effect, since there are no dependencies on
statistics.

## Examples

To destroy two statistics objects in different schemas, without failing if
they don't exist:

    
    
    DROP STATISTICS IF EXISTS
        accounting.users_uid_creation,
        public.grants_user_role;
    

## Compatibility

There is no `DROP STATISTICS` command in the SQL standard.

## See Also

[ALTER STATISTICS](sql-alterstatistics.html "ALTER STATISTICS"), [CREATE
STATISTICS](sql-createstatistics.html "CREATE STATISTICS")

* * *

[Prev](sql-dropserver.html "DROP SERVER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropsubscription.html "DROP SUBSCRIPTION")  
---|---|---  
DROP SERVER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP SUBSCRIPTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropstatistics.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

