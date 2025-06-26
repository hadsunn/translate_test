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

Supported Versions: [Current](/docs/current/sql-rollback-prepared.html
"PostgreSQL 17 - ROLLBACK PREPARED") ([17](/docs/17/sql-rollback-prepared.html
"PostgreSQL 17 - ROLLBACK PREPARED")) / [16](/docs/16/sql-rollback-
prepared.html "PostgreSQL 16 - ROLLBACK PREPARED") / [15](/docs/15/sql-
rollback-prepared.html "PostgreSQL 15 - ROLLBACK PREPARED") /
[14](/docs/14/sql-rollback-prepared.html "PostgreSQL 14 - ROLLBACK PREPARED")
/ [13](/docs/13/sql-rollback-prepared.html "PostgreSQL 13 - ROLLBACK
PREPARED")

Development Versions: [18](/docs/18/sql-rollback-prepared.html "PostgreSQL 18
- ROLLBACK PREPARED") / [devel](/docs/devel/sql-rollback-prepared.html
"PostgreSQL devel - ROLLBACK PREPARED")

Unsupported versions: [12](/docs/12/sql-rollback-prepared.html "PostgreSQL 12
- ROLLBACK PREPARED") / [11](/docs/11/sql-rollback-prepared.html "PostgreSQL
11 - ROLLBACK PREPARED") / [10](/docs/10/sql-rollback-prepared.html
"PostgreSQL 10 - ROLLBACK PREPARED") / [9.6](/docs/9.6/sql-rollback-
prepared.html "PostgreSQL 9.6 - ROLLBACK PREPARED") / [9.5](/docs/9.5/sql-
rollback-prepared.html "PostgreSQL 9.5 - ROLLBACK PREPARED") /
[9.4](/docs/9.4/sql-rollback-prepared.html "PostgreSQL 9.4 - ROLLBACK
PREPARED") / [9.3](/docs/9.3/sql-rollback-prepared.html "PostgreSQL 9.3 -
ROLLBACK PREPARED") / [9.2](/docs/9.2/sql-rollback-prepared.html "PostgreSQL
9.2 - ROLLBACK PREPARED") / [9.1](/docs/9.1/sql-rollback-prepared.html
"PostgreSQL 9.1 - ROLLBACK PREPARED") / [9.0](/docs/9.0/sql-rollback-
prepared.html "PostgreSQL 9.0 - ROLLBACK PREPARED") / [8.4](/docs/8.4/sql-
rollback-prepared.html "PostgreSQL 8.4 - ROLLBACK PREPARED") /
[8.3](/docs/8.3/sql-rollback-prepared.html "PostgreSQL 8.3 - ROLLBACK
PREPARED") / [8.2](/docs/8.2/sql-rollback-prepared.html "PostgreSQL 8.2 -
ROLLBACK PREPARED") / [8.1](/docs/8.1/sql-rollback-prepared.html "PostgreSQL
8.1 - ROLLBACK PREPARED")

__

ROLLBACK PREPARED  
---  
[Prev](sql-rollback.html "ROLLBACK")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-rollback-to.html "ROLLBACK TO SAVEPOINT")  
  
* * *

## ROLLBACK PREPARED

ROLLBACK PREPARED — cancel a transaction that was earlier prepared for two-
phase commit

## Synopsis

    
    
    ROLLBACK PREPARED _transaction_id_
    

## Description

`ROLLBACK PREPARED` rolls back a transaction that is in prepared state.

## Parameters

_`transaction_id`_

    

The transaction identifier of the transaction that is to be rolled back.

## Notes

To roll back a prepared transaction, you must be either the same user that
executed the transaction originally, or a superuser. But you do not have to be
in the same session that executed the transaction.

This command cannot be executed inside a transaction block. The prepared
transaction is rolled back immediately.

All currently available prepared transactions are listed in the
[`pg_prepared_xacts`](view-pg-prepared-xacts.html "54.16. pg_prepared_xacts")
system view.

## Examples

Roll back the transaction identified by the transaction identifier `foobar`:

    
    
    ROLLBACK PREPARED 'foobar';
    

## Compatibility

`ROLLBACK PREPARED` is a PostgreSQL extension. It is intended for use by
external transaction management systems, some of which are covered by
standards (such as X/Open XA), but the SQL side of those systems is not
standardized.

## See Also

[PREPARE TRANSACTION](sql-prepare-transaction.html "PREPARE TRANSACTION"),
[COMMIT PREPARED](sql-commit-prepared.html "COMMIT PREPARED")

* * *

[Prev](sql-rollback.html "ROLLBACK")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-rollback-to.html "ROLLBACK TO SAVEPOINT")  
---|---|---  
ROLLBACK  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ROLLBACK TO SAVEPOINT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-rollback-prepared.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

