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

Supported Versions: [Current](/docs/current/sql-set-transaction.html
"PostgreSQL 17 - SET TRANSACTION") ([17](/docs/17/sql-set-transaction.html
"PostgreSQL 17 - SET TRANSACTION")) / [16](/docs/16/sql-set-transaction.html
"PostgreSQL 16 - SET TRANSACTION") / [15](/docs/15/sql-set-transaction.html
"PostgreSQL 15 - SET TRANSACTION") / [14](/docs/14/sql-set-transaction.html
"PostgreSQL 14 - SET TRANSACTION") / [13](/docs/13/sql-set-transaction.html
"PostgreSQL 13 - SET TRANSACTION")

Development Versions: [18](/docs/18/sql-set-transaction.html "PostgreSQL 18 -
SET TRANSACTION") / [devel](/docs/devel/sql-set-transaction.html "PostgreSQL
devel - SET TRANSACTION")

Unsupported versions: [12](/docs/12/sql-set-transaction.html "PostgreSQL 12 -
SET TRANSACTION") / [11](/docs/11/sql-set-transaction.html "PostgreSQL 11 -
SET TRANSACTION") / [10](/docs/10/sql-set-transaction.html "PostgreSQL 10 -
SET TRANSACTION") / [9.6](/docs/9.6/sql-set-transaction.html "PostgreSQL 9.6 -
SET TRANSACTION") / [9.5](/docs/9.5/sql-set-transaction.html "PostgreSQL 9.5 -
SET TRANSACTION") / [9.4](/docs/9.4/sql-set-transaction.html "PostgreSQL 9.4 -
SET TRANSACTION") / [9.3](/docs/9.3/sql-set-transaction.html "PostgreSQL 9.3 -
SET TRANSACTION") / [9.2](/docs/9.2/sql-set-transaction.html "PostgreSQL 9.2 -
SET TRANSACTION") / [9.1](/docs/9.1/sql-set-transaction.html "PostgreSQL 9.1 -
SET TRANSACTION") / [9.0](/docs/9.0/sql-set-transaction.html "PostgreSQL 9.0 -
SET TRANSACTION") / [8.4](/docs/8.4/sql-set-transaction.html "PostgreSQL 8.4 -
SET TRANSACTION") / [8.3](/docs/8.3/sql-set-transaction.html "PostgreSQL 8.3 -
SET TRANSACTION") / [8.2](/docs/8.2/sql-set-transaction.html "PostgreSQL 8.2 -
SET TRANSACTION") / [8.1](/docs/8.1/sql-set-transaction.html "PostgreSQL 8.1 -
SET TRANSACTION") / [8.0](/docs/8.0/sql-set-transaction.html "PostgreSQL 8.0 -
SET TRANSACTION") / [7.4](/docs/7.4/sql-set-transaction.html "PostgreSQL 7.4 -
SET TRANSACTION") / [7.3](/docs/7.3/sql-set-transaction.html "PostgreSQL 7.3 -
SET TRANSACTION") / [7.2](/docs/7.2/sql-set-transaction.html "PostgreSQL 7.2 -
SET TRANSACTION") / [7.1](/docs/7.1/sql-set-transaction.html "PostgreSQL 7.1 -
SET TRANSACTION")

__

SET TRANSACTION  
---  
[Prev](sql-set-session-authorization.html "SET SESSION AUTHORIZATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-show.html "SHOW")  
  
* * *

## SET TRANSACTION

SET TRANSACTION — set the characteristics of the current transaction

## Synopsis

    
    
    SET TRANSACTION _transaction_mode_ [, ...]
    SET TRANSACTION SNAPSHOT _snapshot_id_
    SET SESSION CHARACTERISTICS AS TRANSACTION _transaction_mode_ [, ...]
    
    where _transaction_mode_ is one of:
    
        ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
        READ WRITE | READ ONLY
        [ NOT ] DEFERRABLE
    

## Description

The `SET TRANSACTION` command sets the characteristics of the current
transaction. It has no effect on any subsequent transactions. `SET SESSION
CHARACTERISTICS` sets the default transaction characteristics for subsequent
transactions of a session. These defaults can be overridden by `SET
TRANSACTION` for an individual transaction.

The available transaction characteristics are the transaction isolation level,
the transaction access mode (read/write or read-only), and the deferrable
mode. In addition, a snapshot can be selected, though only for the current
transaction, not as a session default.

The isolation level of a transaction determines what data the transaction can
see when other transactions are running concurrently:

`READ COMMITTED`

    

A statement can only see rows committed before it began. This is the default.

`REPEATABLE READ`

    

All statements of the current transaction can only see rows committed before
the first query or data-modification statement was executed in this
transaction.

`SERIALIZABLE`

    

All statements of the current transaction can only see rows committed before
the first query or data-modification statement was executed in this
transaction. If a pattern of reads and writes among concurrent serializable
transactions would create a situation which could not have occurred for any
serial (one-at-a-time) execution of those transactions, one of them will be
rolled back with a `serialization_failure` error.

The SQL standard defines one additional level, `READ UNCOMMITTED`. In
PostgreSQL `READ UNCOMMITTED` is treated as `READ COMMITTED`.

The transaction isolation level cannot be changed after the first query or
data-modification statement (`SELECT`, `INSERT`, `DELETE`, `UPDATE`, `MERGE`,
`FETCH`, or `COPY`) of a transaction has been executed. See [Chapter
13](mvcc.html "Chapter 13. Concurrency Control") for more information about
transaction isolation and concurrency control.

The transaction access mode determines whether the transaction is read/write
or read-only. Read/write is the default. When a transaction is read-only, the
following SQL commands are disallowed: `INSERT`, `UPDATE`, `DELETE`, `MERGE`,
and `COPY FROM` if the table they would write to is not a temporary table; all
`CREATE`, `ALTER`, and `DROP` commands; `COMMENT`, `GRANT`, `REVOKE`,
`TRUNCATE`; and `EXPLAIN ANALYZE` and `EXECUTE` if the command they would
execute is among those listed. This is a high-level notion of read-only that
does not prevent all writes to disk.

The `DEFERRABLE` transaction property has no effect unless the transaction is
also `SERIALIZABLE` and `READ ONLY`. When all three of these properties are
selected for a transaction, the transaction may block when first acquiring its
snapshot, after which it is able to run without the normal overhead of a
`SERIALIZABLE` transaction and without any risk of contributing to or being
canceled by a serialization failure. This mode is well suited for long-running
reports or backups.

The `SET TRANSACTION SNAPSHOT` command allows a new transaction to run with
the same _snapshot_ as an existing transaction. The pre-existing transaction
must have exported its snapshot with the `pg_export_snapshot` function (see
[Section 9.27.5](functions-admin.html#FUNCTIONS-SNAPSHOT-SYNCHRONIZATION
"9.27.5. Snapshot Synchronization Functions")). That function returns a
snapshot identifier, which must be given to `SET TRANSACTION SNAPSHOT` to
specify which snapshot is to be imported. The identifier must be written as a
string literal in this command, for example `'00000003-0000001B-1'`. `SET
TRANSACTION SNAPSHOT` can only be executed at the start of a transaction,
before the first query or data-modification statement (`SELECT`, `INSERT`,
`DELETE`, `UPDATE`, `MERGE`, `FETCH`, or `COPY`) of the transaction.
Furthermore, the transaction must already be set to `SERIALIZABLE` or
`REPEATABLE READ` isolation level (otherwise, the snapshot would be discarded
immediately, since `READ COMMITTED` mode takes a new snapshot for each
command). If the importing transaction uses `SERIALIZABLE` isolation level,
then the transaction that exported the snapshot must also use that isolation
level. Also, a non-read-only serializable transaction cannot import a snapshot
from a read-only transaction.

## Notes

If `SET TRANSACTION` is executed without a prior `START TRANSACTION` or
`BEGIN`, it emits a warning and otherwise has no effect.

It is possible to dispense with `SET TRANSACTION` by instead specifying the
desired _`transaction_modes`_ in `BEGIN` or `START TRANSACTION`. But that
option is not available for `SET TRANSACTION SNAPSHOT`.

The session default transaction modes can also be set or examined via the
configuration parameters [default_transaction_isolation](runtime-config-
client.html#GUC-DEFAULT-TRANSACTION-ISOLATION),
[default_transaction_read_only](runtime-config-client.html#GUC-DEFAULT-
TRANSACTION-READ-ONLY), and [default_transaction_deferrable](runtime-config-
client.html#GUC-DEFAULT-TRANSACTION-DEFERRABLE). (In fact `SET SESSION
CHARACTERISTICS` is just a verbose equivalent for setting these variables with
`SET`.) This means the defaults can be set in the configuration file, via
`ALTER DATABASE`, etc. Consult [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") for more information.

The current transaction's modes can similarly be set or examined via the
configuration parameters [transaction_isolation](runtime-config-
client.html#GUC-TRANSACTION-ISOLATION), [transaction_read_only](runtime-
config-client.html#GUC-TRANSACTION-READ-ONLY), and
[transaction_deferrable](runtime-config-client.html#GUC-TRANSACTION-
DEFERRABLE). Setting one of these parameters acts the same as the
corresponding `SET TRANSACTION` option, with the same restrictions on when it
can be done. However, these parameters cannot be set in the configuration
file, or from any source other than live SQL.

## Examples

To begin a new transaction with the same snapshot as an already existing
transaction, first export the snapshot from the existing transaction. That
will return the snapshot identifier, for example:

    
    
    BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;
    SELECT pg_export_snapshot();
     pg_export_snapshot
    ---------------------
     00000003-0000001B-1
    (1 row)
    

Then give the snapshot identifier in a `SET TRANSACTION SNAPSHOT` command at
the beginning of the newly opened transaction:

    
    
    BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;
    SET TRANSACTION SNAPSHOT '00000003-0000001B-1';
    

## Compatibility

These commands are defined in the SQL standard, except for the `DEFERRABLE`
transaction mode and the `SET TRANSACTION SNAPSHOT` form, which are PostgreSQL
extensions.

`SERIALIZABLE` is the default transaction isolation level in the standard. In
PostgreSQL the default is ordinarily `READ COMMITTED`, but you can change it
as mentioned above.

In the SQL standard, there is one other transaction characteristic that can be
set with these commands: the size of the diagnostics area. This concept is
specific to embedded SQL, and therefore is not implemented in the PostgreSQL
server.

The SQL standard requires commas between successive _`transaction_modes`_ ,
but for historical reasons PostgreSQL allows the commas to be omitted.

* * *

[Prev](sql-set-session-authorization.html "SET SESSION AUTHORIZATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-show.html "SHOW")  
---|---|---  
SET SESSION AUTHORIZATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SHOW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-set-transaction.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

