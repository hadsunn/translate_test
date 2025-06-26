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

Supported Versions: [Current](/docs/current/sql-alterprocedure.html
"PostgreSQL 17 - ALTER PROCEDURE") ([17](/docs/17/sql-alterprocedure.html
"PostgreSQL 17 - ALTER PROCEDURE")) / [16](/docs/16/sql-alterprocedure.html
"PostgreSQL 16 - ALTER PROCEDURE") / [15](/docs/15/sql-alterprocedure.html
"PostgreSQL 15 - ALTER PROCEDURE") / [14](/docs/14/sql-alterprocedure.html
"PostgreSQL 14 - ALTER PROCEDURE") / [13](/docs/13/sql-alterprocedure.html
"PostgreSQL 13 - ALTER PROCEDURE")

Development Versions: [18](/docs/18/sql-alterprocedure.html "PostgreSQL 18 -
ALTER PROCEDURE") / [devel](/docs/devel/sql-alterprocedure.html "PostgreSQL
devel - ALTER PROCEDURE")

Unsupported versions: [12](/docs/12/sql-alterprocedure.html "PostgreSQL 12 -
ALTER PROCEDURE") / [11](/docs/11/sql-alterprocedure.html "PostgreSQL 11 -
ALTER PROCEDURE")

__

ALTER PROCEDURE  
---  
[Prev](sql-alterpolicy.html "ALTER POLICY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterpublication.html "ALTER PUBLICATION")  
  
* * *

## ALTER PROCEDURE

ALTER PROCEDURE — change the definition of a procedure

## Synopsis

    
    
    ALTER PROCEDURE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        _action_ [ ... ] [ RESTRICT ]
    ALTER PROCEDURE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        RENAME TO _new_name_
    ALTER PROCEDURE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER PROCEDURE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        SET SCHEMA _new_schema_
    ALTER PROCEDURE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        [ NO ] DEPENDS ON EXTENSION _extension_name_
    
    where _action_ is one of:
    
        [ EXTERNAL ] SECURITY INVOKER | [ EXTERNAL ] SECURITY DEFINER
        SET _configuration_parameter_ { TO | = } { _value_ | DEFAULT }
        SET _configuration_parameter_ FROM CURRENT
        RESET _configuration_parameter_
        RESET ALL
    

## Description

`ALTER PROCEDURE` changes the definition of a procedure.

You must own the procedure to use `ALTER PROCEDURE`. To change a procedure's
schema, you must also have `CREATE` privilege on the new schema. To alter the
owner, you must be able to `SET ROLE` to the new owning role, and that role
must have `CREATE` privilege on the procedure's schema. (These restrictions
enforce that altering the owner doesn't do anything you couldn't do by
dropping and recreating the procedure. However, a superuser can alter
ownership of any procedure anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing procedure. If no
argument list is specified, the name must be unique in its schema.

_`argmode`_

    

The mode of an argument: `IN`, `OUT`, `INOUT`, or `VARIADIC`. If omitted, the
default is `IN`.

_`argname`_

    

The name of an argument. Note that `ALTER PROCEDURE` does not actually pay any
attention to argument names, since only the argument data types are used to
determine the procedure's identity.

_`argtype`_

    

The data type(s) of the procedure's arguments (optionally schema-qualified),
if any. See [DROP PROCEDURE](sql-dropprocedure.html "DROP PROCEDURE") for the
details of how the procedure is looked up using the argument data type(s).

_`new_name`_

    

The new name of the procedure.

_`new_owner`_

    

The new owner of the procedure. Note that if the procedure is marked `SECURITY
DEFINER`, it will subsequently execute as the new owner.

_`new_schema`_

    

The new schema for the procedure.

_`extension_name`_

    

This form marks the procedure as dependent on the extension, or no longer
dependent on the extension if `NO` is specified. A procedure that's marked as
dependent on an extension is dropped when the extension is dropped, even if
cascade is not specified. A procedure can depend upon multiple extensions, and
will be dropped when any one of those extensions is dropped.

`[ EXTERNAL ] SECURITY INVOKER`  
`[ EXTERNAL ] SECURITY DEFINER`

    

Change whether the procedure is a security definer or not. The key word
`EXTERNAL` is ignored for SQL conformance. See [CREATE PROCEDURE](sql-
createprocedure.html "CREATE PROCEDURE") for more information about this
capability.

_`configuration_parameter`_  
 _`value`_

    

Add or change the assignment to be made to a configuration parameter when the
procedure is called. If _`value`_ is `DEFAULT` or, equivalently, `RESET` is
used, the procedure-local setting is removed, so that the procedure executes
with the value present in its environment. Use `RESET ALL` to clear all
procedure-local settings. `SET FROM CURRENT` saves the value of the parameter
that is current when `ALTER PROCEDURE` is executed as the value to be applied
when the procedure is entered.

See [SET](sql-set.html "SET") and [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") for more information about allowed
parameter names and values.

`RESTRICT`

    

Ignored for conformance with the SQL standard.

## Examples

To rename the procedure `insert_data` with two arguments of type `integer` to
`insert_record`:

    
    
    ALTER PROCEDURE insert_data(integer, integer) RENAME TO insert_record;
    

To change the owner of the procedure `insert_data` with two arguments of type
`integer` to `joe`:

    
    
    ALTER PROCEDURE insert_data(integer, integer) OWNER TO joe;
    

To change the schema of the procedure `insert_data` with two arguments of type
`integer` to `accounting`:

    
    
    ALTER PROCEDURE insert_data(integer, integer) SET SCHEMA accounting;
    

To mark the procedure `insert_data(integer, integer)` as being dependent on
the extension `myext`:

    
    
    ALTER PROCEDURE insert_data(integer, integer) DEPENDS ON EXTENSION myext;
    

To adjust the search path that is automatically set for a procedure:

    
    
    ALTER PROCEDURE check_password(text) SET search_path = admin, pg_temp;
    

To disable automatic setting of `search_path` for a procedure:

    
    
    ALTER PROCEDURE check_password(text) RESET search_path;
    

The procedure will now execute with whatever search path is used by its
caller.

## Compatibility

This statement is partially compatible with the `ALTER PROCEDURE` statement in
the SQL standard. The standard allows more properties of a procedure to be
modified, but does not provide the ability to rename a procedure, make a
procedure a security definer, attach configuration parameter values to a
procedure, or change the owner, schema, or volatility of a procedure. The
standard also requires the `RESTRICT` key word, which is optional in
PostgreSQL.

## See Also

[CREATE PROCEDURE](sql-createprocedure.html "CREATE PROCEDURE"), [DROP
PROCEDURE](sql-dropprocedure.html "DROP PROCEDURE"), [ALTER FUNCTION](sql-
alterfunction.html "ALTER FUNCTION"), [ALTER ROUTINE](sql-alterroutine.html
"ALTER ROUTINE")

* * *

[Prev](sql-alterpolicy.html "ALTER POLICY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterpublication.html "ALTER PUBLICATION")  
---|---|---  
ALTER POLICY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER PUBLICATION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterprocedure.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

