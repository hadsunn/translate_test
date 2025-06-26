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

Supported Versions: [Current](/docs/current/sql-begin.html "PostgreSQL 17 -
BEGIN") ([17](/docs/17/sql-begin.html "PostgreSQL 17 - BEGIN")) /
[16](/docs/16/sql-begin.html "PostgreSQL 16 - BEGIN") / [15](/docs/15/sql-
begin.html "PostgreSQL 15 - BEGIN") / [14](/docs/14/sql-begin.html "PostgreSQL
14 - BEGIN") / [13](/docs/13/sql-begin.html "PostgreSQL 13 - BEGIN")

Development Versions: [18](/docs/18/sql-begin.html "PostgreSQL 18 - BEGIN") /
[devel](/docs/devel/sql-begin.html "PostgreSQL devel - BEGIN")

Unsupported versions: [12](/docs/12/sql-begin.html "PostgreSQL 12 - BEGIN") /
[11](/docs/11/sql-begin.html "PostgreSQL 11 - BEGIN") / [10](/docs/10/sql-
begin.html "PostgreSQL 10 - BEGIN") / [9.6](/docs/9.6/sql-begin.html
"PostgreSQL 9.6 - BEGIN") / [9.5](/docs/9.5/sql-begin.html "PostgreSQL 9.5 -
BEGIN") / [9.4](/docs/9.4/sql-begin.html "PostgreSQL 9.4 - BEGIN") /
[9.3](/docs/9.3/sql-begin.html "PostgreSQL 9.3 - BEGIN") /
[9.2](/docs/9.2/sql-begin.html "PostgreSQL 9.2 - BEGIN") /
[9.1](/docs/9.1/sql-begin.html "PostgreSQL 9.1 - BEGIN") /
[9.0](/docs/9.0/sql-begin.html "PostgreSQL 9.0 - BEGIN") /
[8.4](/docs/8.4/sql-begin.html "PostgreSQL 8.4 - BEGIN") /
[8.3](/docs/8.3/sql-begin.html "PostgreSQL 8.3 - BEGIN") /
[8.2](/docs/8.2/sql-begin.html "PostgreSQL 8.2 - BEGIN") /
[8.1](/docs/8.1/sql-begin.html "PostgreSQL 8.1 - BEGIN") /
[8.0](/docs/8.0/sql-begin.html "PostgreSQL 8.0 - BEGIN") /
[7.4](/docs/7.4/sql-begin.html "PostgreSQL 7.4 - BEGIN") /
[7.3](/docs/7.3/sql-begin.html "PostgreSQL 7.3 - BEGIN") /
[7.2](/docs/7.2/sql-begin.html "PostgreSQL 7.2 - BEGIN") /
[7.1](/docs/7.1/sql-begin.html "PostgreSQL 7.1 - BEGIN")

__

BEGIN  
---  
[Prev](sql-analyze.html "ANALYZE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-call.html "CALL")  
  
* * *

## BEGIN

BEGIN — start a transaction block

## Synopsis

    
    
    BEGIN [ WORK | TRANSACTION ] [ _transaction_mode_ [, ...] ]
    
    where _transaction_mode_ is one of:
    
        ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
        READ WRITE | READ ONLY
        [ NOT ] DEFERRABLE
    

## Description

`BEGIN` initiates a transaction block, that is, all statements after a `BEGIN`
command will be executed in a single transaction until an explicit
[`COMMIT`](sql-commit.html "COMMIT") or [`ROLLBACK`](sql-rollback.html
"ROLLBACK") is given. By default (without `BEGIN`), PostgreSQL executes
transactions in “autocommit” mode, that is, each statement is executed in its
own transaction and a commit is implicitly performed at the end of the
statement (if execution was successful, otherwise a rollback is done).

Statements are executed more quickly in a transaction block, because
transaction start/commit requires significant CPU and disk activity. Execution
of multiple statements inside a transaction is also useful to ensure
consistency when making several related changes: other sessions will be unable
to see the intermediate states wherein not all the related updates have been
done.

If the isolation level, read/write mode, or deferrable mode is specified, the
new transaction has those characteristics, as if [`SET TRANSACTION`](sql-set-
transaction.html "SET TRANSACTION") was executed.

## Parameters

`WORK`  
`TRANSACTION`

    

Optional key words. They have no effect.

Refer to [SET TRANSACTION](sql-set-transaction.html "SET TRANSACTION") for
information on the meaning of the other parameters to this statement.

## Notes

[`START TRANSACTION`](sql-start-transaction.html "START TRANSACTION") has the
same functionality as `BEGIN`.

Use [`COMMIT`](sql-commit.html "COMMIT") or [`ROLLBACK`](sql-rollback.html
"ROLLBACK") to terminate a transaction block.

Issuing `BEGIN` when already inside a transaction block will provoke a warning
message. The state of the transaction is not affected. To nest transactions
within a transaction block, use savepoints (see [SAVEPOINT](sql-savepoint.html
"SAVEPOINT")).

For reasons of backwards compatibility, the commas between successive
_`transaction_modes`_ can be omitted.

## Examples

To begin a transaction block:

    
    
    BEGIN;
    

## Compatibility

`BEGIN` is a PostgreSQL language extension. It is equivalent to the SQL-
standard command [`START TRANSACTION`](sql-start-transaction.html "START
TRANSACTION"), whose reference page contains additional compatibility
information.

The `DEFERRABLE` _`transaction_mode`_ is a PostgreSQL language extension.

Incidentally, the `BEGIN` key word is used for a different purpose in embedded
SQL. You are advised to be careful about the transaction semantics when
porting database applications.

## See Also

[COMMIT](sql-commit.html "COMMIT"), [ROLLBACK](sql-rollback.html "ROLLBACK"),
[START TRANSACTION](sql-start-transaction.html "START TRANSACTION"),
[SAVEPOINT](sql-savepoint.html "SAVEPOINT")

* * *

[Prev](sql-analyze.html "ANALYZE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-call.html "CALL")  
---|---|---  
ANALYZE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CALL  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-begin.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

