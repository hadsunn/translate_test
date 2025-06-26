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

Supported Versions: [Current](/docs/current/sql-savepoint.html "PostgreSQL 17
- SAVEPOINT") ([17](/docs/17/sql-savepoint.html "PostgreSQL 17 - SAVEPOINT"))
/ [16](/docs/16/sql-savepoint.html "PostgreSQL 16 - SAVEPOINT") /
[15](/docs/15/sql-savepoint.html "PostgreSQL 15 - SAVEPOINT") /
[14](/docs/14/sql-savepoint.html "PostgreSQL 14 - SAVEPOINT") /
[13](/docs/13/sql-savepoint.html "PostgreSQL 13 - SAVEPOINT")

Development Versions: [18](/docs/18/sql-savepoint.html "PostgreSQL 18 -
SAVEPOINT") / [devel](/docs/devel/sql-savepoint.html "PostgreSQL devel -
SAVEPOINT")

Unsupported versions: [12](/docs/12/sql-savepoint.html "PostgreSQL 12 -
SAVEPOINT") / [11](/docs/11/sql-savepoint.html "PostgreSQL 11 - SAVEPOINT") /
[10](/docs/10/sql-savepoint.html "PostgreSQL 10 - SAVEPOINT") /
[9.6](/docs/9.6/sql-savepoint.html "PostgreSQL 9.6 - SAVEPOINT") /
[9.5](/docs/9.5/sql-savepoint.html "PostgreSQL 9.5 - SAVEPOINT") /
[9.4](/docs/9.4/sql-savepoint.html "PostgreSQL 9.4 - SAVEPOINT") /
[9.3](/docs/9.3/sql-savepoint.html "PostgreSQL 9.3 - SAVEPOINT") /
[9.2](/docs/9.2/sql-savepoint.html "PostgreSQL 9.2 - SAVEPOINT") /
[9.1](/docs/9.1/sql-savepoint.html "PostgreSQL 9.1 - SAVEPOINT") /
[9.0](/docs/9.0/sql-savepoint.html "PostgreSQL 9.0 - SAVEPOINT") /
[8.4](/docs/8.4/sql-savepoint.html "PostgreSQL 8.4 - SAVEPOINT") /
[8.3](/docs/8.3/sql-savepoint.html "PostgreSQL 8.3 - SAVEPOINT") /
[8.2](/docs/8.2/sql-savepoint.html "PostgreSQL 8.2 - SAVEPOINT") /
[8.1](/docs/8.1/sql-savepoint.html "PostgreSQL 8.1 - SAVEPOINT") /
[8.0](/docs/8.0/sql-savepoint.html "PostgreSQL 8.0 - SAVEPOINT")

__

SAVEPOINT  
---  
[Prev](sql-rollback-to.html "ROLLBACK TO SAVEPOINT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-security-label.html "SECURITY LABEL")  
  
* * *

## SAVEPOINT

SAVEPOINT — define a new savepoint within the current transaction

## Synopsis

    
    
    SAVEPOINT _savepoint_name_
    

## Description

`SAVEPOINT` establishes a new savepoint within the current transaction.

A savepoint is a special mark inside a transaction that allows all commands
that are executed after it was established to be rolled back, restoring the
transaction state to what it was at the time of the savepoint.

## Parameters

_`savepoint_name`_

    

The name to give to the new savepoint. If savepoints with the same name
already exist, they will be inaccessible until newer identically-named
savepoints are released.

## Notes

Use [`ROLLBACK TO`](sql-rollback-to.html "ROLLBACK TO SAVEPOINT") to rollback
to a savepoint. Use [`RELEASE SAVEPOINT`](sql-release-savepoint.html "RELEASE
SAVEPOINT") to destroy a savepoint, keeping the effects of commands executed
after it was established.

Savepoints can only be established when inside a transaction block. There can
be multiple savepoints defined within a transaction.

## Examples

To establish a savepoint and later undo the effects of all commands executed
after it was established:

    
    
    BEGIN;
        INSERT INTO table1 VALUES (1);
        SAVEPOINT my_savepoint;
        INSERT INTO table1 VALUES (2);
        ROLLBACK TO SAVEPOINT my_savepoint;
        INSERT INTO table1 VALUES (3);
    COMMIT;
    

The above transaction will insert the values 1 and 3, but not 2.

To establish and later destroy a savepoint:

    
    
    BEGIN;
        INSERT INTO table1 VALUES (3);
        SAVEPOINT my_savepoint;
        INSERT INTO table1 VALUES (4);
        RELEASE SAVEPOINT my_savepoint;
    COMMIT;
    

The above transaction will insert both 3 and 4.

To use a single savepoint name:

    
    
    BEGIN;
        INSERT INTO table1 VALUES (1);
        SAVEPOINT my_savepoint;
        INSERT INTO table1 VALUES (2);
        SAVEPOINT my_savepoint;
        INSERT INTO table1 VALUES (3);
    
        -- rollback to the second savepoint
        ROLLBACK TO SAVEPOINT my_savepoint;
        SELECT * FROM table1;               -- shows rows 1 and 2
    
        -- release the second savepoint
        RELEASE SAVEPOINT my_savepoint;
    
        -- rollback to the first savepoint
        ROLLBACK TO SAVEPOINT my_savepoint;
        SELECT * FROM table1;               -- shows only row 1
    COMMIT;
    

The above transaction shows row 3 being rolled back first, then row 2.

## Compatibility

SQL requires a savepoint to be destroyed automatically when another savepoint
with the same name is established. In PostgreSQL, the old savepoint is kept,
though only the more recent one will be used when rolling back or releasing.
(Releasing the newer savepoint with `RELEASE SAVEPOINT` will cause the older
one to again become accessible to `ROLLBACK TO SAVEPOINT` and `RELEASE
SAVEPOINT`.) Otherwise, `SAVEPOINT` is fully SQL conforming.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"), [RELEASE
SAVEPOINT](sql-release-savepoint.html "RELEASE SAVEPOINT"), [ROLLBACK](sql-
rollback.html "ROLLBACK"), [ROLLBACK TO SAVEPOINT](sql-rollback-to.html
"ROLLBACK TO SAVEPOINT")

* * *

[Prev](sql-rollback-to.html "ROLLBACK TO SAVEPOINT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-security-label.html "SECURITY LABEL")  
---|---|---  
ROLLBACK TO SAVEPOINT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SECURITY LABEL  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-savepoint.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

