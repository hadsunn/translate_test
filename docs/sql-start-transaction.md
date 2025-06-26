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

Supported Versions: [Current](/docs/current/sql-start-transaction.html
"PostgreSQL 17 - START TRANSACTION") ([17](/docs/17/sql-start-transaction.html
"PostgreSQL 17 - START TRANSACTION")) / [16](/docs/16/sql-start-
transaction.html "PostgreSQL 16 - START TRANSACTION") / [15](/docs/15/sql-
start-transaction.html "PostgreSQL 15 - START TRANSACTION") /
[14](/docs/14/sql-start-transaction.html "PostgreSQL 14 - START TRANSACTION")
/ [13](/docs/13/sql-start-transaction.html "PostgreSQL 13 - START
TRANSACTION")

Development Versions: [18](/docs/18/sql-start-transaction.html "PostgreSQL 18
- START TRANSACTION") / [devel](/docs/devel/sql-start-transaction.html
"PostgreSQL devel - START TRANSACTION")

Unsupported versions: [12](/docs/12/sql-start-transaction.html "PostgreSQL 12
- START TRANSACTION") / [11](/docs/11/sql-start-transaction.html "PostgreSQL
11 - START TRANSACTION") / [10](/docs/10/sql-start-transaction.html
"PostgreSQL 10 - START TRANSACTION") / [9.6](/docs/9.6/sql-start-
transaction.html "PostgreSQL 9.6 - START TRANSACTION") / [9.5](/docs/9.5/sql-
start-transaction.html "PostgreSQL 9.5 - START TRANSACTION") /
[9.4](/docs/9.4/sql-start-transaction.html "PostgreSQL 9.4 - START
TRANSACTION") / [9.3](/docs/9.3/sql-start-transaction.html "PostgreSQL 9.3 -
START TRANSACTION") / [9.2](/docs/9.2/sql-start-transaction.html "PostgreSQL
9.2 - START TRANSACTION") / [9.1](/docs/9.1/sql-start-transaction.html
"PostgreSQL 9.1 - START TRANSACTION") / [9.0](/docs/9.0/sql-start-
transaction.html "PostgreSQL 9.0 - START TRANSACTION") / [8.4](/docs/8.4/sql-
start-transaction.html "PostgreSQL 8.4 - START TRANSACTION") /
[8.3](/docs/8.3/sql-start-transaction.html "PostgreSQL 8.3 - START
TRANSACTION") / [8.2](/docs/8.2/sql-start-transaction.html "PostgreSQL 8.2 -
START TRANSACTION") / [8.1](/docs/8.1/sql-start-transaction.html "PostgreSQL
8.1 - START TRANSACTION") / [8.0](/docs/8.0/sql-start-transaction.html
"PostgreSQL 8.0 - START TRANSACTION") / [7.4](/docs/7.4/sql-start-
transaction.html "PostgreSQL 7.4 - START TRANSACTION") / [7.3](/docs/7.3/sql-
start-transaction.html "PostgreSQL 7.3 - START TRANSACTION")

__

START TRANSACTION  
---  
[Prev](sql-show.html "SHOW")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-truncate.html "TRUNCATE")  
  
* * *

## START TRANSACTION

START TRANSACTION — start a transaction block

## Synopsis

    
    
    START TRANSACTION [ _transaction_mode_ [, ...] ]
    
    where _transaction_mode_ is one of:
    
        ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
        READ WRITE | READ ONLY
        [ NOT ] DEFERRABLE
    

## Description

This command begins a new transaction block. If the isolation level,
read/write mode, or deferrable mode is specified, the new transaction has
those characteristics, as if [`SET TRANSACTION`](sql-set-transaction.html "SET
TRANSACTION") was executed. This is the same as the [`BEGIN`](sql-begin.html
"BEGIN") command.

## Parameters

Refer to [SET TRANSACTION](sql-set-transaction.html "SET TRANSACTION") for
information on the meaning of the parameters to this statement.

## Compatibility

In the standard, it is not necessary to issue `START TRANSACTION` to start a
transaction block: any SQL command implicitly begins a block. PostgreSQL's
behavior can be seen as implicitly issuing a `COMMIT` after each command that
does not follow `START TRANSACTION` (or `BEGIN`), and it is therefore often
called “autocommit”. Other relational database systems might offer an
autocommit feature as a convenience.

The `DEFERRABLE` _`transaction_mode`_ is a PostgreSQL language extension.

The SQL standard requires commas between successive _`transaction_modes`_ ,
but for historical reasons PostgreSQL allows the commas to be omitted.

See also the compatibility section of [SET TRANSACTION](sql-set-
transaction.html "SET TRANSACTION").

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"),
[ROLLBACK](sql-rollback.html "ROLLBACK"), [SAVEPOINT](sql-savepoint.html
"SAVEPOINT"), [SET TRANSACTION](sql-set-transaction.html "SET TRANSACTION")

* * *

[Prev](sql-show.html "SHOW")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-truncate.html "TRUNCATE")  
---|---|---  
SHOW  | [Home](index.html "PostgreSQL 16.9 Documentation") |  TRUNCATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-start-transaction.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

