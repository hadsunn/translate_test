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

Supported Versions: [Current](/docs/current/sql-alterlanguage.html "PostgreSQL
17 - ALTER LANGUAGE") ([17](/docs/17/sql-alterlanguage.html "PostgreSQL 17 -
ALTER LANGUAGE")) / [16](/docs/16/sql-alterlanguage.html "PostgreSQL 16 -
ALTER LANGUAGE") / [15](/docs/15/sql-alterlanguage.html "PostgreSQL 15 - ALTER
LANGUAGE") / [14](/docs/14/sql-alterlanguage.html "PostgreSQL 14 - ALTER
LANGUAGE") / [13](/docs/13/sql-alterlanguage.html "PostgreSQL 13 - ALTER
LANGUAGE")

Development Versions: [18](/docs/18/sql-alterlanguage.html "PostgreSQL 18 -
ALTER LANGUAGE") / [devel](/docs/devel/sql-alterlanguage.html "PostgreSQL
devel - ALTER LANGUAGE")

Unsupported versions: [12](/docs/12/sql-alterlanguage.html "PostgreSQL 12 -
ALTER LANGUAGE") / [11](/docs/11/sql-alterlanguage.html "PostgreSQL 11 - ALTER
LANGUAGE") / [10](/docs/10/sql-alterlanguage.html "PostgreSQL 10 - ALTER
LANGUAGE") / [9.6](/docs/9.6/sql-alterlanguage.html "PostgreSQL 9.6 - ALTER
LANGUAGE") / [9.5](/docs/9.5/sql-alterlanguage.html "PostgreSQL 9.5 - ALTER
LANGUAGE") / [9.4](/docs/9.4/sql-alterlanguage.html "PostgreSQL 9.4 - ALTER
LANGUAGE") / [9.3](/docs/9.3/sql-alterlanguage.html "PostgreSQL 9.3 - ALTER
LANGUAGE") / [9.2](/docs/9.2/sql-alterlanguage.html "PostgreSQL 9.2 - ALTER
LANGUAGE") / [9.1](/docs/9.1/sql-alterlanguage.html "PostgreSQL 9.1 - ALTER
LANGUAGE") / [9.0](/docs/9.0/sql-alterlanguage.html "PostgreSQL 9.0 - ALTER
LANGUAGE") / [8.4](/docs/8.4/sql-alterlanguage.html "PostgreSQL 8.4 - ALTER
LANGUAGE") / [8.3](/docs/8.3/sql-alterlanguage.html "PostgreSQL 8.3 - ALTER
LANGUAGE") / [8.2](/docs/8.2/sql-alterlanguage.html "PostgreSQL 8.2 - ALTER
LANGUAGE") / [8.1](/docs/8.1/sql-alterlanguage.html "PostgreSQL 8.1 - ALTER
LANGUAGE") / [8.0](/docs/8.0/sql-alterlanguage.html "PostgreSQL 8.0 - ALTER
LANGUAGE") / [7.4](/docs/7.4/sql-alterlanguage.html "PostgreSQL 7.4 - ALTER
LANGUAGE")

__

ALTER LANGUAGE  
---  
[Prev](sql-alterindex.html "ALTER INDEX")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterlargeobject.html "ALTER LARGE OBJECT")  
  
* * *

## ALTER LANGUAGE

ALTER LANGUAGE — change the definition of a procedural language

## Synopsis

    
    
    ALTER [ PROCEDURAL ] LANGUAGE _name_ RENAME TO _new_name_
    ALTER [ PROCEDURAL ] LANGUAGE _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    

## Description

`ALTER LANGUAGE` changes the definition of a procedural language. The only
functionality is to rename the language or assign a new owner. You must be
superuser or owner of the language to use `ALTER LANGUAGE`.

## Parameters

_`name`_

    

Name of a language

_`new_name`_

    

The new name of the language

_`new_owner`_

    

The new owner of the language

## Compatibility

There is no `ALTER LANGUAGE` statement in the SQL standard.

## See Also

[CREATE LANGUAGE](sql-createlanguage.html "CREATE LANGUAGE"), [DROP
LANGUAGE](sql-droplanguage.html "DROP LANGUAGE")

* * *

[Prev](sql-alterindex.html "ALTER INDEX")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterlargeobject.html "ALTER LARGE OBJECT")  
---|---|---  
ALTER INDEX  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER LARGE OBJECT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterlanguage.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

