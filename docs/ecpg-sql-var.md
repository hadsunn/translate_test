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

Supported Versions: [Current](/docs/current/ecpg-sql-var.html "PostgreSQL 17 -
VAR") ([17](/docs/17/ecpg-sql-var.html "PostgreSQL 17 - VAR")) /
[16](/docs/16/ecpg-sql-var.html "PostgreSQL 16 - VAR") / [15](/docs/15/ecpg-
sql-var.html "PostgreSQL 15 - VAR") / [14](/docs/14/ecpg-sql-var.html
"PostgreSQL 14 - VAR") / [13](/docs/13/ecpg-sql-var.html "PostgreSQL 13 -
VAR")

Development Versions: [18](/docs/18/ecpg-sql-var.html "PostgreSQL 18 - VAR") /
[devel](/docs/devel/ecpg-sql-var.html "PostgreSQL devel - VAR")

Unsupported versions: [12](/docs/12/ecpg-sql-var.html "PostgreSQL 12 - VAR") /
[11](/docs/11/ecpg-sql-var.html "PostgreSQL 11 - VAR") / [10](/docs/10/ecpg-
sql-var.html "PostgreSQL 10 - VAR") / [9.6](/docs/9.6/ecpg-sql-var.html
"PostgreSQL 9.6 - VAR") / [9.5](/docs/9.5/ecpg-sql-var.html "PostgreSQL 9.5 -
VAR") / [9.4](/docs/9.4/ecpg-sql-var.html "PostgreSQL 9.4 - VAR") /
[9.3](/docs/9.3/ecpg-sql-var.html "PostgreSQL 9.3 - VAR") /
[9.2](/docs/9.2/ecpg-sql-var.html "PostgreSQL 9.2 - VAR") /
[9.1](/docs/9.1/ecpg-sql-var.html "PostgreSQL 9.1 - VAR")

__

VAR  
---  
[Prev](ecpg-sql-type.html "TYPE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-whenever.html "WHENEVER")  
  
* * *

## VAR

VAR — define a variable

## Synopsis

    
    
    VAR _varname_ IS _ctype_
    

## Description

The `VAR` command assigns a new C data type to a host variable. The host
variable must be previously declared in a declare section.

## Parameters

_`varname`_ #

    

A C variable name.

_`ctype`_ #

    

A C type specification.

## Examples

    
    
    Exec sql begin declare section;
    short a;
    exec sql end declare section;
    EXEC SQL VAR a IS int;
    

## Compatibility

The `VAR` command is a PostgreSQL extension.

* * *

[Prev](ecpg-sql-type.html "TYPE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-whenever.html "WHENEVER")  
---|---|---  
TYPE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  WHENEVER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-var.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

