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

Supported Versions: [Current](/docs/current/sql-alteroperator.html "PostgreSQL
17 - ALTER OPERATOR") ([17](/docs/17/sql-alteroperator.html "PostgreSQL 17 -
ALTER OPERATOR")) / [16](/docs/16/sql-alteroperator.html "PostgreSQL 16 -
ALTER OPERATOR") / [15](/docs/15/sql-alteroperator.html "PostgreSQL 15 - ALTER
OPERATOR") / [14](/docs/14/sql-alteroperator.html "PostgreSQL 14 - ALTER
OPERATOR") / [13](/docs/13/sql-alteroperator.html "PostgreSQL 13 - ALTER
OPERATOR")

Development Versions: [18](/docs/18/sql-alteroperator.html "PostgreSQL 18 -
ALTER OPERATOR") / [devel](/docs/devel/sql-alteroperator.html "PostgreSQL
devel - ALTER OPERATOR")

Unsupported versions: [12](/docs/12/sql-alteroperator.html "PostgreSQL 12 -
ALTER OPERATOR") / [11](/docs/11/sql-alteroperator.html "PostgreSQL 11 - ALTER
OPERATOR") / [10](/docs/10/sql-alteroperator.html "PostgreSQL 10 - ALTER
OPERATOR") / [9.6](/docs/9.6/sql-alteroperator.html "PostgreSQL 9.6 - ALTER
OPERATOR") / [9.5](/docs/9.5/sql-alteroperator.html "PostgreSQL 9.5 - ALTER
OPERATOR") / [9.4](/docs/9.4/sql-alteroperator.html "PostgreSQL 9.4 - ALTER
OPERATOR") / [9.3](/docs/9.3/sql-alteroperator.html "PostgreSQL 9.3 - ALTER
OPERATOR") / [9.2](/docs/9.2/sql-alteroperator.html "PostgreSQL 9.2 - ALTER
OPERATOR") / [9.1](/docs/9.1/sql-alteroperator.html "PostgreSQL 9.1 - ALTER
OPERATOR") / [9.0](/docs/9.0/sql-alteroperator.html "PostgreSQL 9.0 - ALTER
OPERATOR") / [8.4](/docs/8.4/sql-alteroperator.html "PostgreSQL 8.4 - ALTER
OPERATOR") / [8.3](/docs/8.3/sql-alteroperator.html "PostgreSQL 8.3 - ALTER
OPERATOR") / [8.2](/docs/8.2/sql-alteroperator.html "PostgreSQL 8.2 - ALTER
OPERATOR") / [8.1](/docs/8.1/sql-alteroperator.html "PostgreSQL 8.1 - ALTER
OPERATOR") / [8.0](/docs/8.0/sql-alteroperator.html "PostgreSQL 8.0 - ALTER
OPERATOR")

__

ALTER OPERATOR  
---  
[Prev](sql-altermaterializedview.html "ALTER MATERIALIZED VIEW")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alteropclass.html "ALTER OPERATOR CLASS")  
  
* * *

## ALTER OPERATOR

ALTER OPERATOR — change the definition of an operator

## Synopsis

    
    
    ALTER OPERATOR _name_ ( { _left_type_ | NONE } , _right_type_ )
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    
    ALTER OPERATOR _name_ ( { _left_type_ | NONE } , _right_type_ )
        SET SCHEMA _new_schema_
    
    ALTER OPERATOR _name_ ( { _left_type_ | NONE } , _right_type_ )
        SET ( {  RESTRICT = { _res_proc_ | NONE }
               | JOIN = { _join_proc_ | NONE }
             } [, ... ] )
    

## Description

`ALTER OPERATOR` changes the definition of an operator.

You must own the operator to use `ALTER OPERATOR`. To alter the owner, you
must be able to `SET ROLE` to the new owning role, and that role must have
`CREATE` privilege on the operator's schema. (These restrictions enforce that
altering the owner doesn't do anything you couldn't do by dropping and
recreating the operator. However, a superuser can alter ownership of any
operator anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing operator.

_`left_type`_

    

The data type of the operator's left operand; write `NONE` if the operator has
no left operand.

_`right_type`_

    

The data type of the operator's right operand.

_`new_owner`_

    

The new owner of the operator.

_`new_schema`_

    

The new schema for the operator.

_`res_proc`_

    

The restriction selectivity estimator function for this operator; write NONE
to remove existing selectivity estimator.

_`join_proc`_

    

The join selectivity estimator function for this operator; write NONE to
remove existing selectivity estimator.

## Examples

Change the owner of a custom operator `a @@ b` for type `text`:

    
    
    ALTER OPERATOR @@ (text, text) OWNER TO joe;
    

Change the restriction and join selectivity estimator functions of a custom
operator `a && b` for type `int[]`:

    
    
    ALTER OPERATOR && (_int4, _int4) SET (RESTRICT = _int_contsel, JOIN = _int_contjoinsel);
    

## Compatibility

There is no `ALTER OPERATOR` statement in the SQL standard.

## See Also

[CREATE OPERATOR](sql-createoperator.html "CREATE OPERATOR"), [DROP
OPERATOR](sql-dropoperator.html "DROP OPERATOR")

* * *

[Prev](sql-altermaterializedview.html "ALTER MATERIALIZED VIEW")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alteropclass.html "ALTER OPERATOR CLASS")  
---|---|---  
ALTER MATERIALIZED VIEW  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER OPERATOR CLASS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alteroperator.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

