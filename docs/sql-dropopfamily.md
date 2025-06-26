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

Supported Versions: [Current](/docs/current/sql-dropopfamily.html "PostgreSQL
17 - DROP OPERATOR FAMILY") ([17](/docs/17/sql-dropopfamily.html "PostgreSQL
17 - DROP OPERATOR FAMILY")) / [16](/docs/16/sql-dropopfamily.html "PostgreSQL
16 - DROP OPERATOR FAMILY") / [15](/docs/15/sql-dropopfamily.html "PostgreSQL
15 - DROP OPERATOR FAMILY") / [14](/docs/14/sql-dropopfamily.html "PostgreSQL
14 - DROP OPERATOR FAMILY") / [13](/docs/13/sql-dropopfamily.html "PostgreSQL
13 - DROP OPERATOR FAMILY")

Development Versions: [18](/docs/18/sql-dropopfamily.html "PostgreSQL 18 -
DROP OPERATOR FAMILY") / [devel](/docs/devel/sql-dropopfamily.html "PostgreSQL
devel - DROP OPERATOR FAMILY")

Unsupported versions: [12](/docs/12/sql-dropopfamily.html "PostgreSQL 12 -
DROP OPERATOR FAMILY") / [11](/docs/11/sql-dropopfamily.html "PostgreSQL 11 -
DROP OPERATOR FAMILY") / [10](/docs/10/sql-dropopfamily.html "PostgreSQL 10 -
DROP OPERATOR FAMILY") / [9.6](/docs/9.6/sql-dropopfamily.html "PostgreSQL 9.6
- DROP OPERATOR FAMILY") / [9.5](/docs/9.5/sql-dropopfamily.html "PostgreSQL
9.5 - DROP OPERATOR FAMILY") / [9.4](/docs/9.4/sql-dropopfamily.html
"PostgreSQL 9.4 - DROP OPERATOR FAMILY") / [9.3](/docs/9.3/sql-
dropopfamily.html "PostgreSQL 9.3 - DROP OPERATOR FAMILY") /
[9.2](/docs/9.2/sql-dropopfamily.html "PostgreSQL 9.2 - DROP OPERATOR FAMILY")
/ [9.1](/docs/9.1/sql-dropopfamily.html "PostgreSQL 9.1 - DROP OPERATOR
FAMILY") / [9.0](/docs/9.0/sql-dropopfamily.html "PostgreSQL 9.0 - DROP
OPERATOR FAMILY") / [8.4](/docs/8.4/sql-dropopfamily.html "PostgreSQL 8.4 -
DROP OPERATOR FAMILY") / [8.3](/docs/8.3/sql-dropopfamily.html "PostgreSQL 8.3
- DROP OPERATOR FAMILY")

__

DROP OPERATOR FAMILY  
---  
[Prev](sql-dropopclass.html "DROP OPERATOR CLASS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-drop-owned.html "DROP OWNED")  
  
* * *

## DROP OPERATOR FAMILY

DROP OPERATOR FAMILY — remove an operator family

## Synopsis

    
    
    DROP OPERATOR FAMILY [ IF EXISTS ] _name_ USING _index_method_ [ CASCADE | RESTRICT ]
    

## Description

`DROP OPERATOR FAMILY` drops an existing operator family. To execute this
command you must be the owner of the operator family.

`DROP OPERATOR FAMILY` includes dropping any operator classes contained in the
family, but it does not drop any of the operators or functions referenced by
the family. If there are any indexes depending on operator classes within the
family, you will need to specify `CASCADE` for the drop to complete.

## Parameters

`IF EXISTS`

    

Do not throw an error if the operator family does not exist. A notice is
issued in this case.

_`name`_

    

The name (optionally schema-qualified) of an existing operator family.

_`index_method`_

    

The name of the index access method the operator family is for.

`CASCADE`

    

Automatically drop objects that depend on the operator family, and in turn all
objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the operator family if any objects depend on it. This is the
default.

## Examples

Remove the B-tree operator family `float_ops`:

    
    
    DROP OPERATOR FAMILY float_ops USING btree;
    

This command will not succeed if there are any existing indexes that use
operator classes within the family. Add `CASCADE` to drop such indexes along
with the operator family.

## Compatibility

There is no `DROP OPERATOR FAMILY` statement in the SQL standard.

## See Also

[ALTER OPERATOR FAMILY](sql-alteropfamily.html "ALTER OPERATOR FAMILY"),
[CREATE OPERATOR FAMILY](sql-createopfamily.html "CREATE OPERATOR FAMILY"),
[ALTER OPERATOR CLASS](sql-alteropclass.html "ALTER OPERATOR CLASS"), [CREATE
OPERATOR CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"), [DROP
OPERATOR CLASS](sql-dropopclass.html "DROP OPERATOR CLASS")

* * *

[Prev](sql-dropopclass.html "DROP OPERATOR CLASS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-drop-owned.html "DROP OWNED")  
---|---|---  
DROP OPERATOR CLASS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP OWNED  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropopfamily.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

