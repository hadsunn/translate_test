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

Supported Versions: [Current](/docs/current/sql-vacuum.html "PostgreSQL 17 -
VACUUM") ([17](/docs/17/sql-vacuum.html "PostgreSQL 17 - VACUUM")) /
[16](/docs/16/sql-vacuum.html "PostgreSQL 16 - VACUUM") / [15](/docs/15/sql-
vacuum.html "PostgreSQL 15 - VACUUM") / [14](/docs/14/sql-vacuum.html
"PostgreSQL 14 - VACUUM") / [13](/docs/13/sql-vacuum.html "PostgreSQL 13 -
VACUUM")

Development Versions: [18](/docs/18/sql-vacuum.html "PostgreSQL 18 - VACUUM")
/ [devel](/docs/devel/sql-vacuum.html "PostgreSQL devel - VACUUM")

Unsupported versions: [12](/docs/12/sql-vacuum.html "PostgreSQL 12 - VACUUM")
/ [11](/docs/11/sql-vacuum.html "PostgreSQL 11 - VACUUM") / [10](/docs/10/sql-
vacuum.html "PostgreSQL 10 - VACUUM") / [9.6](/docs/9.6/sql-vacuum.html
"PostgreSQL 9.6 - VACUUM") / [9.5](/docs/9.5/sql-vacuum.html "PostgreSQL 9.5 -
VACUUM") / [9.4](/docs/9.4/sql-vacuum.html "PostgreSQL 9.4 - VACUUM") /
[9.3](/docs/9.3/sql-vacuum.html "PostgreSQL 9.3 - VACUUM") /
[9.2](/docs/9.2/sql-vacuum.html "PostgreSQL 9.2 - VACUUM") /
[9.1](/docs/9.1/sql-vacuum.html "PostgreSQL 9.1 - VACUUM") /
[9.0](/docs/9.0/sql-vacuum.html "PostgreSQL 9.0 - VACUUM") /
[8.4](/docs/8.4/sql-vacuum.html "PostgreSQL 8.4 - VACUUM") /
[8.3](/docs/8.3/sql-vacuum.html "PostgreSQL 8.3 - VACUUM") /
[8.2](/docs/8.2/sql-vacuum.html "PostgreSQL 8.2 - VACUUM") /
[8.1](/docs/8.1/sql-vacuum.html "PostgreSQL 8.1 - VACUUM") /
[8.0](/docs/8.0/sql-vacuum.html "PostgreSQL 8.0 - VACUUM") /
[7.4](/docs/7.4/sql-vacuum.html "PostgreSQL 7.4 - VACUUM") /
[7.3](/docs/7.3/sql-vacuum.html "PostgreSQL 7.3 - VACUUM") /
[7.2](/docs/7.2/sql-vacuum.html "PostgreSQL 7.2 - VACUUM") /
[7.1](/docs/7.1/sql-vacuum.html "PostgreSQL 7.1 - VACUUM")

__

VACUUM  
---  
[Prev](sql-update.html "UPDATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-values.html "VALUES")  
  
* * *

## VACUUM

VACUUM — garbage-collect and optionally analyze a database

## Synopsis

    
    
    VACUUM [ ( _option_ [, ...] ) ] [ _table_and_columns_ [, ...] ]
    VACUUM [ FULL ] [ FREEZE ] [ VERBOSE ] [ ANALYZE ] [ _table_and_columns_ [, ...] ]
    
    where _option_ can be one of:
    
        FULL [ _boolean_ ]
        FREEZE [ _boolean_ ]
        VERBOSE [ _boolean_ ]
        ANALYZE [ _boolean_ ]
        DISABLE_PAGE_SKIPPING [ _boolean_ ]
        SKIP_LOCKED [ _boolean_ ]
        INDEX_CLEANUP { AUTO | ON | OFF }
        PROCESS_MAIN [ _boolean_ ]
        PROCESS_TOAST [ _boolean_ ]
        TRUNCATE [ _boolean_ ]
        PARALLEL _integer_
        SKIP_DATABASE_STATS [ _boolean_ ]
        ONLY_DATABASE_STATS [ _boolean_ ]
        BUFFER_USAGE_LIMIT _size_
    
    and _table_and_columns_ is:
    
        _table_name_ [ ( _column_name_ [, ...] ) ]
    

## Description

`VACUUM` reclaims storage occupied by dead tuples. In normal PostgreSQL
operation, tuples that are deleted or obsoleted by an update are not
physically removed from their table; they remain present until a `VACUUM` is
done. Therefore it's necessary to do `VACUUM` periodically, especially on
frequently-updated tables.

Without a _`table_and_columns`_ list, `VACUUM` processes every table and
materialized view in the current database that the current user has permission
to vacuum. With a list, `VACUUM` processes only those table(s).

`VACUUM ANALYZE` performs a `VACUUM` and then an `ANALYZE` for each selected
table. This is a handy combination form for routine maintenance scripts. See
[ANALYZE](sql-analyze.html "ANALYZE") for more details about its processing.

Plain `VACUUM` (without `FULL`) simply reclaims space and makes it available
for re-use. This form of the command can operate in parallel with normal
reading and writing of the table, as an exclusive lock is not obtained.
However, extra space is not returned to the operating system (in most cases);
it's just kept available for re-use within the same table. It also allows us
to leverage multiple CPUs in order to process indexes. This feature is known
as _parallel vacuum_. To disable this feature, one can use `PARALLEL` option
and specify parallel workers as zero. `VACUUM FULL` rewrites the entire
contents of the table into a new disk file with no extra space, allowing
unused space to be returned to the operating system. This form is much slower
and requires an `ACCESS EXCLUSIVE` lock on each table while it is being
processed.

When the option list is surrounded by parentheses, the options can be written
in any order. Without parentheses, options must be specified in exactly the
order shown above. The parenthesized syntax was added in PostgreSQL 9.0; the
unparenthesized syntax is deprecated.

## Parameters

`FULL`

    

Selects “full” vacuum, which can reclaim more space, but takes much longer and
exclusively locks the table. This method also requires extra disk space, since
it writes a new copy of the table and doesn't release the old copy until the
operation is complete. Usually this should only be used when a significant
amount of space needs to be reclaimed from within the table.

`FREEZE`

    

Selects aggressive “freezing” of tuples. Specifying `FREEZE` is equivalent to
performing `VACUUM` with the [vacuum_freeze_min_age](runtime-config-
client.html#GUC-VACUUM-FREEZE-MIN-AGE) and [vacuum_freeze_table_age](runtime-
config-client.html#GUC-VACUUM-FREEZE-TABLE-AGE) parameters set to zero.
Aggressive freezing is always performed when the table is rewritten, so this
option is redundant when `FULL` is specified.

`VERBOSE`

    

Prints a detailed vacuum activity report for each table.

`ANALYZE`

    

Updates statistics used by the planner to determine the most efficient way to
execute a query.

`DISABLE_PAGE_SKIPPING`

    

Normally, `VACUUM` will skip pages based on the [visibility map](routine-
vacuuming.html#VACUUM-FOR-VISIBILITY-MAP "25.1.4. Updating the Visibility
Map"). Pages where all tuples are known to be frozen can always be skipped,
and those where all tuples are known to be visible to all transactions may be
skipped except when performing an aggressive vacuum. Furthermore, except when
performing an aggressive vacuum, some pages may be skipped in order to avoid
waiting for other sessions to finish using them. This option disables all
page-skipping behavior, and is intended to be used only when the contents of
the visibility map are suspect, which should happen only if there is a
hardware or software issue causing database corruption.

`SKIP_LOCKED`

    

Specifies that `VACUUM` should not wait for any conflicting locks to be
released when beginning work on a relation: if a relation cannot be locked
immediately without waiting, the relation is skipped. Note that even with this
option, `VACUUM` may still block when opening the relation's indexes.
Additionally, `VACUUM ANALYZE` may still block when acquiring sample rows from
partitions, table inheritance children, and some types of foreign tables.
Also, while `VACUUM` ordinarily processes all partitions of specified
partitioned tables, this option will cause `VACUUM` to skip all partitions if
there is a conflicting lock on the partitioned table.

`INDEX_CLEANUP`

    

Normally, `VACUUM` will skip index vacuuming when there are very few dead
tuples in the table. The cost of processing all of the table's indexes is
expected to greatly exceed the benefit of removing dead index tuples when this
happens. This option can be used to force `VACUUM` to process indexes when
there are more than zero dead tuples. The default is `AUTO`, which allows
`VACUUM` to skip index vacuuming when appropriate. If `INDEX_CLEANUP` is set
to `ON`, `VACUUM` will conservatively remove all dead tuples from indexes.
This may be useful for backwards compatibility with earlier releases of
PostgreSQL where this was the standard behavior.

`INDEX_CLEANUP` can also be set to `OFF` to force `VACUUM` to _always_ skip
index vacuuming, even when there are many dead tuples in the table. This may
be useful when it is necessary to make `VACUUM` run as quickly as possible to
avoid imminent transaction ID wraparound (see [Section 25.1.5](routine-
vacuuming.html#VACUUM-FOR-WRAPAROUND "25.1.5. Preventing Transaction ID
Wraparound Failures")). However, the wraparound failsafe mechanism controlled
by [vacuum_failsafe_age](runtime-config-client.html#GUC-VACUUM-FAILSAFE-AGE)
will generally trigger automatically to avoid transaction ID wraparound
failure, and should be preferred. If index cleanup is not performed regularly,
performance may suffer, because as the table is modified indexes will
accumulate dead tuples and the table itself will accumulate dead line pointers
that cannot be removed until index cleanup is completed.

This option has no effect for tables that have no index and is ignored if the
`FULL` option is used. It also has no effect on the transaction ID wraparound
failsafe mechanism. When triggered it will skip index vacuuming, even when
`INDEX_CLEANUP` is set to `ON`.

`PROCESS_MAIN`

    

Specifies that `VACUUM` should attempt to process the main relation. This is
usually the desired behavior and is the default. Setting this option to false
may be useful when it is only necessary to vacuum a relation's corresponding
`TOAST` table.

`PROCESS_TOAST`

    

Specifies that `VACUUM` should attempt to process the corresponding `TOAST`
table for each relation, if one exists. This is usually the desired behavior
and is the default. Setting this option to false may be useful when it is only
necessary to vacuum the main relation. This option is required when the `FULL`
option is used.

`TRUNCATE`

    

Specifies that `VACUUM` should attempt to truncate off any empty pages at the
end of the table and allow the disk space for the truncated pages to be
returned to the operating system. This is normally the desired behavior and is
the default unless the `vacuum_truncate` option has been set to false for the
table to be vacuumed. Setting this option to false may be useful to avoid
`ACCESS EXCLUSIVE` lock on the table that the truncation requires. This option
is ignored if the `FULL` option is used.

`PARALLEL`

    

Perform index vacuum and index cleanup phases of `VACUUM` in parallel using
_`integer`_ background workers (for the details of each vacuum phase, please
refer to [Table 28.45](progress-reporting.html#VACUUM-PHASES
"Table 28.45. VACUUM Phases")). The number of workers used to perform the
operation is equal to the number of indexes on the relation that support
parallel vacuum which is limited by the number of workers specified with
`PARALLEL` option if any which is further limited by
[max_parallel_maintenance_workers](runtime-config-resource.html#GUC-MAX-
PARALLEL-MAINTENANCE-WORKERS). An index can participate in parallel vacuum if
and only if the size of the index is more than
[min_parallel_index_scan_size](runtime-config-query.html#GUC-MIN-PARALLEL-
INDEX-SCAN-SIZE). Please note that it is not guaranteed that the number of
parallel workers specified in _`integer`_ will be used during execution. It is
possible for a vacuum to run with fewer workers than specified, or even with
no workers at all. Only one worker can be used per index. So parallel workers
are launched only when there are at least `2` indexes in the table. Workers
for vacuum are launched before the start of each phase and exit at the end of
the phase. These behaviors might change in a future release. This option can't
be used with the `FULL` option.

`SKIP_DATABASE_STATS`

    

Specifies that `VACUUM` should skip updating the database-wide statistics
about oldest unfrozen XIDs. Normally `VACUUM` will update these statistics
once at the end of the command. However, this can take awhile in a database
with a very large number of tables, and it will accomplish nothing unless the
table that had contained the oldest unfrozen XID was among those vacuumed.
Moreover, if multiple `VACUUM` commands are issued in parallel, only one of
them can update the database-wide statistics at a time. Therefore, if an
application intends to issue a series of many `VACUUM` commands, it can be
helpful to set this option in all but the last such command; or set it in all
the commands and separately issue `VACUUM (ONLY_DATABASE_STATS)` afterwards.

`ONLY_DATABASE_STATS`

    

Specifies that `VACUUM` should do nothing except update the database-wide
statistics about oldest unfrozen XIDs. When this option is specified, the
_`table_and_columns`_ list must be empty, and no other option may be enabled
except `VERBOSE`.

`BUFFER_USAGE_LIMIT`

    

Specifies the [](glossary.html#GLOSSARY-BUFFER-ACCESS-STRATEGY)[Buffer Access
Strategy](glossary.html#GLOSSARY-BUFFER-ACCESS-STRATEGY "Buffer Access
Strategy") ring buffer size for `VACUUM`. This size is used to calculate the
number of shared buffers which will be reused as part of this strategy. `0`
disables use of a `Buffer Access Strategy`. If `ANALYZE` is also specified,
the `BUFFER_USAGE_LIMIT` value is used for both the vacuum and analyze stages.
This option can't be used with the `FULL` option except if `ANALYZE` is also
specified. When this option is not specified, `VACUUM` uses the value from
[vacuum_buffer_usage_limit](runtime-config-resource.html#GUC-VACUUM-BUFFER-
USAGE-LIMIT). Higher settings can allow `VACUUM` to run more quickly, but
having too large a setting may cause too many other useful pages to be evicted
from shared buffers. The minimum value is `128 kB` and the maximum value is
`16 GB`.

_`boolean`_

    

Specifies whether the selected option should be turned on or off. You can
write `TRUE`, `ON`, or `1` to enable the option, and `FALSE`, `OFF`, or `0` to
disable it. The _`boolean`_ value can also be omitted, in which case `TRUE` is
assumed.

_`integer`_

    

Specifies a non-negative integer value passed to the selected option.

_`size`_

    

Specifies an amount of memory in kilobytes. Sizes may also be specified as a
string containing the numerical size followed by any one of the following
memory units: `B` (bytes), `kB` (kilobytes), `MB` (megabytes), `GB`
(gigabytes), or `TB` (terabytes).

_`table_name`_

    

The name (optionally schema-qualified) of a specific table or materialized
view to vacuum. If the specified table is a partitioned table, all of its leaf
partitions are vacuumed.

_`column_name`_

    

The name of a specific column to analyze. Defaults to all columns. If a column
list is specified, `ANALYZE` must also be specified.

## Outputs

When `VERBOSE` is specified, `VACUUM` emits progress messages to indicate
which table is currently being processed. Various statistics about the tables
are printed as well.

## Notes

To vacuum a table, one must ordinarily be the table's owner or a superuser.
However, database owners are allowed to vacuum all tables in their databases,
except shared catalogs. (The restriction for shared catalogs means that a true
database-wide `VACUUM` can only be performed by a superuser.) `VACUUM` will
skip over any tables that the calling user does not have permission to vacuum.

`VACUUM` cannot be executed inside a transaction block.

For tables with GIN indexes, `VACUUM` (in any form) also completes any pending
index insertions, by moving pending index entries to the appropriate places in
the main GIN index structure. See [Section 70.4.1](gin-
implementation.html#GIN-FAST-UPDATE "70.4.1. GIN Fast Update Technique") for
details.

We recommend that all databases be vacuumed regularly in order to remove dead
rows. PostgreSQL includes an “autovacuum” facility which can automate routine
vacuum maintenance. For more information about automatic and manual vacuuming,
see [Section 25.1](routine-vacuuming.html "25.1. Routine Vacuuming").

The `FULL` option is not recommended for routine use, but might be useful in
special cases. An example is when you have deleted or updated most of the rows
in a table and would like the table to physically shrink to occupy less disk
space and allow faster table scans. `VACUUM FULL` will usually shrink the
table more than a plain `VACUUM` would.

The `PARALLEL` option is used only for vacuum purposes. If this option is
specified with the `ANALYZE` option, it does not affect `ANALYZE`.

`VACUUM` causes a substantial increase in I/O traffic, which might cause poor
performance for other active sessions. Therefore, it is sometimes advisable to
use the cost-based vacuum delay feature. For parallel vacuum, each worker
sleeps in proportion to the work done by that worker. See [Section
20.4.4](runtime-config-resource.html#RUNTIME-CONFIG-RESOURCE-VACUUM-COST
"20.4.4. Cost-based Vacuum Delay") for details.

Each backend running `VACUUM` without the `FULL` option will report its
progress in the `pg_stat_progress_vacuum` view. Backends running `VACUUM FULL`
will instead report their progress in the `pg_stat_progress_cluster` view. See
[Section 28.4.5](progress-reporting.html#VACUUM-PROGRESS-REPORTING
"28.4.5. VACUUM Progress Reporting") and [Section 28.4.2](progress-
reporting.html#CLUSTER-PROGRESS-REPORTING "28.4.2. CLUSTER Progress
Reporting") for details.

## Examples

To clean a single table `onek`, analyze it for the optimizer and print a
detailed vacuum activity report:

    
    
    VACUUM (VERBOSE, ANALYZE) onek;
    

## Compatibility

There is no `VACUUM` statement in the SQL standard.

## See Also

[vacuumdb](app-vacuumdb.html "vacuumdb"), [Section 20.4.4](runtime-config-
resource.html#RUNTIME-CONFIG-RESOURCE-VACUUM-COST "20.4.4. Cost-based Vacuum
Delay"), [Section 25.1.6](routine-vacuuming.html#AUTOVACUUM "25.1.6. The
Autovacuum Daemon"), [Section 28.4.5](progress-reporting.html#VACUUM-PROGRESS-
REPORTING "28.4.5. VACUUM Progress Reporting"), [Section 28.4.2](progress-
reporting.html#CLUSTER-PROGRESS-REPORTING "28.4.2. CLUSTER Progress
Reporting")

* * *

[Prev](sql-update.html "UPDATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-values.html "VALUES")  
---|---|---  
UPDATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  VALUES  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-vacuum.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

