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

Supported Versions: [Current](/docs/current/sql-truncate.html "PostgreSQL 17 -
TRUNCATE") ([17](/docs/17/sql-truncate.html "PostgreSQL 17 - TRUNCATE")) /
[16](/docs/16/sql-truncate.html "PostgreSQL 16 - TRUNCATE") /
[15](/docs/15/sql-truncate.html "PostgreSQL 15 - TRUNCATE") /
[14](/docs/14/sql-truncate.html "PostgreSQL 14 - TRUNCATE") /
[13](/docs/13/sql-truncate.html "PostgreSQL 13 - TRUNCATE")

Development Versions: [18](/docs/18/sql-truncate.html "PostgreSQL 18 -
TRUNCATE") / [devel](/docs/devel/sql-truncate.html "PostgreSQL devel -
TRUNCATE")

Unsupported versions: [12](/docs/12/sql-truncate.html "PostgreSQL 12 -
TRUNCATE") / [11](/docs/11/sql-truncate.html "PostgreSQL 11 - TRUNCATE") /
[10](/docs/10/sql-truncate.html "PostgreSQL 10 - TRUNCATE") /
[9.6](/docs/9.6/sql-truncate.html "PostgreSQL 9.6 - TRUNCATE") /
[9.5](/docs/9.5/sql-truncate.html "PostgreSQL 9.5 - TRUNCATE") /
[9.4](/docs/9.4/sql-truncate.html "PostgreSQL 9.4 - TRUNCATE") /
[9.3](/docs/9.3/sql-truncate.html "PostgreSQL 9.3 - TRUNCATE") /
[9.2](/docs/9.2/sql-truncate.html "PostgreSQL 9.2 - TRUNCATE") /
[9.1](/docs/9.1/sql-truncate.html "PostgreSQL 9.1 - TRUNCATE") /
[9.0](/docs/9.0/sql-truncate.html "PostgreSQL 9.0 - TRUNCATE") /
[8.4](/docs/8.4/sql-truncate.html "PostgreSQL 8.4 - TRUNCATE") /
[8.3](/docs/8.3/sql-truncate.html "PostgreSQL 8.3 - TRUNCATE") /
[8.2](/docs/8.2/sql-truncate.html "PostgreSQL 8.2 - TRUNCATE") /
[8.1](/docs/8.1/sql-truncate.html "PostgreSQL 8.1 - TRUNCATE") /
[8.0](/docs/8.0/sql-truncate.html "PostgreSQL 8.0 - TRUNCATE") /
[7.4](/docs/7.4/sql-truncate.html "PostgreSQL 7.4 - TRUNCATE") /
[7.3](/docs/7.3/sql-truncate.html "PostgreSQL 7.3 - TRUNCATE") /
[7.2](/docs/7.2/sql-truncate.html "PostgreSQL 7.2 - TRUNCATE") /
[7.1](/docs/7.1/sql-truncate.html "PostgreSQL 7.1 - TRUNCATE")

__

TRUNCATE  
---  
[Prev](sql-start-transaction.html "START TRANSACTION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-unlisten.html "UNLISTEN")  
  
* * *

## TRUNCATE

TRUNCATE — empty a table or set of tables

## Synopsis

    
    
    TRUNCATE [ TABLE ] [ ONLY ] _name_ [ * ] [, ... ]
        [ RESTART IDENTITY | CONTINUE IDENTITY ] [ CASCADE | RESTRICT ]
    

## Description

`TRUNCATE` quickly removes all rows from a set of tables. It has the same
effect as an unqualified `DELETE` on each table, but since it does not
actually scan the tables it is faster. Furthermore, it reclaims disk space
immediately, rather than requiring a subsequent `VACUUM` operation. This is
most useful on large tables.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of a table to truncate. If `ONLY` is
specified before the table name, only that table is truncated. If `ONLY` is
not specified, the table and all its descendant tables (if any) are truncated.
Optionally, `*` can be specified after the table name to explicitly indicate
that descendant tables are included.

`RESTART IDENTITY`

    

Automatically restart sequences owned by columns of the truncated table(s).

`CONTINUE IDENTITY`

    

Do not change the values of sequences. This is the default.

`CASCADE`

    

Automatically truncate all tables that have foreign-key references to any of
the named tables, or to any tables added to the group due to `CASCADE`.

`RESTRICT`

    

Refuse to truncate if any of the tables have foreign-key references from
tables that are not listed in the command. This is the default.

## Notes

You must have the `TRUNCATE` privilege on a table to truncate it.

`TRUNCATE` acquires an `ACCESS EXCLUSIVE` lock on each table it operates on,
which blocks all other concurrent operations on the table. When `RESTART
IDENTITY` is specified, any sequences that are to be restarted are likewise
locked exclusively. If concurrent access to a table is required, then the
`DELETE` command should be used instead.

`TRUNCATE` cannot be used on a table that has foreign-key references from
other tables, unless all such tables are also truncated in the same command.
Checking validity in such cases would require table scans, and the whole point
is not to do one. The `CASCADE` option can be used to automatically include
all dependent tables — but be very careful when using this option, or else you
might lose data you did not intend to! Note in particular that when the table
to be truncated is a partition, siblings partitions are left untouched, but
cascading occurs to all referencing tables and all their partitions with no
distinction.

`TRUNCATE` will not fire any `ON DELETE` triggers that might exist for the
tables. But it will fire `ON TRUNCATE` triggers. If `ON TRUNCATE` triggers are
defined for any of the tables, then all `BEFORE TRUNCATE` triggers are fired
before any truncation happens, and all `AFTER TRUNCATE` triggers are fired
after the last truncation is performed and any sequences are reset. The
triggers will fire in the order that the tables are to be processed (first
those listed in the command, and then any that were added due to cascading).

`TRUNCATE` is not MVCC-safe. After truncation, the table will appear empty to
concurrent transactions, if they are using a snapshot taken before the
truncation occurred. See [Section 13.6](mvcc-caveats.html "13.6. Caveats") for
more details.

`TRUNCATE` is transaction-safe with respect to the data in the tables: the
truncation will be safely rolled back if the surrounding transaction does not
commit.

When `RESTART IDENTITY` is specified, the implied `ALTER SEQUENCE RESTART`
operations are also done transactionally; that is, they will be rolled back if
the surrounding transaction does not commit. Be aware that if any additional
sequence operations are done on the restarted sequences before the transaction
rolls back, the effects of these operations on the sequences will be rolled
back, but not their effects on `currval()`; that is, after the transaction
`currval()` will continue to reflect the last sequence value obtained inside
the failed transaction, even though the sequence itself may no longer be
consistent with that. This is similar to the usual behavior of `currval()`
after a failed transaction.

`TRUNCATE` can be used for foreign tables if supported by the foreign data
wrapper, for instance, see [postgres_fdw](postgres-fdw.html
"F.38. postgres_fdw — access data stored in external PostgreSQL servers").

## Examples

Truncate the tables `bigtable` and `fattable`:

    
    
    TRUNCATE bigtable, fattable;
    

The same, and also reset any associated sequence generators:

    
    
    TRUNCATE bigtable, fattable RESTART IDENTITY;
    

Truncate the table `othertable`, and cascade to any tables that reference
`othertable` via foreign-key constraints:

    
    
    TRUNCATE othertable CASCADE;
    

## Compatibility

The SQL:2008 standard includes a `TRUNCATE` command with the syntax `TRUNCATE
TABLE _`tablename`_`. The clauses `CONTINUE IDENTITY`/`RESTART IDENTITY` also
appear in that standard, but have slightly different though related meanings.
Some of the concurrency behavior of this command is left implementation-
defined by the standard, so the above notes should be considered and compared
with other implementations if necessary.

## See Also

[DELETE](sql-delete.html "DELETE")

* * *

[Prev](sql-start-transaction.html "START TRANSACTION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-unlisten.html "UNLISTEN")  
---|---|---  
START TRANSACTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  UNLISTEN  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-truncate.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

