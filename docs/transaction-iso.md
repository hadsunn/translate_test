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

Supported Versions: [Current](/docs/current/transaction-iso.html "PostgreSQL
17 - 13.2. Transaction Isolation") ([17](/docs/17/transaction-iso.html
"PostgreSQL 17 - 13.2. Transaction Isolation")) / [16](/docs/16/transaction-
iso.html "PostgreSQL 16 - 13.2. Transaction Isolation") /
[15](/docs/15/transaction-iso.html "PostgreSQL 15 - 13.2. Transaction
Isolation") / [14](/docs/14/transaction-iso.html "PostgreSQL 14 -
13.2. Transaction Isolation") / [13](/docs/13/transaction-iso.html "PostgreSQL
13 - 13.2. Transaction Isolation")

Development Versions: [18](/docs/18/transaction-iso.html "PostgreSQL 18 -
13.2. Transaction Isolation") / [devel](/docs/devel/transaction-iso.html
"PostgreSQL devel - 13.2. Transaction Isolation")

Unsupported versions: [12](/docs/12/transaction-iso.html "PostgreSQL 12 -
13.2. Transaction Isolation") / [11](/docs/11/transaction-iso.html "PostgreSQL
11 - 13.2. Transaction Isolation") / [10](/docs/10/transaction-iso.html
"PostgreSQL 10 - 13.2. Transaction Isolation") / [9.6](/docs/9.6/transaction-
iso.html "PostgreSQL 9.6 - 13.2. Transaction Isolation") /
[9.5](/docs/9.5/transaction-iso.html "PostgreSQL 9.5 - 13.2. Transaction
Isolation") / [9.4](/docs/9.4/transaction-iso.html "PostgreSQL 9.4 -
13.2. Transaction Isolation") / [9.3](/docs/9.3/transaction-iso.html
"PostgreSQL 9.3 - 13.2. Transaction Isolation") / [9.2](/docs/9.2/transaction-
iso.html "PostgreSQL 9.2 - 13.2. Transaction Isolation") /
[9.1](/docs/9.1/transaction-iso.html "PostgreSQL 9.1 - 13.2. Transaction
Isolation") / [9.0](/docs/9.0/transaction-iso.html "PostgreSQL 9.0 -
13.2. Transaction Isolation") / [8.4](/docs/8.4/transaction-iso.html
"PostgreSQL 8.4 - 13.2. Transaction Isolation") / [8.3](/docs/8.3/transaction-
iso.html "PostgreSQL 8.3 - 13.2. Transaction Isolation") /
[8.2](/docs/8.2/transaction-iso.html "PostgreSQL 8.2 - 13.2. Transaction
Isolation") / [8.1](/docs/8.1/transaction-iso.html "PostgreSQL 8.1 -
13.2. Transaction Isolation") / [8.0](/docs/8.0/transaction-iso.html
"PostgreSQL 8.0 - 13.2. Transaction Isolation") / [7.4](/docs/7.4/transaction-
iso.html "PostgreSQL 7.4 - 13.2. Transaction Isolation") /
[7.3](/docs/7.3/transaction-iso.html "PostgreSQL 7.3 - 13.2. Transaction
Isolation") / [7.2](/docs/7.2/transaction-iso.html "PostgreSQL 7.2 -
13.2. Transaction Isolation") / [7.1](/docs/7.1/transaction-iso.html
"PostgreSQL 7.1 - 13.2. Transaction Isolation")

__

13.2. Transaction Isolation  
---  
[Prev](mvcc-intro.html "13.1. Introduction")  | [Up](mvcc.html "Chapter 13. Concurrency Control") | Chapter 13. Concurrency Control | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](explicit-locking.html "13.3. Explicit Locking")  
  
* * *

## 13.2. Transaction Isolation #

[13.2.1. Read Committed Isolation Level](transaction-iso.html#XACT-READ-
COMMITTED)

[13.2.2. Repeatable Read Isolation Level](transaction-iso.html#XACT-
REPEATABLE-READ)

[13.2.3. Serializable Isolation Level](transaction-iso.html#XACT-SERIALIZABLE)

The SQL standard defines four levels of transaction isolation. The most strict
is Serializable, which is defined by the standard in a paragraph which says
that any concurrent execution of a set of Serializable transactions is
guaranteed to produce the same effect as running them one at a time in some
order. The other three levels are defined in terms of phenomena, resulting
from interaction between concurrent transactions, which must not occur at each
level. The standard notes that due to the definition of Serializable, none of
these phenomena are possible at that level. (This is hardly surprising -- if
the effect of the transactions must be consistent with having been run one at
a time, how could you see any phenomena caused by interactions?)

The phenomena which are prohibited at various levels are:

dirty read

    

A transaction reads data written by a concurrent uncommitted transaction.

nonrepeatable read

    

A transaction re-reads data it has previously read and finds that data has
been modified by another transaction (that committed since the initial read).

phantom read

    

A transaction re-executes a query returning a set of rows that satisfy a
search condition and finds that the set of rows satisfying the condition has
changed due to another recently-committed transaction.

serialization anomaly

    

The result of successfully committing a group of transactions is inconsistent
with all possible orderings of running those transactions one at a time.

The SQL standard and PostgreSQL-implemented transaction isolation levels are
described in [Table 13.1](transaction-iso.html#MVCC-ISOLEVEL-TABLE
"Table 13.1. Transaction Isolation Levels").

**Table  13.1. Transaction Isolation Levels**

Isolation Level | Dirty Read | Nonrepeatable Read | Phantom Read | Serialization Anomaly  
---|---|---|---|---  
Read uncommitted | Allowed, but not in PG | Possible | Possible | Possible  
Read committed | Not possible | Possible | Possible | Possible  
Repeatable read | Not possible | Not possible | Allowed, but not in PG | Possible  
Serializable | Not possible | Not possible | Not possible | Not possible  
  
  

In PostgreSQL, you can request any of the four standard transaction isolation
levels, but internally only three distinct isolation levels are implemented,
i.e., PostgreSQL's Read Uncommitted mode behaves like Read Committed. This is
because it is the only sensible way to map the standard isolation levels to
PostgreSQL's multiversion concurrency control architecture.

The table also shows that PostgreSQL's Repeatable Read implementation does not
allow phantom reads. This is acceptable under the SQL standard because the
standard specifies which anomalies must _not_ occur at certain isolation
levels; higher guarantees are acceptable. The behavior of the available
isolation levels is detailed in the following subsections.

To set the transaction isolation level of a transaction, use the command [SET
TRANSACTION](sql-set-transaction.html "SET TRANSACTION").

### Important

Some PostgreSQL data types and functions have special rules regarding
transactional behavior. In particular, changes made to a sequence (and
therefore the counter of a column declared using `serial`) are immediately
visible to all other transactions and are not rolled back if the transaction
that made the changes aborts. See [Section 9.17](functions-sequence.html
"9.17. Sequence Manipulation Functions") and [Section 8.1.4](datatype-
numeric.html#DATATYPE-SERIAL "8.1.4. Serial Types").

### 13.2.1. Read Committed Isolation Level #

_Read Committed_ is the default isolation level in PostgreSQL. When a
transaction uses this isolation level, a `SELECT` query (without a `FOR
UPDATE/SHARE` clause) sees only data committed before the query began; it
never sees either uncommitted data or changes committed by concurrent
transactions during the query's execution. In effect, a `SELECT` query sees a
snapshot of the database as of the instant the query begins to run. However,
`SELECT` does see the effects of previous updates executed within its own
transaction, even though they are not yet committed. Also note that two
successive `SELECT` commands can see different data, even though they are
within a single transaction, if other transactions commit changes after the
first `SELECT` starts and before the second `SELECT` starts.

`UPDATE`, `DELETE`, `SELECT FOR UPDATE`, and `SELECT FOR SHARE` commands
behave the same as `SELECT` in terms of searching for target rows: they will
only find target rows that were committed as of the command start time.
However, such a target row might have already been updated (or deleted or
locked) by another concurrent transaction by the time it is found. In this
case, the would-be updater will wait for the first updating transaction to
commit or roll back (if it is still in progress). If the first updater rolls
back, then its effects are negated and the second updater can proceed with
updating the originally found row. If the first updater commits, the second
updater will ignore the row if the first updater deleted it, otherwise it will
attempt to apply its operation to the updated version of the row. The search
condition of the command (the `WHERE` clause) is re-evaluated to see if the
updated version of the row still matches the search condition. If so, the
second updater proceeds with its operation using the updated version of the
row. In the case of `SELECT FOR UPDATE` and `SELECT FOR SHARE`, this means it
is the updated version of the row that is locked and returned to the client.

`INSERT` with an `ON CONFLICT DO UPDATE` clause behaves similarly. In Read
Committed mode, each row proposed for insertion will either insert or update.
Unless there are unrelated errors, one of those two outcomes is guaranteed. If
a conflict originates in another transaction whose effects are not yet visible
to the `INSERT`, the `UPDATE` clause will affect that row, even though
possibly _no_ version of that row is conventionally visible to the command.

`INSERT` with an `ON CONFLICT DO NOTHING` clause may have insertion not
proceed for a row due to the outcome of another transaction whose effects are
not visible to the `INSERT` snapshot. Again, this is only the case in Read
Committed mode.

`MERGE` allows the user to specify various combinations of `INSERT`, `UPDATE`
and `DELETE` subcommands. A `MERGE` command with both `INSERT` and `UPDATE`
subcommands looks similar to `INSERT` with an `ON CONFLICT DO UPDATE` clause
but does not guarantee that either `INSERT` or `UPDATE` will occur. If `MERGE`
attempts an `UPDATE` or `DELETE` and the row is concurrently updated but the
join condition still passes for the current target and the current source
tuple, then `MERGE` will behave the same as the `UPDATE` or `DELETE` commands
and perform its action on the updated version of the row. However, because
`MERGE` can specify several actions and they can be conditional, the
conditions for each action are re-evaluated on the updated version of the row,
starting from the first action, even if the action that had originally matched
appears later in the list of actions. On the other hand, if the row is
concurrently updated or deleted so that the join condition fails, then `MERGE`
will evaluate the condition's `NOT MATCHED` actions next, and execute the
first one that succeeds. If `MERGE` attempts an `INSERT` and a unique index is
present and a duplicate row is concurrently inserted, then a uniqueness
violation error is raised; `MERGE` does not attempt to avoid such errors by
restarting evaluation of `MATCHED` conditions.

Because of the above rules, it is possible for an updating command to see an
inconsistent snapshot: it can see the effects of concurrent updating commands
on the same rows it is trying to update, but it does not see effects of those
commands on other rows in the database. This behavior makes Read Committed
mode unsuitable for commands that involve complex search conditions; however,
it is just right for simpler cases. For example, consider updating bank
balances with transactions like:

    
    
    BEGIN;
    UPDATE accounts SET balance = balance + 100.00 WHERE acctnum = 12345;
    UPDATE accounts SET balance = balance - 100.00 WHERE acctnum = 7534;
    COMMIT;
    

If two such transactions concurrently try to change the balance of account
12345, we clearly want the second transaction to start with the updated
version of the account's row. Because each command is affecting only a
predetermined row, letting it see the updated version of the row does not
create any troublesome inconsistency.

More complex usage can produce undesirable results in Read Committed mode. For
example, consider a `DELETE` command operating on data that is being both
added and removed from its restriction criteria by another command, e.g.,
assume `website` is a two-row table with `website.hits` equaling `9` and `10`:

    
    
    BEGIN;
    UPDATE website SET hits = hits + 1;
    -- run from another session:  DELETE FROM website WHERE hits = 10;
    COMMIT;
    

The `DELETE` will have no effect even though there is a `website.hits = 10`
row before and after the `UPDATE`. This occurs because the pre-update row
value `9` is skipped, and when the `UPDATE` completes and `DELETE` obtains a
lock, the new row value is no longer `10` but `11`, which no longer matches
the criteria.

Because Read Committed mode starts each command with a new snapshot that
includes all transactions committed up to that instant, subsequent commands in
the same transaction will see the effects of the committed concurrent
transaction in any case. The point at issue above is whether or not a _single_
command sees an absolutely consistent view of the database.

The partial transaction isolation provided by Read Committed mode is adequate
for many applications, and this mode is fast and simple to use; however, it is
not sufficient for all cases. Applications that do complex queries and updates
might require a more rigorously consistent view of the database than Read
Committed mode provides.

### 13.2.2. Repeatable Read Isolation Level #

The _Repeatable Read_ isolation level only sees data committed before the
transaction began; it never sees either uncommitted data or changes committed
by concurrent transactions during the transaction's execution. (However, each
query does see the effects of previous updates executed within its own
transaction, even though they are not yet committed.) This is a stronger
guarantee than is required by the SQL standard for this isolation level, and
prevents all of the phenomena described in [Table 13.1](transaction-
iso.html#MVCC-ISOLEVEL-TABLE "Table 13.1. Transaction Isolation Levels")
except for serialization anomalies. As mentioned above, this is specifically
allowed by the standard, which only describes the _minimum_ protections each
isolation level must provide.

This level is different from Read Committed in that a query in a repeatable
read transaction sees a snapshot as of the start of the first non-transaction-
control statement in the _transaction_ , not as of the start of the current
statement within the transaction. Thus, successive `SELECT` commands within a
_single_ transaction see the same data, i.e., they do not see changes made by
other transactions that committed after their own transaction started.

Applications using this level must be prepared to retry transactions due to
serialization failures.

`UPDATE`, `DELETE`, `MERGE`, `SELECT FOR UPDATE`, and `SELECT FOR SHARE`
commands behave the same as `SELECT` in terms of searching for target rows:
they will only find target rows that were committed as of the transaction
start time. However, such a target row might have already been updated (or
deleted or locked) by another concurrent transaction by the time it is found.
In this case, the repeatable read transaction will wait for the first updating
transaction to commit or roll back (if it is still in progress). If the first
updater rolls back, then its effects are negated and the repeatable read
transaction can proceed with updating the originally found row. But if the
first updater commits (and actually updated or deleted the row, not just
locked it) then the repeatable read transaction will be rolled back with the
message

    
    
    ERROR:  could not serialize access due to concurrent update
    

because a repeatable read transaction cannot modify or lock rows changed by
other transactions after the repeatable read transaction began.

When an application receives this error message, it should abort the current
transaction and retry the whole transaction from the beginning. The second
time through, the transaction will see the previously-committed change as part
of its initial view of the database, so there is no logical conflict in using
the new version of the row as the starting point for the new transaction's
update.

Note that only updating transactions might need to be retried; read-only
transactions will never have serialization conflicts.

The Repeatable Read mode provides a rigorous guarantee that each transaction
sees a completely stable view of the database. However, this view will not
necessarily always be consistent with some serial (one at a time) execution of
concurrent transactions of the same level. For example, even a read-only
transaction at this level may see a control record updated to show that a
batch has been completed but _not_ see one of the detail records which is
logically part of the batch because it read an earlier revision of the control
record. Attempts to enforce business rules by transactions running at this
isolation level are not likely to work correctly without careful use of
explicit locks to block conflicting transactions.

The Repeatable Read isolation level is implemented using a technique known in
academic database literature and in some other database products as _Snapshot
Isolation_. Differences in behavior and performance may be observed when
compared with systems that use a traditional locking technique that reduces
concurrency. Some other systems may even offer Repeatable Read and Snapshot
Isolation as distinct isolation levels with different behavior. The permitted
phenomena that distinguish the two techniques were not formalized by database
researchers until after the SQL standard was developed, and are outside the
scope of this manual. For a full treatment, please see
[[berenson95]](biblio.html#BERENSON95).

### Note

Prior to PostgreSQL version 9.1, a request for the Serializable transaction
isolation level provided exactly the same behavior described here. To retain
the legacy Serializable behavior, Repeatable Read should now be requested.

### 13.2.3. Serializable Isolation Level #

The _Serializable_ isolation level provides the strictest transaction
isolation. This level emulates serial transaction execution for all committed
transactions; as if transactions had been executed one after another,
serially, rather than concurrently. However, like the Repeatable Read level,
applications using this level must be prepared to retry transactions due to
serialization failures. In fact, this isolation level works exactly the same
as Repeatable Read except that it also monitors for conditions which could
make execution of a concurrent set of serializable transactions behave in a
manner inconsistent with all possible serial (one at a time) executions of
those transactions. This monitoring does not introduce any blocking beyond
that present in repeatable read, but there is some overhead to the monitoring,
and detection of the conditions which could cause a _serialization anomaly_
will trigger a _serialization failure_.

As an example, consider a table `mytab`, initially containing:

    
    
     class | value
    -------+-------
         1 |    10
         1 |    20
         2 |   100
         2 |   200
    

Suppose that serializable transaction A computes:

    
    
    SELECT SUM(value) FROM mytab WHERE class = 1;
    

and then inserts the result (30) as the `value` in a new row with `class` `=
2`. Concurrently, serializable transaction B computes:

    
    
    SELECT SUM(value) FROM mytab WHERE class = 2;
    

and obtains the result 300, which it inserts in a new row with `class` `= 1`.
Then both transactions try to commit. If either transaction were running at
the Repeatable Read isolation level, both would be allowed to commit; but
since there is no serial order of execution consistent with the result, using
Serializable transactions will allow one transaction to commit and will roll
the other back with this message:

    
    
    ERROR:  could not serialize access due to read/write dependencies among transactions
    

This is because if A had executed before B, B would have computed the sum 330,
not 300, and similarly the other order would have resulted in a different sum
computed by A.

When relying on Serializable transactions to prevent anomalies, it is
important that any data read from a permanent user table not be considered
valid until the transaction which read it has successfully committed. This is
true even for read-only transactions, except that data read within a
_deferrable_ read-only transaction is known to be valid as soon as it is read,
because such a transaction waits until it can acquire a snapshot guaranteed to
be free from such problems before starting to read any data. In all other
cases applications must not depend on results read during a transaction that
later aborted; instead, they should retry the transaction until it succeeds.

To guarantee true serializability PostgreSQL uses _predicate locking_ , which
means that it keeps locks which allow it to determine when a write would have
had an impact on the result of a previous read from a concurrent transaction,
had it run first. In PostgreSQL these locks do not cause any blocking and
therefore can _not_ play any part in causing a deadlock. They are used to
identify and flag dependencies among concurrent Serializable transactions
which in certain combinations can lead to serialization anomalies. In
contrast, a Read Committed or Repeatable Read transaction which wants to
ensure data consistency may need to take out a lock on an entire table, which
could block other users attempting to use that table, or it may use `SELECT
FOR UPDATE` or `SELECT FOR SHARE` which not only can block other transactions
but cause disk access.

Predicate locks in PostgreSQL, like in most other database systems, are based
on data actually accessed by a transaction. These will show up in the
[`pg_locks`](view-pg-locks.html "54.12. pg_locks") system view with a `mode`
of `SIReadLock`. The particular locks acquired during execution of a query
will depend on the plan used by the query, and multiple finer-grained locks
(e.g., tuple locks) may be combined into fewer coarser-grained locks (e.g.,
page locks) during the course of the transaction to prevent exhaustion of the
memory used to track the locks. A `READ ONLY` transaction may be able to
release its SIRead locks before completion, if it detects that no conflicts
can still occur which could lead to a serialization anomaly. In fact, `READ
ONLY` transactions will often be able to establish that fact at startup and
avoid taking any predicate locks. If you explicitly request a `SERIALIZABLE
READ ONLY DEFERRABLE` transaction, it will block until it can establish this
fact. (This is the _only_ case where Serializable transactions block but
Repeatable Read transactions don't.) On the other hand, SIRead locks often
need to be kept past transaction commit, until overlapping read write
transactions complete.

Consistent use of Serializable transactions can simplify development. The
guarantee that any set of successfully committed concurrent Serializable
transactions will have the same effect as if they were run one at a time means
that if you can demonstrate that a single transaction, as written, will do the
right thing when run by itself, you can have confidence that it will do the
right thing in any mix of Serializable transactions, even without any
information about what those other transactions might do, or it will not
successfully commit. It is important that an environment which uses this
technique have a generalized way of handling serialization failures (which
always return with an SQLSTATE value of '40001'), because it will be very hard
to predict exactly which transactions might contribute to the read/write
dependencies and need to be rolled back to prevent serialization anomalies.
The monitoring of read/write dependencies has a cost, as does the restart of
transactions which are terminated with a serialization failure, but balanced
against the cost and blocking involved in use of explicit locks and `SELECT
FOR UPDATE` or `SELECT FOR SHARE`, Serializable transactions are the best
performance choice for some environments.

While PostgreSQL's Serializable transaction isolation level only allows
concurrent transactions to commit if it can prove there is a serial order of
execution that would produce the same effect, it doesn't always prevent errors
from being raised that would not occur in true serial execution. In
particular, it is possible to see unique constraint violations caused by
conflicts with overlapping Serializable transactions even after explicitly
checking that the key isn't present before attempting to insert it. This can
be avoided by making sure that _all_ Serializable transactions that insert
potentially conflicting keys explicitly check if they can do so first. For
example, imagine an application that asks the user for a new key and then
checks that it doesn't exist already by trying to select it first, or
generates a new key by selecting the maximum existing key and adding one. If
some Serializable transactions insert new keys directly without following this
protocol, unique constraints violations might be reported even in cases where
they could not occur in a serial execution of the concurrent transactions.

For optimal performance when relying on Serializable transactions for
concurrency control, these issues should be considered:

  * Declare transactions as `READ ONLY` when possible.

  * Control the number of active connections, using a connection pool if needed. This is always an important performance consideration, but it can be particularly important in a busy system using Serializable transactions.

  * Don't put more into a single transaction than needed for integrity purposes.

  * Don't leave connections dangling “idle in transaction” longer than necessary. The configuration parameter [idle_in_transaction_session_timeout](runtime-config-client.html#GUC-IDLE-IN-TRANSACTION-SESSION-TIMEOUT) may be used to automatically disconnect lingering sessions.

  * Eliminate explicit locks, `SELECT FOR UPDATE`, and `SELECT FOR SHARE` where no longer needed due to the protections automatically provided by Serializable transactions.

  * When the system is forced to combine multiple page-level predicate locks into a single relation-level predicate lock because the predicate lock table is short of memory, an increase in the rate of serialization failures may occur. You can avoid this by increasing [max_pred_locks_per_transaction](runtime-config-locks.html#GUC-MAX-PRED-LOCKS-PER-TRANSACTION), [max_pred_locks_per_relation](runtime-config-locks.html#GUC-MAX-PRED-LOCKS-PER-RELATION), and/or [max_pred_locks_per_page](runtime-config-locks.html#GUC-MAX-PRED-LOCKS-PER-PAGE).

  * A sequential scan will always necessitate a relation-level predicate lock. This can result in an increased rate of serialization failures. It may be helpful to encourage the use of index scans by reducing [random_page_cost](runtime-config-query.html#GUC-RANDOM-PAGE-COST) and/or increasing [cpu_tuple_cost](runtime-config-query.html#GUC-CPU-TUPLE-COST). Be sure to weigh any decrease in transaction rollbacks and restarts against any overall change in query execution time.

The Serializable isolation level is implemented using a technique known in
academic database literature as Serializable Snapshot Isolation, which builds
on Snapshot Isolation by adding checks for serialization anomalies. Some
differences in behavior and performance may be observed when compared with
other systems that use a traditional locking technique. Please see
[[ports12]](biblio.html#PORTS12) for detailed information.

* * *

[Prev](mvcc-intro.html "13.1. Introduction")  | [Up](mvcc.html "Chapter 13. Concurrency Control") |  [Next](explicit-locking.html "13.3. Explicit Locking")  
---|---|---  
13.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  13.3. Explicit Locking  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/transaction-iso.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

