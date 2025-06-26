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

Supported Versions: [Current](/docs/current/ecpg-sql-declare.html "PostgreSQL
17 - DECLARE") ([17](/docs/17/ecpg-sql-declare.html "PostgreSQL 17 -
DECLARE")) / [16](/docs/16/ecpg-sql-declare.html "PostgreSQL 16 - DECLARE") /
[15](/docs/15/ecpg-sql-declare.html "PostgreSQL 15 - DECLARE") /
[14](/docs/14/ecpg-sql-declare.html "PostgreSQL 14 - DECLARE") /
[13](/docs/13/ecpg-sql-declare.html "PostgreSQL 13 - DECLARE")

Development Versions: [18](/docs/18/ecpg-sql-declare.html "PostgreSQL 18 -
DECLARE") / [devel](/docs/devel/ecpg-sql-declare.html "PostgreSQL devel -
DECLARE")

Unsupported versions: [12](/docs/12/ecpg-sql-declare.html "PostgreSQL 12 -
DECLARE") / [11](/docs/11/ecpg-sql-declare.html "PostgreSQL 11 - DECLARE") /
[10](/docs/10/ecpg-sql-declare.html "PostgreSQL 10 - DECLARE") /
[9.6](/docs/9.6/ecpg-sql-declare.html "PostgreSQL 9.6 - DECLARE") /
[9.5](/docs/9.5/ecpg-sql-declare.html "PostgreSQL 9.5 - DECLARE") /
[9.4](/docs/9.4/ecpg-sql-declare.html "PostgreSQL 9.4 - DECLARE") /
[9.3](/docs/9.3/ecpg-sql-declare.html "PostgreSQL 9.3 - DECLARE") /
[9.2](/docs/9.2/ecpg-sql-declare.html "PostgreSQL 9.2 - DECLARE") /
[9.1](/docs/9.1/ecpg-sql-declare.html "PostgreSQL 9.1 - DECLARE")

__

DECLARE  
---  
[Prev](ecpg-sql-deallocate-descriptor.html "DEALLOCATE DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-declare-statement.html "DECLARE STATEMENT")  
  
* * *

## DECLARE

DECLARE — define a cursor

## Synopsis

    
    
    DECLARE _cursor_name_ [ BINARY ] [ ASENSITIVE | INSENSITIVE ] [ [ NO ] SCROLL ] CURSOR [ { WITH | WITHOUT } HOLD ] FOR _prepared_name_
    DECLARE _cursor_name_ [ BINARY ] [ ASENSITIVE | INSENSITIVE ] [ [ NO ] SCROLL ] CURSOR [ { WITH | WITHOUT } HOLD ] FOR _query_
    

## Description

`DECLARE` declares a cursor for iterating over the result set of a prepared
statement. This command has slightly different semantics from the direct SQL
command `DECLARE`: Whereas the latter executes a query and prepares the result
set for retrieval, this embedded SQL command merely declares a name as a “loop
variable” for iterating over the result set of a query; the actual execution
happens when the cursor is opened with the `OPEN` command.

## Parameters

_`cursor_name`_ #

    

A cursor name, case sensitive. This can be an SQL identifier or a host
variable.

_`prepared_name`_ #

    

The name of a prepared query, either as an SQL identifier or a host variable.

_`query`_ #

    

A [SELECT](sql-select.html "SELECT") or [VALUES](sql-values.html "VALUES")
command which will provide the rows to be returned by the cursor.

For the meaning of the cursor options, see [DECLARE](sql-declare.html
"DECLARE").

## Examples

Examples declaring a cursor for a query:

    
    
    EXEC SQL DECLARE C CURSOR FOR SELECT * FROM My_Table;
    EXEC SQL DECLARE C CURSOR FOR SELECT Item1 FROM T;
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT version();
    

An example declaring a cursor for a prepared statement:

    
    
    EXEC SQL PREPARE stmt1 AS SELECT version();
    EXEC SQL DECLARE cur1 CURSOR FOR stmt1;
    

## Compatibility

`DECLARE` is specified in the SQL standard.

## See Also

[OPEN](ecpg-sql-open.html "OPEN"), [CLOSE](sql-close.html "CLOSE"),
[DECLARE](sql-declare.html "DECLARE")

* * *

[Prev](ecpg-sql-deallocate-descriptor.html "DEALLOCATE DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-declare-statement.html "DECLARE STATEMENT")  
---|---|---  
DEALLOCATE DESCRIPTOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DECLARE STATEMENT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-declare.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

