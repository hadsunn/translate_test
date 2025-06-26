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

Supported Versions: [Current](/docs/current/sql-rollback-to.html "PostgreSQL
17 - ROLLBACK TO SAVEPOINT") ([17](/docs/17/sql-rollback-to.html "PostgreSQL
17 - ROLLBACK TO SAVEPOINT")) / [16](/docs/16/sql-rollback-to.html "PostgreSQL
16 - ROLLBACK TO SAVEPOINT") / [15](/docs/15/sql-rollback-to.html "PostgreSQL
15 - ROLLBACK TO SAVEPOINT") / [14](/docs/14/sql-rollback-to.html "PostgreSQL
14 - ROLLBACK TO SAVEPOINT") / [13](/docs/13/sql-rollback-to.html "PostgreSQL
13 - ROLLBACK TO SAVEPOINT")

Development Versions: [18](/docs/18/sql-rollback-to.html "PostgreSQL 18 -
ROLLBACK TO SAVEPOINT") / [devel](/docs/devel/sql-rollback-to.html "PostgreSQL
devel - ROLLBACK TO SAVEPOINT")

Unsupported versions: [12](/docs/12/sql-rollback-to.html "PostgreSQL 12 -
ROLLBACK TO SAVEPOINT") / [11](/docs/11/sql-rollback-to.html "PostgreSQL 11 -
ROLLBACK TO SAVEPOINT") / [10](/docs/10/sql-rollback-to.html "PostgreSQL 10 -
ROLLBACK TO SAVEPOINT") / [9.6](/docs/9.6/sql-rollback-to.html "PostgreSQL 9.6
- ROLLBACK TO SAVEPOINT") / [9.5](/docs/9.5/sql-rollback-to.html "PostgreSQL
9.5 - ROLLBACK TO SAVEPOINT") / [9.4](/docs/9.4/sql-rollback-to.html
"PostgreSQL 9.4 - ROLLBACK TO SAVEPOINT") / [9.3](/docs/9.3/sql-rollback-
to.html "PostgreSQL 9.3 - ROLLBACK TO SAVEPOINT") / [9.2](/docs/9.2/sql-
rollback-to.html "PostgreSQL 9.2 - ROLLBACK TO SAVEPOINT") /
[9.1](/docs/9.1/sql-rollback-to.html "PostgreSQL 9.1 - ROLLBACK TO SAVEPOINT")
/ [9.0](/docs/9.0/sql-rollback-to.html "PostgreSQL 9.0 - ROLLBACK TO
SAVEPOINT") / [8.4](/docs/8.4/sql-rollback-to.html "PostgreSQL 8.4 - ROLLBACK
TO SAVEPOINT") / [8.3](/docs/8.3/sql-rollback-to.html "PostgreSQL 8.3 -
ROLLBACK TO SAVEPOINT") / [8.2](/docs/8.2/sql-rollback-to.html "PostgreSQL 8.2
- ROLLBACK TO SAVEPOINT") / [8.1](/docs/8.1/sql-rollback-to.html "PostgreSQL
8.1 - ROLLBACK TO SAVEPOINT") / [8.0](/docs/8.0/sql-rollback-to.html
"PostgreSQL 8.0 - ROLLBACK TO SAVEPOINT")

__

ROLLBACK TO SAVEPOINT  
---  
[Prev](sql-rollback-prepared.html "ROLLBACK PREPARED")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-savepoint.html "SAVEPOINT")  
  
* * *

## ROLLBACK TO SAVEPOINT

ROLLBACK TO SAVEPOINT — roll back to a savepoint

## Synopsis

    
    
    ROLLBACK [ WORK | TRANSACTION ] TO [ SAVEPOINT ] _savepoint_name_
    

## Description

Roll back all commands that were executed after the savepoint was established
and then start a new subtransaction at the same transaction level. The
savepoint remains valid and can be rolled back to again later, if needed.

`ROLLBACK TO SAVEPOINT` implicitly destroys all savepoints that were
established after the named savepoint.

## Parameters

_`savepoint_name`_

    

The savepoint to roll back to.

## Notes

Use [`RELEASE SAVEPOINT`](sql-release-savepoint.html "RELEASE SAVEPOINT") to
destroy a savepoint without discarding the effects of commands executed after
it was established.

Specifying a savepoint name that has not been established is an error.

Cursors have somewhat non-transactional behavior with respect to savepoints.
Any cursor that is opened inside a savepoint will be closed when the savepoint
is rolled back. If a previously opened cursor is affected by a `FETCH` or
`MOVE` command inside a savepoint that is later rolled back, the cursor
remains at the position that `FETCH` left it pointing to (that is, the cursor
motion caused by `FETCH` is not rolled back). Closing a cursor is not undone
by rolling back, either. However, other side-effects caused by the cursor's
query (such as side-effects of volatile functions called by the query) _are_
rolled back if they occur during a savepoint that is later rolled back. A
cursor whose execution causes a transaction to abort is put in a cannot-
execute state, so while the transaction can be restored using `ROLLBACK TO
SAVEPOINT`, the cursor can no longer be used.

## Examples

To undo the effects of the commands executed after `my_savepoint` was
established:

    
    
    ROLLBACK TO SAVEPOINT my_savepoint;
    

Cursor positions are not affected by savepoint rollback:

    
    
    BEGIN;
    
    DECLARE foo CURSOR FOR SELECT 1 UNION SELECT 2;
    
    SAVEPOINT foo;
    
    FETCH 1 FROM foo;
     ?column?
    ----------
            1
    
    ROLLBACK TO SAVEPOINT foo;
    
    FETCH 1 FROM foo;
     ?column?
    ----------
            2
    
    COMMIT;
    

## Compatibility

The SQL standard specifies that the key word `SAVEPOINT` is mandatory, but
PostgreSQL and Oracle allow it to be omitted. SQL allows only `WORK`, not
`TRANSACTION`, as a noise word after `ROLLBACK`. Also, SQL has an optional
clause `AND [ NO ] CHAIN` which is not currently supported by PostgreSQL.
Otherwise, this command conforms to the SQL standard.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"), [RELEASE
SAVEPOINT](sql-release-savepoint.html "RELEASE SAVEPOINT"), [ROLLBACK](sql-
rollback.html "ROLLBACK"), [SAVEPOINT](sql-savepoint.html "SAVEPOINT")

* * *

[Prev](sql-rollback-prepared.html "ROLLBACK PREPARED")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-savepoint.html "SAVEPOINT")  
---|---|---  
ROLLBACK PREPARED  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SAVEPOINT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-rollback-to.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

