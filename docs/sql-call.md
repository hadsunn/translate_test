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

Supported Versions: [Current](/docs/current/sql-call.html "PostgreSQL 17 -
CALL") ([17](/docs/17/sql-call.html "PostgreSQL 17 - CALL")) /
[16](/docs/16/sql-call.html "PostgreSQL 16 - CALL") / [15](/docs/15/sql-
call.html "PostgreSQL 15 - CALL") / [14](/docs/14/sql-call.html "PostgreSQL 14
- CALL") / [13](/docs/13/sql-call.html "PostgreSQL 13 - CALL")

Development Versions: [18](/docs/18/sql-call.html "PostgreSQL 18 - CALL") /
[devel](/docs/devel/sql-call.html "PostgreSQL devel - CALL")

Unsupported versions: [12](/docs/12/sql-call.html "PostgreSQL 12 - CALL") /
[11](/docs/11/sql-call.html "PostgreSQL 11 - CALL")

__

CALL  
---  
[Prev](sql-begin.html "BEGIN")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-checkpoint.html "CHECKPOINT")  
  
* * *

## CALL

CALL — invoke a procedure

## Synopsis

    
    
    CALL _name_ ( [ _argument_ ] [, ...] )
    

## Description

`CALL` executes a procedure.

If the procedure has any output parameters, then a result row will be
returned, containing the values of those parameters.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of the procedure.

_`argument`_

    

An argument expression for the procedure call.

Arguments can include parameter names, using the syntax `_`name`_ =>
_`value`_`. This works the same as in ordinary function calls; see [Section
4.3](sql-syntax-calling-funcs.html "4.3. Calling Functions") for details.

Arguments must be supplied for all procedure parameters that lack defaults,
including `OUT` parameters. However, arguments matching `OUT` parameters are
not evaluated, so it's customary to just write `NULL` for them. (Writing
something else for an `OUT` parameter might cause compatibility problems with
future PostgreSQL versions.)

## Notes

The user must have `EXECUTE` privilege on the procedure in order to be allowed
to invoke it.

To call a function (not a procedure), use `SELECT` instead.

If `CALL` is executed in a transaction block, then the called procedure cannot
execute transaction control statements. Transaction control statements are
only allowed if `CALL` is executed in its own transaction.

PL/pgSQL handles output parameters in `CALL` commands differently; see
[Section 43.6.3](plpgsql-control-structures.html#PLPGSQL-STATEMENTS-CALLING-
PROCEDURE "43.6.3. Calling a Procedure").

## Examples

    
    
    CALL do_db_maintenance();
    

## Compatibility

`CALL` conforms to the SQL standard, except for the handling of output
parameters. The standard says that users should write variables to receive the
values of output parameters.

## See Also

[CREATE PROCEDURE](sql-createprocedure.html "CREATE PROCEDURE")

* * *

[Prev](sql-begin.html "BEGIN")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-checkpoint.html "CHECKPOINT")  
---|---|---  
BEGIN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CHECKPOINT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-call.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

