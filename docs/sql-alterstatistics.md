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

Supported Versions: [Current](/docs/current/sql-alterstatistics.html
"PostgreSQL 17 - ALTER STATISTICS") ([17](/docs/17/sql-alterstatistics.html
"PostgreSQL 17 - ALTER STATISTICS")) / [16](/docs/16/sql-alterstatistics.html
"PostgreSQL 16 - ALTER STATISTICS") / [15](/docs/15/sql-alterstatistics.html
"PostgreSQL 15 - ALTER STATISTICS") / [14](/docs/14/sql-alterstatistics.html
"PostgreSQL 14 - ALTER STATISTICS") / [13](/docs/13/sql-alterstatistics.html
"PostgreSQL 13 - ALTER STATISTICS")

Development Versions: [18](/docs/18/sql-alterstatistics.html "PostgreSQL 18 -
ALTER STATISTICS") / [devel](/docs/devel/sql-alterstatistics.html "PostgreSQL
devel - ALTER STATISTICS")

Unsupported versions: [12](/docs/12/sql-alterstatistics.html "PostgreSQL 12 -
ALTER STATISTICS") / [11](/docs/11/sql-alterstatistics.html "PostgreSQL 11 -
ALTER STATISTICS") / [10](/docs/10/sql-alterstatistics.html "PostgreSQL 10 -
ALTER STATISTICS")

__

ALTER STATISTICS  
---  
[Prev](sql-alterserver.html "ALTER SERVER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altersubscription.html "ALTER SUBSCRIPTION")  
  
* * *

## ALTER STATISTICS

ALTER STATISTICS — change the definition of an extended statistics object

## Synopsis

    
    
    ALTER STATISTICS _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER STATISTICS _name_ RENAME TO _new_name_
    ALTER STATISTICS _name_ SET SCHEMA _new_schema_
    ALTER STATISTICS _name_ SET STATISTICS _new_target_
    

## Description

`ALTER STATISTICS` changes the parameters of an existing extended statistics
object. Any parameters not specifically set in the `ALTER STATISTICS` command
retain their prior settings.

You must own the statistics object to use `ALTER STATISTICS`. To change a
statistics object's schema, you must also have `CREATE` privilege on the new
schema. To alter the owner, you must be able to `SET ROLE` to the new owning
role, and that role must have `CREATE` privilege on the statistics object's
schema. (These restrictions enforce that altering the owner doesn't do
anything you couldn't do by dropping and recreating the statistics object.
However, a superuser can alter ownership of any statistics object anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of the statistics object to be altered.

_`new_owner`_

    

The user name of the new owner of the statistics object.

_`new_name`_

    

The new name for the statistics object.

_`new_schema`_

    

The new schema for the statistics object.

_`new_target`_

    

The statistic-gathering target for this statistics object for subsequent
[`ANALYZE`](sql-analyze.html "ANALYZE") operations. The target can be set in
the range 0 to 10000; alternatively, set it to -1 to revert to using the
maximum of the statistics target of the referenced columns, if set, or the
system default statistics target ([default_statistics_target](runtime-config-
query.html#GUC-DEFAULT-STATISTICS-TARGET)). For more information on the use of
statistics by the PostgreSQL query planner, refer to [Section 14.2](planner-
stats.html "14.2. Statistics Used by the Planner").

## Compatibility

There is no `ALTER STATISTICS` command in the SQL standard.

## See Also

[CREATE STATISTICS](sql-createstatistics.html "CREATE STATISTICS"), [DROP
STATISTICS](sql-dropstatistics.html "DROP STATISTICS")

* * *

[Prev](sql-alterserver.html "ALTER SERVER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altersubscription.html "ALTER SUBSCRIPTION")  
---|---|---  
ALTER SERVER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER SUBSCRIPTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterstatistics.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

