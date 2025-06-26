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

Supported Versions: [Current](/docs/current/ecpg-sql-whenever.html "PostgreSQL
17 - WHENEVER") ([17](/docs/17/ecpg-sql-whenever.html "PostgreSQL 17 -
WHENEVER")) / [16](/docs/16/ecpg-sql-whenever.html "PostgreSQL 16 - WHENEVER")
/ [15](/docs/15/ecpg-sql-whenever.html "PostgreSQL 15 - WHENEVER") /
[14](/docs/14/ecpg-sql-whenever.html "PostgreSQL 14 - WHENEVER") /
[13](/docs/13/ecpg-sql-whenever.html "PostgreSQL 13 - WHENEVER")

Development Versions: [18](/docs/18/ecpg-sql-whenever.html "PostgreSQL 18 -
WHENEVER") / [devel](/docs/devel/ecpg-sql-whenever.html "PostgreSQL devel -
WHENEVER")

Unsupported versions: [12](/docs/12/ecpg-sql-whenever.html "PostgreSQL 12 -
WHENEVER") / [11](/docs/11/ecpg-sql-whenever.html "PostgreSQL 11 - WHENEVER")
/ [10](/docs/10/ecpg-sql-whenever.html "PostgreSQL 10 - WHENEVER") /
[9.6](/docs/9.6/ecpg-sql-whenever.html "PostgreSQL 9.6 - WHENEVER") /
[9.5](/docs/9.5/ecpg-sql-whenever.html "PostgreSQL 9.5 - WHENEVER") /
[9.4](/docs/9.4/ecpg-sql-whenever.html "PostgreSQL 9.4 - WHENEVER") /
[9.3](/docs/9.3/ecpg-sql-whenever.html "PostgreSQL 9.3 - WHENEVER") /
[9.2](/docs/9.2/ecpg-sql-whenever.html "PostgreSQL 9.2 - WHENEVER") /
[9.1](/docs/9.1/ecpg-sql-whenever.html "PostgreSQL 9.1 - WHENEVER")

__

WHENEVER  
---  
[Prev](ecpg-sql-var.html "VAR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-informix-compat.html "36.15. Informix Compatibility Mode")  
  
* * *

## WHENEVER

WHENEVER — specify the action to be taken when an SQL statement causes a
specific class condition to be raised

## Synopsis

    
    
    WHENEVER { NOT FOUND | SQLERROR | SQLWARNING } _action_
    

## Description

Define a behavior which is called on the special cases (Rows not found, SQL
warnings or errors) in the result of SQL execution.

## Parameters

See [Section 36.8.1](ecpg-errors.html#ECPG-WHENEVER "36.8.1. Setting
Callbacks") for a description of the parameters.

## Examples

    
    
    EXEC SQL WHENEVER NOT FOUND CONTINUE;
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    EXEC SQL WHENEVER NOT FOUND DO CONTINUE;
    EXEC SQL WHENEVER SQLWARNING SQLPRINT;
    EXEC SQL WHENEVER SQLWARNING DO warn();
    EXEC SQL WHENEVER SQLERROR sqlprint;
    EXEC SQL WHENEVER SQLERROR CALL print2();
    EXEC SQL WHENEVER SQLERROR DO handle_error("select");
    EXEC SQL WHENEVER SQLERROR DO sqlnotice(NULL, NONO);
    EXEC SQL WHENEVER SQLERROR DO sqlprint();
    EXEC SQL WHENEVER SQLERROR GOTO error_label;
    EXEC SQL WHENEVER SQLERROR STOP;
    

A typical application is the use of `WHENEVER NOT FOUND BREAK` to handle
looping through result sets:

    
    
    int
    main(void)
    {
        EXEC SQL CONNECT TO testdb AS con1;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
        EXEC SQL ALLOCATE DESCRIPTOR d;
        EXEC SQL DECLARE cur CURSOR FOR SELECT current_database(), 'hoge', 256;
        EXEC SQL OPEN cur;
    
        /* when end of result set reached, break out of while loop */
        EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
        while (1)
        {
            EXEC SQL FETCH NEXT FROM cur INTO SQL DESCRIPTOR d;
            ...
        }
    
        EXEC SQL CLOSE cur;
        EXEC SQL COMMIT;
    
        EXEC SQL DEALLOCATE DESCRIPTOR d;
        EXEC SQL DISCONNECT ALL;
    
        return 0;
    }
    

## Compatibility

`WHENEVER` is specified in the SQL standard, but most of the actions are
PostgreSQL extensions.

* * *

[Prev](ecpg-sql-var.html "VAR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-informix-compat.html "36.15. Informix Compatibility Mode")  
---|---|---  
VAR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.15. Informix Compatibility Mode  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-whenever.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

