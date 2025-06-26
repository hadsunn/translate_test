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

Supported Versions: [Current](/docs/current/ecpg-sql-set-connection.html
"PostgreSQL 17 - SET CONNECTION") ([17](/docs/17/ecpg-sql-set-connection.html
"PostgreSQL 17 - SET CONNECTION")) / [16](/docs/16/ecpg-sql-set-
connection.html "PostgreSQL 16 - SET CONNECTION") / [15](/docs/15/ecpg-sql-
set-connection.html "PostgreSQL 15 - SET CONNECTION") / [14](/docs/14/ecpg-
sql-set-connection.html "PostgreSQL 14 - SET CONNECTION") /
[13](/docs/13/ecpg-sql-set-connection.html "PostgreSQL 13 - SET CONNECTION")

Development Versions: [18](/docs/18/ecpg-sql-set-connection.html "PostgreSQL
18 - SET CONNECTION") / [devel](/docs/devel/ecpg-sql-set-connection.html
"PostgreSQL devel - SET CONNECTION")

Unsupported versions: [12](/docs/12/ecpg-sql-set-connection.html "PostgreSQL
12 - SET CONNECTION") / [11](/docs/11/ecpg-sql-set-connection.html "PostgreSQL
11 - SET CONNECTION") / [10](/docs/10/ecpg-sql-set-connection.html "PostgreSQL
10 - SET CONNECTION") / [9.6](/docs/9.6/ecpg-sql-set-connection.html
"PostgreSQL 9.6 - SET CONNECTION") / [9.5](/docs/9.5/ecpg-sql-set-
connection.html "PostgreSQL 9.5 - SET CONNECTION") / [9.4](/docs/9.4/ecpg-sql-
set-connection.html "PostgreSQL 9.4 - SET CONNECTION") / [9.3](/docs/9.3/ecpg-
sql-set-connection.html "PostgreSQL 9.3 - SET CONNECTION") /
[9.2](/docs/9.2/ecpg-sql-set-connection.html "PostgreSQL 9.2 - SET
CONNECTION") / [9.1](/docs/9.1/ecpg-sql-set-connection.html "PostgreSQL 9.1 -
SET CONNECTION")

__

SET CONNECTION  
---  
[Prev](ecpg-sql-set-autocommit.html "SET AUTOCOMMIT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-set-descriptor.html "SET DESCRIPTOR")  
  
* * *

## SET CONNECTION

SET CONNECTION — select a database connection

## Synopsis

    
    
    SET CONNECTION [ TO | = ] _connection_name_
    

## Description

`SET CONNECTION` sets the “current” database connection, which is the one that
all commands use unless overridden.

## Parameters

_`connection_name`_ #

    

A database connection name established by the `CONNECT` command.

`CURRENT` #

    

Set the connection to the current connection (thus, nothing happens).

## Examples

    
    
    EXEC SQL SET CONNECTION TO con2;
    EXEC SQL SET CONNECTION = con1;
    

## Compatibility

`SET CONNECTION` is specified in the SQL standard.

## See Also

[CONNECT](ecpg-sql-connect.html "CONNECT"), [DISCONNECT](ecpg-sql-
disconnect.html "DISCONNECT")

* * *

[Prev](ecpg-sql-set-autocommit.html "SET AUTOCOMMIT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-set-descriptor.html "SET DESCRIPTOR")  
---|---|---  
SET AUTOCOMMIT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET DESCRIPTOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-set-connection.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

