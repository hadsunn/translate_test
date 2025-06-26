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

Supported Versions: [Current](/docs/current/sql-dropcollation.html "PostgreSQL
17 - DROP COLLATION") ([17](/docs/17/sql-dropcollation.html "PostgreSQL 17 -
DROP COLLATION")) / [16](/docs/16/sql-dropcollation.html "PostgreSQL 16 - DROP
COLLATION") / [15](/docs/15/sql-dropcollation.html "PostgreSQL 15 - DROP
COLLATION") / [14](/docs/14/sql-dropcollation.html "PostgreSQL 14 - DROP
COLLATION") / [13](/docs/13/sql-dropcollation.html "PostgreSQL 13 - DROP
COLLATION")

Development Versions: [18](/docs/18/sql-dropcollation.html "PostgreSQL 18 -
DROP COLLATION") / [devel](/docs/devel/sql-dropcollation.html "PostgreSQL
devel - DROP COLLATION")

Unsupported versions: [12](/docs/12/sql-dropcollation.html "PostgreSQL 12 -
DROP COLLATION") / [11](/docs/11/sql-dropcollation.html "PostgreSQL 11 - DROP
COLLATION") / [10](/docs/10/sql-dropcollation.html "PostgreSQL 10 - DROP
COLLATION") / [9.6](/docs/9.6/sql-dropcollation.html "PostgreSQL 9.6 - DROP
COLLATION") / [9.5](/docs/9.5/sql-dropcollation.html "PostgreSQL 9.5 - DROP
COLLATION") / [9.4](/docs/9.4/sql-dropcollation.html "PostgreSQL 9.4 - DROP
COLLATION") / [9.3](/docs/9.3/sql-dropcollation.html "PostgreSQL 9.3 - DROP
COLLATION") / [9.2](/docs/9.2/sql-dropcollation.html "PostgreSQL 9.2 - DROP
COLLATION") / [9.1](/docs/9.1/sql-dropcollation.html "PostgreSQL 9.1 - DROP
COLLATION")

__

DROP COLLATION  
---  
[Prev](sql-dropcast.html "DROP CAST")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropconversion.html "DROP CONVERSION")  
  
* * *

## DROP COLLATION

DROP COLLATION — remove a collation

## Synopsis

    
    
    DROP COLLATION [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP COLLATION` removes a previously defined collation. To be able to drop a
collation, you must own the collation.

## Parameters

`IF EXISTS`

    

Do not throw an error if the collation does not exist. A notice is issued in
this case.

_`name`_

    

The name of the collation. The collation name can be schema-qualified.

`CASCADE`

    

Automatically drop objects that depend on the collation, and in turn all
objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the collation if any objects depend on it. This is the default.

## Examples

To drop the collation named `german`:

    
    
    DROP COLLATION german;
    

## Compatibility

The `DROP COLLATION` command conforms to the SQL standard, apart from the `IF
EXISTS` option, which is a PostgreSQL extension.

## See Also

[ALTER COLLATION](sql-altercollation.html "ALTER COLLATION"), [CREATE
COLLATION](sql-createcollation.html "CREATE COLLATION")

* * *

[Prev](sql-dropcast.html "DROP CAST")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropconversion.html "DROP CONVERSION")  
---|---|---  
DROP CAST  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP CONVERSION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropcollation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

