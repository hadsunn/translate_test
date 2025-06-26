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

Supported Versions: [Current](/docs/current/sql-dropserver.html "PostgreSQL 17
- DROP SERVER") ([17](/docs/17/sql-dropserver.html "PostgreSQL 17 - DROP
SERVER")) / [16](/docs/16/sql-dropserver.html "PostgreSQL 16 - DROP SERVER") /
[15](/docs/15/sql-dropserver.html "PostgreSQL 15 - DROP SERVER") /
[14](/docs/14/sql-dropserver.html "PostgreSQL 14 - DROP SERVER") /
[13](/docs/13/sql-dropserver.html "PostgreSQL 13 - DROP SERVER")

Development Versions: [18](/docs/18/sql-dropserver.html "PostgreSQL 18 - DROP
SERVER") / [devel](/docs/devel/sql-dropserver.html "PostgreSQL devel - DROP
SERVER")

Unsupported versions: [12](/docs/12/sql-dropserver.html "PostgreSQL 12 - DROP
SERVER") / [11](/docs/11/sql-dropserver.html "PostgreSQL 11 - DROP SERVER") /
[10](/docs/10/sql-dropserver.html "PostgreSQL 10 - DROP SERVER") /
[9.6](/docs/9.6/sql-dropserver.html "PostgreSQL 9.6 - DROP SERVER") /
[9.5](/docs/9.5/sql-dropserver.html "PostgreSQL 9.5 - DROP SERVER") /
[9.4](/docs/9.4/sql-dropserver.html "PostgreSQL 9.4 - DROP SERVER") /
[9.3](/docs/9.3/sql-dropserver.html "PostgreSQL 9.3 - DROP SERVER") /
[9.2](/docs/9.2/sql-dropserver.html "PostgreSQL 9.2 - DROP SERVER") /
[9.1](/docs/9.1/sql-dropserver.html "PostgreSQL 9.1 - DROP SERVER") /
[9.0](/docs/9.0/sql-dropserver.html "PostgreSQL 9.0 - DROP SERVER") /
[8.4](/docs/8.4/sql-dropserver.html "PostgreSQL 8.4 - DROP SERVER")

__

DROP SERVER  
---  
[Prev](sql-dropsequence.html "DROP SEQUENCE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropstatistics.html "DROP STATISTICS")  
  
* * *

## DROP SERVER

DROP SERVER — remove a foreign server descriptor

## Synopsis

    
    
    DROP SERVER [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP SERVER` removes an existing foreign server descriptor. To execute this
command, the current user must be the owner of the server.

## Parameters

`IF EXISTS`

    

Do not throw an error if the server does not exist. A notice is issued in this
case.

_`name`_

    

The name of an existing server.

`CASCADE`

    

Automatically drop objects that depend on the server (such as user mappings),
and in turn all objects that depend on those objects (see [Section 5.14](ddl-
depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the server if any objects depend on it. This is the default.

## Examples

Drop a server `foo` if it exists:

    
    
    DROP SERVER IF EXISTS foo;
    

## Compatibility

`DROP SERVER` conforms to ISO/IEC 9075-9 (SQL/MED). The `IF EXISTS` clause is
a PostgreSQL extension.

## See Also

[CREATE SERVER](sql-createserver.html "CREATE SERVER"), [ALTER SERVER](sql-
alterserver.html "ALTER SERVER")

* * *

[Prev](sql-dropsequence.html "DROP SEQUENCE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropstatistics.html "DROP STATISTICS")  
---|---|---  
DROP SEQUENCE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP STATISTICS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropserver.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

