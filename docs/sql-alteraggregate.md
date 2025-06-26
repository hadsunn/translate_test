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

Supported Versions: [Current](/docs/current/sql-alteraggregate.html
"PostgreSQL 17 - ALTER AGGREGATE") ([17](/docs/17/sql-alteraggregate.html
"PostgreSQL 17 - ALTER AGGREGATE")) / [16](/docs/16/sql-alteraggregate.html
"PostgreSQL 16 - ALTER AGGREGATE") / [15](/docs/15/sql-alteraggregate.html
"PostgreSQL 15 - ALTER AGGREGATE") / [14](/docs/14/sql-alteraggregate.html
"PostgreSQL 14 - ALTER AGGREGATE") / [13](/docs/13/sql-alteraggregate.html
"PostgreSQL 13 - ALTER AGGREGATE")

Development Versions: [18](/docs/18/sql-alteraggregate.html "PostgreSQL 18 -
ALTER AGGREGATE") / [devel](/docs/devel/sql-alteraggregate.html "PostgreSQL
devel - ALTER AGGREGATE")

Unsupported versions: [12](/docs/12/sql-alteraggregate.html "PostgreSQL 12 -
ALTER AGGREGATE") / [11](/docs/11/sql-alteraggregate.html "PostgreSQL 11 -
ALTER AGGREGATE") / [10](/docs/10/sql-alteraggregate.html "PostgreSQL 10 -
ALTER AGGREGATE") / [9.6](/docs/9.6/sql-alteraggregate.html "PostgreSQL 9.6 -
ALTER AGGREGATE") / [9.5](/docs/9.5/sql-alteraggregate.html "PostgreSQL 9.5 -
ALTER AGGREGATE") / [9.4](/docs/9.4/sql-alteraggregate.html "PostgreSQL 9.4 -
ALTER AGGREGATE") / [9.3](/docs/9.3/sql-alteraggregate.html "PostgreSQL 9.3 -
ALTER AGGREGATE") / [9.2](/docs/9.2/sql-alteraggregate.html "PostgreSQL 9.2 -
ALTER AGGREGATE") / [9.1](/docs/9.1/sql-alteraggregate.html "PostgreSQL 9.1 -
ALTER AGGREGATE") / [9.0](/docs/9.0/sql-alteraggregate.html "PostgreSQL 9.0 -
ALTER AGGREGATE") / [8.4](/docs/8.4/sql-alteraggregate.html "PostgreSQL 8.4 -
ALTER AGGREGATE") / [8.3](/docs/8.3/sql-alteraggregate.html "PostgreSQL 8.3 -
ALTER AGGREGATE") / [8.2](/docs/8.2/sql-alteraggregate.html "PostgreSQL 8.2 -
ALTER AGGREGATE") / [8.1](/docs/8.1/sql-alteraggregate.html "PostgreSQL 8.1 -
ALTER AGGREGATE") / [8.0](/docs/8.0/sql-alteraggregate.html "PostgreSQL 8.0 -
ALTER AGGREGATE") / [7.4](/docs/7.4/sql-alteraggregate.html "PostgreSQL 7.4 -
ALTER AGGREGATE")

__

ALTER AGGREGATE  
---  
[Prev](sql-abort.html "ABORT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altercollation.html "ALTER COLLATION")  
  
* * *

## ALTER AGGREGATE

ALTER AGGREGATE — change the definition of an aggregate function

## Synopsis

    
    
    ALTER AGGREGATE _name_ ( _aggregate_signature_ ) RENAME TO _new_name_
    ALTER AGGREGATE _name_ ( _aggregate_signature_ )
                    OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER AGGREGATE _name_ ( _aggregate_signature_ ) SET SCHEMA _new_schema_
    
    where _aggregate_signature_ is:
    
    * |
    [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ] |
    [ [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ] ] ORDER BY [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ]
    

## Description

`ALTER AGGREGATE` changes the definition of an aggregate function.

You must own the aggregate function to use `ALTER AGGREGATE`. To change the
schema of an aggregate function, you must also have `CREATE` privilege on the
new schema. To alter the owner, you must be able to `SET ROLE` to the new
owning role, and that role must have `CREATE` privilege on the aggregate
function's schema. (These restrictions enforce that altering the owner doesn't
do anything you couldn't do by dropping and recreating the aggregate function.
However, a superuser can alter ownership of any aggregate function anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing aggregate function.

_`argmode`_

    

The mode of an argument: `IN` or `VARIADIC`. If omitted, the default is `IN`.

_`argname`_

    

The name of an argument. Note that `ALTER AGGREGATE` does not actually pay any
attention to argument names, since only the argument data types are needed to
determine the aggregate function's identity.

_`argtype`_

    

An input data type on which the aggregate function operates. To reference a
zero-argument aggregate function, write `*` in place of the list of argument
specifications. To reference an ordered-set aggregate function, write `ORDER
BY` between the direct and aggregated argument specifications.

_`new_name`_

    

The new name of the aggregate function.

_`new_owner`_

    

The new owner of the aggregate function.

_`new_schema`_

    

The new schema for the aggregate function.

## Notes

The recommended syntax for referencing an ordered-set aggregate is to write
`ORDER BY` between the direct and aggregated argument specifications, in the
same style as in [`CREATE AGGREGATE`](sql-createaggregate.html "CREATE
AGGREGATE"). However, it will also work to omit `ORDER BY` and just run the
direct and aggregated argument specifications into a single list. In this
abbreviated form, if `VARIADIC "any"` was used in both the direct and
aggregated argument lists, write `VARIADIC "any"` only once.

## Examples

To rename the aggregate function `myavg` for type `integer` to `my_average`:

    
    
    ALTER AGGREGATE myavg(integer) RENAME TO my_average;
    

To change the owner of the aggregate function `myavg` for type `integer` to
`joe`:

    
    
    ALTER AGGREGATE myavg(integer) OWNER TO joe;
    

To move the ordered-set aggregate `mypercentile` with direct argument of type
`float8` and aggregated argument of type `integer` into schema `myschema`:

    
    
    ALTER AGGREGATE mypercentile(float8 ORDER BY integer) SET SCHEMA myschema;
    

This will work too:

    
    
    ALTER AGGREGATE mypercentile(float8, integer) SET SCHEMA myschema;
    

## Compatibility

There is no `ALTER AGGREGATE` statement in the SQL standard.

## See Also

[CREATE AGGREGATE](sql-createaggregate.html "CREATE AGGREGATE"), [DROP
AGGREGATE](sql-dropaggregate.html "DROP AGGREGATE")

* * *

[Prev](sql-abort.html "ABORT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altercollation.html "ALTER COLLATION")  
---|---|---  
ABORT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER COLLATION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alteraggregate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

