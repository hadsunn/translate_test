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

Supported Versions: [Current](/docs/current/view-pg-locks.html "PostgreSQL 17
- 54.12. pg_locks") ([17](/docs/17/view-pg-locks.html "PostgreSQL 17 -
54.12. pg_locks")) / [16](/docs/16/view-pg-locks.html "PostgreSQL 16 -
54.12. pg_locks") / [15](/docs/15/view-pg-locks.html "PostgreSQL 15 -
54.12. pg_locks") / [14](/docs/14/view-pg-locks.html "PostgreSQL 14 -
54.12. pg_locks") / [13](/docs/13/view-pg-locks.html "PostgreSQL 13 -
54.12. pg_locks")

Development Versions: [18](/docs/18/view-pg-locks.html "PostgreSQL 18 -
54.12. pg_locks") / [devel](/docs/devel/view-pg-locks.html "PostgreSQL devel -
54.12. pg_locks")

Unsupported versions: [12](/docs/12/view-pg-locks.html "PostgreSQL 12 -
54.12. pg_locks") / [11](/docs/11/view-pg-locks.html "PostgreSQL 11 -
54.12. pg_locks") / [10](/docs/10/view-pg-locks.html "PostgreSQL 10 -
54.12. pg_locks") / [9.6](/docs/9.6/view-pg-locks.html "PostgreSQL 9.6 -
54.12. pg_locks") / [9.5](/docs/9.5/view-pg-locks.html "PostgreSQL 9.5 -
54.12. pg_locks") / [9.4](/docs/9.4/view-pg-locks.html "PostgreSQL 9.4 -
54.12. pg_locks") / [9.3](/docs/9.3/view-pg-locks.html "PostgreSQL 9.3 -
54.12. pg_locks") / [9.2](/docs/9.2/view-pg-locks.html "PostgreSQL 9.2 -
54.12. pg_locks") / [9.1](/docs/9.1/view-pg-locks.html "PostgreSQL 9.1 -
54.12. pg_locks") / [9.0](/docs/9.0/view-pg-locks.html "PostgreSQL 9.0 -
54.12. pg_locks") / [8.4](/docs/8.4/view-pg-locks.html "PostgreSQL 8.4 -
54.12. pg_locks") / [8.3](/docs/8.3/view-pg-locks.html "PostgreSQL 8.3 -
54.12. pg_locks") / [8.2](/docs/8.2/view-pg-locks.html "PostgreSQL 8.2 -
54.12. pg_locks") / [8.1](/docs/8.1/view-pg-locks.html "PostgreSQL 8.1 -
54.12. pg_locks") / [8.0](/docs/8.0/view-pg-locks.html "PostgreSQL 8.0 -
54.12. pg_locks") / [7.4](/docs/7.4/view-pg-locks.html "PostgreSQL 7.4 -
54.12. pg_locks")

__

54.12. `pg_locks`  
---  
[Prev](view-pg-indexes.html "54.11. pg_indexes")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-matviews.html "54.13. pg_matviews")  
  
* * *

## 54.12. `pg_locks` #

The view `pg_locks` provides access to information about the locks held by
active processes within the database server. See [Chapter 13](mvcc.html
"Chapter 13. Concurrency Control") for more discussion of locking.

`pg_locks` contains one row per active lockable object, requested lock mode,
and relevant process. Thus, the same lockable object might appear many times,
if multiple processes are holding or waiting for locks on it. However, an
object that currently has no locks on it will not appear at all.

There are several distinct types of lockable objects: whole relations (e.g.,
tables), individual pages of relations, individual tuples of relations,
transaction IDs (both virtual and permanent IDs), and general database objects
(identified by class OID and object OID, in the same way as in
[`pg_description`](catalog-pg-description.html "53.19. pg_description") or
[`pg_depend`](catalog-pg-depend.html "53.18. pg_depend")). Also, the right to
extend a relation is represented as a separate lockable object, as is the
right to update `pg_database`.`datfrozenxid`. Also, “advisory” locks can be
taken on numbers that have user-defined meanings.

**Table  54.12. `pg_locks` Columns**

Column Type Description  
---  
`locktype` `text` Type of the lockable object: `relation`, `extend`,
`frozenid`, `page`, `tuple`, `transactionid`, `virtualxid`, `spectoken`,
`object`, `userlock`, `advisory`, or `applytransaction`. (See also [Table
28.11](monitoring-stats.html#WAIT-EVENT-LOCK-TABLE "Table 28.11. Wait Events
of Type Lock").)  
`database` `oid` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`oid`) OID of the database in which the lock target
exists, or zero if the target is a shared object, or null if the target is a
transaction ID  
`relation` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) OID of the relation targeted by the lock, or null if
the target is not a relation or part of a relation  
`page` `int4` Page number targeted by the lock within the relation, or null if
the target is not a relation page or tuple  
`tuple` `int2` Tuple number targeted by the lock within the page, or null if
the target is not a tuple  
`virtualxid` `text` Virtual ID of the transaction targeted by the lock, or
null if the target is not a virtual transaction ID; see [Chapter
74](transactions.html "Chapter 74. Transaction Processing")  
`transactionid` `xid` ID of the transaction targeted by the lock, or null if
the target is not a transaction ID; [Chapter 74](transactions.html
"Chapter 74. Transaction Processing")  
`classid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) OID of the system catalog containing the lock
target, or null if the target is not a general database object  
`objid` `oid` (references any OID column) OID of the lock target within its
system catalog, or null if the target is not a general database object  
`objsubid` `int2` Column number targeted by the lock (the `classid` and
`objid` refer to the table itself), or zero if the target is some other
general database object, or null if the target is not a general database
object  
`virtualtransaction` `text` Virtual ID of the transaction that is holding or
awaiting this lock  
`pid` `int4` Process ID of the server process holding or awaiting this lock,
or null if the lock is held by a prepared transaction  
`mode` `text` Name of the lock mode held or desired by this process (see
[Section 13.3.1](explicit-locking.html#LOCKING-TABLES "13.3.1. Table-Level
Locks") and [Section 13.2.3](transaction-iso.html#XACT-SERIALIZABLE
"13.2.3. Serializable Isolation Level"))  
`granted` `bool` True if lock is held, false if lock is awaited  
`fastpath` `bool` True if lock was taken via fast path, false if taken via
main lock table  
`waitstart` `timestamptz` Time when the server process started waiting for
this lock, or null if the lock is held. Note that this can be null for a very
short period of time after the wait started even though `granted` is `false`.  
  
  

`granted` is true in a row representing a lock held by the indicated process.
False indicates that this process is currently waiting to acquire this lock,
which implies that at least one other process is holding or waiting for a
conflicting lock mode on the same lockable object. The waiting process will
sleep until the other lock is released (or a deadlock situation is detected).
A single process can be waiting to acquire at most one lock at a time.

Throughout running a transaction, a server process holds an exclusive lock on
the transaction's virtual transaction ID. If a permanent ID is assigned to the
transaction (which normally happens only if the transaction changes the state
of the database), it also holds an exclusive lock on the transaction's
permanent transaction ID until it ends. When a process finds it necessary to
wait specifically for another transaction to end, it does so by attempting to
acquire share lock on the other transaction's ID (either virtual or permanent
ID depending on the situation). That will succeed only when the other
transaction terminates and releases its locks.

Although tuples are a lockable type of object, information about row-level
locks is stored on disk, not in memory, and therefore row-level locks normally
do not appear in this view. If a process is waiting for a row-level lock, it
will usually appear in the view as waiting for the permanent transaction ID of
the current holder of that row lock.

A speculative insertion lock consists of a transaction ID and a speculative
insertion token. The speculative insertion token is displayed in the `objid`
column.

Advisory locks can be acquired on keys consisting of either a single `bigint` value or two integer values. A `bigint` key is displayed with its high-order half in the `classid` column, its low-order half in the `objid` column, and `objsubid` equal to 1. The original `bigint` value can be reassembled with the expression `(classid::bigint << 32) | objid::bigint`. Integer keys are displayed with the first key in the `classid` column, the second key in the `objid` column, and `objsubid` equal to 2. The actual meaning of the keys is up to the user. Advisory locks are local to each database, so the `database` column is meaningful for an advisory lock.

Apply transaction locks are used in parallel mode to apply the transaction in
logical replication. The remote transaction ID is displayed in the
`transactionid` column. The `objsubid` displays the lock subtype which is 0
for the lock used to synchronize the set of changes, and 1 for the lock used
to wait for the transaction to finish to ensure commit order.

`pg_locks` provides a global view of all locks in the database cluster, not
only those relevant to the current database. Although its `relation` column
can be joined against [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid` to identify locked relations, this will only work
correctly for relations in the current database (those for which the
`database` column is either the current database's OID or zero).

The `pid` column can be joined to the `pid` column of the
[`pg_stat_activity`](monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW
"28.2.3. pg_stat_activity") view to get more information on the session
holding or awaiting each lock, for example

    
    
    SELECT * FROM pg_locks pl LEFT JOIN pg_stat_activity psa
        ON pl.pid = psa.pid;
    

Also, if you are using prepared transactions, the `virtualtransaction` column
can be joined to the `transaction` column of the [`pg_prepared_xacts`](view-
pg-prepared-xacts.html "54.16. pg_prepared_xacts") view to get more
information on prepared transactions that hold locks. (A prepared transaction
can never be waiting for a lock, but it continues to hold the locks it
acquired while running.) For example:

    
    
    SELECT * FROM pg_locks pl LEFT JOIN pg_prepared_xacts ppx
        ON pl.virtualtransaction = '-1/' || ppx.transaction;
    

While it is possible to obtain information about which processes block which
other processes by joining `pg_locks` against itself, this is very difficult
to get right in detail. Such a query would have to encode knowledge about
which lock modes conflict with which others. Worse, the `pg_locks` view does
not expose information about which processes are ahead of which others in lock
wait queues, nor information about which processes are parallel workers
running on behalf of which other client sessions. It is better to use the
`pg_blocking_pids()` function (see [Table 9.67](functions-info.html#FUNCTIONS-
INFO-SESSION-TABLE "Table 9.67. Session Information Functions")) to identify
which process(es) a waiting process is blocked behind.

The `pg_locks` view displays data from both the regular lock manager and the
predicate lock manager, which are separate systems; in addition, the regular
lock manager subdivides its locks into regular and _fast-path_ locks. This
data is not guaranteed to be entirely consistent. When the view is queried,
data on fast-path locks (with `fastpath` = `true`) is gathered from each
backend one at a time, without freezing the state of the entire lock manager,
so it is possible for locks to be taken or released while information is
gathered. Note, however, that these locks are known not to conflict with any
other lock currently in place. After all backends have been queried for fast-
path locks, the remainder of the regular lock manager is locked as a unit, and
a consistent snapshot of all remaining locks is collected as an atomic action.
After unlocking the regular lock manager, the predicate lock manager is
similarly locked and all predicate locks are collected as an atomic action.
Thus, with the exception of fast-path locks, each lock manager will deliver a
consistent set of results, but as we do not lock both lock managers
simultaneously, it is possible for locks to be taken or released after we
interrogate the regular lock manager and before we interrogate the predicate
lock manager.

Locking the regular and/or predicate lock manager could have some impact on
database performance if this view is very frequently accessed. The locks are
held only for the minimum amount of time necessary to obtain data from the
lock managers, but this does not completely eliminate the possibility of a
performance impact.

* * *

[Prev](view-pg-indexes.html "54.11. pg_indexes")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-matviews.html "54.13. pg_matviews")  
---|---|---  
54.11. `pg_indexes`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.13. `pg_matviews`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-locks.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

