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

Supported Versions: [Current](/docs/current/ecpg-sql-open.html "PostgreSQL 17
- OPEN") ([17](/docs/17/ecpg-sql-open.html "PostgreSQL 17 - OPEN")) /
[16](/docs/16/ecpg-sql-open.html "PostgreSQL 16 - OPEN") / [15](/docs/15/ecpg-
sql-open.html "PostgreSQL 15 - OPEN") / [14](/docs/14/ecpg-sql-open.html
"PostgreSQL 14 - OPEN") / [13](/docs/13/ecpg-sql-open.html "PostgreSQL 13 -
OPEN")

Development Versions: [18](/docs/18/ecpg-sql-open.html "PostgreSQL 18 - OPEN")
/ [devel](/docs/devel/ecpg-sql-open.html "PostgreSQL devel - OPEN")

Unsupported versions: [12](/docs/12/ecpg-sql-open.html "PostgreSQL 12 - OPEN")
/ [11](/docs/11/ecpg-sql-open.html "PostgreSQL 11 - OPEN") /
[10](/docs/10/ecpg-sql-open.html "PostgreSQL 10 - OPEN") /
[9.6](/docs/9.6/ecpg-sql-open.html "PostgreSQL 9.6 - OPEN") /
[9.5](/docs/9.5/ecpg-sql-open.html "PostgreSQL 9.5 - OPEN") /
[9.4](/docs/9.4/ecpg-sql-open.html "PostgreSQL 9.4 - OPEN") /
[9.3](/docs/9.3/ecpg-sql-open.html "PostgreSQL 9.3 - OPEN") /
[9.2](/docs/9.2/ecpg-sql-open.html "PostgreSQL 9.2 - OPEN") /
[9.1](/docs/9.1/ecpg-sql-open.html "PostgreSQL 9.1 - OPEN")

__

OPEN  
---  
[Prev](ecpg-sql-get-descriptor.html "GET DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-prepare.html "PREPARE")  
  
* * *

## OPEN

OPEN — open a dynamic cursor

## Synopsis

    
    
    OPEN _cursor_name_
    OPEN _cursor_name_ USING _value_ [, ... ]
    OPEN _cursor_name_ USING SQL DESCRIPTOR _descriptor_name_
    

## Description

`OPEN` opens a cursor and optionally binds actual values to the placeholders
in the cursor's declaration. The cursor must previously have been declared
with the `DECLARE` command. The execution of `OPEN` causes the query to start
executing on the server.

## Parameters

_`cursor_name`_ #

    

The name of the cursor to be opened. This can be an SQL identifier or a host
variable.

_`value`_ #

    

A value to be bound to a placeholder in the cursor. This can be an SQL
constant, a host variable, or a host variable with indicator.

_`descriptor_name`_ #

    

The name of a descriptor containing values to be bound to the placeholders in
the cursor. This can be an SQL identifier or a host variable.

## Examples

    
    
    EXEC SQL OPEN a;
    EXEC SQL OPEN d USING 1, 'test';
    EXEC SQL OPEN c1 USING SQL DESCRIPTOR mydesc;
    EXEC SQL OPEN :curname1;
    

## Compatibility

`OPEN` is specified in the SQL standard.

## See Also

[DECLARE](ecpg-sql-declare.html "DECLARE"), [CLOSE](sql-close.html "CLOSE")

* * *

[Prev](ecpg-sql-get-descriptor.html "GET DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-prepare.html "PREPARE")  
---|---|---  
GET DESCRIPTOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  PREPARE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-open.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

