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

Supported Versions: [Current](/docs/current/warm-standby.html "PostgreSQL 17 -
27.2. Log-Shipping Standby Servers") ([17](/docs/17/warm-standby.html
"PostgreSQL 17 - 27.2. Log-Shipping Standby Servers")) / [16](/docs/16/warm-
standby.html "PostgreSQL 16 - 27.2. Log-Shipping Standby Servers") /
[15](/docs/15/warm-standby.html "PostgreSQL 15 - 27.2. Log-Shipping Standby
Servers") / [14](/docs/14/warm-standby.html "PostgreSQL 14 - 27.2. Log-
Shipping Standby Servers") / [13](/docs/13/warm-standby.html "PostgreSQL 13 -
27.2. Log-Shipping Standby Servers")

Development Versions: [18](/docs/18/warm-standby.html "PostgreSQL 18 -
27.2. Log-Shipping Standby Servers") / [devel](/docs/devel/warm-standby.html
"PostgreSQL devel - 27.2. Log-Shipping Standby Servers")

Unsupported versions: [12](/docs/12/warm-standby.html "PostgreSQL 12 -
27.2. Log-Shipping Standby Servers") / [11](/docs/11/warm-standby.html
"PostgreSQL 11 - 27.2. Log-Shipping Standby Servers") / [10](/docs/10/warm-
standby.html "PostgreSQL 10 - 27.2. Log-Shipping Standby Servers") /
[9.6](/docs/9.6/warm-standby.html "PostgreSQL 9.6 - 27.2. Log-Shipping Standby
Servers") / [9.5](/docs/9.5/warm-standby.html "PostgreSQL 9.5 - 27.2. Log-
Shipping Standby Servers") / [9.4](/docs/9.4/warm-standby.html "PostgreSQL 9.4
- 27.2. Log-Shipping Standby Servers") / [9.3](/docs/9.3/warm-standby.html
"PostgreSQL 9.3 - 27.2. Log-Shipping Standby Servers") / [9.2](/docs/9.2/warm-
standby.html "PostgreSQL 9.2 - 27.2. Log-Shipping Standby Servers") /
[9.1](/docs/9.1/warm-standby.html "PostgreSQL 9.1 - 27.2. Log-Shipping Standby
Servers") / [9.0](/docs/9.0/warm-standby.html "PostgreSQL 9.0 - 27.2. Log-
Shipping Standby Servers") / [8.4](/docs/8.4/warm-standby.html "PostgreSQL 8.4
- 27.2. Log-Shipping Standby Servers") / [8.3](/docs/8.3/warm-standby.html
"PostgreSQL 8.3 - 27.2. Log-Shipping Standby Servers") / [8.2](/docs/8.2/warm-
standby.html "PostgreSQL 8.2 - 27.2. Log-Shipping Standby Servers")

__

27.2. Log-Shipping Standby Servers  
---  
[Prev](different-replication-solutions.html "27.1. Comparison of Different Solutions")  | [Up](high-availability.html "Chapter 27. High Availability, Load Balancing, and Replication") | Chapter 27. High Availability, Load Balancing, and Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](warm-standby-failover.html "27.3. Failover")  
  
* * *

## 27.2. Log-Shipping Standby Servers #

[27.2.1. Planning](warm-standby.html#STANDBY-PLANNING)

[27.2.2. Standby Server Operation](warm-standby.html#STANDBY-SERVER-OPERATION)

[27.2.3. Preparing the Primary for Standby Servers](warm-
standby.html#PREPARING-PRIMARY-FOR-STANDBY)

[27.2.4. Setting Up a Standby Server](warm-standby.html#STANDBY-SERVER-SETUP)

[27.2.5. Streaming Replication](warm-standby.html#STREAMING-REPLICATION)

[27.2.6. Replication Slots](warm-standby.html#STREAMING-REPLICATION-SLOTS)

[27.2.7. Cascading Replication](warm-standby.html#CASCADING-REPLICATION)

[27.2.8. Synchronous Replication](warm-standby.html#SYNCHRONOUS-REPLICATION)

[27.2.9. Continuous Archiving in Standby](warm-standby.html#CONTINUOUS-
ARCHIVING-IN-STANDBY)

Continuous archiving can be used to create a _high availability_ (HA) cluster
configuration with one or more _standby servers_ ready to take over operations
if the primary server fails. This capability is widely referred to as _warm
standby_ or _log shipping_.

The primary and standby server work together to provide this capability,
though the servers are only loosely coupled. The primary server operates in
continuous archiving mode, while each standby server operates in continuous
recovery mode, reading the WAL files from the primary. No changes to the
database tables are required to enable this capability, so it offers low
administration overhead compared to some other replication solutions. This
configuration also has relatively low performance impact on the primary
server.

Directly moving WAL records from one database server to another is typically
described as log shipping. PostgreSQL implements file-based log shipping by
transferring WAL records one file (WAL segment) at a time. WAL files (16MB)
can be shipped easily and cheaply over any distance, whether it be to an
adjacent system, another system at the same site, or another system on the far
side of the globe. The bandwidth required for this technique varies according
to the transaction rate of the primary server. Record-based log shipping is
more granular and streams WAL changes incrementally over a network connection
(see [Section 27.2.5](warm-standby.html#STREAMING-REPLICATION
"27.2.5. Streaming Replication")).

It should be noted that log shipping is asynchronous, i.e., the WAL records
are shipped after transaction commit. As a result, there is a window for data
loss should the primary server suffer a catastrophic failure; transactions not
yet shipped will be lost. The size of the data loss window in file-based log
shipping can be limited by use of the `archive_timeout` parameter, which can
be set as low as a few seconds. However such a low setting will substantially
increase the bandwidth required for file shipping. Streaming replication (see
[Section 27.2.5](warm-standby.html#STREAMING-REPLICATION "27.2.5. Streaming
Replication")) allows a much smaller window of data loss.

Recovery performance is sufficiently good that the standby will typically be
only moments away from full availability once it has been activated. As a
result, this is called a warm standby configuration which offers high
availability. Restoring a server from an archived base backup and rollforward
will take considerably longer, so that technique only offers a solution for
disaster recovery, not high availability. A standby server can also be used
for read-only queries, in which case it is called a _hot standby_ server. See
[Section 27.4](hot-standby.html "27.4. Hot Standby") for more information.

### 27.2.1. Planning #

It is usually wise to create the primary and standby servers so that they are
as similar as possible, at least from the perspective of the database server.
In particular, the path names associated with tablespaces will be passed
across unmodified, so both primary and standby servers must have the same
mount paths for tablespaces if that feature is used. Keep in mind that if
[CREATE TABLESPACE](sql-createtablespace.html "CREATE TABLESPACE") is executed
on the primary, any new mount point needed for it must be created on the
primary and all standby servers before the command is executed. Hardware need
not be exactly the same, but experience shows that maintaining two identical
systems is easier than maintaining two dissimilar ones over the lifetime of
the application and system. In any case the hardware architecture must be the
same — shipping from, say, a 32-bit to a 64-bit system will not work.

In general, log shipping between servers running different major PostgreSQL
release levels is not possible. It is the policy of the PostgreSQL Global
Development Group not to make changes to disk formats during minor release
upgrades, so it is likely that running different minor release levels on
primary and standby servers will work successfully. However, no formal support
for that is offered and you are advised to keep primary and standby servers at
the same release level as much as possible. When updating to a new minor
release, the safest policy is to update the standby servers first — a new
minor release is more likely to be able to read WAL files from a previous
minor release than vice versa.

### 27.2.2. Standby Server Operation #

A server enters standby mode if a  `standby.signal` file exists in the data
directory when the server is started.

In standby mode, the server continuously applies WAL received from the primary
server. The standby server can read WAL from a WAL archive (see
[restore_command](runtime-config-wal.html#GUC-RESTORE-COMMAND)) or directly
from the primary over a TCP connection (streaming replication). The standby
server will also attempt to restore any WAL found in the standby cluster's
`pg_wal` directory. That typically happens after a server restart, when the
standby replays again WAL that was streamed from the primary before the
restart, but you can also manually copy files to `pg_wal` at any time to have
them replayed.

At startup, the standby begins by restoring all WAL available in the archive
location, calling `restore_command`. Once it reaches the end of WAL available
there and `restore_command` fails, it tries to restore any WAL available in
the `pg_wal` directory. If that fails, and streaming replication has been
configured, the standby tries to connect to the primary server and start
streaming WAL from the last valid record found in archive or `pg_wal`. If that
fails or streaming replication is not configured, or if the connection is
later disconnected, the standby goes back to step 1 and tries to restore the
file from the archive again. This loop of retries from the archive, `pg_wal`,
and via streaming replication goes on until the server is stopped or is
promoted.

Standby mode is exited and the server switches to normal operation when
`pg_ctl promote` is run, or `pg_promote()` is called. Before failover, any WAL
immediately available in the archive or in `pg_wal` will be restored, but no
attempt is made to connect to the primary.

### 27.2.3. Preparing the Primary for Standby Servers #

Set up continuous archiving on the primary to an archive directory accessible
from the standby, as described in [Section 26.3](continuous-archiving.html
"26.3. Continuous Archiving and Point-in-Time Recovery \(PITR\)"). The archive
location should be accessible from the standby even when the primary is down,
i.e., it should reside on the standby server itself or another trusted server,
not on the primary server.

If you want to use streaming replication, set up authentication on the primary
server to allow replication connections from the standby server(s); that is,
create a role and provide a suitable entry or entries in `pg_hba.conf` with
the database field set to `replication`. Also ensure `max_wal_senders` is set
to a sufficiently large value in the configuration file of the primary server.
If replication slots will be used, ensure that `max_replication_slots` is set
sufficiently high as well.

Take a base backup as described in [Section 26.3.2](continuous-
archiving.html#BACKUP-BASE-BACKUP "26.3.2. Making a Base Backup") to bootstrap
the standby server.

### 27.2.4. Setting Up a Standby Server #

To set up the standby server, restore the base backup taken from primary
server (see [Section 26.3.4](continuous-archiving.html#BACKUP-PITR-RECOVERY
"26.3.4. Recovering Using a Continuous Archive Backup")). Create a file
[`standby.signal`](warm-standby.html#FILE-STANDBY-SIGNAL) in the standby's
cluster data directory. Set [restore_command](runtime-config-wal.html#GUC-
RESTORE-COMMAND) to a simple command to copy files from the WAL archive. If
you plan to have multiple standby servers for high availability purposes, make
sure that `recovery_target_timeline` is set to `latest` (the default), to make
the standby server follow the timeline change that occurs at failover to
another standby.

### Note

[restore_command](runtime-config-wal.html#GUC-RESTORE-COMMAND) should return
immediately if the file does not exist; the server will retry the command
again if necessary.

If you want to use streaming replication, fill in [primary_conninfo](runtime-
config-replication.html#GUC-PRIMARY-CONNINFO) with a libpq connection string,
including the host name (or IP address) and any additional details needed to
connect to the primary server. If the primary needs a password for
authentication, the password needs to be specified in
[primary_conninfo](runtime-config-replication.html#GUC-PRIMARY-CONNINFO) as
well.

If you're setting up the standby server for high availability purposes, set up
WAL archiving, connections and authentication like the primary server, because
the standby server will work as a primary server after failover.

If you're using a WAL archive, its size can be minimized using the
[archive_cleanup_command](runtime-config-wal.html#GUC-ARCHIVE-CLEANUP-COMMAND)
parameter to remove files that are no longer required by the standby server.
The pg_archivecleanup utility is designed specifically to be used with
`archive_cleanup_command` in typical single-standby configurations, see
[pg_archivecleanup](pgarchivecleanup.html "pg_archivecleanup"). Note however,
that if you're using the archive for backup purposes, you need to retain files
needed to recover from at least the latest base backup, even if they're no
longer needed by the standby.

A simple example of configuration is:

    
    
    primary_conninfo = 'host=192.168.1.50 port=5432 user=foo password=foopass options=''-c wal_sender_timeout=5000'''
    restore_command = 'cp /path/to/archive/%f %p'
    archive_cleanup_command = 'pg_archivecleanup /path/to/archive %r'
    

You can have any number of standby servers, but if you use streaming
replication, make sure you set `max_wal_senders` high enough in the primary to
allow them to be connected simultaneously.

### 27.2.5. Streaming Replication #

Streaming replication allows a standby server to stay more up-to-date than is
possible with file-based log shipping. The standby connects to the primary,
which streams WAL records to the standby as they're generated, without waiting
for the WAL file to be filled.

Streaming replication is asynchronous by default (see [Section 27.2.8](warm-
standby.html#SYNCHRONOUS-REPLICATION "27.2.8. Synchronous Replication")), in
which case there is a small delay between committing a transaction in the
primary and the changes becoming visible in the standby. This delay is however
much smaller than with file-based log shipping, typically under one second
assuming the standby is powerful enough to keep up with the load. With
streaming replication, `archive_timeout` is not required to reduce the data
loss window.

If you use streaming replication without file-based continuous archiving, the
server might recycle old WAL segments before the standby has received them. If
this occurs, the standby will need to be reinitialized from a new base backup.
You can avoid this by setting `wal_keep_size` to a value large enough to
ensure that WAL segments are not recycled too early, or by configuring a
replication slot for the standby. If you set up a WAL archive that's
accessible from the standby, these solutions are not required, since the
standby can always use the archive to catch up provided it retains enough
segments.

To use streaming replication, set up a file-based log-shipping standby server
as described in [Section 27.2](warm-standby.html "27.2. Log-Shipping Standby
Servers"). The step that turns a file-based log-shipping standby into
streaming replication standby is setting the `primary_conninfo` setting to
point to the primary server. Set [listen_addresses](runtime-config-
connection.html#GUC-LISTEN-ADDRESSES) and authentication options (see
`pg_hba.conf`) on the primary so that the standby server can connect to the
`replication` pseudo-database on the primary server (see [Section
27.2.5.1](warm-standby.html#STREAMING-REPLICATION-AUTHENTICATION
"27.2.5.1. Authentication")).

On systems that support the keepalive socket option, setting
[tcp_keepalives_idle](runtime-config-connection.html#GUC-TCP-KEEPALIVES-IDLE),
[tcp_keepalives_interval](runtime-config-connection.html#GUC-TCP-KEEPALIVES-
INTERVAL) and [tcp_keepalives_count](runtime-config-connection.html#GUC-TCP-
KEEPALIVES-COUNT) helps the primary promptly notice a broken connection.

Set the maximum number of concurrent connections from the standby servers (see
[max_wal_senders](runtime-config-replication.html#GUC-MAX-WAL-SENDERS) for
details).

When the standby is started and `primary_conninfo` is set correctly, the
standby will connect to the primary after replaying all WAL files available in
the archive. If the connection is established successfully, you will see a
`walreceiver` in the standby, and a corresponding `walsender` process in the
primary.

#### 27.2.5.1. Authentication #

It is very important that the access privileges for replication be set up so
that only trusted users can read the WAL stream, because it is easy to extract
privileged information from it. Standby servers must authenticate to the
primary as an account that has the `REPLICATION` privilege or a superuser. It
is recommended to create a dedicated user account with `REPLICATION` and
`LOGIN` privileges for replication. While `REPLICATION` privilege gives very
high permissions, it does not allow the user to modify any data on the primary
system, which the `SUPERUSER` privilege does.

Client authentication for replication is controlled by a `pg_hba.conf` record
specifying `replication` in the _`database`_ field. For example, if the
standby is running on host IP `192.168.1.100` and the account name for
replication is `foo`, the administrator can add the following line to the
`pg_hba.conf` file on the primary:

    
    
    # Allow the user "foo" from host 192.168.1.100 to connect to the primary
    # as a replication standby if the user's password is correctly supplied.
    #
    # TYPE  DATABASE        USER            ADDRESS                 METHOD
    host    replication     foo             192.168.1.100/32        md5
    

The host name and port number of the primary, connection user name, and
password are specified in the [primary_conninfo](runtime-config-
replication.html#GUC-PRIMARY-CONNINFO). The password can also be set in the
`~/.pgpass` file on the standby (specify `replication` in the _`database`_
field). For example, if the primary is running on host IP `192.168.1.50`, port
`5432`, the account name for replication is `foo`, and the password is
`foopass`, the administrator can add the following line to the
`postgresql.conf` file on the standby:

    
    
    # The standby connects to the primary that is running on host 192.168.1.50
    # and port 5432 as the user "foo" whose password is "foopass".
    primary_conninfo = 'host=192.168.1.50 port=5432 user=foo password=foopass'
    

#### 27.2.5.2. Monitoring #

An important health indicator of streaming replication is the amount of WAL
records generated in the primary, but not yet applied in the standby. You can
calculate this lag by comparing the current WAL write location on the primary
with the last WAL location received by the standby. These locations can be
retrieved using `pg_current_wal_lsn` on the primary and
`pg_last_wal_receive_lsn` on the standby, respectively (see [Table
9.91](functions-admin.html#FUNCTIONS-ADMIN-BACKUP-TABLE "Table 9.91. Backup
Control Functions") and [Table 9.92](functions-admin.html#FUNCTIONS-RECOVERY-
INFO-TABLE "Table 9.92. Recovery Information Functions") for details). The
last WAL receive location in the standby is also displayed in the process
status of the WAL receiver process, displayed using the `ps` command (see
[Section 28.1](monitoring-ps.html "28.1. Standard Unix Tools") for details).

You can retrieve a list of WAL sender processes via the
[`pg_stat_replication`](monitoring-stats.html#MONITORING-PG-STAT-REPLICATION-
VIEW "28.2.4. pg_stat_replication") view. Large differences between
`pg_current_wal_lsn` and the view's `sent_lsn` field might indicate that the
primary server is under heavy load, while differences between `sent_lsn` and
`pg_last_wal_receive_lsn` on the standby might indicate network delay, or that
the standby is under heavy load.

On a hot standby, the status of the WAL receiver process can be retrieved via
the [`pg_stat_wal_receiver`](monitoring-stats.html#MONITORING-PG-STAT-WAL-
RECEIVER-VIEW "28.2.6. pg_stat_wal_receiver") view. A large difference between
`pg_last_wal_replay_lsn` and the view's `flushed_lsn` indicates that WAL is
being received faster than it can be replayed.

### 27.2.6. Replication Slots #

Replication slots provide an automated way to ensure that the primary does not
remove WAL segments until they have been received by all standbys, and that
the primary does not remove rows which could cause a [recovery conflict](hot-
standby.html#HOT-STANDBY-CONFLICT "27.4.2. Handling Query Conflicts") even
when the standby is disconnected.

In lieu of using replication slots, it is possible to prevent the removal of
old WAL segments using [wal_keep_size](runtime-config-replication.html#GUC-
WAL-KEEP-SIZE), or by storing the segments in an archive using
[archive_command](runtime-config-wal.html#GUC-ARCHIVE-COMMAND) or
[archive_library](runtime-config-wal.html#GUC-ARCHIVE-LIBRARY). However, these
methods often result in retaining more WAL segments than required, whereas
replication slots retain only the number of segments known to be needed. On
the other hand, replication slots can retain so many WAL segments that they
fill up the space allocated for `pg_wal`; [max_slot_wal_keep_size](runtime-
config-replication.html#GUC-MAX-SLOT-WAL-KEEP-SIZE) limits the size of WAL
files retained by replication slots.

Similarly, [hot_standby_feedback](runtime-config-replication.html#GUC-HOT-
STANDBY-FEEDBACK) on its own, without also using a replication slot, provides
protection against relevant rows being removed by vacuum, but provides no
protection during any time period when the standby is not connected.
Replication slots overcome these disadvantages.

#### 27.2.6.1. Querying and Manipulating Replication Slots #

Each replication slot has a name, which can contain lower-case letters,
numbers, and the underscore character.

Existing replication slots and their state can be seen in the
[`pg_replication_slots`](view-pg-replication-slots.html
"54.19. pg_replication_slots") view.

Slots can be created and dropped either via the streaming replication protocol
(see [Section 55.4](protocol-replication.html "55.4. Streaming Replication
Protocol")) or via SQL functions (see [Section 9.27.6](functions-
admin.html#FUNCTIONS-REPLICATION "9.27.6. Replication Management Functions")).

#### 27.2.6.2. Configuration Example #

You can create a replication slot like this:

    
    
    postgres=# SELECT * FROM pg_create_physical_replication_slot('node_a_slot');
      slot_name  | lsn
    -------------+-----
     node_a_slot |
    
    postgres=# SELECT slot_name, slot_type, active FROM pg_replication_slots;
      slot_name  | slot_type | active
    -------------+-----------+--------
     node_a_slot | physical  | f
    (1 row)
    

To configure the standby to use this slot, `primary_slot_name` should be
configured on the standby. Here is a simple example:

    
    
    primary_conninfo = 'host=192.168.1.50 port=5432 user=foo password=foopass'
    primary_slot_name = 'node_a_slot'
    

### 27.2.7. Cascading Replication #

The cascading replication feature allows a standby server to accept
replication connections and stream WAL records to other standbys, acting as a
relay. This can be used to reduce the number of direct connections to the
primary and also to minimize inter-site bandwidth overheads.

A standby acting as both a receiver and a sender is known as a cascading
standby. Standbys that are more directly connected to the primary are known as
upstream servers, while those standby servers further away are downstream
servers. Cascading replication does not place limits on the number or
arrangement of downstream servers, though each standby connects to only one
upstream server which eventually links to a single primary server.

A cascading standby sends not only WAL records received from the primary but
also those restored from the archive. So even if the replication connection in
some upstream connection is terminated, streaming replication continues
downstream for as long as new WAL records are available.

Cascading replication is currently asynchronous. Synchronous replication (see
[Section 27.2.8](warm-standby.html#SYNCHRONOUS-REPLICATION
"27.2.8. Synchronous Replication")) settings have no effect on cascading
replication at present.

Hot standby feedback propagates upstream, whatever the cascaded arrangement.

If an upstream standby server is promoted to become the new primary,
downstream servers will continue to stream from the new primary if
`recovery_target_timeline` is set to `'latest'` (the default).

To use cascading replication, set up the cascading standby so that it can
accept replication connections (that is, set [max_wal_senders](runtime-config-
replication.html#GUC-MAX-WAL-SENDERS) and [hot_standby](runtime-config-
replication.html#GUC-HOT-STANDBY), and configure [host-based
authentication](auth-pg-hba-conf.html "21.1. The pg_hba.conf File")). You will
also need to set `primary_conninfo` in the downstream standby to point to the
cascading standby.

### 27.2.8. Synchronous Replication #

PostgreSQL streaming replication is asynchronous by default. If the primary
server crashes then some transactions that were committed may not have been
replicated to the standby server, causing data loss. The amount of data loss
is proportional to the replication delay at the time of failover.

Synchronous replication offers the ability to confirm that all changes made by
a transaction have been transferred to one or more synchronous standby
servers. This extends that standard level of durability offered by a
transaction commit. This level of protection is referred to as 2-safe
replication in computer science theory, and group-1-safe (group-safe and
1-safe) when `synchronous_commit` is set to `remote_write`.

When requesting synchronous replication, each commit of a write transaction
will wait until confirmation is received that the commit has been written to
the write-ahead log on disk of both the primary and standby server. The only
possibility that data can be lost is if both the primary and the standby
suffer crashes at the same time. This can provide a much higher level of
durability, though only if the sysadmin is cautious about the placement and
management of the two servers. Waiting for confirmation increases the user's
confidence that the changes will not be lost in the event of server crashes
but it also necessarily increases the response time for the requesting
transaction. The minimum wait time is the round-trip time between primary and
standby.

Read-only transactions and transaction rollbacks need not wait for replies
from standby servers. Subtransaction commits do not wait for responses from
standby servers, only top-level commits. Long running actions such as data
loading or index building do not wait until the very final commit message. All
two-phase commit actions require commit waits, including both prepare and
commit.

A synchronous standby can be a physical replication standby or a logical
replication subscriber. It can also be any other physical or logical WAL
replication stream consumer that knows how to send the appropriate feedback
messages. Besides the built-in physical and logical replication systems, this
includes special programs such as `pg_receivewal` and `pg_recvlogical` as well
as some third-party replication systems and custom programs. Check the
respective documentation for details on synchronous replication support.

#### 27.2.8.1. Basic Configuration #

Once streaming replication has been configured, configuring synchronous
replication requires only one additional configuration step:
[synchronous_standby_names](runtime-config-replication.html#GUC-SYNCHRONOUS-
STANDBY-NAMES) must be set to a non-empty value. `synchronous_commit` must
also be set to `on`, but since this is the default value, typically no change
is required. (See [Section 20.5.1](runtime-config-wal.html#RUNTIME-CONFIG-WAL-
SETTINGS "20.5.1. Settings") and [Section 20.6.2](runtime-config-
replication.html#RUNTIME-CONFIG-REPLICATION-PRIMARY "20.6.2. Primary
Server").) This configuration will cause each commit to wait for confirmation
that the standby has written the commit record to durable storage.
`synchronous_commit` can be set by individual users, so it can be configured
in the configuration file, for particular users or databases, or dynamically
by applications, in order to control the durability guarantee on a per-
transaction basis.

After a commit record has been written to disk on the primary, the WAL record
is then sent to the standby. The standby sends reply messages each time a new
batch of WAL data is written to disk, unless `wal_receiver_status_interval` is
set to zero on the standby. In the case that `synchronous_commit` is set to
`remote_apply`, the standby sends reply messages when the commit record is
replayed, making the transaction visible. If the standby is chosen as a
synchronous standby, according to the setting of `synchronous_standby_names`
on the primary, the reply messages from that standby will be considered along
with those from other synchronous standbys to decide when to release
transactions waiting for confirmation that the commit record has been
received. These parameters allow the administrator to specify which standby
servers should be synchronous standbys. Note that the configuration of
synchronous replication is mainly on the primary. Named standbys must be
directly connected to the primary; the primary knows nothing about downstream
standby servers using cascaded replication.

Setting `synchronous_commit` to `remote_write` will cause each commit to wait
for confirmation that the standby has received the commit record and written
it out to its own operating system, but not for the data to be flushed to disk
on the standby. This setting provides a weaker guarantee of durability than
`on` does: the standby could lose the data in the event of an operating system
crash, though not a PostgreSQL crash. However, it's a useful setting in
practice because it can decrease the response time for the transaction. Data
loss could only occur if both the primary and the standby crash and the
database of the primary gets corrupted at the same time.

Setting `synchronous_commit` to `remote_apply` will cause each commit to wait
until the current synchronous standbys report that they have replayed the
transaction, making it visible to user queries. In simple cases, this allows
for load balancing with causal consistency.

Users will stop waiting if a fast shutdown is requested. However, as when
using asynchronous replication, the server will not fully shutdown until all
outstanding WAL records are transferred to the currently connected standby
servers.

#### 27.2.8.2. Multiple Synchronous Standbys #

Synchronous replication supports one or more synchronous standby servers;
transactions will wait until all the standby servers which are considered as
synchronous confirm receipt of their data. The number of synchronous standbys
that transactions must wait for replies from is specified in
`synchronous_standby_names`. This parameter also specifies a list of standby
names and the method (`FIRST` and `ANY`) to choose synchronous standbys from
the listed ones.

The method `FIRST` specifies a priority-based synchronous replication and
makes transaction commits wait until their WAL records are replicated to the
requested number of synchronous standbys chosen based on their priorities. The
standbys whose names appear earlier in the list are given higher priority and
will be considered as synchronous. Other standby servers appearing later in
this list represent potential synchronous standbys. If any of the current
synchronous standbys disconnects for whatever reason, it will be replaced
immediately with the next-highest-priority standby.

An example of `synchronous_standby_names` for a priority-based multiple
synchronous standbys is:

    
    
    synchronous_standby_names = 'FIRST 2 (s1, s2, s3)'
    

In this example, if four standby servers `s1`, `s2`, `s3` and `s4` are
running, the two standbys `s1` and `s2` will be chosen as synchronous standbys
because their names appear early in the list of standby names. `s3` is a
potential synchronous standby and will take over the role of synchronous
standby when either of `s1` or `s2` fails. `s4` is an asynchronous standby
since its name is not in the list.

The method `ANY` specifies a quorum-based synchronous replication and makes
transaction commits wait until their WAL records are replicated to _at least_
the requested number of synchronous standbys in the list.

An example of `synchronous_standby_names` for a quorum-based multiple
synchronous standbys is:

    
    
    synchronous_standby_names = 'ANY 2 (s1, s2, s3)'
    

In this example, if four standby servers `s1`, `s2`, `s3` and `s4` are
running, transaction commits will wait for replies from at least any two
standbys of `s1`, `s2` and `s3`. `s4` is an asynchronous standby since its
name is not in the list.

The synchronous states of standby servers can be viewed using the
`pg_stat_replication` view.

#### 27.2.8.3. Planning for Performance #

Synchronous replication usually requires carefully planned and placed standby
servers to ensure applications perform acceptably. Waiting doesn't utilize
system resources, but transaction locks continue to be held until the transfer
is confirmed. As a result, incautious use of synchronous replication will
reduce performance for database applications because of increased response
times and higher contention.

PostgreSQL allows the application developer to specify the durability level
required via replication. This can be specified for the system overall, though
it can also be specified for specific users or connections, or even individual
transactions.

For example, an application workload might consist of: 10% of changes are
important customer details, while 90% of changes are less important data that
the business can more easily survive if it is lost, such as chat messages
between users.

With synchronous replication options specified at the application level (on
the primary) we can offer synchronous replication for the most important
changes, without slowing down the bulk of the total workload. Application
level options are an important and practical tool for allowing the benefits of
synchronous replication for high performance applications.

You should consider that the network bandwidth must be higher than the rate of
generation of WAL data.

#### 27.2.8.4. Planning for High Availability #

`synchronous_standby_names` specifies the number and names of synchronous
standbys that transaction commits made when `synchronous_commit` is set to
`on`, `remote_apply` or `remote_write` will wait for responses from. Such
transaction commits may never be completed if any one of the synchronous
standbys should crash.

The best solution for high availability is to ensure you keep as many
synchronous standbys as requested. This can be achieved by naming multiple
potential synchronous standbys using `synchronous_standby_names`.

In a priority-based synchronous replication, the standbys whose names appear
earlier in the list will be used as synchronous standbys. Standbys listed
after these will take over the role of synchronous standby if one of current
ones should fail.

In a quorum-based synchronous replication, all the standbys appearing in the
list will be used as candidates for synchronous standbys. Even if one of them
should fail, the other standbys will keep performing the role of candidates of
synchronous standby.

When a standby first attaches to the primary, it will not yet be properly
synchronized. This is described as `catchup` mode. Once the lag between
standby and primary reaches zero for the first time we move to real-time
`streaming` state. The catch-up duration may be long immediately after the
standby has been created. If the standby is shut down, then the catch-up
period will increase according to the length of time the standby has been
down. The standby is only able to become a synchronous standby once it has
reached `streaming` state. This state can be viewed using the
`pg_stat_replication` view.

If primary restarts while commits are waiting for acknowledgment, those
waiting transactions will be marked fully committed once the primary database
recovers. There is no way to be certain that all standbys have received all
outstanding WAL data at time of the crash of the primary. Some transactions
may not show as committed on the standby, even though they show as committed
on the primary. The guarantee we offer is that the application will not
receive explicit acknowledgment of the successful commit of a transaction
until the WAL data is known to be safely received by all the synchronous
standbys.

If you really cannot keep as many synchronous standbys as requested then you
should decrease the number of synchronous standbys that transaction commits
must wait for responses from in `synchronous_standby_names` (or disable it)
and reload the configuration file on the primary server.

If the primary is isolated from remaining standby servers you should fail over
to the best candidate of those other remaining standby servers.

If you need to re-create a standby server while transactions are waiting, make
sure that the commands pg_backup_start() and pg_backup_stop() are run in a
session with `synchronous_commit` = `off`, otherwise those requests will wait
forever for the standby to appear.

### 27.2.9. Continuous Archiving in Standby #

When continuous WAL archiving is used in a standby, there are two different
scenarios: the WAL archive can be shared between the primary and the standby,
or the standby can have its own WAL archive. When the standby has its own WAL
archive, set `archive_mode` to `always`, and the standby will call the archive
command for every WAL segment it receives, whether it's by restoring from the
archive or by streaming replication. The shared archive can be handled
similarly, but the `archive_command` or `archive_library` must test if the
file being archived exists already, and if the existing file has identical
contents. This requires more care in the `archive_command` or
`archive_library`, as it must be careful to not overwrite an existing file
with different contents, but return success if the exactly same file is
archived twice. And all that must be done free of race conditions, if two
servers attempt to archive the same file at the same time.

If `archive_mode` is set to `on`, the archiver is not enabled during recovery
or standby mode. If the standby server is promoted, it will start archiving
after the promotion, but will not archive any WAL or timeline history files
that it did not generate itself. To get a complete series of WAL files in the
archive, you must ensure that all WAL is archived, before it reaches the
standby. This is inherently true with file-based log shipping, as the standby
can only restore files that are found in the archive, but not if streaming
replication is enabled. When a server is not in recovery mode, there is no
difference between `on` and `always` modes.

* * *

[Prev](different-replication-solutions.html "27.1. Comparison of Different Solutions")  | [Up](high-availability.html "Chapter 27. High Availability, Load Balancing, and Replication") |  [Next](warm-standby-failover.html "27.3. Failover")  
---|---|---  
27.1. Comparison of Different Solutions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  27.3. Failover  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/warm-standby.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

