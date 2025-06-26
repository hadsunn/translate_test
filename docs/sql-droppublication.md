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

Supported Versions: [Current](/docs/current/sql-droppublication.html
"PostgreSQL 17 - DROP PUBLICATION") ([17](/docs/17/sql-droppublication.html
"PostgreSQL 17 - DROP PUBLICATION")) / [16](/docs/16/sql-droppublication.html
"PostgreSQL 16 - DROP PUBLICATION") / [15](/docs/15/sql-droppublication.html
"PostgreSQL 15 - DROP PUBLICATION") / [14](/docs/14/sql-droppublication.html
"PostgreSQL 14 - DROP PUBLICATION") / [13](/docs/13/sql-droppublication.html
"PostgreSQL 13 - DROP PUBLICATION")

Development Versions: [18](/docs/18/sql-droppublication.html "PostgreSQL 18 -
DROP PUBLICATION") / [devel](/docs/devel/sql-droppublication.html "PostgreSQL
devel - DROP PUBLICATION")

Unsupported versions: [12](/docs/12/sql-droppublication.html "PostgreSQL 12 -
DROP PUBLICATION") / [11](/docs/11/sql-droppublication.html "PostgreSQL 11 -
DROP PUBLICATION") / [10](/docs/10/sql-droppublication.html "PostgreSQL 10 -
DROP PUBLICATION")

__

DROP PUBLICATION  
---  
[Prev](sql-dropprocedure.html "DROP PROCEDURE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droprole.html "DROP ROLE")  
  
* * *

## DROP PUBLICATION

DROP PUBLICATION — remove a publication

## Synopsis

    
    
    DROP PUBLICATION [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP PUBLICATION` removes an existing publication from the database.

A publication can only be dropped by its owner or a superuser.

## Parameters

`IF EXISTS`

    

Do not throw an error if the publication does not exist. A notice is issued in
this case.

_`name`_

    

The name of an existing publication.

`CASCADE`  
`RESTRICT`

    

These key words do not have any effect, since there are no dependencies on
publications.

## Examples

Drop a publication:

    
    
    DROP PUBLICATION mypublication;
    

## Compatibility

`DROP PUBLICATION` is a PostgreSQL extension.

## See Also

[CREATE PUBLICATION](sql-createpublication.html "CREATE PUBLICATION"), [ALTER
PUBLICATION](sql-alterpublication.html "ALTER PUBLICATION")

* * *

[Prev](sql-dropprocedure.html "DROP PROCEDURE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droprole.html "DROP ROLE")  
---|---|---  
DROP PROCEDURE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP ROLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droppublication.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

