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

Supported Versions: [Current](/docs/current/ecpg-sql-disconnect.html
"PostgreSQL 17 - DISCONNECT") ([17](/docs/17/ecpg-sql-disconnect.html
"PostgreSQL 17 - DISCONNECT")) / [16](/docs/16/ecpg-sql-disconnect.html
"PostgreSQL 16 - DISCONNECT") / [15](/docs/15/ecpg-sql-disconnect.html
"PostgreSQL 15 - DISCONNECT") / [14](/docs/14/ecpg-sql-disconnect.html
"PostgreSQL 14 - DISCONNECT") / [13](/docs/13/ecpg-sql-disconnect.html
"PostgreSQL 13 - DISCONNECT")

Development Versions: [18](/docs/18/ecpg-sql-disconnect.html "PostgreSQL 18 -
DISCONNECT") / [devel](/docs/devel/ecpg-sql-disconnect.html "PostgreSQL devel
- DISCONNECT")

Unsupported versions: [12](/docs/12/ecpg-sql-disconnect.html "PostgreSQL 12 -
DISCONNECT") / [11](/docs/11/ecpg-sql-disconnect.html "PostgreSQL 11 -
DISCONNECT") / [10](/docs/10/ecpg-sql-disconnect.html "PostgreSQL 10 -
DISCONNECT") / [9.6](/docs/9.6/ecpg-sql-disconnect.html "PostgreSQL 9.6 -
DISCONNECT") / [9.5](/docs/9.5/ecpg-sql-disconnect.html "PostgreSQL 9.5 -
DISCONNECT") / [9.4](/docs/9.4/ecpg-sql-disconnect.html "PostgreSQL 9.4 -
DISCONNECT") / [9.3](/docs/9.3/ecpg-sql-disconnect.html "PostgreSQL 9.3 -
DISCONNECT") / [9.2](/docs/9.2/ecpg-sql-disconnect.html "PostgreSQL 9.2 -
DISCONNECT") / [9.1](/docs/9.1/ecpg-sql-disconnect.html "PostgreSQL 9.1 -
DISCONNECT")

__

DISCONNECT  
---  
[Prev](ecpg-sql-describe.html "DESCRIBE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-execute-immediate.html "EXECUTE IMMEDIATE")  
  
* * *

## DISCONNECT

DISCONNECT — terminate a database connection

## Synopsis

    
    
    DISCONNECT _connection_name_
    DISCONNECT [ CURRENT ]
    DISCONNECT ALL
    

## Description

`DISCONNECT` closes a connection (or all connections) to the database.

## Parameters

_`connection_name`_ #

    

A database connection name established by the `CONNECT` command.

`CURRENT` #

    

Close the “current” connection, which is either the most recently opened
connection, or the connection set by the `SET CONNECTION` command. This is
also the default if no argument is given to the `DISCONNECT` command.

`ALL` #

    

Close all open connections.

## Examples

    
    
    int
    main(void)
    {
        EXEC SQL CONNECT TO testdb AS con1 USER testuser;
        EXEC SQL CONNECT TO testdb AS con2 USER testuser;
        EXEC SQL CONNECT TO testdb AS con3 USER testuser;
    
        EXEC SQL DISCONNECT CURRENT;  /* close con3          */
        EXEC SQL DISCONNECT ALL;      /* close con2 and con1 */
    
        return 0;
    }
    

## Compatibility

`DISCONNECT` is specified in the SQL standard.

## See Also

[CONNECT](ecpg-sql-connect.html "CONNECT"), [SET CONNECTION](ecpg-sql-set-
connection.html "SET CONNECTION")

* * *

[Prev](ecpg-sql-describe.html "DESCRIBE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-execute-immediate.html "EXECUTE IMMEDIATE")  
---|---|---  
DESCRIBE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  EXECUTE IMMEDIATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-disconnect.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

