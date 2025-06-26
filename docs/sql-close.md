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

Supported Versions: [Current](/docs/current/sql-close.html "PostgreSQL 17 -
CLOSE") ([17](/docs/17/sql-close.html "PostgreSQL 17 - CLOSE")) /
[16](/docs/16/sql-close.html "PostgreSQL 16 - CLOSE") / [15](/docs/15/sql-
close.html "PostgreSQL 15 - CLOSE") / [14](/docs/14/sql-close.html "PostgreSQL
14 - CLOSE") / [13](/docs/13/sql-close.html "PostgreSQL 13 - CLOSE")

Development Versions: [18](/docs/18/sql-close.html "PostgreSQL 18 - CLOSE") /
[devel](/docs/devel/sql-close.html "PostgreSQL devel - CLOSE")

Unsupported versions: [12](/docs/12/sql-close.html "PostgreSQL 12 - CLOSE") /
[11](/docs/11/sql-close.html "PostgreSQL 11 - CLOSE") / [10](/docs/10/sql-
close.html "PostgreSQL 10 - CLOSE") / [9.6](/docs/9.6/sql-close.html
"PostgreSQL 9.6 - CLOSE") / [9.5](/docs/9.5/sql-close.html "PostgreSQL 9.5 -
CLOSE") / [9.4](/docs/9.4/sql-close.html "PostgreSQL 9.4 - CLOSE") /
[9.3](/docs/9.3/sql-close.html "PostgreSQL 9.3 - CLOSE") /
[9.2](/docs/9.2/sql-close.html "PostgreSQL 9.2 - CLOSE") /
[9.1](/docs/9.1/sql-close.html "PostgreSQL 9.1 - CLOSE") /
[9.0](/docs/9.0/sql-close.html "PostgreSQL 9.0 - CLOSE") /
[8.4](/docs/8.4/sql-close.html "PostgreSQL 8.4 - CLOSE") /
[8.3](/docs/8.3/sql-close.html "PostgreSQL 8.3 - CLOSE") /
[8.2](/docs/8.2/sql-close.html "PostgreSQL 8.2 - CLOSE") /
[8.1](/docs/8.1/sql-close.html "PostgreSQL 8.1 - CLOSE") /
[8.0](/docs/8.0/sql-close.html "PostgreSQL 8.0 - CLOSE") /
[7.4](/docs/7.4/sql-close.html "PostgreSQL 7.4 - CLOSE") /
[7.3](/docs/7.3/sql-close.html "PostgreSQL 7.3 - CLOSE") /
[7.2](/docs/7.2/sql-close.html "PostgreSQL 7.2 - CLOSE") /
[7.1](/docs/7.1/sql-close.html "PostgreSQL 7.1 - CLOSE")

__

CLOSE  
---  
[Prev](sql-checkpoint.html "CHECKPOINT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-cluster.html "CLUSTER")  
  
* * *

## CLOSE

CLOSE — close a cursor

## Synopsis

    
    
    CLOSE { _name_ | ALL }
    

## Description

`CLOSE` frees the resources associated with an open cursor. After the cursor
is closed, no subsequent operations are allowed on it. A cursor should be
closed when it is no longer needed.

Every non-holdable open cursor is implicitly closed when a transaction is
terminated by `COMMIT` or `ROLLBACK`. A holdable cursor is implicitly closed
if the transaction that created it aborts via `ROLLBACK`. If the creating
transaction successfully commits, the holdable cursor remains open until an
explicit `CLOSE` is executed, or the client disconnects.

## Parameters

_`name`_

    

The name of an open cursor to close.

`ALL`

    

Close all open cursors.

## Notes

PostgreSQL does not have an explicit `OPEN` cursor statement; a cursor is
considered open when it is declared. Use the [`DECLARE`](sql-declare.html
"DECLARE") statement to declare a cursor.

You can see all available cursors by querying the [`pg_cursors`](view-pg-
cursors.html "54.6. pg_cursors") system view.

If a cursor is closed after a savepoint which is later rolled back, the
`CLOSE` is not rolled back; that is, the cursor remains closed.

## Examples

Close the cursor `liahona`:

    
    
    CLOSE liahona;
    

## Compatibility

`CLOSE` is fully conforming with the SQL standard. `CLOSE ALL` is a PostgreSQL
extension.

## See Also

[DECLARE](sql-declare.html "DECLARE"), [FETCH](sql-fetch.html "FETCH"),
[MOVE](sql-move.html "MOVE")

* * *

[Prev](sql-checkpoint.html "CHECKPOINT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-cluster.html "CLUSTER")  
---|---|---  
CHECKPOINT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CLUSTER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-close.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

