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

Supported Versions: [Current](/docs/current/sql-alterconversion.html
"PostgreSQL 17 - ALTER CONVERSION") ([17](/docs/17/sql-alterconversion.html
"PostgreSQL 17 - ALTER CONVERSION")) / [16](/docs/16/sql-alterconversion.html
"PostgreSQL 16 - ALTER CONVERSION") / [15](/docs/15/sql-alterconversion.html
"PostgreSQL 15 - ALTER CONVERSION") / [14](/docs/14/sql-alterconversion.html
"PostgreSQL 14 - ALTER CONVERSION") / [13](/docs/13/sql-alterconversion.html
"PostgreSQL 13 - ALTER CONVERSION")

Development Versions: [18](/docs/18/sql-alterconversion.html "PostgreSQL 18 -
ALTER CONVERSION") / [devel](/docs/devel/sql-alterconversion.html "PostgreSQL
devel - ALTER CONVERSION")

Unsupported versions: [12](/docs/12/sql-alterconversion.html "PostgreSQL 12 -
ALTER CONVERSION") / [11](/docs/11/sql-alterconversion.html "PostgreSQL 11 -
ALTER CONVERSION") / [10](/docs/10/sql-alterconversion.html "PostgreSQL 10 -
ALTER CONVERSION") / [9.6](/docs/9.6/sql-alterconversion.html "PostgreSQL 9.6
- ALTER CONVERSION") / [9.5](/docs/9.5/sql-alterconversion.html "PostgreSQL
9.5 - ALTER CONVERSION") / [9.4](/docs/9.4/sql-alterconversion.html
"PostgreSQL 9.4 - ALTER CONVERSION") / [9.3](/docs/9.3/sql-
alterconversion.html "PostgreSQL 9.3 - ALTER CONVERSION") /
[9.2](/docs/9.2/sql-alterconversion.html "PostgreSQL 9.2 - ALTER CONVERSION")
/ [9.1](/docs/9.1/sql-alterconversion.html "PostgreSQL 9.1 - ALTER
CONVERSION") / [9.0](/docs/9.0/sql-alterconversion.html "PostgreSQL 9.0 -
ALTER CONVERSION") / [8.4](/docs/8.4/sql-alterconversion.html "PostgreSQL 8.4
- ALTER CONVERSION") / [8.3](/docs/8.3/sql-alterconversion.html "PostgreSQL
8.3 - ALTER CONVERSION") / [8.2](/docs/8.2/sql-alterconversion.html
"PostgreSQL 8.2 - ALTER CONVERSION") / [8.1](/docs/8.1/sql-
alterconversion.html "PostgreSQL 8.1 - ALTER CONVERSION") /
[8.0](/docs/8.0/sql-alterconversion.html "PostgreSQL 8.0 - ALTER CONVERSION")
/ [7.4](/docs/7.4/sql-alterconversion.html "PostgreSQL 7.4 - ALTER
CONVERSION")

__

ALTER CONVERSION  
---  
[Prev](sql-altercollation.html "ALTER COLLATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterdatabase.html "ALTER DATABASE")  
  
* * *

## ALTER CONVERSION

ALTER CONVERSION — change the definition of a conversion

## Synopsis

    
    
    ALTER CONVERSION _name_ RENAME TO _new_name_
    ALTER CONVERSION _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER CONVERSION _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER CONVERSION` changes the definition of a conversion.

You must own the conversion to use `ALTER CONVERSION`. To alter the owner, you
must be able to `SET ROLE` to the new owning role, and that role must have
`CREATE` privilege on the conversion's schema. (These restrictions enforce
that altering the owner doesn't do anything you couldn't do by dropping and
recreating the conversion. However, a superuser can alter ownership of any
conversion anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing conversion.

_`new_name`_

    

The new name of the conversion.

_`new_owner`_

    

The new owner of the conversion.

_`new_schema`_

    

The new schema for the conversion.

## Examples

To rename the conversion `iso_8859_1_to_utf8` to `latin1_to_unicode`:

    
    
    ALTER CONVERSION iso_8859_1_to_utf8 RENAME TO latin1_to_unicode;
    

To change the owner of the conversion `iso_8859_1_to_utf8` to `joe`:

    
    
    ALTER CONVERSION iso_8859_1_to_utf8 OWNER TO joe;
    

## Compatibility

There is no `ALTER CONVERSION` statement in the SQL standard.

## See Also

[CREATE CONVERSION](sql-createconversion.html "CREATE CONVERSION"), [DROP
CONVERSION](sql-dropconversion.html "DROP CONVERSION")

* * *

[Prev](sql-altercollation.html "ALTER COLLATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterdatabase.html "ALTER DATABASE")  
---|---|---  
ALTER COLLATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER DATABASE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterconversion.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

