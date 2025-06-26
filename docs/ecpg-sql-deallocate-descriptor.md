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

Supported Versions: [Current](/docs/current/ecpg-sql-deallocate-
descriptor.html "PostgreSQL 17 - DEALLOCATE DESCRIPTOR") ([17](/docs/17/ecpg-
sql-deallocate-descriptor.html "PostgreSQL 17 - DEALLOCATE DESCRIPTOR")) /
[16](/docs/16/ecpg-sql-deallocate-descriptor.html "PostgreSQL 16 - DEALLOCATE
DESCRIPTOR") / [15](/docs/15/ecpg-sql-deallocate-descriptor.html "PostgreSQL
15 - DEALLOCATE DESCRIPTOR") / [14](/docs/14/ecpg-sql-deallocate-
descriptor.html "PostgreSQL 14 - DEALLOCATE DESCRIPTOR") / [13](/docs/13/ecpg-
sql-deallocate-descriptor.html "PostgreSQL 13 - DEALLOCATE DESCRIPTOR")

Development Versions: [18](/docs/18/ecpg-sql-deallocate-descriptor.html
"PostgreSQL 18 - DEALLOCATE DESCRIPTOR") / [devel](/docs/devel/ecpg-sql-
deallocate-descriptor.html "PostgreSQL devel - DEALLOCATE DESCRIPTOR")

Unsupported versions: [12](/docs/12/ecpg-sql-deallocate-descriptor.html
"PostgreSQL 12 - DEALLOCATE DESCRIPTOR") / [11](/docs/11/ecpg-sql-deallocate-
descriptor.html "PostgreSQL 11 - DEALLOCATE DESCRIPTOR") / [10](/docs/10/ecpg-
sql-deallocate-descriptor.html "PostgreSQL 10 - DEALLOCATE DESCRIPTOR") /
[9.6](/docs/9.6/ecpg-sql-deallocate-descriptor.html "PostgreSQL 9.6 -
DEALLOCATE DESCRIPTOR") / [9.5](/docs/9.5/ecpg-sql-deallocate-descriptor.html
"PostgreSQL 9.5 - DEALLOCATE DESCRIPTOR") / [9.4](/docs/9.4/ecpg-sql-
deallocate-descriptor.html "PostgreSQL 9.4 - DEALLOCATE DESCRIPTOR") /
[9.3](/docs/9.3/ecpg-sql-deallocate-descriptor.html "PostgreSQL 9.3 -
DEALLOCATE DESCRIPTOR") / [9.2](/docs/9.2/ecpg-sql-deallocate-descriptor.html
"PostgreSQL 9.2 - DEALLOCATE DESCRIPTOR") / [9.1](/docs/9.1/ecpg-sql-
deallocate-descriptor.html "PostgreSQL 9.1 - DEALLOCATE DESCRIPTOR")

__

DEALLOCATE DESCRIPTOR  
---  
[Prev](ecpg-sql-connect.html "CONNECT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-declare.html "DECLARE")  
  
* * *

## DEALLOCATE DESCRIPTOR

DEALLOCATE DESCRIPTOR — deallocate an SQL descriptor area

## Synopsis

    
    
    DEALLOCATE DESCRIPTOR _name_
    

## Description

`DEALLOCATE DESCRIPTOR` deallocates a named SQL descriptor area.

## Parameters

_`name`_ #

    

The name of the descriptor which is going to be deallocated. It is case
sensitive. This can be an SQL identifier or a host variable.

## Examples

    
    
    EXEC SQL DEALLOCATE DESCRIPTOR mydesc;
    

## Compatibility

`DEALLOCATE DESCRIPTOR` is specified in the SQL standard.

## See Also

[ALLOCATE DESCRIPTOR](ecpg-sql-allocate-descriptor.html "ALLOCATE
DESCRIPTOR"), [GET DESCRIPTOR](ecpg-sql-get-descriptor.html "GET DESCRIPTOR"),
[SET DESCRIPTOR](ecpg-sql-set-descriptor.html "SET DESCRIPTOR")

* * *

[Prev](ecpg-sql-connect.html "CONNECT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-declare.html "DECLARE")  
---|---|---  
CONNECT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DECLARE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-deallocate-
descriptor.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

