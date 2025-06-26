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

Supported Versions: [Current](/docs/current/ecpg-sql-set-autocommit.html
"PostgreSQL 17 - SET AUTOCOMMIT") ([17](/docs/17/ecpg-sql-set-autocommit.html
"PostgreSQL 17 - SET AUTOCOMMIT")) / [16](/docs/16/ecpg-sql-set-
autocommit.html "PostgreSQL 16 - SET AUTOCOMMIT") / [15](/docs/15/ecpg-sql-
set-autocommit.html "PostgreSQL 15 - SET AUTOCOMMIT") / [14](/docs/14/ecpg-
sql-set-autocommit.html "PostgreSQL 14 - SET AUTOCOMMIT") /
[13](/docs/13/ecpg-sql-set-autocommit.html "PostgreSQL 13 - SET AUTOCOMMIT")

Development Versions: [18](/docs/18/ecpg-sql-set-autocommit.html "PostgreSQL
18 - SET AUTOCOMMIT") / [devel](/docs/devel/ecpg-sql-set-autocommit.html
"PostgreSQL devel - SET AUTOCOMMIT")

Unsupported versions: [12](/docs/12/ecpg-sql-set-autocommit.html "PostgreSQL
12 - SET AUTOCOMMIT") / [11](/docs/11/ecpg-sql-set-autocommit.html "PostgreSQL
11 - SET AUTOCOMMIT") / [10](/docs/10/ecpg-sql-set-autocommit.html "PostgreSQL
10 - SET AUTOCOMMIT") / [9.6](/docs/9.6/ecpg-sql-set-autocommit.html
"PostgreSQL 9.6 - SET AUTOCOMMIT") / [9.5](/docs/9.5/ecpg-sql-set-
autocommit.html "PostgreSQL 9.5 - SET AUTOCOMMIT") / [9.4](/docs/9.4/ecpg-sql-
set-autocommit.html "PostgreSQL 9.4 - SET AUTOCOMMIT") / [9.3](/docs/9.3/ecpg-
sql-set-autocommit.html "PostgreSQL 9.3 - SET AUTOCOMMIT") /
[9.2](/docs/9.2/ecpg-sql-set-autocommit.html "PostgreSQL 9.2 - SET
AUTOCOMMIT") / [9.1](/docs/9.1/ecpg-sql-set-autocommit.html "PostgreSQL 9.1 -
SET AUTOCOMMIT")

__

SET AUTOCOMMIT  
---  
[Prev](ecpg-sql-prepare.html "PREPARE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-set-connection.html "SET CONNECTION")  
  
* * *

## SET AUTOCOMMIT

SET AUTOCOMMIT — set the autocommit behavior of the current session

## Synopsis

    
    
    SET AUTOCOMMIT { = | TO } { ON | OFF }
    

## Description

`SET AUTOCOMMIT` sets the autocommit behavior of the current database session.
By default, embedded SQL programs are _not_ in autocommit mode, so `COMMIT`
needs to be issued explicitly when desired. This command can change the
session to autocommit mode, where each individual statement is committed
implicitly.

## Compatibility

`SET AUTOCOMMIT` is an extension of PostgreSQL ECPG.

* * *

[Prev](ecpg-sql-prepare.html "PREPARE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-set-connection.html "SET CONNECTION")  
---|---|---  
PREPARE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET CONNECTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-set-autocommit.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

