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

Supported Versions: [Current](/docs/current/wal-configuration.html "PostgreSQL
17 - 30.5. WAL Configuration") ([17](/docs/17/wal-configuration.html
"PostgreSQL 17 - 30.5. WAL Configuration")) / [16](/docs/16/wal-
configuration.html "PostgreSQL 16 - 30.5. WAL Configuration") /
[15](/docs/15/wal-configuration.html "PostgreSQL 15 - 30.5. WAL
Configuration") / [14](/docs/14/wal-configuration.html "PostgreSQL 14 -
30.5. WAL Configuration") / [13](/docs/13/wal-configuration.html "PostgreSQL
13 - 30.5. WAL Configuration")

Development Versions: [18](/docs/18/wal-configuration.html "PostgreSQL 18 -
30.5. WAL Configuration") / [devel](/docs/devel/wal-configuration.html
"PostgreSQL devel - 30.5. WAL Configuration")

Unsupported versions: [12](/docs/12/wal-configuration.html "PostgreSQL 12 -
30.5. WAL Configuration") / [11](/docs/11/wal-configuration.html "PostgreSQL
11 - 30.5. WAL Configuration") / [10](/docs/10/wal-configuration.html
"PostgreSQL 10 - 30.5. WAL Configuration") / [9.6](/docs/9.6/wal-
configuration.html "PostgreSQL 9.6 - 30.5. WAL Configuration") /
[9.5](/docs/9.5/wal-configuration.html "PostgreSQL 9.5 - 30.5. WAL
Configuration") / [9.4](/docs/9.4/wal-configuration.html "PostgreSQL 9.4 -
30.5. WAL Configuration") / [9.3](/docs/9.3/wal-configuration.html "PostgreSQL
9.3 - 30.5. WAL Configuration") / [9.2](/docs/9.2/wal-configuration.html
"PostgreSQL 9.2 - 30.5. WAL Configuration") / [9.1](/docs/9.1/wal-
configuration.html "PostgreSQL 9.1 - 30.5. WAL Configuration") /
[9.0](/docs/9.0/wal-configuration.html "PostgreSQL 9.0 - 30.5. WAL
Configuration") / [8.4](/docs/8.4/wal-configuration.html "PostgreSQL 8.4 -
30.5. WAL Configuration") / [8.3](/docs/8.3/wal-configuration.html "PostgreSQL
8.3 - 30.5. WAL Configuration") / [8.2](/docs/8.2/wal-configuration.html
"PostgreSQL 8.2 - 30.5. WAL Configuration") / [8.1](/docs/8.1/wal-
configuration.html "PostgreSQL 8.1 - 30.5. WAL Configuration") /
[8.0](/docs/8.0/wal-configuration.html "PostgreSQL 8.0 - 30.5. WAL
Configuration") / [7.4](/docs/7.4/wal-configuration.html "PostgreSQL 7.4 -
30.5. WAL Configuration") / [7.3](/docs/7.3/wal-configuration.html "PostgreSQL
7.3 - 30.5. WAL Configuration") / [7.2](/docs/7.2/wal-configuration.html
"PostgreSQL 7.2 - 30.5. WAL Configuration") / [7.1](/docs/7.1/wal-
configuration.html "PostgreSQL 7.1 - 30.5. WAL Configuration")

__

30.5. WAL Configuration  
---  
[Prev](wal-async-commit.html "30.4. Asynchronous Commit")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") | Chapter 30. Reliability and the Write-Ahead Log | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](wal-internals.html "30.6. WAL Internals")  
  
* * *

## 30.5. WAL Configuration #

There are several WAL-related configuration parameters that affect database
performance. This section explains their use. Consult [Chapter 20](runtime-
config.html "Chapter 20. Server Configuration") for general information about
setting server configuration parameters.

_Checkpoints_ are points in the sequence of transactions at which it is
guaranteed that the heap and index data files have been updated with all
information written before that checkpoint. At checkpoint time, all dirty data
pages are flushed to disk and a special checkpoint record is written to the
WAL file. (The change records were previously flushed to the WAL files.) In
the event of a crash, the crash recovery procedure looks at the latest
checkpoint record to determine the point in the WAL (known as the redo record)
from which it should start the REDO operation. Any changes made to data files
before that point are guaranteed to be already on disk. Hence, after a
checkpoint, WAL segments preceding the one containing the redo record are no
longer needed and can be recycled or removed. (When WAL archiving is being
done, the WAL segments must be archived before being recycled or removed.)

The checkpoint requirement of flushing all dirty data pages to disk can cause
a significant I/O load. For this reason, checkpoint activity is throttled so
that I/O begins at checkpoint start and completes before the next checkpoint
is due to start; this minimizes performance degradation during checkpoints.

The server's checkpointer process automatically performs a checkpoint every so
often. A checkpoint is begun every [checkpoint_timeout](runtime-config-
wal.html#GUC-CHECKPOINT-TIMEOUT) seconds, or if [max_wal_size](runtime-config-
wal.html#GUC-MAX-WAL-SIZE) is about to be exceeded, whichever comes first. The
default settings are 5 minutes and 1 GB, respectively. If no WAL has been
written since the previous checkpoint, new checkpoints will be skipped even if
`checkpoint_timeout` has passed. (If WAL archiving is being used and you want
to put a lower limit on how often files are archived in order to bound
potential data loss, you should adjust the [archive_timeout](runtime-config-
wal.html#GUC-ARCHIVE-TIMEOUT) parameter rather than the checkpoint
parameters.) It is also possible to force a checkpoint by using the SQL
command `CHECKPOINT`.

Reducing `checkpoint_timeout` and/or `max_wal_size` causes checkpoints to
occur more often. This allows faster after-crash recovery, since less work
will need to be redone. However, one must balance this against the increased
cost of flushing dirty data pages more often. If [full_page_writes](runtime-
config-wal.html#GUC-FULL-PAGE-WRITES) is set (as is the default), there is
another factor to consider. To ensure data page consistency, the first
modification of a data page after each checkpoint results in logging the
entire page content. In that case, a smaller checkpoint interval increases the
volume of output to the WAL, partially negating the goal of using a smaller
interval, and in any case causing more disk I/O.

Checkpoints are fairly expensive, first because they require writing out all
currently dirty buffers, and second because they result in extra subsequent
WAL traffic as discussed above. It is therefore wise to set the checkpointing
parameters high enough so that checkpoints don't happen too often. As a simple
sanity check on your checkpointing parameters, you can set the
[checkpoint_warning](runtime-config-wal.html#GUC-CHECKPOINT-WARNING)
parameter. If checkpoints happen closer together than `checkpoint_warning`
seconds, a message will be output to the server log recommending increasing
`max_wal_size`. Occasional appearance of such a message is not cause for
alarm, but if it appears often then the checkpoint control parameters should
be increased. Bulk operations such as large `COPY` transfers might cause a
number of such warnings to appear if you have not set `max_wal_size` high
enough.

To avoid flooding the I/O system with a burst of page writes, writing dirty
buffers during a checkpoint is spread over a period of time. That period is
controlled by [checkpoint_completion_target](runtime-config-wal.html#GUC-
CHECKPOINT-COMPLETION-TARGET), which is given as a fraction of the checkpoint
interval (configured by using `checkpoint_timeout`). The I/O rate is adjusted
so that the checkpoint finishes when the given fraction of
`checkpoint_timeout` seconds have elapsed, or before `max_wal_size` is
exceeded, whichever is sooner. With the default value of 0.9, PostgreSQL can
be expected to complete each checkpoint a bit before the next scheduled
checkpoint (at around 90% of the last checkpoint's duration). This spreads out
the I/O as much as possible so that the checkpoint I/O load is consistent
throughout the checkpoint interval. The disadvantage of this is that
prolonging checkpoints affects recovery time, because more WAL segments will
need to be kept around for possible use in recovery. A user concerned about
the amount of time required to recover might wish to reduce
`checkpoint_timeout` so that checkpoints occur more frequently but still
spread the I/O across the checkpoint interval. Alternatively,
`checkpoint_completion_target` could be reduced, but this would result in
times of more intense I/O (during the checkpoint) and times of less I/O (after
the checkpoint completed but before the next scheduled checkpoint) and
therefore is not recommended. Although `checkpoint_completion_target` could be
set as high as 1.0, it is typically recommended to set it to no higher than
0.9 (the default) since checkpoints include some other activities besides
writing dirty buffers. A setting of 1.0 is quite likely to result in
checkpoints not being completed on time, which would result in performance
loss due to unexpected variation in the number of WAL segments needed.

On Linux and POSIX platforms [checkpoint_flush_after](runtime-config-
wal.html#GUC-CHECKPOINT-FLUSH-AFTER) allows to force the OS that pages written
by the checkpoint should be flushed to disk after a configurable number of
bytes. Otherwise, these pages may be kept in the OS's page cache, inducing a
stall when `fsync` is issued at the end of a checkpoint. This setting will
often help to reduce transaction latency, but it also can have an adverse
effect on performance; particularly for workloads that are bigger than
[shared_buffers](runtime-config-resource.html#GUC-SHARED-BUFFERS), but smaller
than the OS's page cache.

The number of WAL segment files in `pg_wal` directory depends on
`min_wal_size`, `max_wal_size` and the amount of WAL generated in previous
checkpoint cycles. When old WAL segment files are no longer needed, they are
removed or recycled (that is, renamed to become future segments in the
numbered sequence). If, due to a short-term peak of WAL output rate,
`max_wal_size` is exceeded, the unneeded segment files will be removed until
the system gets back under this limit. Below that limit, the system recycles
enough WAL files to cover the estimated need until the next checkpoint, and
removes the rest. The estimate is based on a moving average of the number of
WAL files used in previous checkpoint cycles. The moving average is increased
immediately if the actual usage exceeds the estimate, so it accommodates peak
usage rather than average usage to some extent. `min_wal_size` puts a minimum
on the amount of WAL files recycled for future usage; that much WAL is always
recycled for future use, even if the system is idle and the WAL usage estimate
suggests that little WAL is needed.

Independently of `max_wal_size`, the most recent [wal_keep_size](runtime-
config-replication.html#GUC-WAL-KEEP-SIZE) megabytes of WAL files plus one
additional WAL file are kept at all times. Also, if WAL archiving is used, old
segments cannot be removed or recycled until they are archived. If WAL
archiving cannot keep up with the pace that WAL is generated, or if
`archive_command` or `archive_library` fails repeatedly, old WAL files will
accumulate in `pg_wal` until the situation is resolved. A slow or failed
standby server that uses a replication slot will have the same effect (see
[Section 27.2.6](warm-standby.html#STREAMING-REPLICATION-SLOTS
"27.2.6. Replication Slots")).

In archive recovery or standby mode, the server periodically performs
_restartpoints_ , which are similar to checkpoints in normal operation: the
server forces all its state to disk, updates the `pg_control` file to indicate
that the already-processed WAL data need not be scanned again, and then
recycles any old WAL segment files in the `pg_wal` directory. Restartpoints
can't be performed more frequently than checkpoints on the primary because
restartpoints can only be performed at checkpoint records. A restartpoint is
triggered when a checkpoint record is reached if at least `checkpoint_timeout`
seconds have passed since the last restartpoint, or if WAL size is about to
exceed `max_wal_size`. However, because of limitations on when a restartpoint
can be performed, `max_wal_size` is often exceeded during recovery, by up to
one checkpoint cycle's worth of WAL. (`max_wal_size` is never a hard limit
anyway, so you should always leave plenty of headroom to avoid running out of
disk space.)

There are two commonly used internal WAL functions: `XLogInsertRecord` and
`XLogFlush`. `XLogInsertRecord` is used to place a new record into the WAL
buffers in shared memory. If there is no space for the new record,
`XLogInsertRecord` will have to write (move to kernel cache) a few filled WAL
buffers. This is undesirable because `XLogInsertRecord` is used on every
database low level modification (for example, row insertion) at a time when an
exclusive lock is held on affected data pages, so the operation needs to be as
fast as possible. What is worse, writing WAL buffers might also force the
creation of a new WAL segment, which takes even more time. Normally, WAL
buffers should be written and flushed by an `XLogFlush` request, which is
made, for the most part, at transaction commit time to ensure that transaction
records are flushed to permanent storage. On systems with high WAL output,
`XLogFlush` requests might not occur often enough to prevent
`XLogInsertRecord` from having to do writes. On such systems one should
increase the number of WAL buffers by modifying the [wal_buffers](runtime-
config-wal.html#GUC-WAL-BUFFERS) parameter. When [full_page_writes](runtime-
config-wal.html#GUC-FULL-PAGE-WRITES) is set and the system is very busy,
setting `wal_buffers` higher will help smooth response times during the period
immediately following each checkpoint.

The [commit_delay](runtime-config-wal.html#GUC-COMMIT-DELAY) parameter defines
for how many microseconds a group commit leader process will sleep after
acquiring a lock within `XLogFlush`, while group commit followers queue up
behind the leader. This delay allows other server processes to add their
commit records to the WAL buffers so that all of them will be flushed by the
leader's eventual sync operation. No sleep will occur if [fsync](runtime-
config-wal.html#GUC-FSYNC) is not enabled, or if fewer than
[commit_siblings](runtime-config-wal.html#GUC-COMMIT-SIBLINGS) other sessions
are currently in active transactions; this avoids sleeping when it's unlikely
that any other session will commit soon. Note that on some platforms, the
resolution of a sleep request is ten milliseconds, so that any nonzero
`commit_delay` setting between 1 and 10000 microseconds would have the same
effect. Note also that on some platforms, sleep operations may take slightly
longer than requested by the parameter.

Since the purpose of `commit_delay` is to allow the cost of each flush
operation to be amortized across concurrently committing transactions
(potentially at the expense of transaction latency), it is necessary to
quantify that cost before the setting can be chosen intelligently. The higher
that cost is, the more effective `commit_delay` is expected to be in
increasing transaction throughput, up to a point. The
[pg_test_fsync](pgtestfsync.html "pg_test_fsync") program can be used to
measure the average time in microseconds that a single WAL flush operation
takes. A value of half of the average time the program reports it takes to
flush after a single 8kB write operation is often the most effective setting
for `commit_delay`, so this value is recommended as the starting point to use
when optimizing for a particular workload. While tuning `commit_delay` is
particularly useful when the WAL is stored on high-latency rotating disks,
benefits can be significant even on storage media with very fast sync times,
such as solid-state drives or RAID arrays with a battery-backed write cache;
but this should definitely be tested against a representative workload. Higher
values of `commit_siblings` should be used in such cases, whereas smaller
`commit_siblings` values are often helpful on higher latency media. Note that
it is quite possible that a setting of `commit_delay` that is too high can
increase transaction latency by so much that total transaction throughput
suffers.

When `commit_delay` is set to zero (the default), it is still possible for a
form of group commit to occur, but each group will consist only of sessions
that reach the point where they need to flush their commit records during the
window in which the previous flush operation (if any) is occurring. At higher
client counts a “gangway effect” tends to occur, so that the effects of group
commit become significant even when `commit_delay` is zero, and thus
explicitly setting `commit_delay` tends to help less. Setting `commit_delay`
can only help when (1) there are some concurrently committing transactions,
and (2) throughput is limited to some degree by commit rate; but with high
rotational latency this setting can be effective in increasing transaction
throughput with as few as two clients (that is, a single committing client
with one sibling transaction).

The [wal_sync_method](runtime-config-wal.html#GUC-WAL-SYNC-METHOD) parameter
determines how PostgreSQL will ask the kernel to force WAL updates out to
disk. All the options should be the same in terms of reliability, with the
exception of `fsync_writethrough`, which can sometimes force a flush of the
disk cache even when other options do not do so. However, it's quite platform-
specific which one will be the fastest. You can test the speeds of different
options using the [pg_test_fsync](pgtestfsync.html "pg_test_fsync") program.
Note that this parameter is irrelevant if `fsync` has been turned off.

Enabling the [wal_debug](runtime-config-developer.html#GUC-WAL-DEBUG)
configuration parameter (provided that PostgreSQL has been compiled with
support for it) will result in each `XLogInsertRecord` and `XLogFlush` WAL
call being logged to the server log. This option might be replaced by a more
general mechanism in the future.

There are two internal functions to write WAL data to disk: `XLogWrite` and
`issue_xlog_fsync`. When [track_wal_io_timing](runtime-config-
statistics.html#GUC-TRACK-WAL-IO-TIMING) is enabled, the total amounts of time
`XLogWrite` writes and `issue_xlog_fsync` syncs WAL data to disk are counted
as `wal_write_time` and `wal_sync_time` in [pg_stat_wal](monitoring-
stats.html#PG-STAT-WAL-VIEW "Table 28.25. pg_stat_wal View"), respectively.
`XLogWrite` is normally called by `XLogInsertRecord` (when there is no space
for the new record in WAL buffers), `XLogFlush` and the WAL writer, to write
WAL buffers to disk and call `issue_xlog_fsync`. `issue_xlog_fsync` is
normally called by `XLogWrite` to sync WAL files to disk. If `wal_sync_method`
is either `open_datasync` or `open_sync`, a write operation in `XLogWrite`
guarantees to sync written WAL data to disk and `issue_xlog_fsync` does
nothing. If `wal_sync_method` is either `fdatasync`, `fsync`, or
`fsync_writethrough`, the write operation moves WAL buffers to kernel cache
and `issue_xlog_fsync` syncs them to disk. Regardless of the setting of
`track_wal_io_timing`, the number of times `XLogWrite` writes and
`issue_xlog_fsync` syncs WAL data to disk are also counted as `wal_write` and
`wal_sync` in `pg_stat_wal`, respectively.

The [recovery_prefetch](runtime-config-wal.html#GUC-RECOVERY-PREFETCH)
parameter can be used to reduce I/O wait times during recovery by instructing
the kernel to initiate reads of disk blocks that will soon be needed but are
not currently in PostgreSQL's buffer pool. The
[maintenance_io_concurrency](runtime-config-resource.html#GUC-MAINTENANCE-IO-
CONCURRENCY) and [wal_decode_buffer_size](runtime-config-wal.html#GUC-WAL-
DECODE-BUFFER-SIZE) settings limit prefetching concurrency and distance,
respectively. By default, it is set to `try`, which enables the feature on
systems where `posix_fadvise` is available.

* * *

[Prev](wal-async-commit.html "30.4. Asynchronous Commit")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") |  [Next](wal-internals.html "30.6. WAL Internals")  
---|---|---  
30.4. Asynchronous Commit  | [Home](index.html "PostgreSQL 16.9 Documentation") |  30.6. WAL Internals  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/wal-configuration.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

