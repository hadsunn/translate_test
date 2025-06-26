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

Supported Versions: [Current](/docs/current/sql-rollback.html "PostgreSQL 17 -
ROLLBACK") ([17](/docs/17/sql-rollback.html "PostgreSQL 17 - ROLLBACK")) /
[16](/docs/16/sql-rollback.html "PostgreSQL 16 - ROLLBACK") /
[15](/docs/15/sql-rollback.html "PostgreSQL 15 - ROLLBACK") /
[14](/docs/14/sql-rollback.html "PostgreSQL 14 - ROLLBACK") /
[13](/docs/13/sql-rollback.html "PostgreSQL 13 - ROLLBACK")

Development Versions: [18](/docs/18/sql-rollback.html "PostgreSQL 18 -
ROLLBACK") / [devel](/docs/devel/sql-rollback.html "PostgreSQL devel -
ROLLBACK")

Unsupported versions: [12](/docs/12/sql-rollback.html "PostgreSQL 12 -
ROLLBACK") / [11](/docs/11/sql-rollback.html "PostgreSQL 11 - ROLLBACK") /
[10](/docs/10/sql-rollback.html "PostgreSQL 10 - ROLLBACK") /
[9.6](/docs/9.6/sql-rollback.html "PostgreSQL 9.6 - ROLLBACK") /
[9.5](/docs/9.5/sql-rollback.html "PostgreSQL 9.5 - ROLLBACK") /
[9.4](/docs/9.4/sql-rollback.html "PostgreSQL 9.4 - ROLLBACK") /
[9.3](/docs/9.3/sql-rollback.html "PostgreSQL 9.3 - ROLLBACK") /
[9.2](/docs/9.2/sql-rollback.html "PostgreSQL 9.2 - ROLLBACK") /
[9.1](/docs/9.1/sql-rollback.html "PostgreSQL 9.1 - ROLLBACK") /
[9.0](/docs/9.0/sql-rollback.html "PostgreSQL 9.0 - ROLLBACK") /
[8.4](/docs/8.4/sql-rollback.html "PostgreSQL 8.4 - ROLLBACK") /
[8.3](/docs/8.3/sql-rollback.html "PostgreSQL 8.3 - ROLLBACK") /
[8.2](/docs/8.2/sql-rollback.html "PostgreSQL 8.2 - ROLLBACK") /
[8.1](/docs/8.1/sql-rollback.html "PostgreSQL 8.1 - ROLLBACK") /
[8.0](/docs/8.0/sql-rollback.html "PostgreSQL 8.0 - ROLLBACK") /
[7.4](/docs/7.4/sql-rollback.html "PostgreSQL 7.4 - ROLLBACK") /
[7.3](/docs/7.3/sql-rollback.html "PostgreSQL 7.3 - ROLLBACK") /
[7.2](/docs/7.2/sql-rollback.html "PostgreSQL 7.2 - ROLLBACK") /
[7.1](/docs/7.1/sql-rollback.html "PostgreSQL 7.1 - ROLLBACK")

__

ROLLBACK  
---  
[Prev](sql-revoke.html "REVOKE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-rollback-prepared.html "ROLLBACK PREPARED")  
  
* * *

## ROLLBACK

ROLLBACK — abort the current transaction

## Synopsis

    
    
    ROLLBACK [ WORK | TRANSACTION ] [ AND [ NO ] CHAIN ]
    

## Description

`ROLLBACK` rolls back the current transaction and causes all the updates made
by the transaction to be discarded.

## Parameters

`WORK`  
`TRANSACTION` #

    

Optional key words. They have no effect.

`AND CHAIN` #

    

If `AND CHAIN` is specified, a new (not aborted) transaction is immediately
started with the same transaction characteristics (see [SET TRANSACTION](sql-
set-transaction.html "SET TRANSACTION")) as the just finished one. Otherwise,
no new transaction is started.

## Notes

Use [`COMMIT`](sql-commit.html "COMMIT") to successfully terminate a
transaction.

Issuing `ROLLBACK` outside of a transaction block emits a warning and
otherwise has no effect. `ROLLBACK AND CHAIN` outside of a transaction block
is an error.

## Examples

To abort all changes:

    
    
    ROLLBACK;
    

## Compatibility

The command `ROLLBACK` conforms to the SQL standard. The form `ROLLBACK
TRANSACTION` is a PostgreSQL extension.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"), [ROLLBACK
TO SAVEPOINT](sql-rollback-to.html "ROLLBACK TO SAVEPOINT")

* * *

[Prev](sql-revoke.html "REVOKE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-rollback-prepared.html "ROLLBACK PREPARED")  
---|---|---  
REVOKE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ROLLBACK PREPARED  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-rollback.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

