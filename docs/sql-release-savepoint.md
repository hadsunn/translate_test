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

Supported Versions: [Current](/docs/current/sql-release-savepoint.html
"PostgreSQL 17 - RELEASE SAVEPOINT") ([17](/docs/17/sql-release-savepoint.html
"PostgreSQL 17 - RELEASE SAVEPOINT")) / [16](/docs/16/sql-release-
savepoint.html "PostgreSQL 16 - RELEASE SAVEPOINT") / [15](/docs/15/sql-
release-savepoint.html "PostgreSQL 15 - RELEASE SAVEPOINT") /
[14](/docs/14/sql-release-savepoint.html "PostgreSQL 14 - RELEASE SAVEPOINT")
/ [13](/docs/13/sql-release-savepoint.html "PostgreSQL 13 - RELEASE
SAVEPOINT")

Development Versions: [18](/docs/18/sql-release-savepoint.html "PostgreSQL 18
- RELEASE SAVEPOINT") / [devel](/docs/devel/sql-release-savepoint.html
"PostgreSQL devel - RELEASE SAVEPOINT")

Unsupported versions: [12](/docs/12/sql-release-savepoint.html "PostgreSQL 12
- RELEASE SAVEPOINT") / [11](/docs/11/sql-release-savepoint.html "PostgreSQL
11 - RELEASE SAVEPOINT") / [10](/docs/10/sql-release-savepoint.html
"PostgreSQL 10 - RELEASE SAVEPOINT") / [9.6](/docs/9.6/sql-release-
savepoint.html "PostgreSQL 9.6 - RELEASE SAVEPOINT") / [9.5](/docs/9.5/sql-
release-savepoint.html "PostgreSQL 9.5 - RELEASE SAVEPOINT") /
[9.4](/docs/9.4/sql-release-savepoint.html "PostgreSQL 9.4 - RELEASE
SAVEPOINT") / [9.3](/docs/9.3/sql-release-savepoint.html "PostgreSQL 9.3 -
RELEASE SAVEPOINT") / [9.2](/docs/9.2/sql-release-savepoint.html "PostgreSQL
9.2 - RELEASE SAVEPOINT") / [9.1](/docs/9.1/sql-release-savepoint.html
"PostgreSQL 9.1 - RELEASE SAVEPOINT") / [9.0](/docs/9.0/sql-release-
savepoint.html "PostgreSQL 9.0 - RELEASE SAVEPOINT") / [8.4](/docs/8.4/sql-
release-savepoint.html "PostgreSQL 8.4 - RELEASE SAVEPOINT") /
[8.3](/docs/8.3/sql-release-savepoint.html "PostgreSQL 8.3 - RELEASE
SAVEPOINT") / [8.2](/docs/8.2/sql-release-savepoint.html "PostgreSQL 8.2 -
RELEASE SAVEPOINT") / [8.1](/docs/8.1/sql-release-savepoint.html "PostgreSQL
8.1 - RELEASE SAVEPOINT") / [8.0](/docs/8.0/sql-release-savepoint.html
"PostgreSQL 8.0 - RELEASE SAVEPOINT")

__

RELEASE SAVEPOINT  
---  
[Prev](sql-reindex.html "REINDEX")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-reset.html "RESET")  
  
* * *

## RELEASE SAVEPOINT

RELEASE SAVEPOINT — release a previously defined savepoint

## Synopsis

    
    
    RELEASE [ SAVEPOINT ] _savepoint_name_
    

## Description

`RELEASE SAVEPOINT` releases the named savepoint and all active savepoints
that were created after the named savepoint, and frees their resources. All
changes made since the creation of the savepoint that didn't already get
rolled back are merged into the transaction or savepoint that was active when
the named savepoint was created. Changes made after `RELEASE SAVEPOINT` will
also be part of this active transaction or savepoint.

## Parameters

_`savepoint_name`_

    

The name of the savepoint to release.

## Notes

Specifying a savepoint name that was not previously defined is an error.

It is not possible to release a savepoint when the transaction is in an
aborted state; to do that, use [ROLLBACK TO SAVEPOINT](sql-rollback-to.html
"ROLLBACK TO SAVEPOINT").

If multiple savepoints have the same name, only the most recently defined
unreleased one is released. Repeated commands will release progressively older
savepoints.

## Examples

To establish and later release a savepoint:

    
    
    BEGIN;
        INSERT INTO table1 VALUES (3);
        SAVEPOINT my_savepoint;
        INSERT INTO table1 VALUES (4);
        RELEASE SAVEPOINT my_savepoint;
    COMMIT;
    

The above transaction will insert both 3 and 4.

A more complex example with multiple nested subtransactions:

    
    
    BEGIN;
        INSERT INTO table1 VALUES (1);
        SAVEPOINT sp1;
        INSERT INTO table1 VALUES (2);
        SAVEPOINT sp2;
        INSERT INTO table1 VALUES (3);
        RELEASE SAVEPOINT sp2;
        INSERT INTO table1 VALUES (4))); -- generates an error
    

In this example, the application requests the release of the savepoint `sp2`,
which inserted 3. This changes the insert's transaction context to `sp1`. When
the statement attempting to insert value 4 generates an error, the insertion
of 2 and 4 are lost because they are in the same, now-rolled back savepoint,
and value 3 is in the same transaction context. The application can now only
choose one of these two commands, since all other commands will be ignored:

    
    
       ROLLBACK;
       ROLLBACK TO SAVEPOINT sp1;
    

Choosing `ROLLBACK` will abort everything, including value 1, whereas
`ROLLBACK TO SAVEPOINT sp1` will retain value 1 and allow the transaction to
continue.

## Compatibility

This command conforms to the SQL standard. The standard specifies that the key
word `SAVEPOINT` is mandatory, but PostgreSQL allows it to be omitted.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"),
[ROLLBACK](sql-rollback.html "ROLLBACK"), [ROLLBACK TO SAVEPOINT](sql-
rollback-to.html "ROLLBACK TO SAVEPOINT"), [SAVEPOINT](sql-savepoint.html
"SAVEPOINT")

* * *

[Prev](sql-reindex.html "REINDEX")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-reset.html "RESET")  
---|---|---  
REINDEX  | [Home](index.html "PostgreSQL 16.9 Documentation") |  RESET  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-release-savepoint.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

