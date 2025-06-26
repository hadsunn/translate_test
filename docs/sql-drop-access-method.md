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

Supported Versions: [Current](/docs/current/sql-drop-access-method.html
"PostgreSQL 17 - DROP ACCESS METHOD") ([17](/docs/17/sql-drop-access-
method.html "PostgreSQL 17 - DROP ACCESS METHOD")) / [16](/docs/16/sql-drop-
access-method.html "PostgreSQL 16 - DROP ACCESS METHOD") / [15](/docs/15/sql-
drop-access-method.html "PostgreSQL 15 - DROP ACCESS METHOD") /
[14](/docs/14/sql-drop-access-method.html "PostgreSQL 14 - DROP ACCESS
METHOD") / [13](/docs/13/sql-drop-access-method.html "PostgreSQL 13 - DROP
ACCESS METHOD")

Development Versions: [18](/docs/18/sql-drop-access-method.html "PostgreSQL 18
- DROP ACCESS METHOD") / [devel](/docs/devel/sql-drop-access-method.html
"PostgreSQL devel - DROP ACCESS METHOD")

Unsupported versions: [12](/docs/12/sql-drop-access-method.html "PostgreSQL 12
- DROP ACCESS METHOD") / [11](/docs/11/sql-drop-access-method.html "PostgreSQL
11 - DROP ACCESS METHOD") / [10](/docs/10/sql-drop-access-method.html
"PostgreSQL 10 - DROP ACCESS METHOD") / [9.6](/docs/9.6/sql-drop-access-
method.html "PostgreSQL 9.6 - DROP ACCESS METHOD")

__

DROP ACCESS METHOD  
---  
[Prev](sql-do.html "DO")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropaggregate.html "DROP AGGREGATE")  
  
* * *

## DROP ACCESS METHOD

DROP ACCESS METHOD — remove an access method

## Synopsis

    
    
    DROP ACCESS METHOD [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP ACCESS METHOD` removes an existing access method. Only superusers can
drop access methods.

## Parameters

`IF EXISTS`

    

Do not throw an error if the access method does not exist. A notice is issued
in this case.

_`name`_

    

The name of an existing access method.

`CASCADE`

    

Automatically drop objects that depend on the access method (such as operator
classes, operator families, and indexes), and in turn all objects that depend
on those objects (see [Section 5.14](ddl-depend.html "5.14. Dependency
Tracking")).

`RESTRICT`

    

Refuse to drop the access method if any objects depend on it. This is the
default.

## Examples

Drop the access method `heptree`:

    
    
    DROP ACCESS METHOD heptree;
    

## Compatibility

`DROP ACCESS METHOD` is a PostgreSQL extension.

## See Also

[CREATE ACCESS METHOD](sql-create-access-method.html "CREATE ACCESS METHOD")

* * *

[Prev](sql-do.html "DO")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropaggregate.html "DROP AGGREGATE")  
---|---|---  
DO  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP AGGREGATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-drop-access-method.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

