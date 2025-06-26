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

Supported Versions: [Current](/docs/current/sql-droptype.html "PostgreSQL 17 -
DROP TYPE") ([17](/docs/17/sql-droptype.html "PostgreSQL 17 - DROP TYPE")) /
[16](/docs/16/sql-droptype.html "PostgreSQL 16 - DROP TYPE") /
[15](/docs/15/sql-droptype.html "PostgreSQL 15 - DROP TYPE") /
[14](/docs/14/sql-droptype.html "PostgreSQL 14 - DROP TYPE") /
[13](/docs/13/sql-droptype.html "PostgreSQL 13 - DROP TYPE")

Development Versions: [18](/docs/18/sql-droptype.html "PostgreSQL 18 - DROP
TYPE") / [devel](/docs/devel/sql-droptype.html "PostgreSQL devel - DROP TYPE")

Unsupported versions: [12](/docs/12/sql-droptype.html "PostgreSQL 12 - DROP
TYPE") / [11](/docs/11/sql-droptype.html "PostgreSQL 11 - DROP TYPE") /
[10](/docs/10/sql-droptype.html "PostgreSQL 10 - DROP TYPE") /
[9.6](/docs/9.6/sql-droptype.html "PostgreSQL 9.6 - DROP TYPE") /
[9.5](/docs/9.5/sql-droptype.html "PostgreSQL 9.5 - DROP TYPE") /
[9.4](/docs/9.4/sql-droptype.html "PostgreSQL 9.4 - DROP TYPE") /
[9.3](/docs/9.3/sql-droptype.html "PostgreSQL 9.3 - DROP TYPE") /
[9.2](/docs/9.2/sql-droptype.html "PostgreSQL 9.2 - DROP TYPE") /
[9.1](/docs/9.1/sql-droptype.html "PostgreSQL 9.1 - DROP TYPE") /
[9.0](/docs/9.0/sql-droptype.html "PostgreSQL 9.0 - DROP TYPE") /
[8.4](/docs/8.4/sql-droptype.html "PostgreSQL 8.4 - DROP TYPE") /
[8.3](/docs/8.3/sql-droptype.html "PostgreSQL 8.3 - DROP TYPE") /
[8.2](/docs/8.2/sql-droptype.html "PostgreSQL 8.2 - DROP TYPE") /
[8.1](/docs/8.1/sql-droptype.html "PostgreSQL 8.1 - DROP TYPE") /
[8.0](/docs/8.0/sql-droptype.html "PostgreSQL 8.0 - DROP TYPE") /
[7.4](/docs/7.4/sql-droptype.html "PostgreSQL 7.4 - DROP TYPE") /
[7.3](/docs/7.3/sql-droptype.html "PostgreSQL 7.3 - DROP TYPE") /
[7.2](/docs/7.2/sql-droptype.html "PostgreSQL 7.2 - DROP TYPE") /
[7.1](/docs/7.1/sql-droptype.html "PostgreSQL 7.1 - DROP TYPE")

__

DROP TYPE  
---  
[Prev](sql-droptrigger.html "DROP TRIGGER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropuser.html "DROP USER")  
  
* * *

## DROP TYPE

DROP TYPE — remove a data type

## Synopsis

    
    
    DROP TYPE [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP TYPE` removes a user-defined data type. Only the owner of a type can
remove it.

## Parameters

`IF EXISTS`

    

Do not throw an error if the type does not exist. A notice is issued in this
case.

_`name`_

    

The name (optionally schema-qualified) of the data type to remove.

`CASCADE`

    

Automatically drop objects that depend on the type (such as table columns,
functions, and operators), and in turn all objects that depend on those
objects (see [Section 5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the type if any objects depend on it. This is the default.

## Examples

To remove the data type `box`:

    
    
    DROP TYPE box;
    

## Compatibility

This command is similar to the corresponding command in the SQL standard,
apart from the `IF EXISTS` option, which is a PostgreSQL extension. But note
that much of the `CREATE TYPE` command and the data type extension mechanisms
in PostgreSQL differ from the SQL standard.

## See Also

[ALTER TYPE](sql-altertype.html "ALTER TYPE"), [CREATE TYPE](sql-
createtype.html "CREATE TYPE")

* * *

[Prev](sql-droptrigger.html "DROP TRIGGER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropuser.html "DROP USER")  
---|---|---  
DROP TRIGGER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP USER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droptype.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

