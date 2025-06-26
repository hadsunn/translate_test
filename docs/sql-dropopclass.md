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

Supported Versions: [Current](/docs/current/sql-dropopclass.html "PostgreSQL
17 - DROP OPERATOR CLASS") ([17](/docs/17/sql-dropopclass.html "PostgreSQL 17
- DROP OPERATOR CLASS")) / [16](/docs/16/sql-dropopclass.html "PostgreSQL 16 -
DROP OPERATOR CLASS") / [15](/docs/15/sql-dropopclass.html "PostgreSQL 15 -
DROP OPERATOR CLASS") / [14](/docs/14/sql-dropopclass.html "PostgreSQL 14 -
DROP OPERATOR CLASS") / [13](/docs/13/sql-dropopclass.html "PostgreSQL 13 -
DROP OPERATOR CLASS")

Development Versions: [18](/docs/18/sql-dropopclass.html "PostgreSQL 18 - DROP
OPERATOR CLASS") / [devel](/docs/devel/sql-dropopclass.html "PostgreSQL devel
- DROP OPERATOR CLASS")

Unsupported versions: [12](/docs/12/sql-dropopclass.html "PostgreSQL 12 - DROP
OPERATOR CLASS") / [11](/docs/11/sql-dropopclass.html "PostgreSQL 11 - DROP
OPERATOR CLASS") / [10](/docs/10/sql-dropopclass.html "PostgreSQL 10 - DROP
OPERATOR CLASS") / [9.6](/docs/9.6/sql-dropopclass.html "PostgreSQL 9.6 - DROP
OPERATOR CLASS") / [9.5](/docs/9.5/sql-dropopclass.html "PostgreSQL 9.5 - DROP
OPERATOR CLASS") / [9.4](/docs/9.4/sql-dropopclass.html "PostgreSQL 9.4 - DROP
OPERATOR CLASS") / [9.3](/docs/9.3/sql-dropopclass.html "PostgreSQL 9.3 - DROP
OPERATOR CLASS") / [9.2](/docs/9.2/sql-dropopclass.html "PostgreSQL 9.2 - DROP
OPERATOR CLASS") / [9.1](/docs/9.1/sql-dropopclass.html "PostgreSQL 9.1 - DROP
OPERATOR CLASS") / [9.0](/docs/9.0/sql-dropopclass.html "PostgreSQL 9.0 - DROP
OPERATOR CLASS") / [8.4](/docs/8.4/sql-dropopclass.html "PostgreSQL 8.4 - DROP
OPERATOR CLASS") / [8.3](/docs/8.3/sql-dropopclass.html "PostgreSQL 8.3 - DROP
OPERATOR CLASS") / [8.2](/docs/8.2/sql-dropopclass.html "PostgreSQL 8.2 - DROP
OPERATOR CLASS") / [8.1](/docs/8.1/sql-dropopclass.html "PostgreSQL 8.1 - DROP
OPERATOR CLASS") / [8.0](/docs/8.0/sql-dropopclass.html "PostgreSQL 8.0 - DROP
OPERATOR CLASS") / [7.4](/docs/7.4/sql-dropopclass.html "PostgreSQL 7.4 - DROP
OPERATOR CLASS") / [7.3](/docs/7.3/sql-dropopclass.html "PostgreSQL 7.3 - DROP
OPERATOR CLASS")

__

DROP OPERATOR CLASS  
---  
[Prev](sql-dropoperator.html "DROP OPERATOR")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropopfamily.html "DROP OPERATOR FAMILY")  
  
* * *

## DROP OPERATOR CLASS

DROP OPERATOR CLASS — remove an operator class

## Synopsis

    
    
    DROP OPERATOR CLASS [ IF EXISTS ] _name_ USING _index_method_ [ CASCADE | RESTRICT ]
    

## Description

`DROP OPERATOR CLASS` drops an existing operator class. To execute this
command you must be the owner of the operator class.

`DROP OPERATOR CLASS` does not drop any of the operators or functions
referenced by the class. If there are any indexes depending on the operator
class, you will need to specify `CASCADE` for the drop to complete.

## Parameters

`IF EXISTS`

    

Do not throw an error if the operator class does not exist. A notice is issued
in this case.

_`name`_

    

The name (optionally schema-qualified) of an existing operator class.

_`index_method`_

    

The name of the index access method the operator class is for.

`CASCADE`

    

Automatically drop objects that depend on the operator class (such as
indexes), and in turn all objects that depend on those objects (see [Section
5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the operator class if any objects depend on it. This is the
default.

## Notes

`DROP OPERATOR CLASS` will not drop the operator family containing the class,
even if there is nothing else left in the family (in particular, in the case
where the family was implicitly created by `CREATE OPERATOR CLASS`). An empty
operator family is harmless, but for the sake of tidiness you might wish to
remove the family with `DROP OPERATOR FAMILY`; or perhaps better, use `DROP
OPERATOR FAMILY` in the first place.

## Examples

Remove the B-tree operator class `widget_ops`:

    
    
    DROP OPERATOR CLASS widget_ops USING btree;
    

This command will not succeed if there are any existing indexes that use the
operator class. Add `CASCADE` to drop such indexes along with the operator
class.

## Compatibility

There is no `DROP OPERATOR CLASS` statement in the SQL standard.

## See Also

[ALTER OPERATOR CLASS](sql-alteropclass.html "ALTER OPERATOR CLASS"), [CREATE
OPERATOR CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"), [DROP
OPERATOR FAMILY](sql-dropopfamily.html "DROP OPERATOR FAMILY")

* * *

[Prev](sql-dropoperator.html "DROP OPERATOR")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropopfamily.html "DROP OPERATOR FAMILY")  
---|---|---  
DROP OPERATOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP OPERATOR FAMILY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropopclass.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

