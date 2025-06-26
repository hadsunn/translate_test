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

Supported Versions: [Current](/docs/current/sql-dropforeigndatawrapper.html
"PostgreSQL 17 - DROP FOREIGN DATA WRAPPER") ([17](/docs/17/sql-
dropforeigndatawrapper.html "PostgreSQL 17 - DROP FOREIGN DATA WRAPPER")) /
[16](/docs/16/sql-dropforeigndatawrapper.html "PostgreSQL 16 - DROP FOREIGN
DATA WRAPPER") / [15](/docs/15/sql-dropforeigndatawrapper.html "PostgreSQL 15
- DROP FOREIGN DATA WRAPPER") / [14](/docs/14/sql-dropforeigndatawrapper.html
"PostgreSQL 14 - DROP FOREIGN DATA WRAPPER") / [13](/docs/13/sql-
dropforeigndatawrapper.html "PostgreSQL 13 - DROP FOREIGN DATA WRAPPER")

Development Versions: [18](/docs/18/sql-dropforeigndatawrapper.html
"PostgreSQL 18 - DROP FOREIGN DATA WRAPPER") / [devel](/docs/devel/sql-
dropforeigndatawrapper.html "PostgreSQL devel - DROP FOREIGN DATA WRAPPER")

Unsupported versions: [12](/docs/12/sql-dropforeigndatawrapper.html
"PostgreSQL 12 - DROP FOREIGN DATA WRAPPER") / [11](/docs/11/sql-
dropforeigndatawrapper.html "PostgreSQL 11 - DROP FOREIGN DATA WRAPPER") /
[10](/docs/10/sql-dropforeigndatawrapper.html "PostgreSQL 10 - DROP FOREIGN
DATA WRAPPER") / [9.6](/docs/9.6/sql-dropforeigndatawrapper.html "PostgreSQL
9.6 - DROP FOREIGN DATA WRAPPER") / [9.5](/docs/9.5/sql-
dropforeigndatawrapper.html "PostgreSQL 9.5 - DROP FOREIGN DATA WRAPPER") /
[9.4](/docs/9.4/sql-dropforeigndatawrapper.html "PostgreSQL 9.4 - DROP FOREIGN
DATA WRAPPER") / [9.3](/docs/9.3/sql-dropforeigndatawrapper.html "PostgreSQL
9.3 - DROP FOREIGN DATA WRAPPER") / [9.2](/docs/9.2/sql-
dropforeigndatawrapper.html "PostgreSQL 9.2 - DROP FOREIGN DATA WRAPPER") /
[9.1](/docs/9.1/sql-dropforeigndatawrapper.html "PostgreSQL 9.1 - DROP FOREIGN
DATA WRAPPER") / [9.0](/docs/9.0/sql-dropforeigndatawrapper.html "PostgreSQL
9.0 - DROP FOREIGN DATA WRAPPER") / [8.4](/docs/8.4/sql-
dropforeigndatawrapper.html "PostgreSQL 8.4 - DROP FOREIGN DATA WRAPPER")

__

DROP FOREIGN DATA WRAPPER  
---  
[Prev](sql-dropextension.html "DROP EXTENSION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropforeigntable.html "DROP FOREIGN TABLE")  
  
* * *

## DROP FOREIGN DATA WRAPPER

DROP FOREIGN DATA WRAPPER — remove a foreign-data wrapper

## Synopsis

    
    
    DROP FOREIGN DATA WRAPPER [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP FOREIGN DATA WRAPPER` removes an existing foreign-data wrapper. To
execute this command, the current user must be the owner of the foreign-data
wrapper.

## Parameters

`IF EXISTS`

    

Do not throw an error if the foreign-data wrapper does not exist. A notice is
issued in this case.

_`name`_

    

The name of an existing foreign-data wrapper.

`CASCADE`

    

Automatically drop objects that depend on the foreign-data wrapper (such as
foreign tables and servers), and in turn all objects that depend on those
objects (see [Section 5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the foreign-data wrapper if any objects depend on it. This is
the default.

## Examples

Drop the foreign-data wrapper `dbi`:

    
    
    DROP FOREIGN DATA WRAPPER dbi;
    

## Compatibility

`DROP FOREIGN DATA WRAPPER` conforms to ISO/IEC 9075-9 (SQL/MED). The `IF
EXISTS` clause is a PostgreSQL extension.

## See Also

[CREATE FOREIGN DATA WRAPPER](sql-createforeigndatawrapper.html "CREATE
FOREIGN DATA WRAPPER"), [ALTER FOREIGN DATA WRAPPER](sql-
alterforeigndatawrapper.html "ALTER FOREIGN DATA WRAPPER")

* * *

[Prev](sql-dropextension.html "DROP EXTENSION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropforeigntable.html "DROP FOREIGN TABLE")  
---|---|---  
DROP EXTENSION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP FOREIGN TABLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
dropforeigndatawrapper.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

