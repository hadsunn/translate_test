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

Supported Versions: [Current](/docs/current/sql-dropschema.html "PostgreSQL 17
- DROP SCHEMA") ([17](/docs/17/sql-dropschema.html "PostgreSQL 17 - DROP
SCHEMA")) / [16](/docs/16/sql-dropschema.html "PostgreSQL 16 - DROP SCHEMA") /
[15](/docs/15/sql-dropschema.html "PostgreSQL 15 - DROP SCHEMA") /
[14](/docs/14/sql-dropschema.html "PostgreSQL 14 - DROP SCHEMA") /
[13](/docs/13/sql-dropschema.html "PostgreSQL 13 - DROP SCHEMA")

Development Versions: [18](/docs/18/sql-dropschema.html "PostgreSQL 18 - DROP
SCHEMA") / [devel](/docs/devel/sql-dropschema.html "PostgreSQL devel - DROP
SCHEMA")

Unsupported versions: [12](/docs/12/sql-dropschema.html "PostgreSQL 12 - DROP
SCHEMA") / [11](/docs/11/sql-dropschema.html "PostgreSQL 11 - DROP SCHEMA") /
[10](/docs/10/sql-dropschema.html "PostgreSQL 10 - DROP SCHEMA") /
[9.6](/docs/9.6/sql-dropschema.html "PostgreSQL 9.6 - DROP SCHEMA") /
[9.5](/docs/9.5/sql-dropschema.html "PostgreSQL 9.5 - DROP SCHEMA") /
[9.4](/docs/9.4/sql-dropschema.html "PostgreSQL 9.4 - DROP SCHEMA") /
[9.3](/docs/9.3/sql-dropschema.html "PostgreSQL 9.3 - DROP SCHEMA") /
[9.2](/docs/9.2/sql-dropschema.html "PostgreSQL 9.2 - DROP SCHEMA") /
[9.1](/docs/9.1/sql-dropschema.html "PostgreSQL 9.1 - DROP SCHEMA") /
[9.0](/docs/9.0/sql-dropschema.html "PostgreSQL 9.0 - DROP SCHEMA") /
[8.4](/docs/8.4/sql-dropschema.html "PostgreSQL 8.4 - DROP SCHEMA") /
[8.3](/docs/8.3/sql-dropschema.html "PostgreSQL 8.3 - DROP SCHEMA") /
[8.2](/docs/8.2/sql-dropschema.html "PostgreSQL 8.2 - DROP SCHEMA") /
[8.1](/docs/8.1/sql-dropschema.html "PostgreSQL 8.1 - DROP SCHEMA") /
[8.0](/docs/8.0/sql-dropschema.html "PostgreSQL 8.0 - DROP SCHEMA") /
[7.4](/docs/7.4/sql-dropschema.html "PostgreSQL 7.4 - DROP SCHEMA") /
[7.3](/docs/7.3/sql-dropschema.html "PostgreSQL 7.3 - DROP SCHEMA")

__

DROP SCHEMA  
---  
[Prev](sql-droprule.html "DROP RULE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropsequence.html "DROP SEQUENCE")  
  
* * *

## DROP SCHEMA

DROP SCHEMA — remove a schema

## Synopsis

    
    
    DROP SCHEMA [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP SCHEMA` removes schemas from the database.

A schema can only be dropped by its owner or a superuser. Note that the owner
can drop the schema (and thereby all contained objects) even if they do not
own some of the objects within the schema.

## Parameters

`IF EXISTS`

    

Do not throw an error if the schema does not exist. A notice is issued in this
case.

_`name`_

    

The name of a schema.

`CASCADE`

    

Automatically drop objects (tables, functions, etc.) that are contained in the
schema, and in turn all objects that depend on those objects (see [Section
5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the schema if it contains any objects. This is the default.

## Notes

Using the `CASCADE` option might make the command remove objects in other
schemas besides the one(s) named.

## Examples

To remove schema `mystuff` from the database, along with everything it
contains:

    
    
    DROP SCHEMA mystuff CASCADE;
    

## Compatibility

`DROP SCHEMA` is fully conforming with the SQL standard, except that the
standard only allows one schema to be dropped per command, and apart from the
`IF EXISTS` option, which is a PostgreSQL extension.

## See Also

[ALTER SCHEMA](sql-alterschema.html "ALTER SCHEMA"), [CREATE SCHEMA](sql-
createschema.html "CREATE SCHEMA")

* * *

[Prev](sql-droprule.html "DROP RULE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropsequence.html "DROP SEQUENCE")  
---|---|---  
DROP RULE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP SEQUENCE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropschema.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

