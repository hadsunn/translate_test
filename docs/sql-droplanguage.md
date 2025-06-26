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

Supported Versions: [Current](/docs/current/sql-droplanguage.html "PostgreSQL
17 - DROP LANGUAGE") ([17](/docs/17/sql-droplanguage.html "PostgreSQL 17 -
DROP LANGUAGE")) / [16](/docs/16/sql-droplanguage.html "PostgreSQL 16 - DROP
LANGUAGE") / [15](/docs/15/sql-droplanguage.html "PostgreSQL 15 - DROP
LANGUAGE") / [14](/docs/14/sql-droplanguage.html "PostgreSQL 14 - DROP
LANGUAGE") / [13](/docs/13/sql-droplanguage.html "PostgreSQL 13 - DROP
LANGUAGE")

Development Versions: [18](/docs/18/sql-droplanguage.html "PostgreSQL 18 -
DROP LANGUAGE") / [devel](/docs/devel/sql-droplanguage.html "PostgreSQL devel
- DROP LANGUAGE")

Unsupported versions: [12](/docs/12/sql-droplanguage.html "PostgreSQL 12 -
DROP LANGUAGE") / [11](/docs/11/sql-droplanguage.html "PostgreSQL 11 - DROP
LANGUAGE") / [10](/docs/10/sql-droplanguage.html "PostgreSQL 10 - DROP
LANGUAGE") / [9.6](/docs/9.6/sql-droplanguage.html "PostgreSQL 9.6 - DROP
LANGUAGE") / [9.5](/docs/9.5/sql-droplanguage.html "PostgreSQL 9.5 - DROP
LANGUAGE") / [9.4](/docs/9.4/sql-droplanguage.html "PostgreSQL 9.4 - DROP
LANGUAGE") / [9.3](/docs/9.3/sql-droplanguage.html "PostgreSQL 9.3 - DROP
LANGUAGE") / [9.2](/docs/9.2/sql-droplanguage.html "PostgreSQL 9.2 - DROP
LANGUAGE") / [9.1](/docs/9.1/sql-droplanguage.html "PostgreSQL 9.1 - DROP
LANGUAGE") / [9.0](/docs/9.0/sql-droplanguage.html "PostgreSQL 9.0 - DROP
LANGUAGE") / [8.4](/docs/8.4/sql-droplanguage.html "PostgreSQL 8.4 - DROP
LANGUAGE") / [8.3](/docs/8.3/sql-droplanguage.html "PostgreSQL 8.3 - DROP
LANGUAGE") / [8.2](/docs/8.2/sql-droplanguage.html "PostgreSQL 8.2 - DROP
LANGUAGE") / [8.1](/docs/8.1/sql-droplanguage.html "PostgreSQL 8.1 - DROP
LANGUAGE") / [8.0](/docs/8.0/sql-droplanguage.html "PostgreSQL 8.0 - DROP
LANGUAGE") / [7.4](/docs/7.4/sql-droplanguage.html "PostgreSQL 7.4 - DROP
LANGUAGE") / [7.3](/docs/7.3/sql-droplanguage.html "PostgreSQL 7.3 - DROP
LANGUAGE") / [7.2](/docs/7.2/sql-droplanguage.html "PostgreSQL 7.2 - DROP
LANGUAGE") / [7.1](/docs/7.1/sql-droplanguage.html "PostgreSQL 7.1 - DROP
LANGUAGE")

__

DROP LANGUAGE  
---  
[Prev](sql-dropindex.html "DROP INDEX")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropmaterializedview.html "DROP MATERIALIZED VIEW")  
  
* * *

## DROP LANGUAGE

DROP LANGUAGE — remove a procedural language

## Synopsis

    
    
    DROP [ PROCEDURAL ] LANGUAGE [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP LANGUAGE` removes the definition of a previously registered procedural
language. You must be a superuser or the owner of the language to use `DROP
LANGUAGE`.

### Note

As of PostgreSQL 9.1, most procedural languages have been made into
“extensions”, and should therefore be removed with [`DROP EXTENSION`](sql-
dropextension.html "DROP EXTENSION") not `DROP LANGUAGE`.

## Parameters

`IF EXISTS`

    

Do not throw an error if the language does not exist. A notice is issued in
this case.

_`name`_

    

The name of an existing procedural language.

`CASCADE`

    

Automatically drop objects that depend on the language (such as functions in
the language), and in turn all objects that depend on those objects (see
[Section 5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the language if any objects depend on it. This is the default.

## Examples

This command removes the procedural language `plsample`:

    
    
    DROP LANGUAGE plsample;
    

## Compatibility

There is no `DROP LANGUAGE` statement in the SQL standard.

## See Also

[ALTER LANGUAGE](sql-alterlanguage.html "ALTER LANGUAGE"), [CREATE
LANGUAGE](sql-createlanguage.html "CREATE LANGUAGE")

* * *

[Prev](sql-dropindex.html "DROP INDEX")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropmaterializedview.html "DROP MATERIALIZED VIEW")  
---|---|---  
DROP INDEX  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP MATERIALIZED VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droplanguage.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

