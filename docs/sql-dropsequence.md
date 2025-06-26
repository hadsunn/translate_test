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

Supported Versions: [Current](/docs/current/sql-dropsequence.html "PostgreSQL
17 - DROP SEQUENCE") ([17](/docs/17/sql-dropsequence.html "PostgreSQL 17 -
DROP SEQUENCE")) / [16](/docs/16/sql-dropsequence.html "PostgreSQL 16 - DROP
SEQUENCE") / [15](/docs/15/sql-dropsequence.html "PostgreSQL 15 - DROP
SEQUENCE") / [14](/docs/14/sql-dropsequence.html "PostgreSQL 14 - DROP
SEQUENCE") / [13](/docs/13/sql-dropsequence.html "PostgreSQL 13 - DROP
SEQUENCE")

Development Versions: [18](/docs/18/sql-dropsequence.html "PostgreSQL 18 -
DROP SEQUENCE") / [devel](/docs/devel/sql-dropsequence.html "PostgreSQL devel
- DROP SEQUENCE")

Unsupported versions: [12](/docs/12/sql-dropsequence.html "PostgreSQL 12 -
DROP SEQUENCE") / [11](/docs/11/sql-dropsequence.html "PostgreSQL 11 - DROP
SEQUENCE") / [10](/docs/10/sql-dropsequence.html "PostgreSQL 10 - DROP
SEQUENCE") / [9.6](/docs/9.6/sql-dropsequence.html "PostgreSQL 9.6 - DROP
SEQUENCE") / [9.5](/docs/9.5/sql-dropsequence.html "PostgreSQL 9.5 - DROP
SEQUENCE") / [9.4](/docs/9.4/sql-dropsequence.html "PostgreSQL 9.4 - DROP
SEQUENCE") / [9.3](/docs/9.3/sql-dropsequence.html "PostgreSQL 9.3 - DROP
SEQUENCE") / [9.2](/docs/9.2/sql-dropsequence.html "PostgreSQL 9.2 - DROP
SEQUENCE") / [9.1](/docs/9.1/sql-dropsequence.html "PostgreSQL 9.1 - DROP
SEQUENCE") / [9.0](/docs/9.0/sql-dropsequence.html "PostgreSQL 9.0 - DROP
SEQUENCE") / [8.4](/docs/8.4/sql-dropsequence.html "PostgreSQL 8.4 - DROP
SEQUENCE") / [8.3](/docs/8.3/sql-dropsequence.html "PostgreSQL 8.3 - DROP
SEQUENCE") / [8.2](/docs/8.2/sql-dropsequence.html "PostgreSQL 8.2 - DROP
SEQUENCE") / [8.1](/docs/8.1/sql-dropsequence.html "PostgreSQL 8.1 - DROP
SEQUENCE") / [8.0](/docs/8.0/sql-dropsequence.html "PostgreSQL 8.0 - DROP
SEQUENCE") / [7.4](/docs/7.4/sql-dropsequence.html "PostgreSQL 7.4 - DROP
SEQUENCE") / [7.3](/docs/7.3/sql-dropsequence.html "PostgreSQL 7.3 - DROP
SEQUENCE") / [7.2](/docs/7.2/sql-dropsequence.html "PostgreSQL 7.2 - DROP
SEQUENCE") / [7.1](/docs/7.1/sql-dropsequence.html "PostgreSQL 7.1 - DROP
SEQUENCE")

__

DROP SEQUENCE  
---  
[Prev](sql-dropschema.html "DROP SCHEMA")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropserver.html "DROP SERVER")  
  
* * *

## DROP SEQUENCE

DROP SEQUENCE — remove a sequence

## Synopsis

    
    
    DROP SEQUENCE [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP SEQUENCE` removes sequence number generators. A sequence can only be
dropped by its owner or a superuser.

## Parameters

`IF EXISTS`

    

Do not throw an error if the sequence does not exist. A notice is issued in
this case.

_`name`_

    

The name (optionally schema-qualified) of a sequence.

`CASCADE`

    

Automatically drop objects that depend on the sequence, and in turn all
objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the sequence if any objects depend on it. This is the default.

## Examples

To remove the sequence `serial`:

    
    
    DROP SEQUENCE serial;
    

## Compatibility

`DROP SEQUENCE` conforms to the SQL standard, except that the standard only
allows one sequence to be dropped per command, and apart from the `IF EXISTS`
option, which is a PostgreSQL extension.

## See Also

[CREATE SEQUENCE](sql-createsequence.html "CREATE SEQUENCE"), [ALTER
SEQUENCE](sql-altersequence.html "ALTER SEQUENCE")

* * *

[Prev](sql-dropschema.html "DROP SCHEMA")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropserver.html "DROP SERVER")  
---|---|---  
DROP SCHEMA  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP SERVER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropsequence.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

