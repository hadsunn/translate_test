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

Supported Versions: [Current](/docs/current/sql-commit.html "PostgreSQL 17 -
COMMIT") ([17](/docs/17/sql-commit.html "PostgreSQL 17 - COMMIT")) /
[16](/docs/16/sql-commit.html "PostgreSQL 16 - COMMIT") / [15](/docs/15/sql-
commit.html "PostgreSQL 15 - COMMIT") / [14](/docs/14/sql-commit.html
"PostgreSQL 14 - COMMIT") / [13](/docs/13/sql-commit.html "PostgreSQL 13 -
COMMIT")

Development Versions: [18](/docs/18/sql-commit.html "PostgreSQL 18 - COMMIT")
/ [devel](/docs/devel/sql-commit.html "PostgreSQL devel - COMMIT")

Unsupported versions: [12](/docs/12/sql-commit.html "PostgreSQL 12 - COMMIT")
/ [11](/docs/11/sql-commit.html "PostgreSQL 11 - COMMIT") / [10](/docs/10/sql-
commit.html "PostgreSQL 10 - COMMIT") / [9.6](/docs/9.6/sql-commit.html
"PostgreSQL 9.6 - COMMIT") / [9.5](/docs/9.5/sql-commit.html "PostgreSQL 9.5 -
COMMIT") / [9.4](/docs/9.4/sql-commit.html "PostgreSQL 9.4 - COMMIT") /
[9.3](/docs/9.3/sql-commit.html "PostgreSQL 9.3 - COMMIT") /
[9.2](/docs/9.2/sql-commit.html "PostgreSQL 9.2 - COMMIT") /
[9.1](/docs/9.1/sql-commit.html "PostgreSQL 9.1 - COMMIT") /
[9.0](/docs/9.0/sql-commit.html "PostgreSQL 9.0 - COMMIT") /
[8.4](/docs/8.4/sql-commit.html "PostgreSQL 8.4 - COMMIT") /
[8.3](/docs/8.3/sql-commit.html "PostgreSQL 8.3 - COMMIT") /
[8.2](/docs/8.2/sql-commit.html "PostgreSQL 8.2 - COMMIT") /
[8.1](/docs/8.1/sql-commit.html "PostgreSQL 8.1 - COMMIT") /
[8.0](/docs/8.0/sql-commit.html "PostgreSQL 8.0 - COMMIT") /
[7.4](/docs/7.4/sql-commit.html "PostgreSQL 7.4 - COMMIT") /
[7.3](/docs/7.3/sql-commit.html "PostgreSQL 7.3 - COMMIT") /
[7.2](/docs/7.2/sql-commit.html "PostgreSQL 7.2 - COMMIT") /
[7.1](/docs/7.1/sql-commit.html "PostgreSQL 7.1 - COMMIT")

__

COMMIT  
---  
[Prev](sql-comment.html "COMMENT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-commit-prepared.html "COMMIT PREPARED")  
  
* * *

## COMMIT

COMMIT — commit the current transaction

## Synopsis

    
    
    COMMIT [ WORK | TRANSACTION ] [ AND [ NO ] CHAIN ]
    

## Description

`COMMIT` commits the current transaction. All changes made by the transaction
become visible to others and are guaranteed to be durable if a crash occurs.

## Parameters

`WORK`  
`TRANSACTION` #

    

Optional key words. They have no effect.

`AND CHAIN` #

    

If `AND CHAIN` is specified, a new transaction is immediately started with the
same transaction characteristics (see [SET TRANSACTION](sql-set-
transaction.html "SET TRANSACTION")) as the just finished one. Otherwise, no
new transaction is started.

## Notes

Use [ROLLBACK](sql-rollback.html "ROLLBACK") to abort a transaction.

Issuing `COMMIT` when not inside a transaction does no harm, but it will
provoke a warning message. `COMMIT AND CHAIN` when not inside a transaction is
an error.

## Examples

To commit the current transaction and make all changes permanent:

    
    
    COMMIT;
    

## Compatibility

The command `COMMIT` conforms to the SQL standard. The form `COMMIT
TRANSACTION` is a PostgreSQL extension.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [ROLLBACK](sql-rollback.html "ROLLBACK")

* * *

[Prev](sql-comment.html "COMMENT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-commit-prepared.html "COMMIT PREPARED")  
---|---|---  
COMMENT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  COMMIT PREPARED  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-commit.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

