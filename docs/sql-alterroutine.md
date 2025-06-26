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

Supported Versions: [Current](/docs/current/sql-alterroutine.html "PostgreSQL
17 - ALTER ROUTINE") ([17](/docs/17/sql-alterroutine.html "PostgreSQL 17 -
ALTER ROUTINE")) / [16](/docs/16/sql-alterroutine.html "PostgreSQL 16 - ALTER
ROUTINE") / [15](/docs/15/sql-alterroutine.html "PostgreSQL 15 - ALTER
ROUTINE") / [14](/docs/14/sql-alterroutine.html "PostgreSQL 14 - ALTER
ROUTINE") / [13](/docs/13/sql-alterroutine.html "PostgreSQL 13 - ALTER
ROUTINE")

Development Versions: [18](/docs/18/sql-alterroutine.html "PostgreSQL 18 -
ALTER ROUTINE") / [devel](/docs/devel/sql-alterroutine.html "PostgreSQL devel
- ALTER ROUTINE")

Unsupported versions: [12](/docs/12/sql-alterroutine.html "PostgreSQL 12 -
ALTER ROUTINE") / [11](/docs/11/sql-alterroutine.html "PostgreSQL 11 - ALTER
ROUTINE")

__

ALTER ROUTINE  
---  
[Prev](sql-alterrole.html "ALTER ROLE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterrule.html "ALTER RULE")  
  
* * *

## ALTER ROUTINE

ALTER ROUTINE — change the definition of a routine

## Synopsis

    
    
    ALTER ROUTINE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        _action_ [ ... ] [ RESTRICT ]
    ALTER ROUTINE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        RENAME TO _new_name_
    ALTER ROUTINE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER ROUTINE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        SET SCHEMA _new_schema_
    ALTER ROUTINE _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ]
        [ NO ] DEPENDS ON EXTENSION _extension_name_
    
    where _action_ is one of:
    
        IMMUTABLE | STABLE | VOLATILE
        [ NOT ] LEAKPROOF
        [ EXTERNAL ] SECURITY INVOKER | [ EXTERNAL ] SECURITY DEFINER
        PARALLEL { UNSAFE | RESTRICTED | SAFE }
        COST _execution_cost_
        ROWS _result_rows_
        SET _configuration_parameter_ { TO | = } { _value_ | DEFAULT }
        SET _configuration_parameter_ FROM CURRENT
        RESET _configuration_parameter_
        RESET ALL
    

## Description

`ALTER ROUTINE` changes the definition of a routine, which can be an aggregate
function, a normal function, or a procedure. See under [ALTER AGGREGATE](sql-
alteraggregate.html "ALTER AGGREGATE"), [ALTER FUNCTION](sql-
alterfunction.html "ALTER FUNCTION"), and [ALTER PROCEDURE](sql-
alterprocedure.html "ALTER PROCEDURE") for the description of the parameters,
more examples, and further details.

## Examples

To rename the routine `foo` for type `integer` to `foobar`:

    
    
    ALTER ROUTINE foo(integer) RENAME TO foobar;
    

This command will work independent of whether `foo` is an aggregate, function,
or procedure.

## Compatibility

This statement is partially compatible with the `ALTER ROUTINE` statement in
the SQL standard. See under [ALTER FUNCTION](sql-alterfunction.html "ALTER
FUNCTION") and [ALTER PROCEDURE](sql-alterprocedure.html "ALTER PROCEDURE")
for more details. Allowing routine names to refer to aggregate functions is a
PostgreSQL extension.

## See Also

[ALTER AGGREGATE](sql-alteraggregate.html "ALTER AGGREGATE"), [ALTER
FUNCTION](sql-alterfunction.html "ALTER FUNCTION"), [ALTER PROCEDURE](sql-
alterprocedure.html "ALTER PROCEDURE"), [DROP ROUTINE](sql-droproutine.html
"DROP ROUTINE")

Note that there is no `CREATE ROUTINE` command.

* * *

[Prev](sql-alterrole.html "ALTER ROLE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterrule.html "ALTER RULE")  
---|---|---  
ALTER ROLE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER RULE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterroutine.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

