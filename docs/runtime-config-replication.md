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

Supported Versions: [Current](/docs/current/runtime-config-replication.html
"PostgreSQL 17 - 20.6. Replication") ([17](/docs/17/runtime-config-
replication.html "PostgreSQL 17 - 20.6. Replication")) /
[16](/docs/16/runtime-config-replication.html "PostgreSQL 16 -
20.6. Replication") / [15](/docs/15/runtime-config-replication.html
"PostgreSQL 15 - 20.6. Replication") / [14](/docs/14/runtime-config-
replication.html "PostgreSQL 14 - 20.6. Replication") / [13](/docs/13/runtime-
config-replication.html "PostgreSQL 13 - 20.6. Replication")

Development Versions: [18](/docs/18/runtime-config-replication.html
"PostgreSQL 18 - 20.6. Replication") / [devel](/docs/devel/runtime-config-
replication.html "PostgreSQL devel - 20.6. Replication")

Unsupported versions: [12](/docs/12/runtime-config-replication.html
"PostgreSQL 12 - 20.6. Replication") / [11](/docs/11/runtime-config-
replication.html "PostgreSQL 11 - 20.6. Replication") / [10](/docs/10/runtime-
config-replication.html "PostgreSQL 10 - 20.6. Replication") /
[9.6](/docs/9.6/runtime-config-replication.html "PostgreSQL 9.6 -
20.6. Replication") / [9.5](/docs/9.5/runtime-config-replication.html
"PostgreSQL 9.5 - 20.6. Replication") / [9.4](/docs/9.4/runtime-config-
replication.html "PostgreSQL 9.4 - 20.6. Replication") /
[9.3](/docs/9.3/runtime-config-replication.html "PostgreSQL 9.3 -
20.6. Replication") / [9.2](/docs/9.2/runtime-config-replication.html
"PostgreSQL 9.2 - 20.6. Replication") / [9.1](/docs/9.1/runtime-config-
replication.html "PostgreSQL 9.1 - 20.6. Replication")

__

20.6. Replication  
---  
[Prev](runtime-config-wal.html "20.5. Write Ahead Log")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-query.html "20.7. Query Planning")  
  
* * *

## 20.6. Replication #

[20.6.1. Sending Servers](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-SENDER)

[20.6.2. Primary Server](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-PRIMARY)

[20.6.3. Standby Servers](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-STANDBY)

[20.6.4. Subscribers](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-SUBSCRIBER)

These settings control the behavior of the built-in _streaming replication_
feature (see [Section 27.2.5](warm-standby.html#STREAMING-REPLICATION
"27.2.5. Streaming Replication")), and the built-in _logical replication_
feature (see [Chapter 31](logical-replication.html "Chapter 31. Logical
Replication")).

For _streaming replication_ , servers will be either a primary or a standby
server. Primaries can send data, while standbys are always receivers of
replicated data. When cascading replication (see [Section 27.2.7](warm-
standby.html#CASCADING-REPLICATION "27.2.7. Cascading Replication")) is used,
standby servers can also be senders, as well as receivers. Parameters are
mainly for sending and standby servers, though some parameters have meaning
only on the primary server. Settings may vary across the cluster without
problems if that is required.

For _logical replication_ , _publishers_ (servers that do [`CREATE
PUBLICATION`](sql-createpublication.html "CREATE PUBLICATION")) replicate data
to _subscribers_ (servers that do [`CREATE SUBSCRIPTION`](sql-
createsubscription.html "CREATE SUBSCRIPTION")). Servers can also be
publishers and subscribers at the same time. Note, the following sections
refer to publishers as "senders". For more details about logical replication
configuration settings refer to [Section 31.10](logical-replication-
config.html "31.10. Configuration Settings").

### 20.6.1. Sending Servers #

These parameters can be set on any server that is to send replication data to
one or more standby servers. The primary is always a sending server, so these
parameters must always be set on the primary. The role and meaning of these
parameters does not change after a standby becomes the primary.

`max_wal_senders` (`integer`)  #

    

Specifies the maximum number of concurrent connections from standby servers or
streaming base backup clients (i.e., the maximum number of simultaneously
running WAL sender processes). The default is `10`. The value `0` means
replication is disabled. Abrupt disconnection of a streaming client might
leave an orphaned connection slot behind until a timeout is reached, so this
parameter should be set slightly higher than the maximum number of expected
clients so disconnected clients can immediately reconnect. This parameter can
only be set at server start. Also, `wal_level` must be set to `replica` or
higher to allow connections from standby servers.

When running a standby server, you must set this parameter to the same or
higher value than on the primary server. Otherwise, queries will not be
allowed in the standby server.

`max_replication_slots` (`integer`)  #

    

Specifies the maximum number of replication slots (see [Section 27.2.6](warm-
standby.html#STREAMING-REPLICATION-SLOTS "27.2.6. Replication Slots")) that
the server can support. The default is 10. This parameter can only be set at
server start. Setting it to a lower value than the number of currently
existing replication slots will prevent the server from starting. Also,
`wal_level` must be set to `replica` or higher to allow replication slots to
be used.

Note that this parameter also applies on the subscriber side, but with a
different meaning.

`wal_keep_size` (`integer`)  #

    

Specifies the minimum size of past WAL files kept in the `pg_wal` directory,
in case a standby server needs to fetch them for streaming replication. If a
standby server connected to the sending server falls behind by more than
`wal_keep_size` megabytes, the sending server might remove a WAL segment still
needed by the standby, in which case the replication connection will be
terminated. Downstream connections will also eventually fail as a result.
(However, the standby server can recover by fetching the segment from archive,
if WAL archiving is in use.)

This sets only the minimum size of segments retained in `pg_wal`; the system
might need to retain more segments for WAL archival or to recover from a
checkpoint. If `wal_keep_size` is zero (the default), the system doesn't keep
any extra segments for standby purposes, so the number of old WAL segments
available to standby servers is a function of the location of the previous
checkpoint and status of WAL archiving. If this value is specified without
units, it is taken as megabytes. This parameter can only be set in the
`postgresql.conf` file or on the server command line.

`max_slot_wal_keep_size` (`integer`)  #

    

Specify the maximum size of WAL files that [replication slots](warm-
standby.html#STREAMING-REPLICATION-SLOTS "27.2.6. Replication Slots") are
allowed to retain in the `pg_wal` directory at checkpoint time. If
`max_slot_wal_keep_size` is -1 (the default), replication slots may retain an
unlimited amount of WAL files. Otherwise, if restart_lsn of a replication slot
falls behind the current LSN by more than the given size, the standby using
the slot may no longer be able to continue replication due to removal of
required WAL files. You can see the WAL availability of replication slots in
[pg_replication_slots](view-pg-replication-slots.html
"54.19. pg_replication_slots"). If this value is specified without units, it
is taken as megabytes. This parameter can only be set in the `postgresql.conf`
file or on the server command line.

`wal_sender_timeout` (`integer`)  #

    

Terminate replication connections that are inactive for longer than this
amount of time. This is useful for the sending server to detect a standby
crash or network outage. If this value is specified without units, it is taken
as milliseconds. The default value is 60 seconds. A value of zero disables the
timeout mechanism.

With a cluster distributed across multiple geographic locations, using
different values per location brings more flexibility in the cluster
management. A smaller value is useful for faster failure detection with a
standby having a low-latency network connection, and a larger value helps in
judging better the health of a standby if located on a remote location, with a
high-latency network connection.

`track_commit_timestamp` (`boolean`)  #

    

Record commit time of transactions. This parameter can only be set in
`postgresql.conf` file or on the server command line. The default value is
`off`.

### 20.6.2. Primary Server #

These parameters can be set on the primary server that is to send replication
data to one or more standby servers. Note that in addition to these
parameters, [wal_level](runtime-config-wal.html#GUC-WAL-LEVEL) must be set
appropriately on the primary server, and optionally WAL archiving can be
enabled as well (see [Section 20.5.3](runtime-config-wal.html#RUNTIME-CONFIG-
WAL-ARCHIVING "20.5.3. Archiving")). The values of these parameters on standby
servers are irrelevant, although you may wish to set them there in preparation
for the possibility of a standby becoming the primary.

`synchronous_standby_names` (`string`)  #

    

Specifies a list of standby servers that can support _synchronous replication_
, as described in [Section 27.2.8](warm-standby.html#SYNCHRONOUS-REPLICATION
"27.2.8. Synchronous Replication"). There will be one or more active
synchronous standbys; transactions waiting for commit will be allowed to
proceed after these standby servers confirm receipt of their data. The
synchronous standbys will be those whose names appear in this list, and that
are both currently connected and streaming data in real-time (as shown by a
state of `streaming` in the [`pg_stat_replication`](monitoring-
stats.html#MONITORING-PG-STAT-REPLICATION-VIEW "28.2.4. pg_stat_replication")
view). Specifying more than one synchronous standby can allow for very high
availability and protection against data loss.

The name of a standby server for this purpose is the `application_name`
setting of the standby, as set in the standby's connection information. In
case of a physical replication standby, this should be set in the
`primary_conninfo` setting; the default is the setting of
[cluster_name](runtime-config-logging.html#GUC-CLUSTER-NAME) if set, else
`walreceiver`. For logical replication, this can be set in the connection
information of the subscription, and it defaults to the subscription name. For
other replication stream consumers, consult their documentation.

This parameter specifies a list of standby servers using either of the
following syntaxes:

    
    
    [FIRST] _num_sync_ ( _standby_name_ [, ...] )
    ANY _num_sync_ ( _standby_name_ [, ...] )
    _standby_name_ [, ...]
    

where _`num_sync`_ is the number of synchronous standbys that transactions
need to wait for replies from, and _`standby_name`_ is the name of a standby
server. `FIRST` and `ANY` specify the method to choose synchronous standbys
from the listed servers.

The keyword `FIRST`, coupled with _`num_sync`_ , specifies a priority-based
synchronous replication and makes transaction commits wait until their WAL
records are replicated to _`num_sync`_ synchronous standbys chosen based on
their priorities. For example, a setting of `FIRST 3 (s1, s2, s3, s4)` will
cause each commit to wait for replies from three higher-priority standbys
chosen from standby servers `s1`, `s2`, `s3` and `s4`. The standbys whose
names appear earlier in the list are given higher priority and will be
considered as synchronous. Other standby servers appearing later in this list
represent potential synchronous standbys. If any of the current synchronous
standbys disconnects for whatever reason, it will be replaced immediately with
the next-highest-priority standby. The keyword `FIRST` is optional.

The keyword `ANY`, coupled with _`num_sync`_ , specifies a quorum-based
synchronous replication and makes transaction commits wait until their WAL
records are replicated to _at least_ _`num_sync`_ listed standbys. For
example, a setting of `ANY 3 (s1, s2, s3, s4)` will cause each commit to
proceed as soon as at least any three standbys of `s1`, `s2`, `s3` and `s4`
reply.

`FIRST` and `ANY` are case-insensitive. If these keywords are used as the name
of a standby server, its _`standby_name`_ must be double-quoted.

The third syntax was used before PostgreSQL version 9.6 and is still
supported. It's the same as the first syntax with `FIRST` and _`num_sync`_
equal to 1. For example, `FIRST 1 (s1, s2)` and `s1, s2` have the same
meaning: either `s1` or `s2` is chosen as a synchronous standby.

The special entry `*` matches any standby name.

There is no mechanism to enforce uniqueness of standby names. In case of
duplicates one of the matching standbys will be considered as higher priority,
though exactly which one is indeterminate.

### Note

Each _`standby_name`_ should have the form of a valid SQL identifier, unless
it is `*`. You can use double-quoting if necessary. But note that
_`standby_name`_ s are compared to standby application names case-
insensitively, whether double-quoted or not.

If no synchronous standby names are specified here, then synchronous
replication is not enabled and transaction commits will not wait for
replication. This is the default configuration. Even when synchronous
replication is enabled, individual transactions can be configured not to wait
for replication by setting the [synchronous_commit](runtime-config-
wal.html#GUC-SYNCHRONOUS-COMMIT) parameter to `local` or `off`.

This parameter can only be set in the `postgresql.conf` file or on the server
command line.

### 20.6.3. Standby Servers #

These settings control the behavior of a [standby server](warm-
standby.html#STANDBY-SERVER-OPERATION "27.2.2. Standby Server Operation") that
is to receive replication data. Their values on the primary server are
irrelevant.

`primary_conninfo` (`string`)  #

    

Specifies a connection string to be used for the standby server to connect
with a sending server. This string is in the format described in [Section
34.1.1](libpq-connect.html#LIBPQ-CONNSTRING "34.1.1. Connection Strings"). If
any option is unspecified in this string, then the corresponding environment
variable (see [Section 34.15](libpq-envars.html "34.15. Environment
Variables")) is checked. If the environment variable is not set either, then
defaults are used.

The connection string should specify the host name (or address) of the sending
server, as well as the port number if it is not the same as the standby
server's default. Also specify a user name corresponding to a suitably-
privileged role on the sending server (see [Section 27.2.5.1](warm-
standby.html#STREAMING-REPLICATION-AUTHENTICATION
"27.2.5.1. Authentication")). A password needs to be provided too, if the
sender demands password authentication. It can be provided in the
`primary_conninfo` string, or in a separate `~/.pgpass` file on the standby
server (use `replication` as the database name). Do not specify a database
name in the `primary_conninfo` string.

This parameter can only be set in the `postgresql.conf` file or on the server
command line. If this parameter is changed while the WAL receiver process is
running, that process is signaled to shut down and expected to restart with
the new setting (except if `primary_conninfo` is an empty string). This
setting has no effect if the server is not in standby mode.

`primary_slot_name` (`string`)  #

    

Optionally specifies an existing replication slot to be used when connecting
to the sending server via streaming replication to control resource removal on
the upstream node (see [Section 27.2.6](warm-standby.html#STREAMING-
REPLICATION-SLOTS "27.2.6. Replication Slots")). This parameter can only be
set in the `postgresql.conf` file or on the server command line. If this
parameter is changed while the WAL receiver process is running, that process
is signaled to shut down and expected to restart with the new setting. This
setting has no effect if `primary_conninfo` is not set or the server is not in
standby mode.

`hot_standby` (`boolean`)  #

    

Specifies whether or not you can connect and run queries during recovery, as
described in [Section 27.4](hot-standby.html "27.4. Hot Standby"). The default
value is `on`. This parameter can only be set at server start. It only has
effect during archive recovery or in standby mode.

`max_standby_archive_delay` (`integer`)  #

    

When hot standby is active, this parameter determines how long the standby
server should wait before canceling standby queries that conflict with about-
to-be-applied WAL entries, as described in [Section 27.4.2](hot-
standby.html#HOT-STANDBY-CONFLICT "27.4.2. Handling Query Conflicts").
`max_standby_archive_delay` applies when WAL data is being read from WAL
archive (and is therefore not current). If this value is specified without
units, it is taken as milliseconds. The default is 30 seconds. A value of -1
allows the standby to wait forever for conflicting queries to complete. This
parameter can only be set in the `postgresql.conf` file or on the server
command line.

Note that `max_standby_archive_delay` is not the same as the maximum length of
time a query can run before cancellation; rather it is the maximum total time
allowed to apply any one WAL segment's data. Thus, if one query has resulted
in significant delay earlier in the WAL segment, subsequent conflicting
queries will have much less grace time.

`max_standby_streaming_delay` (`integer`)  #

    

When hot standby is active, this parameter determines how long the standby
server should wait before canceling standby queries that conflict with about-
to-be-applied WAL entries, as described in [Section 27.4.2](hot-
standby.html#HOT-STANDBY-CONFLICT "27.4.2. Handling Query Conflicts").
`max_standby_streaming_delay` applies when WAL data is being received via
streaming replication. If this value is specified without units, it is taken
as milliseconds. The default is 30 seconds. A value of -1 allows the standby
to wait forever for conflicting queries to complete. This parameter can only
be set in the `postgresql.conf` file or on the server command line.

Note that `max_standby_streaming_delay` is not the same as the maximum length
of time a query can run before cancellation; rather it is the maximum total
time allowed to apply WAL data once it has been received from the primary
server. Thus, if one query has resulted in significant delay, subsequent
conflicting queries will have much less grace time until the standby server
has caught up again.

`wal_receiver_create_temp_slot` (`boolean`)  #

    

Specifies whether the WAL receiver process should create a temporary
replication slot on the remote instance when no permanent replication slot to
use has been configured (using [primary_slot_name](runtime-config-
replication.html#GUC-PRIMARY-SLOT-NAME)). The default is off. This parameter
can only be set in the `postgresql.conf` file or on the server command line.
If this parameter is changed while the WAL receiver process is running, that
process is signaled to shut down and expected to restart with the new setting.

`wal_receiver_status_interval` (`integer`)  #

    

Specifies the minimum frequency for the WAL receiver process on the standby to
send information about replication progress to the primary or upstream
standby, where it can be seen using the [`pg_stat_replication`](monitoring-
stats.html#MONITORING-PG-STAT-REPLICATION-VIEW "28.2.4. pg_stat_replication")
view. The standby will report the last write-ahead log location it has
written, the last position it has flushed to disk, and the last position it
has applied. This parameter's value is the maximum amount of time between
reports. Updates are sent each time the write or flush positions change, or as
often as specified by this parameter if set to a non-zero value. There are
additional cases where updates are sent while ignoring this parameter; for
example, when processing of the existing WAL completes or when
`synchronous_commit` is set to `remote_apply`. Thus, the apply position may
lag slightly behind the true position. If this value is specified without
units, it is taken as seconds. The default value is 10 seconds. This parameter
can only be set in the `postgresql.conf` file or on the server command line.

`hot_standby_feedback` (`boolean`)  #

    

Specifies whether or not a hot standby will send feedback to the primary or
upstream standby about queries currently executing on the standby. This
parameter can be used to eliminate query cancels caused by cleanup records,
but can cause database bloat on the primary for some workloads. Feedback
messages will not be sent more frequently than once per
`wal_receiver_status_interval`. The default value is `off`. This parameter can
only be set in the `postgresql.conf` file or on the server command line.

If cascaded replication is in use the feedback is passed upstream until it
eventually reaches the primary. Standbys make no other use of feedback they
receive other than to pass upstream.

This setting does not override the behavior of `old_snapshot_threshold` on the
primary; a snapshot on the standby which exceeds the primary's age threshold
can become invalid, resulting in cancellation of transactions on the standby.
This is because `old_snapshot_threshold` is intended to provide an absolute
limit on the time which dead rows can contribute to bloat, which would
otherwise be violated because of the configuration of a standby.

`wal_receiver_timeout` (`integer`)  #

    

Terminate replication connections that are inactive for longer than this
amount of time. This is useful for the receiving standby server to detect a
primary node crash or network outage. If this value is specified without
units, it is taken as milliseconds. The default value is 60 seconds. A value
of zero disables the timeout mechanism. This parameter can only be set in the
`postgresql.conf` file or on the server command line.

`wal_retrieve_retry_interval` (`integer`)  #

    

Specifies how long the standby server should wait when WAL data is not
available from any sources (streaming replication, local `pg_wal` or WAL
archive) before trying again to retrieve WAL data. If this value is specified
without units, it is taken as milliseconds. The default value is 5 seconds.
This parameter can only be set in the `postgresql.conf` file or on the server
command line.

This parameter is useful in configurations where a node in recovery needs to
control the amount of time to wait for new WAL data to be available. For
example, in archive recovery, it is possible to make the recovery more
responsive in the detection of a new WAL file by reducing the value of this
parameter. On a system with low WAL activity, increasing it reduces the amount
of requests necessary to access WAL archives, something useful for example in
cloud environments where the number of times an infrastructure is accessed is
taken into account.

In logical replication, this parameter also limits how often a failing
replication apply worker will be respawned.

`recovery_min_apply_delay` (`integer`)  #

    

By default, a standby server restores WAL records from the sending server as
soon as possible. It may be useful to have a time-delayed copy of the data,
offering opportunities to correct data loss errors. This parameter allows you
to delay recovery by a specified amount of time. For example, if you set this
parameter to `5min`, the standby will replay each transaction commit only when
the system time on the standby is at least five minutes past the commit time
reported by the primary. If this value is specified without units, it is taken
as milliseconds. The default is zero, adding no delay.

It is possible that the replication delay between servers exceeds the value of
this parameter, in which case no delay is added. Note that the delay is
calculated between the WAL time stamp as written on primary and the current
time on the standby. Delays in transfer because of network lag or cascading
replication configurations may reduce the actual wait time significantly. If
the system clocks on primary and standby are not synchronized, this may lead
to recovery applying records earlier than expected; but that is not a major
issue because useful settings of this parameter are much larger than typical
time deviations between servers.

The delay occurs only on WAL records for transaction commits. Other records
are replayed as quickly as possible, which is not a problem because MVCC
visibility rules ensure their effects are not visible until the corresponding
commit record is applied.

The delay occurs once the database in recovery has reached a consistent state,
until the standby is promoted or triggered. After that the standby will end
recovery without further waiting.

WAL records must be kept on the standby until they are ready to be applied.
Therefore, longer delays will result in a greater accumulation of WAL files,
increasing disk space requirements for the standby's `pg_wal` directory.

This parameter is intended for use with streaming replication deployments;
however, if the parameter is specified it will be honored in all cases except
crash recovery. `hot_standby_feedback` will be delayed by use of this feature
which could lead to bloat on the primary; use both together with care.

### Warning

Synchronous replication is affected by this setting when `synchronous_commit`
is set to `remote_apply`; every `COMMIT` will need to wait to be applied.

This parameter can only be set in the `postgresql.conf` file or on the server
command line.

### 20.6.4. Subscribers #

These settings control the behavior of a logical replication subscriber. Their
values on the publisher are irrelevant. See [Section 31.10](logical-
replication-config.html "31.10. Configuration Settings") for more details.

`max_replication_slots` (`integer`)  #

    

Specifies how many replication origins (see [Chapter 50](replication-
origins.html "Chapter 50. Replication Progress Tracking")) can be tracked
simultaneously, effectively limiting how many logical replication
subscriptions can be created on the server. Setting it to a lower value than
the current number of tracked replication origins (reflected in
[pg_replication_origin_status](view-pg-replication-origin-status.html
"54.18. pg_replication_origin_status")) will prevent the server from starting.
`max_replication_slots` must be set to at least the number of subscriptions
that will be added to the subscriber, plus some reserve for table
synchronization.

Note that this parameter also applies on a sending server, but with a
different meaning.

`max_logical_replication_workers` (`integer`)  #

    

Specifies maximum number of logical replication workers. This includes leader
apply workers, parallel apply workers, and table synchronization workers.

Logical replication workers are taken from the pool defined by
`max_worker_processes`.

The default value is 4. This parameter can only be set at server start.

`max_sync_workers_per_subscription` (`integer`)  #

    

Maximum number of synchronization workers per subscription. This parameter
controls the amount of parallelism of the initial data copy during the
subscription initialization or when new tables are added.

Currently, there can be only one synchronization worker per table.

The synchronization workers are taken from the pool defined by
`max_logical_replication_workers`.

The default value is 2. This parameter can only be set in the
`postgresql.conf` file or on the server command line.

`max_parallel_apply_workers_per_subscription` (`integer`)  #

    

Maximum number of parallel apply workers per subscription. This parameter
controls the amount of parallelism for streaming of in-progress transactions
with subscription parameter `streaming = parallel`.

The parallel apply workers are taken from the pool defined by
`max_logical_replication_workers`.

The default value is 2. This parameter can only be set in the
`postgresql.conf` file or on the server command line.

* * *

[Prev](runtime-config-wal.html "20.5. Write Ahead Log")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-query.html "20.7. Query Planning")  
---|---|---  
20.5. Write Ahead Log  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.7. Query Planning  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-
replication.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

