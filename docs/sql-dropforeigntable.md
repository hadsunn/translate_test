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

Supported Versions: [Current](/docs/current/sql-dropforeigntable.html
"PostgreSQL 17 - DROP FOREIGN TABLE") ([17](/docs/17/sql-dropforeigntable.html
"PostgreSQL 17 - DROP FOREIGN TABLE")) / [16](/docs/16/sql-
dropforeigntable.html "PostgreSQL 16 - DROP FOREIGN TABLE") /
[15](/docs/15/sql-dropforeigntable.html "PostgreSQL 15 - DROP FOREIGN TABLE")
/ [14](/docs/14/sql-dropforeigntable.html "PostgreSQL 14 - DROP FOREIGN
TABLE") / [13](/docs/13/sql-dropforeigntable.html "PostgreSQL 13 - DROP
FOREIGN TABLE")

Development Versions: [18](/docs/18/sql-dropforeigntable.html "PostgreSQL 18 -
DROP FOREIGN TABLE") / [devel](/docs/devel/sql-dropforeigntable.html
"PostgreSQL devel - DROP FOREIGN TABLE")

Unsupported versions: [12](/docs/12/sql-dropforeigntable.html "PostgreSQL 12 -
DROP FOREIGN TABLE") / [11](/docs/11/sql-dropforeigntable.html "PostgreSQL 11
- DROP FOREIGN TABLE") / [10](/docs/10/sql-dropforeigntable.html "PostgreSQL
10 - DROP FOREIGN TABLE") / [9.6](/docs/9.6/sql-dropforeigntable.html
"PostgreSQL 9.6 - DROP FOREIGN TABLE") / [9.5](/docs/9.5/sql-
dropforeigntable.html "PostgreSQL 9.5 - DROP FOREIGN TABLE") /
[9.4](/docs/9.4/sql-dropforeigntable.html "PostgreSQL 9.4 - DROP FOREIGN
TABLE") / [9.3](/docs/9.3/sql-dropforeigntable.html "PostgreSQL 9.3 - DROP
FOREIGN TABLE") / [9.2](/docs/9.2/sql-dropforeigntable.html "PostgreSQL 9.2 -
DROP FOREIGN TABLE") / [9.1](/docs/9.1/sql-dropforeigntable.html "PostgreSQL
9.1 - DROP FOREIGN TABLE")

__

DROP FOREIGN TABLE  
---  
[Prev](sql-dropforeigndatawrapper.html "DROP FOREIGN DATA WRAPPER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropfunction.html "DROP FUNCTION")  
  
* * *

## DROP FOREIGN TABLE

DROP FOREIGN TABLE — remove a foreign table

## Synopsis

    
    
    DROP FOREIGN TABLE [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP FOREIGN TABLE` removes a foreign table. Only the owner of a foreign
table can remove it.

## Parameters

`IF EXISTS`

    

Do not throw an error if the foreign table does not exist. A notice is issued
in this case.

_`name`_

    

The name (optionally schema-qualified) of the foreign table to drop.

`CASCADE`

    

Automatically drop objects that depend on the foreign table (such as views),
and in turn all objects that depend on those objects (see [Section 5.14](ddl-
depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the foreign table if any objects depend on it. This is the
default.

## Examples

To destroy two foreign tables, `films` and `distributors`:

    
    
    DROP FOREIGN TABLE films, distributors;
    

## Compatibility

This command conforms to ISO/IEC 9075-9 (SQL/MED), except that the standard
only allows one foreign table to be dropped per command, and apart from the
`IF EXISTS` option, which is a PostgreSQL extension.

## See Also

[ALTER FOREIGN TABLE](sql-alterforeigntable.html "ALTER FOREIGN TABLE"),
[CREATE FOREIGN TABLE](sql-createforeigntable.html "CREATE FOREIGN TABLE")

* * *

[Prev](sql-dropforeigndatawrapper.html "DROP FOREIGN DATA WRAPPER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropfunction.html "DROP FUNCTION")  
---|---|---  
DROP FOREIGN DATA WRAPPER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP FUNCTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropforeigntable.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

