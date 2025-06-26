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

Supported Versions: [Current](/docs/current/ecpg-sql-prepare.html "PostgreSQL
17 - PREPARE") ([17](/docs/17/ecpg-sql-prepare.html "PostgreSQL 17 -
PREPARE")) / [16](/docs/16/ecpg-sql-prepare.html "PostgreSQL 16 - PREPARE") /
[15](/docs/15/ecpg-sql-prepare.html "PostgreSQL 15 - PREPARE") /
[14](/docs/14/ecpg-sql-prepare.html "PostgreSQL 14 - PREPARE") /
[13](/docs/13/ecpg-sql-prepare.html "PostgreSQL 13 - PREPARE")

Development Versions: [18](/docs/18/ecpg-sql-prepare.html "PostgreSQL 18 -
PREPARE") / [devel](/docs/devel/ecpg-sql-prepare.html "PostgreSQL devel -
PREPARE")

Unsupported versions: [12](/docs/12/ecpg-sql-prepare.html "PostgreSQL 12 -
PREPARE") / [11](/docs/11/ecpg-sql-prepare.html "PostgreSQL 11 - PREPARE") /
[10](/docs/10/ecpg-sql-prepare.html "PostgreSQL 10 - PREPARE") /
[9.6](/docs/9.6/ecpg-sql-prepare.html "PostgreSQL 9.6 - PREPARE") /
[9.5](/docs/9.5/ecpg-sql-prepare.html "PostgreSQL 9.5 - PREPARE") /
[9.4](/docs/9.4/ecpg-sql-prepare.html "PostgreSQL 9.4 - PREPARE") /
[9.3](/docs/9.3/ecpg-sql-prepare.html "PostgreSQL 9.3 - PREPARE") /
[9.2](/docs/9.2/ecpg-sql-prepare.html "PostgreSQL 9.2 - PREPARE") /
[9.1](/docs/9.1/ecpg-sql-prepare.html "PostgreSQL 9.1 - PREPARE")

__

PREPARE  
---  
[Prev](ecpg-sql-open.html "OPEN")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-set-autocommit.html "SET AUTOCOMMIT")  
  
* * *

## PREPARE

PREPARE — prepare a statement for execution

## Synopsis

    
    
    PREPARE _prepared_name_ FROM _string_
    

## Description

`PREPARE` prepares a statement dynamically specified as a string for
execution. This is different from the direct SQL statement [PREPARE](sql-
prepare.html "PREPARE"), which can also be used in embedded programs. The
[EXECUTE](sql-execute.html "EXECUTE") command is used to execute either kind
of prepared statement.

## Parameters

_`prepared_name`_ #

    

An identifier for the prepared query.

_`string`_ #

    

A literal string or a host variable containing a preparable SQL statement, one
of SELECT, INSERT, UPDATE, or DELETE. Use question marks (`?`) for parameter
values to be supplied at execution.

## Notes

In typical usage, the _`string`_ is a host variable reference to a string
containing a dynamically-constructed SQL statement. The case of a literal
string is not very useful; you might as well just write a direct SQL `PREPARE`
statement.

If you do use a literal string, keep in mind that any double quotes you might
wish to include in the SQL statement must be written as octal escapes (`\042`)
not the usual C idiom `\"`. This is because the string is inside an `EXEC SQL`
section, so the ECPG lexer parses it according to SQL rules not C rules. Any
embedded backslashes will later be handled according to C rules; but `\"`
causes an immediate syntax error because it is seen as ending the literal.

## Examples

    
    
    char *stmt = "SELECT * FROM test1 WHERE a = ? AND b = ?";
    
    EXEC SQL ALLOCATE DESCRIPTOR outdesc;
    EXEC SQL PREPARE foo FROM :stmt;
    
    EXEC SQL EXECUTE foo USING SQL DESCRIPTOR indesc INTO SQL DESCRIPTOR outdesc;
    

## Compatibility

`PREPARE` is specified in the SQL standard.

## See Also

[EXECUTE](sql-execute.html "EXECUTE")

* * *

[Prev](ecpg-sql-open.html "OPEN")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-set-autocommit.html "SET AUTOCOMMIT")  
---|---|---  
OPEN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET AUTOCOMMIT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-prepare.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

