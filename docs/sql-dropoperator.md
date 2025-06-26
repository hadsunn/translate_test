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

Supported Versions: [Current](/docs/current/sql-dropoperator.html "PostgreSQL
17 - DROP OPERATOR") ([17](/docs/17/sql-dropoperator.html "PostgreSQL 17 -
DROP OPERATOR")) / [16](/docs/16/sql-dropoperator.html "PostgreSQL 16 - DROP
OPERATOR") / [15](/docs/15/sql-dropoperator.html "PostgreSQL 15 - DROP
OPERATOR") / [14](/docs/14/sql-dropoperator.html "PostgreSQL 14 - DROP
OPERATOR") / [13](/docs/13/sql-dropoperator.html "PostgreSQL 13 - DROP
OPERATOR")

Development Versions: [18](/docs/18/sql-dropoperator.html "PostgreSQL 18 -
DROP OPERATOR") / [devel](/docs/devel/sql-dropoperator.html "PostgreSQL devel
- DROP OPERATOR")

Unsupported versions: [12](/docs/12/sql-dropoperator.html "PostgreSQL 12 -
DROP OPERATOR") / [11](/docs/11/sql-dropoperator.html "PostgreSQL 11 - DROP
OPERATOR") / [10](/docs/10/sql-dropoperator.html "PostgreSQL 10 - DROP
OPERATOR") / [9.6](/docs/9.6/sql-dropoperator.html "PostgreSQL 9.6 - DROP
OPERATOR") / [9.5](/docs/9.5/sql-dropoperator.html "PostgreSQL 9.5 - DROP
OPERATOR") / [9.4](/docs/9.4/sql-dropoperator.html "PostgreSQL 9.4 - DROP
OPERATOR") / [9.3](/docs/9.3/sql-dropoperator.html "PostgreSQL 9.3 - DROP
OPERATOR") / [9.2](/docs/9.2/sql-dropoperator.html "PostgreSQL 9.2 - DROP
OPERATOR") / [9.1](/docs/9.1/sql-dropoperator.html "PostgreSQL 9.1 - DROP
OPERATOR") / [9.0](/docs/9.0/sql-dropoperator.html "PostgreSQL 9.0 - DROP
OPERATOR") / [8.4](/docs/8.4/sql-dropoperator.html "PostgreSQL 8.4 - DROP
OPERATOR") / [8.3](/docs/8.3/sql-dropoperator.html "PostgreSQL 8.3 - DROP
OPERATOR") / [8.2](/docs/8.2/sql-dropoperator.html "PostgreSQL 8.2 - DROP
OPERATOR") / [8.1](/docs/8.1/sql-dropoperator.html "PostgreSQL 8.1 - DROP
OPERATOR") / [8.0](/docs/8.0/sql-dropoperator.html "PostgreSQL 8.0 - DROP
OPERATOR") / [7.4](/docs/7.4/sql-dropoperator.html "PostgreSQL 7.4 - DROP
OPERATOR") / [7.3](/docs/7.3/sql-dropoperator.html "PostgreSQL 7.3 - DROP
OPERATOR") / [7.2](/docs/7.2/sql-dropoperator.html "PostgreSQL 7.2 - DROP
OPERATOR") / [7.1](/docs/7.1/sql-dropoperator.html "PostgreSQL 7.1 - DROP
OPERATOR")

__

DROP OPERATOR  
---  
[Prev](sql-dropmaterializedview.html "DROP MATERIALIZED VIEW")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropopclass.html "DROP OPERATOR CLASS")  
  
* * *

## DROP OPERATOR

DROP OPERATOR — remove an operator

## Synopsis

    
    
    DROP OPERATOR [ IF EXISTS ] _name_ ( { _left_type_ | NONE } , _right_type_ ) [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP OPERATOR` drops an existing operator from the database system. To
execute this command you must be the owner of the operator.

## Parameters

`IF EXISTS`

    

Do not throw an error if the operator does not exist. A notice is issued in
this case.

_`name`_

    

The name (optionally schema-qualified) of an existing operator.

_`left_type`_

    

The data type of the operator's left operand; write `NONE` if the operator has
no left operand.

_`right_type`_

    

The data type of the operator's right operand.

`CASCADE`

    

Automatically drop objects that depend on the operator (such as views using
it), and in turn all objects that depend on those objects (see [Section
5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the operator if any objects depend on it. This is the default.

## Examples

Remove the power operator `a^b` for type `integer`:

    
    
    DROP OPERATOR ^ (integer, integer);
    

Remove the bitwise-complement prefix operator `~b` for type `bit`:

    
    
    DROP OPERATOR ~ (none, bit);
    

Remove multiple operators in one command:

    
    
    DROP OPERATOR ~ (none, bit), ^ (integer, integer);
    

## Compatibility

There is no `DROP OPERATOR` statement in the SQL standard.

## See Also

[CREATE OPERATOR](sql-createoperator.html "CREATE OPERATOR"), [ALTER
OPERATOR](sql-alteroperator.html "ALTER OPERATOR")

* * *

[Prev](sql-dropmaterializedview.html "DROP MATERIALIZED VIEW")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropopclass.html "DROP OPERATOR CLASS")  
---|---|---  
DROP MATERIALIZED VIEW  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP OPERATOR CLASS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropoperator.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

