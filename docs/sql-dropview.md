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

Supported Versions: [Current](/docs/current/sql-dropview.html "PostgreSQL 17 -
DROP VIEW") ([17](/docs/17/sql-dropview.html "PostgreSQL 17 - DROP VIEW")) /
[16](/docs/16/sql-dropview.html "PostgreSQL 16 - DROP VIEW") /
[15](/docs/15/sql-dropview.html "PostgreSQL 15 - DROP VIEW") /
[14](/docs/14/sql-dropview.html "PostgreSQL 14 - DROP VIEW") /
[13](/docs/13/sql-dropview.html "PostgreSQL 13 - DROP VIEW")

Development Versions: [18](/docs/18/sql-dropview.html "PostgreSQL 18 - DROP
VIEW") / [devel](/docs/devel/sql-dropview.html "PostgreSQL devel - DROP VIEW")

Unsupported versions: [12](/docs/12/sql-dropview.html "PostgreSQL 12 - DROP
VIEW") / [11](/docs/11/sql-dropview.html "PostgreSQL 11 - DROP VIEW") /
[10](/docs/10/sql-dropview.html "PostgreSQL 10 - DROP VIEW") /
[9.6](/docs/9.6/sql-dropview.html "PostgreSQL 9.6 - DROP VIEW") /
[9.5](/docs/9.5/sql-dropview.html "PostgreSQL 9.5 - DROP VIEW") /
[9.4](/docs/9.4/sql-dropview.html "PostgreSQL 9.4 - DROP VIEW") /
[9.3](/docs/9.3/sql-dropview.html "PostgreSQL 9.3 - DROP VIEW") /
[9.2](/docs/9.2/sql-dropview.html "PostgreSQL 9.2 - DROP VIEW") /
[9.1](/docs/9.1/sql-dropview.html "PostgreSQL 9.1 - DROP VIEW") /
[9.0](/docs/9.0/sql-dropview.html "PostgreSQL 9.0 - DROP VIEW") /
[8.4](/docs/8.4/sql-dropview.html "PostgreSQL 8.4 - DROP VIEW") /
[8.3](/docs/8.3/sql-dropview.html "PostgreSQL 8.3 - DROP VIEW") /
[8.2](/docs/8.2/sql-dropview.html "PostgreSQL 8.2 - DROP VIEW") /
[8.1](/docs/8.1/sql-dropview.html "PostgreSQL 8.1 - DROP VIEW") /
[8.0](/docs/8.0/sql-dropview.html "PostgreSQL 8.0 - DROP VIEW") /
[7.4](/docs/7.4/sql-dropview.html "PostgreSQL 7.4 - DROP VIEW") /
[7.3](/docs/7.3/sql-dropview.html "PostgreSQL 7.3 - DROP VIEW") /
[7.2](/docs/7.2/sql-dropview.html "PostgreSQL 7.2 - DROP VIEW") /
[7.1](/docs/7.1/sql-dropview.html "PostgreSQL 7.1 - DROP VIEW")

__

DROP VIEW  
---  
[Prev](sql-dropusermapping.html "DROP USER MAPPING")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-end.html "END")  
  
* * *

## DROP VIEW

DROP VIEW — remove a view

## Synopsis

    
    
    DROP VIEW [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP VIEW` drops an existing view. To execute this command you must be the
owner of the view.

## Parameters

`IF EXISTS`

    

Do not throw an error if the view does not exist. A notice is issued in this
case.

_`name`_

    

The name (optionally schema-qualified) of the view to remove.

`CASCADE`

    

Automatically drop objects that depend on the view (such as other views), and
in turn all objects that depend on those objects (see [Section 5.14](ddl-
depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the view if any objects depend on it. This is the default.

## Examples

This command will remove the view called `kinds`:

    
    
    DROP VIEW kinds;
    

## Compatibility

This command conforms to the SQL standard, except that the standard only
allows one view to be dropped per command, and apart from the `IF EXISTS`
option, which is a PostgreSQL extension.

## See Also

[ALTER VIEW](sql-alterview.html "ALTER VIEW"), [CREATE VIEW](sql-
createview.html "CREATE VIEW")

* * *

[Prev](sql-dropusermapping.html "DROP USER MAPPING")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-end.html "END")  
---|---|---  
DROP USER MAPPING  | [Home](index.html "PostgreSQL 16.9 Documentation") |  END  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropview.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

