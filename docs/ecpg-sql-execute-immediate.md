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

Supported Versions: [Current](/docs/current/ecpg-sql-execute-immediate.html
"PostgreSQL 17 - EXECUTE IMMEDIATE") ([17](/docs/17/ecpg-sql-execute-
immediate.html "PostgreSQL 17 - EXECUTE IMMEDIATE")) / [16](/docs/16/ecpg-sql-
execute-immediate.html "PostgreSQL 16 - EXECUTE IMMEDIATE") /
[15](/docs/15/ecpg-sql-execute-immediate.html "PostgreSQL 15 - EXECUTE
IMMEDIATE") / [14](/docs/14/ecpg-sql-execute-immediate.html "PostgreSQL 14 -
EXECUTE IMMEDIATE") / [13](/docs/13/ecpg-sql-execute-immediate.html
"PostgreSQL 13 - EXECUTE IMMEDIATE")

Development Versions: [18](/docs/18/ecpg-sql-execute-immediate.html
"PostgreSQL 18 - EXECUTE IMMEDIATE") / [devel](/docs/devel/ecpg-sql-execute-
immediate.html "PostgreSQL devel - EXECUTE IMMEDIATE")

Unsupported versions: [12](/docs/12/ecpg-sql-execute-immediate.html
"PostgreSQL 12 - EXECUTE IMMEDIATE") / [11](/docs/11/ecpg-sql-execute-
immediate.html "PostgreSQL 11 - EXECUTE IMMEDIATE") / [10](/docs/10/ecpg-sql-
execute-immediate.html "PostgreSQL 10 - EXECUTE IMMEDIATE") /
[9.6](/docs/9.6/ecpg-sql-execute-immediate.html "PostgreSQL 9.6 - EXECUTE
IMMEDIATE") / [9.5](/docs/9.5/ecpg-sql-execute-immediate.html "PostgreSQL 9.5
- EXECUTE IMMEDIATE") / [9.4](/docs/9.4/ecpg-sql-execute-immediate.html
"PostgreSQL 9.4 - EXECUTE IMMEDIATE") / [9.3](/docs/9.3/ecpg-sql-execute-
immediate.html "PostgreSQL 9.3 - EXECUTE IMMEDIATE") / [9.2](/docs/9.2/ecpg-
sql-execute-immediate.html "PostgreSQL 9.2 - EXECUTE IMMEDIATE") /
[9.1](/docs/9.1/ecpg-sql-execute-immediate.html "PostgreSQL 9.1 - EXECUTE
IMMEDIATE")

__

EXECUTE IMMEDIATE  
---  
[Prev](ecpg-sql-disconnect.html "DISCONNECT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-get-descriptor.html "GET DESCRIPTOR")  
  
* * *

## EXECUTE IMMEDIATE

EXECUTE IMMEDIATE — dynamically prepare and execute a statement

## Synopsis

    
    
    EXECUTE IMMEDIATE _string_
    

## Description

`EXECUTE IMMEDIATE` immediately prepares and executes a dynamically specified
SQL statement, without retrieving result rows.

## Parameters

_`string`_ #

    

A literal string or a host variable containing the SQL statement to be
executed.

## Notes

In typical usage, the _`string`_ is a host variable reference to a string
containing a dynamically-constructed SQL statement. The case of a literal
string is not very useful; you might as well just write the SQL statement
directly, without the extra typing of `EXECUTE IMMEDIATE`.

If you do use a literal string, keep in mind that any double quotes you might
wish to include in the SQL statement must be written as octal escapes (`\042`)
not the usual C idiom `\"`. This is because the string is inside an `EXEC SQL`
section, so the ECPG lexer parses it according to SQL rules not C rules. Any
embedded backslashes will later be handled according to C rules; but `\"`
causes an immediate syntax error because it is seen as ending the literal.

## Examples

Here is an example that executes an `INSERT` statement using `EXECUTE
IMMEDIATE` and a host variable named `command`:

    
    
    sprintf(command, "INSERT INTO test (name, amount, letter) VALUES ('db: ''r1''', 1, 'f')");
    EXEC SQL EXECUTE IMMEDIATE :command;
    

## Compatibility

`EXECUTE IMMEDIATE` is specified in the SQL standard.

* * *

[Prev](ecpg-sql-disconnect.html "DISCONNECT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-get-descriptor.html "GET DESCRIPTOR")  
---|---|---  
DISCONNECT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  GET DESCRIPTOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-execute-
immediate.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

