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

Supported Versions: [Current](/docs/current/sql-move.html "PostgreSQL 17 -
MOVE") ([17](/docs/17/sql-move.html "PostgreSQL 17 - MOVE")) /
[16](/docs/16/sql-move.html "PostgreSQL 16 - MOVE") / [15](/docs/15/sql-
move.html "PostgreSQL 15 - MOVE") / [14](/docs/14/sql-move.html "PostgreSQL 14
- MOVE") / [13](/docs/13/sql-move.html "PostgreSQL 13 - MOVE")

Development Versions: [18](/docs/18/sql-move.html "PostgreSQL 18 - MOVE") /
[devel](/docs/devel/sql-move.html "PostgreSQL devel - MOVE")

Unsupported versions: [12](/docs/12/sql-move.html "PostgreSQL 12 - MOVE") /
[11](/docs/11/sql-move.html "PostgreSQL 11 - MOVE") / [10](/docs/10/sql-
move.html "PostgreSQL 10 - MOVE") / [9.6](/docs/9.6/sql-move.html "PostgreSQL
9.6 - MOVE") / [9.5](/docs/9.5/sql-move.html "PostgreSQL 9.5 - MOVE") /
[9.4](/docs/9.4/sql-move.html "PostgreSQL 9.4 - MOVE") / [9.3](/docs/9.3/sql-
move.html "PostgreSQL 9.3 - MOVE") / [9.2](/docs/9.2/sql-move.html "PostgreSQL
9.2 - MOVE") / [9.1](/docs/9.1/sql-move.html "PostgreSQL 9.1 - MOVE") /
[9.0](/docs/9.0/sql-move.html "PostgreSQL 9.0 - MOVE") / [8.4](/docs/8.4/sql-
move.html "PostgreSQL 8.4 - MOVE") / [8.3](/docs/8.3/sql-move.html "PostgreSQL
8.3 - MOVE") / [8.2](/docs/8.2/sql-move.html "PostgreSQL 8.2 - MOVE") /
[8.1](/docs/8.1/sql-move.html "PostgreSQL 8.1 - MOVE") / [8.0](/docs/8.0/sql-
move.html "PostgreSQL 8.0 - MOVE") / [7.4](/docs/7.4/sql-move.html "PostgreSQL
7.4 - MOVE") / [7.3](/docs/7.3/sql-move.html "PostgreSQL 7.3 - MOVE") /
[7.2](/docs/7.2/sql-move.html "PostgreSQL 7.2 - MOVE") / [7.1](/docs/7.1/sql-
move.html "PostgreSQL 7.1 - MOVE")

__

MOVE  
---  
[Prev](sql-merge.html "MERGE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-notify.html "NOTIFY")  
  
* * *

## MOVE

MOVE — position a cursor

## Synopsis

    
    
    MOVE [ _direction_ ] [ FROM | IN ] _cursor_name_
    
    where _direction_ can be one of:
    
        NEXT
        PRIOR
        FIRST
        LAST
        ABSOLUTE _count_
        RELATIVE _count_
        _count_
        ALL
        FORWARD
        FORWARD _count_
        FORWARD ALL
        BACKWARD
        BACKWARD _count_
        BACKWARD ALL
    

## Description

`MOVE` repositions a cursor without retrieving any data. `MOVE` works exactly
like the `FETCH` command, except it only positions the cursor and does not
return rows.

The parameters for the `MOVE` command are identical to those of the `FETCH`
command; refer to [FETCH](sql-fetch.html "FETCH") for details on syntax and
usage.

## Outputs

On successful completion, a `MOVE` command returns a command tag of the form

    
    
    MOVE _count_
    

The _`count`_ is the number of rows that a `FETCH` command with the same
parameters would have returned (possibly zero).

## Examples

    
    
    BEGIN WORK;
    DECLARE liahona CURSOR FOR SELECT * FROM films;
    
    -- Skip the first 5 rows:
    MOVE FORWARD 5 IN liahona;
    MOVE 5
    
    -- Fetch the 6th row from the cursor liahona:
    FETCH 1 FROM liahona;
     code  | title  | did | date_prod  |  kind  |  len
    -------+--------+-----+------------+--------+-------
     P_303 | 48 Hrs | 103 | 1982-10-22 | Action | 01:37
    (1 row)
    
    -- Close the cursor liahona and end the transaction:
    CLOSE liahona;
    COMMIT WORK;
    

## Compatibility

There is no `MOVE` statement in the SQL standard.

## See Also

[CLOSE](sql-close.html "CLOSE"), [DECLARE](sql-declare.html "DECLARE"),
[FETCH](sql-fetch.html "FETCH")

* * *

[Prev](sql-merge.html "MERGE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-notify.html "NOTIFY")  
---|---|---  
MERGE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  NOTIFY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-move.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

