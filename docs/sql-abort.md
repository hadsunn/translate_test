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

Supported Versions: [Current](/docs/current/sql-abort.html "PostgreSQL 17 -
ABORT") ([17](/docs/17/sql-abort.html "PostgreSQL 17 - ABORT")) /
[16](/docs/16/sql-abort.html "PostgreSQL 16 - ABORT") / [15](/docs/15/sql-
abort.html "PostgreSQL 15 - ABORT") / [14](/docs/14/sql-abort.html "PostgreSQL
14 - ABORT") / [13](/docs/13/sql-abort.html "PostgreSQL 13 - ABORT")

Development Versions: [18](/docs/18/sql-abort.html "PostgreSQL 18 - ABORT") /
[devel](/docs/devel/sql-abort.html "PostgreSQL devel - ABORT")

Unsupported versions: [12](/docs/12/sql-abort.html "PostgreSQL 12 - ABORT") /
[11](/docs/11/sql-abort.html "PostgreSQL 11 - ABORT") / [10](/docs/10/sql-
abort.html "PostgreSQL 10 - ABORT") / [9.6](/docs/9.6/sql-abort.html
"PostgreSQL 9.6 - ABORT") / [9.5](/docs/9.5/sql-abort.html "PostgreSQL 9.5 -
ABORT") / [9.4](/docs/9.4/sql-abort.html "PostgreSQL 9.4 - ABORT") /
[9.3](/docs/9.3/sql-abort.html "PostgreSQL 9.3 - ABORT") /
[9.2](/docs/9.2/sql-abort.html "PostgreSQL 9.2 - ABORT") /
[9.1](/docs/9.1/sql-abort.html "PostgreSQL 9.1 - ABORT") /
[9.0](/docs/9.0/sql-abort.html "PostgreSQL 9.0 - ABORT") /
[8.4](/docs/8.4/sql-abort.html "PostgreSQL 8.4 - ABORT") /
[8.3](/docs/8.3/sql-abort.html "PostgreSQL 8.3 - ABORT") /
[8.2](/docs/8.2/sql-abort.html "PostgreSQL 8.2 - ABORT") /
[8.1](/docs/8.1/sql-abort.html "PostgreSQL 8.1 - ABORT") /
[8.0](/docs/8.0/sql-abort.html "PostgreSQL 8.0 - ABORT") /
[7.4](/docs/7.4/sql-abort.html "PostgreSQL 7.4 - ABORT") /
[7.3](/docs/7.3/sql-abort.html "PostgreSQL 7.3 - ABORT") /
[7.2](/docs/7.2/sql-abort.html "PostgreSQL 7.2 - ABORT") /
[7.1](/docs/7.1/sql-abort.html "PostgreSQL 7.1 - ABORT")

__

ABORT  
---  
[Prev](sql-commands.html "SQL Commands")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alteraggregate.html "ALTER AGGREGATE")  
  
* * *

## ABORT

ABORT — abort the current transaction

## Synopsis

    
    
    ABORT [ WORK | TRANSACTION ] [ AND [ NO ] CHAIN ]
    

## Description

`ABORT` rolls back the current transaction and causes all the updates made by
the transaction to be discarded. This command is identical in behavior to the
standard SQL command [`ROLLBACK`](sql-rollback.html "ROLLBACK"), and is
present only for historical reasons.

## Parameters

`WORK`  
`TRANSACTION`

    

Optional key words. They have no effect.

`AND CHAIN`

    

If `AND CHAIN` is specified, a new transaction is immediately started with the
same transaction characteristics (see [`SET TRANSACTION`](sql-set-
transaction.html "SET TRANSACTION")) as the just finished one. Otherwise, no
new transaction is started.

## Notes

Use [`COMMIT`](sql-commit.html "COMMIT") to successfully terminate a
transaction.

Issuing `ABORT` outside of a transaction block emits a warning and otherwise
has no effect.

## Examples

To abort all changes:

    
    
    ABORT;
    

## Compatibility

This command is a PostgreSQL extension present for historical reasons.
`ROLLBACK` is the equivalent standard SQL command.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"),
[ROLLBACK](sql-rollback.html "ROLLBACK")

* * *

[Prev](sql-commands.html "SQL Commands")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alteraggregate.html "ALTER AGGREGATE")  
---|---|---  
SQL Commands  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER AGGREGATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-abort.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

