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

Supported Versions: [Current](/docs/current/sql-droptablespace.html
"PostgreSQL 17 - DROP TABLESPACE") ([17](/docs/17/sql-droptablespace.html
"PostgreSQL 17 - DROP TABLESPACE")) / [16](/docs/16/sql-droptablespace.html
"PostgreSQL 16 - DROP TABLESPACE") / [15](/docs/15/sql-droptablespace.html
"PostgreSQL 15 - DROP TABLESPACE") / [14](/docs/14/sql-droptablespace.html
"PostgreSQL 14 - DROP TABLESPACE") / [13](/docs/13/sql-droptablespace.html
"PostgreSQL 13 - DROP TABLESPACE")

Development Versions: [18](/docs/18/sql-droptablespace.html "PostgreSQL 18 -
DROP TABLESPACE") / [devel](/docs/devel/sql-droptablespace.html "PostgreSQL
devel - DROP TABLESPACE")

Unsupported versions: [12](/docs/12/sql-droptablespace.html "PostgreSQL 12 -
DROP TABLESPACE") / [11](/docs/11/sql-droptablespace.html "PostgreSQL 11 -
DROP TABLESPACE") / [10](/docs/10/sql-droptablespace.html "PostgreSQL 10 -
DROP TABLESPACE") / [9.6](/docs/9.6/sql-droptablespace.html "PostgreSQL 9.6 -
DROP TABLESPACE") / [9.5](/docs/9.5/sql-droptablespace.html "PostgreSQL 9.5 -
DROP TABLESPACE") / [9.4](/docs/9.4/sql-droptablespace.html "PostgreSQL 9.4 -
DROP TABLESPACE") / [9.3](/docs/9.3/sql-droptablespace.html "PostgreSQL 9.3 -
DROP TABLESPACE") / [9.2](/docs/9.2/sql-droptablespace.html "PostgreSQL 9.2 -
DROP TABLESPACE") / [9.1](/docs/9.1/sql-droptablespace.html "PostgreSQL 9.1 -
DROP TABLESPACE") / [9.0](/docs/9.0/sql-droptablespace.html "PostgreSQL 9.0 -
DROP TABLESPACE") / [8.4](/docs/8.4/sql-droptablespace.html "PostgreSQL 8.4 -
DROP TABLESPACE") / [8.3](/docs/8.3/sql-droptablespace.html "PostgreSQL 8.3 -
DROP TABLESPACE") / [8.2](/docs/8.2/sql-droptablespace.html "PostgreSQL 8.2 -
DROP TABLESPACE") / [8.1](/docs/8.1/sql-droptablespace.html "PostgreSQL 8.1 -
DROP TABLESPACE") / [8.0](/docs/8.0/sql-droptablespace.html "PostgreSQL 8.0 -
DROP TABLESPACE")

__

DROP TABLESPACE  
---  
[Prev](sql-droptable.html "DROP TABLE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droptsconfig.html "DROP TEXT SEARCH CONFIGURATION")  
  
* * *

## DROP TABLESPACE

DROP TABLESPACE — remove a tablespace

## Synopsis

    
    
    DROP TABLESPACE [ IF EXISTS ] _name_
    

## Description

`DROP TABLESPACE` removes a tablespace from the system.

A tablespace can only be dropped by its owner or a superuser. The tablespace
must be empty of all database objects before it can be dropped. It is possible
that objects in other databases might still reside in the tablespace even if
no objects in the current database are using the tablespace. Also, if the
tablespace is listed in the [temp_tablespaces](runtime-config-client.html#GUC-
TEMP-TABLESPACES) setting of any active session, the `DROP` might fail due to
temporary files residing in the tablespace.

## Parameters

`IF EXISTS`

    

Do not throw an error if the tablespace does not exist. A notice is issued in
this case.

_`name`_

    

The name of a tablespace.

## Notes

`DROP TABLESPACE` cannot be executed inside a transaction block.

## Examples

To remove tablespace `mystuff` from the system:

    
    
    DROP TABLESPACE mystuff;
    

## Compatibility

`DROP TABLESPACE` is a PostgreSQL extension.

## See Also

[CREATE TABLESPACE](sql-createtablespace.html "CREATE TABLESPACE"), [ALTER
TABLESPACE](sql-altertablespace.html "ALTER TABLESPACE")

* * *

[Prev](sql-droptable.html "DROP TABLE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droptsconfig.html "DROP TEXT SEARCH CONFIGURATION")  
---|---|---  
DROP TABLE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP TEXT SEARCH CONFIGURATION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droptablespace.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

