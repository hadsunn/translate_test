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

Supported Versions: [Current](/docs/current/sql-dropconversion.html
"PostgreSQL 17 - DROP CONVERSION") ([17](/docs/17/sql-dropconversion.html
"PostgreSQL 17 - DROP CONVERSION")) / [16](/docs/16/sql-dropconversion.html
"PostgreSQL 16 - DROP CONVERSION") / [15](/docs/15/sql-dropconversion.html
"PostgreSQL 15 - DROP CONVERSION") / [14](/docs/14/sql-dropconversion.html
"PostgreSQL 14 - DROP CONVERSION") / [13](/docs/13/sql-dropconversion.html
"PostgreSQL 13 - DROP CONVERSION")

Development Versions: [18](/docs/18/sql-dropconversion.html "PostgreSQL 18 -
DROP CONVERSION") / [devel](/docs/devel/sql-dropconversion.html "PostgreSQL
devel - DROP CONVERSION")

Unsupported versions: [12](/docs/12/sql-dropconversion.html "PostgreSQL 12 -
DROP CONVERSION") / [11](/docs/11/sql-dropconversion.html "PostgreSQL 11 -
DROP CONVERSION") / [10](/docs/10/sql-dropconversion.html "PostgreSQL 10 -
DROP CONVERSION") / [9.6](/docs/9.6/sql-dropconversion.html "PostgreSQL 9.6 -
DROP CONVERSION") / [9.5](/docs/9.5/sql-dropconversion.html "PostgreSQL 9.5 -
DROP CONVERSION") / [9.4](/docs/9.4/sql-dropconversion.html "PostgreSQL 9.4 -
DROP CONVERSION") / [9.3](/docs/9.3/sql-dropconversion.html "PostgreSQL 9.3 -
DROP CONVERSION") / [9.2](/docs/9.2/sql-dropconversion.html "PostgreSQL 9.2 -
DROP CONVERSION") / [9.1](/docs/9.1/sql-dropconversion.html "PostgreSQL 9.1 -
DROP CONVERSION") / [9.0](/docs/9.0/sql-dropconversion.html "PostgreSQL 9.0 -
DROP CONVERSION") / [8.4](/docs/8.4/sql-dropconversion.html "PostgreSQL 8.4 -
DROP CONVERSION") / [8.3](/docs/8.3/sql-dropconversion.html "PostgreSQL 8.3 -
DROP CONVERSION") / [8.2](/docs/8.2/sql-dropconversion.html "PostgreSQL 8.2 -
DROP CONVERSION") / [8.1](/docs/8.1/sql-dropconversion.html "PostgreSQL 8.1 -
DROP CONVERSION") / [8.0](/docs/8.0/sql-dropconversion.html "PostgreSQL 8.0 -
DROP CONVERSION") / [7.4](/docs/7.4/sql-dropconversion.html "PostgreSQL 7.4 -
DROP CONVERSION") / [7.3](/docs/7.3/sql-dropconversion.html "PostgreSQL 7.3 -
DROP CONVERSION")

__

DROP CONVERSION  
---  
[Prev](sql-dropcollation.html "DROP COLLATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropdatabase.html "DROP DATABASE")  
  
* * *

## DROP CONVERSION

DROP CONVERSION — remove a conversion

## Synopsis

    
    
    DROP CONVERSION [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP CONVERSION` removes a previously defined conversion. To be able to drop
a conversion, you must own the conversion.

## Parameters

`IF EXISTS`

    

Do not throw an error if the conversion does not exist. A notice is issued in
this case.

_`name`_

    

The name of the conversion. The conversion name can be schema-qualified.

`CASCADE`  
`RESTRICT`

    

These key words do not have any effect, since there are no dependencies on
conversions.

## Examples

To drop the conversion named `myname`:

    
    
    DROP CONVERSION myname;
    

## Compatibility

There is no `DROP CONVERSION` statement in the SQL standard, but a `DROP
TRANSLATION` statement that goes along with the `CREATE TRANSLATION` statement
that is similar to the `CREATE CONVERSION` statement in PostgreSQL.

## See Also

[ALTER CONVERSION](sql-alterconversion.html "ALTER CONVERSION"), [CREATE
CONVERSION](sql-createconversion.html "CREATE CONVERSION")

* * *

[Prev](sql-dropcollation.html "DROP COLLATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropdatabase.html "DROP DATABASE")  
---|---|---  
DROP COLLATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP DATABASE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropconversion.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

