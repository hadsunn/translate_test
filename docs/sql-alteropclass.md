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

Supported Versions: [Current](/docs/current/sql-alteropclass.html "PostgreSQL
17 - ALTER OPERATOR CLASS") ([17](/docs/17/sql-alteropclass.html "PostgreSQL
17 - ALTER OPERATOR CLASS")) / [16](/docs/16/sql-alteropclass.html "PostgreSQL
16 - ALTER OPERATOR CLASS") / [15](/docs/15/sql-alteropclass.html "PostgreSQL
15 - ALTER OPERATOR CLASS") / [14](/docs/14/sql-alteropclass.html "PostgreSQL
14 - ALTER OPERATOR CLASS") / [13](/docs/13/sql-alteropclass.html "PostgreSQL
13 - ALTER OPERATOR CLASS")

Development Versions: [18](/docs/18/sql-alteropclass.html "PostgreSQL 18 -
ALTER OPERATOR CLASS") / [devel](/docs/devel/sql-alteropclass.html "PostgreSQL
devel - ALTER OPERATOR CLASS")

Unsupported versions: [12](/docs/12/sql-alteropclass.html "PostgreSQL 12 -
ALTER OPERATOR CLASS") / [11](/docs/11/sql-alteropclass.html "PostgreSQL 11 -
ALTER OPERATOR CLASS") / [10](/docs/10/sql-alteropclass.html "PostgreSQL 10 -
ALTER OPERATOR CLASS") / [9.6](/docs/9.6/sql-alteropclass.html "PostgreSQL 9.6
- ALTER OPERATOR CLASS") / [9.5](/docs/9.5/sql-alteropclass.html "PostgreSQL
9.5 - ALTER OPERATOR CLASS") / [9.4](/docs/9.4/sql-alteropclass.html
"PostgreSQL 9.4 - ALTER OPERATOR CLASS") / [9.3](/docs/9.3/sql-
alteropclass.html "PostgreSQL 9.3 - ALTER OPERATOR CLASS") /
[9.2](/docs/9.2/sql-alteropclass.html "PostgreSQL 9.2 - ALTER OPERATOR CLASS")
/ [9.1](/docs/9.1/sql-alteropclass.html "PostgreSQL 9.1 - ALTER OPERATOR
CLASS") / [9.0](/docs/9.0/sql-alteropclass.html "PostgreSQL 9.0 - ALTER
OPERATOR CLASS") / [8.4](/docs/8.4/sql-alteropclass.html "PostgreSQL 8.4 -
ALTER OPERATOR CLASS") / [8.3](/docs/8.3/sql-alteropclass.html "PostgreSQL 8.3
- ALTER OPERATOR CLASS") / [8.2](/docs/8.2/sql-alteropclass.html "PostgreSQL
8.2 - ALTER OPERATOR CLASS") / [8.1](/docs/8.1/sql-alteropclass.html
"PostgreSQL 8.1 - ALTER OPERATOR CLASS") / [8.0](/docs/8.0/sql-
alteropclass.html "PostgreSQL 8.0 - ALTER OPERATOR CLASS") /
[7.4](/docs/7.4/sql-alteropclass.html "PostgreSQL 7.4 - ALTER OPERATOR CLASS")

__

ALTER OPERATOR CLASS  
---  
[Prev](sql-alteroperator.html "ALTER OPERATOR")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alteropfamily.html "ALTER OPERATOR FAMILY")  
  
* * *

## ALTER OPERATOR CLASS

ALTER OPERATOR CLASS — change the definition of an operator class

## Synopsis

    
    
    ALTER OPERATOR CLASS _name_ USING _index_method_
        RENAME TO _new_name_
    
    ALTER OPERATOR CLASS _name_ USING _index_method_
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    
    ALTER OPERATOR CLASS _name_ USING _index_method_
        SET SCHEMA _new_schema_
    

## Description

`ALTER OPERATOR CLASS` changes the definition of an operator class.

You must own the operator class to use `ALTER OPERATOR CLASS`. To alter the
owner, you must be able to `SET ROLE` to the new owning role, and that role
must have `CREATE` privilege on the operator class's schema. (These
restrictions enforce that altering the owner doesn't do anything you couldn't
do by dropping and recreating the operator class. However, a superuser can
alter ownership of any operator class anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing operator class.

_`index_method`_

    

The name of the index method this operator class is for.

_`new_name`_

    

The new name of the operator class.

_`new_owner`_

    

The new owner of the operator class.

_`new_schema`_

    

The new schema for the operator class.

## Compatibility

There is no `ALTER OPERATOR CLASS` statement in the SQL standard.

## See Also

[CREATE OPERATOR CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"), [DROP
OPERATOR CLASS](sql-dropopclass.html "DROP OPERATOR CLASS"), [ALTER OPERATOR
FAMILY](sql-alteropfamily.html "ALTER OPERATOR FAMILY")

* * *

[Prev](sql-alteroperator.html "ALTER OPERATOR")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alteropfamily.html "ALTER OPERATOR FAMILY")  
---|---|---  
ALTER OPERATOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER OPERATOR FAMILY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alteropclass.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

