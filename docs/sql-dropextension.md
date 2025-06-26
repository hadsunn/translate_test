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

Supported Versions: [Current](/docs/current/sql-dropextension.html "PostgreSQL
17 - DROP EXTENSION") ([17](/docs/17/sql-dropextension.html "PostgreSQL 17 -
DROP EXTENSION")) / [16](/docs/16/sql-dropextension.html "PostgreSQL 16 - DROP
EXTENSION") / [15](/docs/15/sql-dropextension.html "PostgreSQL 15 - DROP
EXTENSION") / [14](/docs/14/sql-dropextension.html "PostgreSQL 14 - DROP
EXTENSION") / [13](/docs/13/sql-dropextension.html "PostgreSQL 13 - DROP
EXTENSION")

Development Versions: [18](/docs/18/sql-dropextension.html "PostgreSQL 18 -
DROP EXTENSION") / [devel](/docs/devel/sql-dropextension.html "PostgreSQL
devel - DROP EXTENSION")

Unsupported versions: [12](/docs/12/sql-dropextension.html "PostgreSQL 12 -
DROP EXTENSION") / [11](/docs/11/sql-dropextension.html "PostgreSQL 11 - DROP
EXTENSION") / [10](/docs/10/sql-dropextension.html "PostgreSQL 10 - DROP
EXTENSION") / [9.6](/docs/9.6/sql-dropextension.html "PostgreSQL 9.6 - DROP
EXTENSION") / [9.5](/docs/9.5/sql-dropextension.html "PostgreSQL 9.5 - DROP
EXTENSION") / [9.4](/docs/9.4/sql-dropextension.html "PostgreSQL 9.4 - DROP
EXTENSION") / [9.3](/docs/9.3/sql-dropextension.html "PostgreSQL 9.3 - DROP
EXTENSION") / [9.2](/docs/9.2/sql-dropextension.html "PostgreSQL 9.2 - DROP
EXTENSION") / [9.1](/docs/9.1/sql-dropextension.html "PostgreSQL 9.1 - DROP
EXTENSION")

__

DROP EXTENSION  
---  
[Prev](sql-dropeventtrigger.html "DROP EVENT TRIGGER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropforeigndatawrapper.html "DROP FOREIGN DATA WRAPPER")  
  
* * *

## DROP EXTENSION

DROP EXTENSION — remove an extension

## Synopsis

    
    
    DROP EXTENSION [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP EXTENSION` removes extensions from the database. Dropping an extension
causes its member objects, and other explicitly dependent routines (see [ALTER
ROUTINE](sql-alterroutine.html "ALTER ROUTINE"), the `DEPENDS ON EXTENSION
_`extension_name`_` action), to be dropped as well.

You must own the extension to use `DROP EXTENSION`.

## Parameters

`IF EXISTS`

    

Do not throw an error if the extension does not exist. A notice is issued in
this case.

_`name`_

    

The name of an installed extension.

`CASCADE`

    

Automatically drop objects that depend on the extension, and in turn all
objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

This option prevents the specified extensions from being dropped if other
objects, besides these extensions, their members, and their explicitly
dependent routines, depend on them. This is the default.

## Examples

To remove the extension `hstore` from the current database:

    
    
    DROP EXTENSION hstore;
    

This command will fail if any of `hstore`'s objects are in use in the
database, for example if any tables have columns of the `hstore` type. Add the
`CASCADE` option to forcibly remove those dependent objects as well.

## Compatibility

`DROP EXTENSION` is a PostgreSQL extension.

## See Also

[CREATE EXTENSION](sql-createextension.html "CREATE EXTENSION"), [ALTER
EXTENSION](sql-alterextension.html "ALTER EXTENSION")

* * *

[Prev](sql-dropeventtrigger.html "DROP EVENT TRIGGER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropforeigndatawrapper.html "DROP FOREIGN DATA WRAPPER")  
---|---|---  
DROP EVENT TRIGGER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP FOREIGN DATA WRAPPER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropextension.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

