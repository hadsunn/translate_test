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

Supported Versions: [Current](/docs/current/sql-cluster.html "PostgreSQL 17 -
CLUSTER") ([17](/docs/17/sql-cluster.html "PostgreSQL 17 - CLUSTER")) /
[16](/docs/16/sql-cluster.html "PostgreSQL 16 - CLUSTER") / [15](/docs/15/sql-
cluster.html "PostgreSQL 15 - CLUSTER") / [14](/docs/14/sql-cluster.html
"PostgreSQL 14 - CLUSTER") / [13](/docs/13/sql-cluster.html "PostgreSQL 13 -
CLUSTER")

Development Versions: [18](/docs/18/sql-cluster.html "PostgreSQL 18 -
CLUSTER") / [devel](/docs/devel/sql-cluster.html "PostgreSQL devel - CLUSTER")

Unsupported versions: [12](/docs/12/sql-cluster.html "PostgreSQL 12 -
CLUSTER") / [11](/docs/11/sql-cluster.html "PostgreSQL 11 - CLUSTER") /
[10](/docs/10/sql-cluster.html "PostgreSQL 10 - CLUSTER") /
[9.6](/docs/9.6/sql-cluster.html "PostgreSQL 9.6 - CLUSTER") /
[9.5](/docs/9.5/sql-cluster.html "PostgreSQL 9.5 - CLUSTER") /
[9.4](/docs/9.4/sql-cluster.html "PostgreSQL 9.4 - CLUSTER") /
[9.3](/docs/9.3/sql-cluster.html "PostgreSQL 9.3 - CLUSTER") /
[9.2](/docs/9.2/sql-cluster.html "PostgreSQL 9.2 - CLUSTER") /
[9.1](/docs/9.1/sql-cluster.html "PostgreSQL 9.1 - CLUSTER") /
[9.0](/docs/9.0/sql-cluster.html "PostgreSQL 9.0 - CLUSTER") /
[8.4](/docs/8.4/sql-cluster.html "PostgreSQL 8.4 - CLUSTER") /
[8.3](/docs/8.3/sql-cluster.html "PostgreSQL 8.3 - CLUSTER") /
[8.2](/docs/8.2/sql-cluster.html "PostgreSQL 8.2 - CLUSTER") /
[8.1](/docs/8.1/sql-cluster.html "PostgreSQL 8.1 - CLUSTER") /
[8.0](/docs/8.0/sql-cluster.html "PostgreSQL 8.0 - CLUSTER") /
[7.4](/docs/7.4/sql-cluster.html "PostgreSQL 7.4 - CLUSTER") /
[7.3](/docs/7.3/sql-cluster.html "PostgreSQL 7.3 - CLUSTER") /
[7.2](/docs/7.2/sql-cluster.html "PostgreSQL 7.2 - CLUSTER") /
[7.1](/docs/7.1/sql-cluster.html "PostgreSQL 7.1 - CLUSTER")

__

CLUSTER  
---  
[Prev](sql-close.html "CLOSE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-comment.html "COMMENT")  
  
* * *

## CLUSTER

CLUSTER — cluster a table according to an index

## Synopsis

    
    
    CLUSTER [VERBOSE] _table_name_ [ USING _index_name_ ]
    CLUSTER ( _option_ [, ...] ) _table_name_ [ USING _index_name_ ]
    CLUSTER [VERBOSE]
    
    where _option_ can be one of:
    
        VERBOSE [ _boolean_ ]
    

## Description

`CLUSTER` instructs PostgreSQL to cluster the table specified by
_`table_name`_ based on the index specified by _`index_name`_. The index must
already have been defined on _`table_name`_.

When a table is clustered, it is physically reordered based on the index
information. Clustering is a one-time operation: when the table is
subsequently updated, the changes are not clustered. That is, no attempt is
made to store new or updated rows according to their index order. (If one
wishes, one can periodically recluster by issuing the command again. Also,
setting the table's `fillfactor` storage parameter to less than 100% can aid
in preserving cluster ordering during updates, since updated rows are kept on
the same page if enough space is available there.)

When a table is clustered, PostgreSQL remembers which index it was clustered
by. The form `CLUSTER _`table_name`_` reclusters the table using the same
index as before. You can also use the `CLUSTER` or `SET WITHOUT CLUSTER` forms
of [`ALTER TABLE`](sql-altertable.html "ALTER TABLE") to set the index to be
used for future cluster operations, or to clear any previous setting.

`CLUSTER` without a _`table_name`_ reclusters all the previously-clustered
tables in the current database that the calling user owns, or all such tables
if called by a superuser. This form of `CLUSTER` cannot be executed inside a
transaction block.

When a table is being clustered, an `ACCESS EXCLUSIVE` lock is acquired on it.
This prevents any other database operations (both reads and writes) from
operating on the table until the `CLUSTER` is finished.

## Parameters

_`table_name`_

    

The name (possibly schema-qualified) of a table.

_`index_name`_

    

The name of an index.

`VERBOSE`

    

Prints a progress report as each table is clustered.

_`boolean`_

    

Specifies whether the selected option should be turned on or off. You can
write `TRUE`, `ON`, or `1` to enable the option, and `FALSE`, `OFF`, or `0` to
disable it. The _`boolean`_ value can also be omitted, in which case `TRUE` is
assumed.

## Notes

In cases where you are accessing single rows randomly within a table, the
actual order of the data in the table is unimportant. However, if you tend to
access some data more than others, and there is an index that groups them
together, you will benefit from using `CLUSTER`. If you are requesting a range
of indexed values from a table, or a single indexed value that has multiple
rows that match, `CLUSTER` will help because once the index identifies the
table page for the first row that matches, all other rows that match are
probably already on the same table page, and so you save disk accesses and
speed up the query.

`CLUSTER` can re-sort the table using either an index scan on the specified
index, or (if the index is a b-tree) a sequential scan followed by sorting. It
will attempt to choose the method that will be faster, based on planner cost
parameters and available statistical information.

When an index scan is used, a temporary copy of the table is created that
contains the table data in the index order. Temporary copies of each index on
the table are created as well. Therefore, you need free space on disk at least
equal to the sum of the table size and the index sizes.

When a sequential scan and sort is used, a temporary sort file is also
created, so that the peak temporary space requirement is as much as double the
table size, plus the index sizes. This method is often faster than the index
scan method, but if the disk space requirement is intolerable, you can disable
this choice by temporarily setting [enable_sort](runtime-config-
query.html#GUC-ENABLE-SORT) to `off`.

It is advisable to set [maintenance_work_mem](runtime-config-
resource.html#GUC-MAINTENANCE-WORK-MEM) to a reasonably large value (but not
more than the amount of RAM you can dedicate to the `CLUSTER` operation)
before clustering.

Because the planner records statistics about the ordering of tables, it is
advisable to run [`ANALYZE`](sql-analyze.html "ANALYZE") on the newly
clustered table. Otherwise, the planner might make poor choices of query
plans.

Because `CLUSTER` remembers which indexes are clustered, one can cluster the
tables one wants clustered manually the first time, then set up a periodic
maintenance script that executes `CLUSTER` without any parameters, so that the
desired tables are periodically reclustered.

Each backend running `CLUSTER` will report its progress in the
`pg_stat_progress_cluster` view. See [Section 28.4.2](progress-
reporting.html#CLUSTER-PROGRESS-REPORTING "28.4.2. CLUSTER Progress
Reporting") for details.

Clustering a partitioned table clusters each of its partitions using the
partition of the specified partitioned index. When clustering a partitioned
table, the index may not be omitted. `CLUSTER` on a partitioned table cannot
be executed inside a transaction block.

## Examples

Cluster the table `employees` on the basis of its index `employees_ind`:

    
    
    CLUSTER employees USING employees_ind;
    

Cluster the `employees` table using the same index that was used before:

    
    
    CLUSTER employees;
    

Cluster all tables in the database that have previously been clustered:

    
    
    CLUSTER;
    

## Compatibility

There is no `CLUSTER` statement in the SQL standard.

The syntax

    
    
    CLUSTER _index_name_ ON _table_name_
    

is also supported for compatibility with pre-8.3 PostgreSQL versions.

## See Also

[clusterdb](app-clusterdb.html "clusterdb"), [Section 28.4.2](progress-
reporting.html#CLUSTER-PROGRESS-REPORTING "28.4.2. CLUSTER Progress
Reporting")

* * *

[Prev](sql-close.html "CLOSE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-comment.html "COMMENT")  
---|---|---  
CLOSE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  COMMENT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-cluster.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

