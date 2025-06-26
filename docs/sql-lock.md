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

Supported Versions: [Current](/docs/current/sql-lock.html "PostgreSQL 17 -
LOCK") ([17](/docs/17/sql-lock.html "PostgreSQL 17 - LOCK")) /
[16](/docs/16/sql-lock.html "PostgreSQL 16 - LOCK") / [15](/docs/15/sql-
lock.html "PostgreSQL 15 - LOCK") / [14](/docs/14/sql-lock.html "PostgreSQL 14
- LOCK") / [13](/docs/13/sql-lock.html "PostgreSQL 13 - LOCK")

Development Versions: [18](/docs/18/sql-lock.html "PostgreSQL 18 - LOCK") /
[devel](/docs/devel/sql-lock.html "PostgreSQL devel - LOCK")

Unsupported versions: [12](/docs/12/sql-lock.html "PostgreSQL 12 - LOCK") /
[11](/docs/11/sql-lock.html "PostgreSQL 11 - LOCK") / [10](/docs/10/sql-
lock.html "PostgreSQL 10 - LOCK") / [9.6](/docs/9.6/sql-lock.html "PostgreSQL
9.6 - LOCK") / [9.5](/docs/9.5/sql-lock.html "PostgreSQL 9.5 - LOCK") /
[9.4](/docs/9.4/sql-lock.html "PostgreSQL 9.4 - LOCK") / [9.3](/docs/9.3/sql-
lock.html "PostgreSQL 9.3 - LOCK") / [9.2](/docs/9.2/sql-lock.html "PostgreSQL
9.2 - LOCK") / [9.1](/docs/9.1/sql-lock.html "PostgreSQL 9.1 - LOCK") /
[9.0](/docs/9.0/sql-lock.html "PostgreSQL 9.0 - LOCK") / [8.4](/docs/8.4/sql-
lock.html "PostgreSQL 8.4 - LOCK") / [8.3](/docs/8.3/sql-lock.html "PostgreSQL
8.3 - LOCK") / [8.2](/docs/8.2/sql-lock.html "PostgreSQL 8.2 - LOCK") /
[8.1](/docs/8.1/sql-lock.html "PostgreSQL 8.1 - LOCK") / [8.0](/docs/8.0/sql-
lock.html "PostgreSQL 8.0 - LOCK") / [7.4](/docs/7.4/sql-lock.html "PostgreSQL
7.4 - LOCK") / [7.3](/docs/7.3/sql-lock.html "PostgreSQL 7.3 - LOCK") /
[7.2](/docs/7.2/sql-lock.html "PostgreSQL 7.2 - LOCK") / [7.1](/docs/7.1/sql-
lock.html "PostgreSQL 7.1 - LOCK")

__

LOCK  
---  
[Prev](sql-load.html "LOAD")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-merge.html "MERGE")  
  
* * *

## LOCK

LOCK — lock a table

## Synopsis

    
    
    LOCK [ TABLE ] [ ONLY ] _name_ [ * ] [, ...] [ IN _lockmode_ MODE ] [ NOWAIT ]
    
    where _lockmode_ is one of:
    
        ACCESS SHARE | ROW SHARE | ROW EXCLUSIVE | SHARE UPDATE EXCLUSIVE
        | SHARE | SHARE ROW EXCLUSIVE | EXCLUSIVE | ACCESS EXCLUSIVE
    

## Description

`LOCK TABLE` obtains a table-level lock, waiting if necessary for any
conflicting locks to be released. If `NOWAIT` is specified, `LOCK TABLE` does
not wait to acquire the desired lock: if it cannot be acquired immediately,
the command is aborted and an error is emitted. Once obtained, the lock is
held for the remainder of the current transaction. (There is no `UNLOCK TABLE`
command; locks are always released at transaction end.)

When a view is locked, all relations appearing in the view definition query
are also locked recursively with the same lock mode.

When acquiring locks automatically for commands that reference tables,
PostgreSQL always uses the least restrictive lock mode possible. `LOCK TABLE`
provides for cases when you might need more restrictive locking. For example,
suppose an application runs a transaction at the `READ COMMITTED` isolation
level and needs to ensure that data in a table remains stable for the duration
of the transaction. To achieve this you could obtain `SHARE` lock mode over
the table before querying. This will prevent concurrent data changes and
ensure subsequent reads of the table see a stable view of committed data,
because `SHARE` lock mode conflicts with the `ROW EXCLUSIVE` lock acquired by
writers, and your `LOCK TABLE _`name`_ IN SHARE MODE` statement will wait
until any concurrent holders of `ROW EXCLUSIVE` mode locks commit or roll
back. Thus, once you obtain the lock, there are no uncommitted writes
outstanding; furthermore none can begin until you release the lock.

To achieve a similar effect when running a transaction at the `REPEATABLE
READ` or `SERIALIZABLE` isolation level, you have to execute the `LOCK TABLE`
statement before executing any `SELECT` or data modification statement. A
`REPEATABLE READ` or `SERIALIZABLE` transaction's view of data will be frozen
when its first `SELECT` or data modification statement begins. A `LOCK TABLE`
later in the transaction will still prevent concurrent writes — but it won't
ensure that what the transaction reads corresponds to the latest committed
values.

If a transaction of this sort is going to change the data in the table, then
it should use `SHARE ROW EXCLUSIVE` lock mode instead of `SHARE` mode. This
ensures that only one transaction of this type runs at a time. Without this, a
deadlock is possible: two transactions might both acquire `SHARE` mode, and
then be unable to also acquire `ROW EXCLUSIVE` mode to actually perform their
updates. (Note that a transaction's own locks never conflict, so a transaction
can acquire `ROW EXCLUSIVE` mode when it holds `SHARE` mode — but not if
anyone else holds `SHARE` mode.) To avoid deadlocks, make sure all
transactions acquire locks on the same objects in the same order, and if
multiple lock modes are involved for a single object, then transactions should
always acquire the most restrictive mode first.

More information about the lock modes and locking strategies can be found in
[Section 13.3](explicit-locking.html "13.3. Explicit Locking").

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing table to lock. If `ONLY`
is specified before the table name, only that table is locked. If `ONLY` is
not specified, the table and all its descendant tables (if any) are locked.
Optionally, `*` can be specified after the table name to explicitly indicate
that descendant tables are included.

The command `LOCK TABLE a, b;` is equivalent to `LOCK TABLE a; LOCK TABLE b;`.
The tables are locked one-by-one in the order specified in the `LOCK TABLE`
command.

_`lockmode`_

    

The lock mode specifies which locks this lock conflicts with. Lock modes are
described in [Section 13.3](explicit-locking.html "13.3. Explicit Locking").

If no lock mode is specified, then `ACCESS EXCLUSIVE`, the most restrictive
mode, is used.

`NOWAIT`

    

Specifies that `LOCK TABLE` should not wait for any conflicting locks to be
released: if the specified lock(s) cannot be acquired immediately without
waiting, the transaction is aborted.

## Notes

To lock a table, the user must have the right privilege for the specified
_`lockmode`_ , or be the table's owner or a superuser. If the user has
`UPDATE`, `DELETE`, or `TRUNCATE` privileges on the table, any _`lockmode`_ is
permitted. If the user has `INSERT` privileges on the table, `ROW EXCLUSIVE
MODE` (or a less-conflicting mode as described in [Section 13.3](explicit-
locking.html "13.3. Explicit Locking")) is permitted. If a user has `SELECT`
privileges on the table, `ACCESS SHARE MODE` is permitted.

The user performing the lock on the view must have the corresponding privilege
on the view. In addition, by default, the view's owner must have the relevant
privileges on the underlying base relations, whereas the user performing the
lock does not need any permissions on the underlying base relations. However,
if the view has `security_invoker` set to `true` (see [`CREATE VIEW`](sql-
createview.html "CREATE VIEW")), the user performing the lock, rather than the
view owner, must have the relevant privileges on the underlying base
relations.

`LOCK TABLE` is useless outside a transaction block: the lock would remain
held only to the completion of the statement. Therefore PostgreSQL reports an
error if `LOCK` is used outside a transaction block. Use [`BEGIN`](sql-
begin.html "BEGIN") and [`COMMIT`](sql-commit.html "COMMIT") (or
[`ROLLBACK`](sql-rollback.html "ROLLBACK")) to define a transaction block.

`LOCK TABLE` only deals with table-level locks, and so the mode names
involving `ROW` are all misnomers. These mode names should generally be read
as indicating the intention of the user to acquire row-level locks within the
locked table. Also, `ROW EXCLUSIVE` mode is a shareable table lock. Keep in
mind that all the lock modes have identical semantics so far as `LOCK TABLE`
is concerned, differing only in the rules about which modes conflict with
which. For information on how to acquire an actual row-level lock, see
[Section 13.3.2](explicit-locking.html#LOCKING-ROWS "13.3.2. Row-Level Locks")
and [The Locking Clause](sql-select.html#SQL-FOR-UPDATE-SHARE "The Locking
Clause") in the [SELECT](sql-select.html "SELECT") documentation.

## Examples

Obtain a `SHARE` lock on a primary key table when going to perform inserts
into a foreign key table:

    
    
    BEGIN WORK;
    LOCK TABLE films IN SHARE MODE;
    SELECT id FROM films
        WHERE name = 'Star Wars: Episode I - The Phantom Menace';
    -- Do ROLLBACK if record was not returned
    INSERT INTO films_user_comments VALUES
        (_id_, 'GREAT! I was waiting for it for so long!');
    COMMIT WORK;
    

Take a `SHARE ROW EXCLUSIVE` lock on a primary key table when going to perform
a delete operation:

    
    
    BEGIN WORK;
    LOCK TABLE films IN SHARE ROW EXCLUSIVE MODE;
    DELETE FROM films_user_comments WHERE id IN
        (SELECT id FROM films WHERE rating < 5);
    DELETE FROM films WHERE rating < 5;
    COMMIT WORK;
    

## Compatibility

There is no `LOCK TABLE` in the SQL standard, which instead uses `SET
TRANSACTION` to specify concurrency levels on transactions. PostgreSQL
supports that too; see [SET TRANSACTION](sql-set-transaction.html "SET
TRANSACTION") for details.

Except for `ACCESS SHARE`, `ACCESS EXCLUSIVE`, and `SHARE UPDATE EXCLUSIVE`
lock modes, the PostgreSQL lock modes and the `LOCK TABLE` syntax are
compatible with those present in Oracle.

* * *

[Prev](sql-load.html "LOAD")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-merge.html "MERGE")  
---|---|---  
LOAD  | [Home](index.html "PostgreSQL 16.9 Documentation") |  MERGE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-lock.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

