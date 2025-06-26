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

Supported Versions: [Current](/docs/current/sql-droptransform.html "PostgreSQL
17 - DROP TRANSFORM") ([17](/docs/17/sql-droptransform.html "PostgreSQL 17 -
DROP TRANSFORM")) / [16](/docs/16/sql-droptransform.html "PostgreSQL 16 - DROP
TRANSFORM") / [15](/docs/15/sql-droptransform.html "PostgreSQL 15 - DROP
TRANSFORM") / [14](/docs/14/sql-droptransform.html "PostgreSQL 14 - DROP
TRANSFORM") / [13](/docs/13/sql-droptransform.html "PostgreSQL 13 - DROP
TRANSFORM")

Development Versions: [18](/docs/18/sql-droptransform.html "PostgreSQL 18 -
DROP TRANSFORM") / [devel](/docs/devel/sql-droptransform.html "PostgreSQL
devel - DROP TRANSFORM")

Unsupported versions: [12](/docs/12/sql-droptransform.html "PostgreSQL 12 -
DROP TRANSFORM") / [11](/docs/11/sql-droptransform.html "PostgreSQL 11 - DROP
TRANSFORM") / [10](/docs/10/sql-droptransform.html "PostgreSQL 10 - DROP
TRANSFORM") / [9.6](/docs/9.6/sql-droptransform.html "PostgreSQL 9.6 - DROP
TRANSFORM") / [9.5](/docs/9.5/sql-droptransform.html "PostgreSQL 9.5 - DROP
TRANSFORM")

__

DROP TRANSFORM  
---  
[Prev](sql-droptstemplate.html "DROP TEXT SEARCH TEMPLATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droptrigger.html "DROP TRIGGER")  
  
* * *

## DROP TRANSFORM

DROP TRANSFORM — remove a transform

## Synopsis

    
    
    DROP TRANSFORM [ IF EXISTS ] FOR _type_name_ LANGUAGE _lang_name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP TRANSFORM` removes a previously defined transform.

To be able to drop a transform, you must own the type and the language. These
are the same privileges that are required to create a transform.

## Parameters

`IF EXISTS`

    

Do not throw an error if the transform does not exist. A notice is issued in
this case.

_`type_name`_

    

The name of the data type of the transform.

_`lang_name`_

    

The name of the language of the transform.

`CASCADE`

    

Automatically drop objects that depend on the transform, and in turn all
objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the transform if any objects depend on it. This is the default.

## Examples

To drop the transform for type `hstore` and language `plpython3u`:

    
    
    DROP TRANSFORM FOR hstore LANGUAGE plpython3u;
    

## Compatibility

This form of `DROP TRANSFORM` is a PostgreSQL extension. See [CREATE
TRANSFORM](sql-createtransform.html "CREATE TRANSFORM") for details.

## See Also

[CREATE TRANSFORM](sql-createtransform.html "CREATE TRANSFORM")

* * *

[Prev](sql-droptstemplate.html "DROP TEXT SEARCH TEMPLATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droptrigger.html "DROP TRIGGER")  
---|---|---  
DROP TEXT SEARCH TEMPLATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP TRIGGER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droptransform.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

