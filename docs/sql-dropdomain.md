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

Supported Versions: [Current](/docs/current/sql-dropdomain.html "PostgreSQL 17
- DROP DOMAIN") ([17](/docs/17/sql-dropdomain.html "PostgreSQL 17 - DROP
DOMAIN")) / [16](/docs/16/sql-dropdomain.html "PostgreSQL 16 - DROP DOMAIN") /
[15](/docs/15/sql-dropdomain.html "PostgreSQL 15 - DROP DOMAIN") /
[14](/docs/14/sql-dropdomain.html "PostgreSQL 14 - DROP DOMAIN") /
[13](/docs/13/sql-dropdomain.html "PostgreSQL 13 - DROP DOMAIN")

Development Versions: [18](/docs/18/sql-dropdomain.html "PostgreSQL 18 - DROP
DOMAIN") / [devel](/docs/devel/sql-dropdomain.html "PostgreSQL devel - DROP
DOMAIN")

Unsupported versions: [12](/docs/12/sql-dropdomain.html "PostgreSQL 12 - DROP
DOMAIN") / [11](/docs/11/sql-dropdomain.html "PostgreSQL 11 - DROP DOMAIN") /
[10](/docs/10/sql-dropdomain.html "PostgreSQL 10 - DROP DOMAIN") /
[9.6](/docs/9.6/sql-dropdomain.html "PostgreSQL 9.6 - DROP DOMAIN") /
[9.5](/docs/9.5/sql-dropdomain.html "PostgreSQL 9.5 - DROP DOMAIN") /
[9.4](/docs/9.4/sql-dropdomain.html "PostgreSQL 9.4 - DROP DOMAIN") /
[9.3](/docs/9.3/sql-dropdomain.html "PostgreSQL 9.3 - DROP DOMAIN") /
[9.2](/docs/9.2/sql-dropdomain.html "PostgreSQL 9.2 - DROP DOMAIN") /
[9.1](/docs/9.1/sql-dropdomain.html "PostgreSQL 9.1 - DROP DOMAIN") /
[9.0](/docs/9.0/sql-dropdomain.html "PostgreSQL 9.0 - DROP DOMAIN") /
[8.4](/docs/8.4/sql-dropdomain.html "PostgreSQL 8.4 - DROP DOMAIN") /
[8.3](/docs/8.3/sql-dropdomain.html "PostgreSQL 8.3 - DROP DOMAIN") /
[8.2](/docs/8.2/sql-dropdomain.html "PostgreSQL 8.2 - DROP DOMAIN") /
[8.1](/docs/8.1/sql-dropdomain.html "PostgreSQL 8.1 - DROP DOMAIN") /
[8.0](/docs/8.0/sql-dropdomain.html "PostgreSQL 8.0 - DROP DOMAIN") /
[7.4](/docs/7.4/sql-dropdomain.html "PostgreSQL 7.4 - DROP DOMAIN") /
[7.3](/docs/7.3/sql-dropdomain.html "PostgreSQL 7.3 - DROP DOMAIN")

__

DROP DOMAIN  
---  
[Prev](sql-dropdatabase.html "DROP DATABASE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropeventtrigger.html "DROP EVENT TRIGGER")  
  
* * *

## DROP DOMAIN

DROP DOMAIN — remove a domain

## Synopsis

    
    
    DROP DOMAIN [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP DOMAIN` removes a domain. Only the owner of a domain can remove it.

## Parameters

`IF EXISTS`

    

Do not throw an error if the domain does not exist. A notice is issued in this
case.

_`name`_

    

The name (optionally schema-qualified) of an existing domain.

`CASCADE`

    

Automatically drop objects that depend on the domain (such as table columns),
and in turn all objects that depend on those objects (see [Section 5.14](ddl-
depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the domain if any objects depend on it. This is the default.

## Examples

To remove the domain `box`:

    
    
    DROP DOMAIN box;
    

## Compatibility

This command conforms to the SQL standard, except for the `IF EXISTS` option,
which is a PostgreSQL extension.

## See Also

[CREATE DOMAIN](sql-createdomain.html "CREATE DOMAIN"), [ALTER DOMAIN](sql-
alterdomain.html "ALTER DOMAIN")

* * *

[Prev](sql-dropdatabase.html "DROP DATABASE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropeventtrigger.html "DROP EVENT TRIGGER")  
---|---|---  
DROP DATABASE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP EVENT TRIGGER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropdomain.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

