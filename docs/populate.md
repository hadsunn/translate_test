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

Supported Versions: [Current](/docs/current/populate.html "PostgreSQL 17 -
14.4. Populating a Database") ([17](/docs/17/populate.html "PostgreSQL 17 -
14.4. Populating a Database")) / [16](/docs/16/populate.html "PostgreSQL 16 -
14.4. Populating a Database") / [15](/docs/15/populate.html "PostgreSQL 15 -
14.4. Populating a Database") / [14](/docs/14/populate.html "PostgreSQL 14 -
14.4. Populating a Database") / [13](/docs/13/populate.html "PostgreSQL 13 -
14.4. Populating a Database")

Development Versions: [18](/docs/18/populate.html "PostgreSQL 18 -
14.4. Populating a Database") / [devel](/docs/devel/populate.html "PostgreSQL
devel - 14.4. Populating a Database")

Unsupported versions: [12](/docs/12/populate.html "PostgreSQL 12 -
14.4. Populating a Database") / [11](/docs/11/populate.html "PostgreSQL 11 -
14.4. Populating a Database") / [10](/docs/10/populate.html "PostgreSQL 10 -
14.4. Populating a Database") / [9.6](/docs/9.6/populate.html "PostgreSQL 9.6
- 14.4. Populating a Database") / [9.5](/docs/9.5/populate.html "PostgreSQL
9.5 - 14.4. Populating a Database") / [9.4](/docs/9.4/populate.html
"PostgreSQL 9.4 - 14.4. Populating a Database") /
[9.3](/docs/9.3/populate.html "PostgreSQL 9.3 - 14.4. Populating a Database")
/ [9.2](/docs/9.2/populate.html "PostgreSQL 9.2 - 14.4. Populating a
Database") / [9.1](/docs/9.1/populate.html "PostgreSQL 9.1 - 14.4. Populating
a Database") / [9.0](/docs/9.0/populate.html "PostgreSQL 9.0 -
14.4. Populating a Database") / [8.4](/docs/8.4/populate.html "PostgreSQL 8.4
- 14.4. Populating a Database") / [8.3](/docs/8.3/populate.html "PostgreSQL
8.3 - 14.4. Populating a Database") / [8.2](/docs/8.2/populate.html
"PostgreSQL 8.2 - 14.4. Populating a Database") /
[8.1](/docs/8.1/populate.html "PostgreSQL 8.1 - 14.4. Populating a Database")
/ [8.0](/docs/8.0/populate.html "PostgreSQL 8.0 - 14.4. Populating a
Database") / [7.4](/docs/7.4/populate.html "PostgreSQL 7.4 - 14.4. Populating
a Database") / [7.3](/docs/7.3/populate.html "PostgreSQL 7.3 -
14.4. Populating a Database") / [7.2](/docs/7.2/populate.html "PostgreSQL 7.2
- 14.4. Populating a Database") / [7.1](/docs/7.1/populate.html "PostgreSQL
7.1 - 14.4. Populating a Database")

__

14.4. Populating a Database  
---  
[Prev](explicit-joins.html "14.3. Controlling the Planner with Explicit JOIN Clauses")  | [Up](performance-tips.html "Chapter 14. Performance Tips") | Chapter 14. Performance Tips | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](non-durability.html "14.5. Non-Durable Settings")  
  
* * *

## 14.4. Populating a Database #

[14.4.1. Disable Autocommit](populate.html#DISABLE-AUTOCOMMIT)

[14.4.2. Use `COPY`](populate.html#POPULATE-COPY-FROM)

[14.4.3. Remove Indexes](populate.html#POPULATE-RM-INDEXES)

[14.4.4. Remove Foreign Key Constraints](populate.html#POPULATE-RM-FKEYS)

[14.4.5. Increase `maintenance_work_mem`](populate.html#POPULATE-WORK-MEM)

[14.4.6. Increase `max_wal_size`](populate.html#POPULATE-MAX-WAL-SIZE)

[14.4.7. Disable WAL Archival and Streaming
Replication](populate.html#POPULATE-PITR)

[14.4.8. Run `ANALYZE` Afterwards](populate.html#POPULATE-ANALYZE)

[14.4.9. Some Notes about pg_dump](populate.html#POPULATE-PG-DUMP)

One might need to insert a large amount of data when first populating a
database. This section contains some suggestions on how to make this process
as efficient as possible.

### 14.4.1. Disable Autocommit #

When using multiple `INSERT`s, turn off autocommit and just do one commit at
the end. (In plain SQL, this means issuing `BEGIN` at the start and `COMMIT`
at the end. Some client libraries might do this behind your back, in which
case you need to make sure the library does it when you want it done.) If you
allow each insertion to be committed separately, PostgreSQL is doing a lot of
work for each row that is added. An additional benefit of doing all insertions
in one transaction is that if the insertion of one row were to fail then the
insertion of all rows inserted up to that point would be rolled back, so you
won't be stuck with partially loaded data.

### 14.4.2. Use `COPY` #

Use [`COPY`](sql-copy.html "COPY") to load all the rows in one command,
instead of using a series of `INSERT` commands. The `COPY` command is
optimized for loading large numbers of rows; it is less flexible than
`INSERT`, but incurs significantly less overhead for large data loads. Since
`COPY` is a single command, there is no need to disable autocommit if you use
this method to populate a table.

If you cannot use `COPY`, it might help to use [`PREPARE`](sql-prepare.html
"PREPARE") to create a prepared `INSERT` statement, and then use `EXECUTE` as
many times as required. This avoids some of the overhead of repeatedly parsing
and planning `INSERT`. Different interfaces provide this facility in different
ways; look for “prepared statements” in the interface documentation.

Note that loading a large number of rows using `COPY` is almost always faster
than using `INSERT`, even if `PREPARE` is used and multiple insertions are
batched into a single transaction.

`COPY` is fastest when used within the same transaction as an earlier `CREATE
TABLE` or `TRUNCATE` command. In such cases no WAL needs to be written,
because in case of an error, the files containing the newly loaded data will
be removed anyway. However, this consideration only applies when
[wal_level](runtime-config-wal.html#GUC-WAL-LEVEL) is `minimal` as all
commands must write WAL otherwise.

### 14.4.3. Remove Indexes #

If you are loading a freshly created table, the fastest method is to create
the table, bulk load the table's data using `COPY`, then create any indexes
needed for the table. Creating an index on pre-existing data is quicker than
updating it incrementally as each row is loaded.

If you are adding large amounts of data to an existing table, it might be a
win to drop the indexes, load the table, and then recreate the indexes. Of
course, the database performance for other users might suffer during the time
the indexes are missing. One should also think twice before dropping a unique
index, since the error checking afforded by the unique constraint will be lost
while the index is missing.

### 14.4.4. Remove Foreign Key Constraints #

Just as with indexes, a foreign key constraint can be checked “in bulk” more
efficiently than row-by-row. So it might be useful to drop foreign key
constraints, load data, and re-create the constraints. Again, there is a
trade-off between data load speed and loss of error checking while the
constraint is missing.

What's more, when you load data into a table with existing foreign key
constraints, each new row requires an entry in the server's list of pending
trigger events (since it is the firing of a trigger that checks the row's
foreign key constraint). Loading many millions of rows can cause the trigger
event queue to overflow available memory, leading to intolerable swapping or
even outright failure of the command. Therefore it may be _necessary_ , not
just desirable, to drop and re-apply foreign keys when loading large amounts
of data. If temporarily removing the constraint isn't acceptable, the only
other recourse may be to split up the load operation into smaller
transactions.

### 14.4.5. Increase `maintenance_work_mem` #

Temporarily increasing the [maintenance_work_mem](runtime-config-
resource.html#GUC-MAINTENANCE-WORK-MEM) configuration variable when loading
large amounts of data can lead to improved performance. This will help to
speed up `CREATE INDEX` commands and `ALTER TABLE ADD FOREIGN KEY` commands.
It won't do much for `COPY` itself, so this advice is only useful when you are
using one or both of the above techniques.

### 14.4.6. Increase `max_wal_size` #

Temporarily increasing the [max_wal_size](runtime-config-wal.html#GUC-MAX-WAL-
SIZE) configuration variable can also make large data loads faster. This is
because loading a large amount of data into PostgreSQL will cause checkpoints
to occur more often than the normal checkpoint frequency (specified by the
`checkpoint_timeout` configuration variable). Whenever a checkpoint occurs,
all dirty pages must be flushed to disk. By increasing `max_wal_size`
temporarily during bulk data loads, the number of checkpoints that are
required can be reduced.

### 14.4.7. Disable WAL Archival and Streaming Replication #

When loading large amounts of data into an installation that uses WAL
archiving or streaming replication, it might be faster to take a new base
backup after the load has completed than to process a large amount of
incremental WAL data. To prevent incremental WAL logging while loading,
disable archiving and streaming replication, by setting [wal_level](runtime-
config-wal.html#GUC-WAL-LEVEL) to `minimal`, [archive_mode](runtime-config-
wal.html#GUC-ARCHIVE-MODE) to `off`, and [max_wal_senders](runtime-config-
replication.html#GUC-MAX-WAL-SENDERS) to zero. But note that changing these
settings requires a server restart, and makes any base backups taken before
unavailable for archive recovery and standby server, which may lead to data
loss.

Aside from avoiding the time for the archiver or WAL sender to process the WAL
data, doing this will actually make certain commands faster, because they do
not to write WAL at all if `wal_level` is `minimal` and the current
subtransaction (or top-level transaction) created or truncated the table or
index they change. (They can guarantee crash safety more cheaply by doing an
`fsync` at the end than by writing WAL.)

### 14.4.8. Run `ANALYZE` Afterwards #

Whenever you have significantly altered the distribution of data within a
table, running [`ANALYZE`](sql-analyze.html "ANALYZE") is strongly
recommended. This includes bulk loading large amounts of data into the table.
Running `ANALYZE` (or `VACUUM ANALYZE`) ensures that the planner has up-to-
date statistics about the table. With no statistics or obsolete statistics,
the planner might make poor decisions during query planning, leading to poor
performance on any tables with inaccurate or nonexistent statistics. Note that
if the autovacuum daemon is enabled, it might run `ANALYZE` automatically; see
[Section 25.1.3](routine-vacuuming.html#VACUUM-FOR-STATISTICS
"25.1.3. Updating Planner Statistics") and [Section 25.1.6](routine-
vacuuming.html#AUTOVACUUM "25.1.6. The Autovacuum Daemon") for more
information.

### 14.4.9. Some Notes about pg_dump #

Dump scripts generated by pg_dump automatically apply several, but not all, of
the above guidelines. To restore a pg_dump dump as quickly as possible, you
need to do a few extra things manually. (Note that these points apply while
_restoring_ a dump, not while _creating_ it. The same points apply whether
loading a text dump with psql or using pg_restore to load from a pg_dump
archive file.)

By default, pg_dump uses `COPY`, and when it is generating a complete schema-
and-data dump, it is careful to load data before creating indexes and foreign
keys. So in this case several guidelines are handled automatically. What is
left for you to do is to:

  * Set appropriate (i.e., larger than normal) values for `maintenance_work_mem` and `max_wal_size`.

  * If using WAL archiving or streaming replication, consider disabling them during the restore. To do that, set `archive_mode` to `off`, `wal_level` to `minimal`, and `max_wal_senders` to zero before loading the dump. Afterwards, set them back to the right values and take a fresh base backup.

  * Experiment with the parallel dump and restore modes of both pg_dump and pg_restore and find the optimal number of concurrent jobs to use. Dumping and restoring in parallel by means of the `-j` option should give you a significantly higher performance over the serial mode.

  * Consider whether the whole dump should be restored as a single transaction. To do that, pass the `-1` or `--single-transaction` command-line option to psql or pg_restore. When using this mode, even the smallest of errors will rollback the entire restore, possibly discarding many hours of processing. Depending on how interrelated the data is, that might seem preferable to manual cleanup, or not. `COPY` commands will run fastest if you use a single transaction and have WAL archiving turned off.

  * If multiple CPUs are available in the database server, consider using pg_restore's `--jobs` option. This allows concurrent data loading and index creation.

  * Run `ANALYZE` afterwards.

A data-only dump will still use `COPY`, but it does not drop or recreate
indexes, and it does not normally touch foreign keys. [14] So when loading a
data-only dump, it is up to you to drop and recreate indexes and foreign keys
if you wish to use those techniques. It's still useful to increase
`max_wal_size` while loading the data, but don't bother increasing
`maintenance_work_mem`; rather, you'd do that while manually recreating
indexes and foreign keys afterwards. And don't forget to `ANALYZE` when you're
done; see [Section 25.1.3](routine-vacuuming.html#VACUUM-FOR-STATISTICS
"25.1.3. Updating Planner Statistics") and [Section 25.1.6](routine-
vacuuming.html#AUTOVACUUM "25.1.6. The Autovacuum Daemon") for more
information.

  

* * *

[14] You can get the effect of disabling foreign keys by using the `--disable-
triggers` option — but realize that that eliminates, rather than just
postpones, foreign key validation, and so it is possible to insert bad data if
you use it.

* * *

[Prev](explicit-joins.html "14.3. Controlling the Planner with Explicit JOIN Clauses")  | [Up](performance-tips.html "Chapter 14. Performance Tips") |  [Next](non-durability.html "14.5. Non-Durable Settings")  
---|---|---  
14.3. Controlling the Planner with Explicit `JOIN` Clauses  | [Home](index.html "PostgreSQL 16.9 Documentation") |  14.5. Non-Durable Settings  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/populate.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

