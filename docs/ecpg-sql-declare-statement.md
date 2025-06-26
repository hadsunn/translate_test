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

Supported Versions: [Current](/docs/current/ecpg-sql-declare-statement.html
"PostgreSQL 17 - DECLARE STATEMENT") ([17](/docs/17/ecpg-sql-declare-
statement.html "PostgreSQL 17 - DECLARE STATEMENT")) / [16](/docs/16/ecpg-sql-
declare-statement.html "PostgreSQL 16 - DECLARE STATEMENT") /
[15](/docs/15/ecpg-sql-declare-statement.html "PostgreSQL 15 - DECLARE
STATEMENT") / [14](/docs/14/ecpg-sql-declare-statement.html "PostgreSQL 14 -
DECLARE STATEMENT")

Development Versions: [18](/docs/18/ecpg-sql-declare-statement.html
"PostgreSQL 18 - DECLARE STATEMENT") / [devel](/docs/devel/ecpg-sql-declare-
statement.html "PostgreSQL devel - DECLARE STATEMENT")

__

DECLARE STATEMENT  
---  
[Prev](ecpg-sql-declare.html "DECLARE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-describe.html "DESCRIBE")  
  
* * *

## DECLARE STATEMENT

DECLARE STATEMENT — declare SQL statement identifier

## Synopsis

    
    
    EXEC SQL [ AT _connection_name_ ] DECLARE _statement_name_ STATEMENT
    

## Description

`DECLARE STATEMENT` declares an SQL statement identifier. SQL statement
identifier can be associated with the connection. When the identifier is used
by dynamic SQL statements, the statements are executed using the associated
connection. The namespace of the declaration is the precompile unit, and
multiple declarations to the same SQL statement identifier are not allowed.
Note that if the precompiler runs in Informix compatibility mode and some SQL
statement is declared, "database" can not be used as a cursor name.

## Parameters

_`connection_name`_ #

    

A database connection name established by the `CONNECT` command.

AT clause can be omitted, but such statement has no meaning.

_`statement_name`_ #

    

The name of an SQL statement identifier, either as an SQL identifier or a host
variable.

## Notes

This association is valid only if the declaration is physically placed on top
of a dynamic statement.

## Examples

    
    
    EXEC SQL CONNECT TO postgres AS con1;
    EXEC SQL AT con1 DECLARE sql_stmt STATEMENT;
    EXEC SQL DECLARE cursor_name CURSOR FOR sql_stmt;
    EXEC SQL PREPARE sql_stmt FROM :dyn_string;
    EXEC SQL OPEN cursor_name;
    EXEC SQL FETCH cursor_name INTO :column1;
    EXEC SQL CLOSE cursor_name;
    

## Compatibility

`DECLARE STATEMENT` is an extension of the SQL standard, but can be used in
famous DBMSs.

## See Also

[CONNECT](ecpg-sql-connect.html "CONNECT"), [DECLARE](ecpg-sql-declare.html
"DECLARE"), [OPEN](ecpg-sql-open.html "OPEN")

* * *

[Prev](ecpg-sql-declare.html "DECLARE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-describe.html "DESCRIBE")  
---|---|---  
DECLARE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DESCRIBE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-declare-
statement.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

