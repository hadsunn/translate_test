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

Supported Versions: [Current](/docs/current/sql-droproutine.html "PostgreSQL
17 - DROP ROUTINE") ([17](/docs/17/sql-droproutine.html "PostgreSQL 17 - DROP
ROUTINE")) / [16](/docs/16/sql-droproutine.html "PostgreSQL 16 - DROP
ROUTINE") / [15](/docs/15/sql-droproutine.html "PostgreSQL 15 - DROP ROUTINE")
/ [14](/docs/14/sql-droproutine.html "PostgreSQL 14 - DROP ROUTINE") /
[13](/docs/13/sql-droproutine.html "PostgreSQL 13 - DROP ROUTINE")

Development Versions: [18](/docs/18/sql-droproutine.html "PostgreSQL 18 - DROP
ROUTINE") / [devel](/docs/devel/sql-droproutine.html "PostgreSQL devel - DROP
ROUTINE")

Unsupported versions: [12](/docs/12/sql-droproutine.html "PostgreSQL 12 - DROP
ROUTINE") / [11](/docs/11/sql-droproutine.html "PostgreSQL 11 - DROP ROUTINE")

__

DROP ROUTINE  
---  
[Prev](sql-droprole.html "DROP ROLE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droprule.html "DROP RULE")  
  
* * *

## DROP ROUTINE

DROP ROUTINE — remove a routine

## Synopsis

    
    
    DROP ROUTINE [ IF EXISTS ] _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ] [, ...]
        [ CASCADE | RESTRICT ]
    

## Description

`DROP ROUTINE` removes the definition of one or more existing routines. The
term “routine” includes aggregate functions, normal functions, and procedures.
See under [DROP AGGREGATE](sql-dropaggregate.html "DROP AGGREGATE"), [DROP
FUNCTION](sql-dropfunction.html "DROP FUNCTION"), and [DROP PROCEDURE](sql-
dropprocedure.html "DROP PROCEDURE") for the description of the parameters,
more examples, and further details.

## Notes

The lookup rules used by `DROP ROUTINE` are fundamentally the same as for
`DROP PROCEDURE`; in particular, `DROP ROUTINE` shares that command's behavior
of considering an argument list that has no _`argmode`_ markers to be possibly
using the SQL standard's definition that `OUT` arguments are included in the
list. (`DROP AGGREGATE` and `DROP FUNCTION` do not do that.)

In some cases where the same name is shared by routines of different kinds, it
is possible for `DROP ROUTINE` to fail with an ambiguity error when a more
specific command (`DROP FUNCTION`, etc.) would work. Specifying the argument
type list more carefully will also resolve such problems.

These lookup rules are also used by other commands that act on existing
routines, such as `ALTER ROUTINE` and `COMMENT ON ROUTINE`.

## Examples

To drop the routine `foo` for type `integer`:

    
    
    DROP ROUTINE foo(integer);
    

This command will work independent of whether `foo` is an aggregate, function,
or procedure.

## Compatibility

This command conforms to the SQL standard, with these PostgreSQL extensions:

  * The standard only allows one routine to be dropped per command.

  * The `IF EXISTS` option is an extension.

  * The ability to specify argument modes and names is an extension, and the lookup rules differ when modes are given.

  * User-definable aggregate functions are an extension.

## See Also

[DROP AGGREGATE](sql-dropaggregate.html "DROP AGGREGATE"), [DROP
FUNCTION](sql-dropfunction.html "DROP FUNCTION"), [DROP PROCEDURE](sql-
dropprocedure.html "DROP PROCEDURE"), [ALTER ROUTINE](sql-alterroutine.html
"ALTER ROUTINE")

Note that there is no `CREATE ROUTINE` command.

* * *

[Prev](sql-droprole.html "DROP ROLE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droprule.html "DROP RULE")  
---|---|---  
DROP ROLE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP RULE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droproutine.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

