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

Supported Versions: [Current](/docs/current/sql-altertrigger.html "PostgreSQL
17 - ALTER TRIGGER") ([17](/docs/17/sql-altertrigger.html "PostgreSQL 17 -
ALTER TRIGGER")) / [16](/docs/16/sql-altertrigger.html "PostgreSQL 16 - ALTER
TRIGGER") / [15](/docs/15/sql-altertrigger.html "PostgreSQL 15 - ALTER
TRIGGER") / [14](/docs/14/sql-altertrigger.html "PostgreSQL 14 - ALTER
TRIGGER") / [13](/docs/13/sql-altertrigger.html "PostgreSQL 13 - ALTER
TRIGGER")

Development Versions: [18](/docs/18/sql-altertrigger.html "PostgreSQL 18 -
ALTER TRIGGER") / [devel](/docs/devel/sql-altertrigger.html "PostgreSQL devel
- ALTER TRIGGER")

Unsupported versions: [12](/docs/12/sql-altertrigger.html "PostgreSQL 12 -
ALTER TRIGGER") / [11](/docs/11/sql-altertrigger.html "PostgreSQL 11 - ALTER
TRIGGER") / [10](/docs/10/sql-altertrigger.html "PostgreSQL 10 - ALTER
TRIGGER") / [9.6](/docs/9.6/sql-altertrigger.html "PostgreSQL 9.6 - ALTER
TRIGGER") / [9.5](/docs/9.5/sql-altertrigger.html "PostgreSQL 9.5 - ALTER
TRIGGER") / [9.4](/docs/9.4/sql-altertrigger.html "PostgreSQL 9.4 - ALTER
TRIGGER") / [9.3](/docs/9.3/sql-altertrigger.html "PostgreSQL 9.3 - ALTER
TRIGGER") / [9.2](/docs/9.2/sql-altertrigger.html "PostgreSQL 9.2 - ALTER
TRIGGER") / [9.1](/docs/9.1/sql-altertrigger.html "PostgreSQL 9.1 - ALTER
TRIGGER") / [9.0](/docs/9.0/sql-altertrigger.html "PostgreSQL 9.0 - ALTER
TRIGGER") / [8.4](/docs/8.4/sql-altertrigger.html "PostgreSQL 8.4 - ALTER
TRIGGER") / [8.3](/docs/8.3/sql-altertrigger.html "PostgreSQL 8.3 - ALTER
TRIGGER") / [8.2](/docs/8.2/sql-altertrigger.html "PostgreSQL 8.2 - ALTER
TRIGGER") / [8.1](/docs/8.1/sql-altertrigger.html "PostgreSQL 8.1 - ALTER
TRIGGER") / [8.0](/docs/8.0/sql-altertrigger.html "PostgreSQL 8.0 - ALTER
TRIGGER") / [7.4](/docs/7.4/sql-altertrigger.html "PostgreSQL 7.4 - ALTER
TRIGGER") / [7.3](/docs/7.3/sql-altertrigger.html "PostgreSQL 7.3 - ALTER
TRIGGER")

__

ALTER TRIGGER  
---  
[Prev](sql-altertstemplate.html "ALTER TEXT SEARCH TEMPLATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altertype.html "ALTER TYPE")  
  
* * *

## ALTER TRIGGER

ALTER TRIGGER — change the definition of a trigger

## Synopsis

    
    
    ALTER TRIGGER _name_ ON _table_name_ RENAME TO _new_name_
    ALTER TRIGGER _name_ ON _table_name_ [ NO ] DEPENDS ON EXTENSION _extension_name_
    

## Description

`ALTER TRIGGER` changes properties of an existing trigger.

The `RENAME` clause changes the name of the given trigger without otherwise
changing the trigger definition. If the table that the trigger is on is a
partitioned table, then corresponding clone triggers in the partitions are
renamed too.

The `DEPENDS ON EXTENSION` clause marks the trigger as dependent on an
extension, such that if the extension is dropped, the trigger will
automatically be dropped as well.

You must own the table on which the trigger acts to be allowed to change its
properties.

## Parameters

_`name`_

    

The name of an existing trigger to alter.

_`table_name`_

    

The name of the table on which this trigger acts.

_`new_name`_

    

The new name for the trigger.

_`extension_name`_

    

The name of the extension that the trigger is to depend on (or no longer
dependent on, if `NO` is specified). A trigger that's marked as dependent on
an extension is automatically dropped when the extension is dropped.

## Notes

The ability to temporarily enable or disable a trigger is provided by [`ALTER
TABLE`](sql-altertable.html "ALTER TABLE"), not by `ALTER TRIGGER`, because
`ALTER TRIGGER` has no convenient way to express the option of enabling or
disabling all of a table's triggers at once.

## Examples

To rename an existing trigger:

    
    
    ALTER TRIGGER emp_stamp ON emp RENAME TO emp_track_chgs;
    

To mark a trigger as being dependent on an extension:

    
    
    ALTER TRIGGER emp_stamp ON emp DEPENDS ON EXTENSION emplib;
    

## Compatibility

`ALTER TRIGGER` is a PostgreSQL extension of the SQL standard.

## See Also

[ALTER TABLE](sql-altertable.html "ALTER TABLE")

* * *

[Prev](sql-altertstemplate.html "ALTER TEXT SEARCH TEMPLATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altertype.html "ALTER TYPE")  
---|---|---  
ALTER TEXT SEARCH TEMPLATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER TYPE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altertrigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

