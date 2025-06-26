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

Supported Versions: [16](/docs/16/release-16.html "PostgreSQL 16 -
E.10. Release 16")

__

E.10. Release 16  
---  
[Prev](release-16-1.html "E.9. Release 16.1")  | [Up](release.html "Appendix E. Release Notes") | Appendix E. Release Notes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](release-prior.html "E.11. Prior Releases")  
  
* * *

## E.10. Release 16 #

[E.10.1. Overview](release-16.html#RELEASE-16-HIGHLIGHTS)

[E.10.2. Migration to Version 16](release-16.html#RELEASE-16-MIGRATION)

[E.10.3. Changes](release-16.html#RELEASE-16-CHANGES)

[E.10.4. Acknowledgments](release-16.html#RELEASE-16-ACKNOWLEDGEMENTS)

**Release date:  **2023-09-14

### E.10.1. Overview #

PostgreSQL 16 contains many new features and enhancements, including:

  * Allow parallelization of `FULL` and internal right `OUTER` hash joins

  * Allow logical replication from standby servers

  * Allow logical replication subscribers to apply large transactions in parallel

  * Allow monitoring of I/O statistics using the new `pg_stat_io` view

  * Add SQL/JSON constructors and identity functions

  * Improve performance of vacuum freezing

  * Add support for regular expression matching of user and database names in `pg_hba.conf`, and user names in `pg_ident.conf`

The above items and other new features of PostgreSQL 16 are explained in more
detail in the sections below.

### E.10.2. Migration to Version 16 #

A dump/restore using [pg_dumpall](app-pg-dumpall.html "pg_dumpall") or use of
[pg_upgrade](pgupgrade.html "pg_upgrade") or logical replication is required
for those wishing to migrate data from any previous release. See [Section
19.6](upgrading.html "19.6. Upgrading a PostgreSQL Cluster") for general
information on migrating to new major releases.

Version 16 contains a number of changes that may affect compatibility with
previous releases. Observe the following incompatibilities:

  * Change assignment rules for [PL/pgSQL](plpgsql-cursors.html#PLPGSQL-OPEN-BOUND-CURSOR "43.7.2.3. Opening a Bound Cursor") bound cursor variables (Tom Lane) [§](https://postgr.es/c/d747dc85a)

Previously, the string value of such variables was set to match the variable
name during cursor assignment; now it will be assigned during
[`OPEN`](plpgsql-cursors.html#PLPGSQL-CURSOR-OPENING "43.7.2. Opening
Cursors"), and will not match the variable name. To restore the previous
behavior, assign the desired portal name to the cursor variable before `OPEN`.

  * Disallow [`NULLS NOT DISTINCT`](sql-createindex.html "CREATE INDEX") indexes for primary keys (Daniel Gustafsson) [§](https://postgr.es/c/d95952325)

  * Change [`REINDEX DATABASE`](sql-reindex.html "REINDEX") and [reindexdb](app-reindexdb.html "reindexdb") to not process indexes on system catalogs (Simon Riggs) [§](https://postgr.es/c/2cbc3c17a) [§](https://postgr.es/c/0a5f06b84)

Processing such indexes is still possible using `REINDEX SYSTEM` and
[`reindexdb --system`](app-reindexdb.html "reindexdb").

  * Tighten [`GENERATED`](ddl-generated-columns.html "5.3. Generated Columns") expression restrictions on inherited and partitioned tables (Amit Langote, Tom Lane) [§](https://postgr.es/c/8bf6ec3ba)

Columns of parent/partitioned and child/partition tables must all have the
same generation status, though now the actual generation expressions can be
different.

  * Remove [pg_walinspect](pgwalinspect.html "F.37. pg_walinspect — low-level WAL inspection") functions `pg_get_wal_records_info_till_end_of_wal()` and `pg_get_wal_stats_till_end_of_wal()` (Bharath Rupireddy) [§](https://postgr.es/c/5c1b66280)

  * Rename server variable `force_parallel_mode` to [`debug_parallel_query`](runtime-config-developer.html#GUC-DEBUG-PARALLEL-QUERY) (David Rowley) [§](https://postgr.es/c/5352ca22e) [§](https://postgr.es/c/0981846b9)

  * Remove the ability to [create views](sql-createview.html "CREATE VIEW") manually with `ON SELECT` rules (Tom Lane) [§](https://postgr.es/c/b23cd185f)

  * Remove the server variable `vacuum_defer_cleanup_age` (Andres Freund) [§](https://postgr.es/c/1118cd37e)

This has been unnecessary since [`hot_standby_feedback`](runtime-config-
replication.html#GUC-HOT-STANDBY-FEEDBACK) and [replication slots](warm-
standby.html#STREAMING-REPLICATION-SLOTS "27.2.6. Replication Slots") were
added.

  * Remove server variable `promote_trigger_file` (Simon Riggs) [§](https://postgr.es/c/cd4329d93)

This was used to promote a standby to primary, but is now more easily
accomplished with [`pg_ctl promote`](app-pg-ctl.html "pg_ctl") or
[`pg_promote()`](functions-admin.html#FUNCTIONS-RECOVERY-CONTROL-TABLE
"Table 9.93. Recovery Control Functions").

  * Remove read-only server variables `lc_collate` and `lc_ctype` (Peter Eisentraut) [§](https://postgr.es/c/b0f6c4371)

Collations and locales can vary between databases so having them as read-only
server variables was unhelpful.

  * Role inheritance now controls the default inheritance status of member roles added during [`GRANT`](sql-grant.html "GRANT") (Robert Haas) [§](https://postgr.es/c/e3ce2de09)

The role's default inheritance behavior can be overridden with the new `GRANT
... WITH INHERIT` clause. This allows inheritance of some roles and not others
because the members' inheritance status is set at `GRANT` time. Previously the
inheritance status of member roles was controlled only by the role's
inheritance status, and changes to a role's inheritance status affected all
previous and future member roles.

  * Restrict the privileges of [`CREATEROLE`](sql-createrole.html "CREATE ROLE") and its ability to modify other roles (Robert Haas) [§](https://postgr.es/c/cf5eb37c5) [§](https://postgr.es/c/f1358ca52)

Previously roles with `CREATEROLE` privileges could change many aspects of any
non-superuser role. Such changes, including adding members, now require the
role requesting the change to have `ADMIN OPTION` permission. For example,
they can now change the `CREATEDB`, `REPLICATION`, and `BYPASSRLS` properties
only if they also have those permissions.

  * Remove symbolic links for the postmaster binary (Peter Eisentraut) [§](https://postgr.es/c/37e267335)

### E.10.3. Changes #

Below you will find a detailed account of the changes between PostgreSQL 16
and the previous major release.

#### E.10.3.1. Server #

##### E.10.3.1.1. Optimizer #

  * Allow incremental sorts in more cases, including `DISTINCT` (David Rowley) [§](https://postgr.es/c/b59242209) [§](https://postgr.es/c/3c6fc5820)

  * Add the ability for aggregates having `ORDER BY` or `DISTINCT` to use pre-sorted data (David Rowley) [§](https://postgr.es/c/1349d2790) [§](https://postgr.es/c/3226f4728) [§](https://postgr.es/c/da5800d5f)

The new server variable [`enable_presorted_aggregate`](runtime-config-
query.html#GUC-ENABLE-PRESORTED-AGGREGATE) can be used to disable this.

  * Allow memoize atop a `UNION ALL` (Richard Guo) [§](https://postgr.es/c/9bfd2822b)

  * Allow anti-joins to be performed with the non-nullable input as the inner relation (Richard Guo) [§](https://postgr.es/c/16dc2703c)

  * Allow parallelization of [`FULL`](queries-table-expressions.html#QUERIES-JOIN "7.2.1.1. Joined Tables") and internal right `OUTER` hash joins (Melanie Plageman, Thomas Munro) [§](https://postgr.es/c/11c2d6fdf)

  * Improve the accuracy of [`GIN`](gin.html "Chapter 70. GIN Indexes") index access optimizer costs (Ronan Dunklau) [§](https://postgr.es/c/cd9479af2)

##### E.10.3.1.2. General Performance #

  * Allow more efficient addition of heap and index pages (Andres Freund) [§](https://postgr.es/c/00d1e02be) [§](https://postgr.es/c/26158b852)

  * During non-freeze operations, perform page [freezing](routine-vacuuming.html#VACUUM-FOR-WRAPAROUND "25.1.5. Preventing Transaction ID Wraparound Failures") where appropriate (Peter Geoghegan) [§](https://postgr.es/c/d977ffd92) [§](https://postgr.es/c/9e5405993) [§](https://postgr.es/c/1de58df4f)

This makes full-table freeze vacuums less necessary.

  * Allow window functions to use the faster [`ROWS`](sql-expressions.html#SYNTAX-WINDOW-FUNCTIONS "4.2.8. Window Function Calls") mode internally when `RANGE` mode is active but unnecessary (David Rowley) [§](https://postgr.es/c/ed1a88dda)

  * Allow optimization of always-increasing window functions [`ntile()`](functions-window.html#FUNCTIONS-WINDOW-TABLE "Table 9.64. General-Purpose Window Functions"), `cume_dist()` and `percent_rank()` (David Rowley) [§](https://postgr.es/c/456fa635a)

  * Allow aggregate functions [`string_agg()`](functions-aggregate.html#FUNCTIONS-AGGREGATE-TABLE "Table 9.59. General-Purpose Aggregate Functions") and `array_agg()` to be parallelized (David Rowley) [§](https://postgr.es/c/16fd03e95)

  * Improve performance by caching [`RANGE`](ddl-partitioning.html#DDL-PARTITIONING-OVERVIEW "5.11.1. Overview") and `LIST` partition lookups (Amit Langote, Hou Zhijie, David Rowley) [§](https://postgr.es/c/3592e0ff9)

  * Allow control of the shared buffer usage by vacuum and analyze (Melanie Plageman) [§](https://postgr.es/c/1cbbee033) [§](https://postgr.es/c/ae78cae3b) [§](https://postgr.es/c/b72f564d8)

The [`VACUUM`](sql-vacuum.html "VACUUM")/[`ANALYZE`](sql-analyze.html
"ANALYZE") option is `BUFFER_USAGE_LIMIT`, and the [vacuumdb](app-
vacuumdb.html "vacuumdb") option is `--buffer-usage-limit`. The default value
is set by server variable [`vacuum_buffer_usage_limit`](runtime-config-
resource.html#GUC-VACUUM-BUFFER-USAGE-LIMIT), which also controls autovacuum.

  * Support [`wal_sync_method=fdatasync`](runtime-config-wal.html#GUC-WAL-SYNC-METHOD) on Windows (Thomas Munro) [§](https://postgr.es/c/9430fb407)

  * Allow [HOT](storage-hot.html "73.7. Heap-Only Tuples \(HOT\)") updates if only `BRIN`-indexed columns are updated (Matthias van de Meent, Josef Simanek, Tomas Vondra) [§](https://postgr.es/c/19d8e2308)

  * Improve the speed of updating the [process title](runtime-config-logging.html#GUC-UPDATE-PROCESS-TITLE) (David Rowley) [§](https://postgr.es/c/2cb82e2ac)

  * Allow `xid`/`subxid` searches and ASCII string detection to use vector operations (Nathan Bossart, John Naylor) [§](https://postgr.es/c/37a6e5df3) [§](https://postgr.es/c/121d2d3d7) [§](https://postgr.es/c/b6ef16756) [§](https://postgr.es/c/e813e0e16)

ASCII detection is particularly useful for [`COPY FROM`](sql-copy.html
"COPY"). Vector operations are also used for some C array searches.

  * Reduce overhead of memory allocations (Andres Freund, David Rowley) [§](https://postgr.es/c/c6e0fe1f2)

##### E.10.3.1.3. Monitoring #

  * Add system view [`pg_stat_io`](monitoring-stats.html#MONITORING-PG-STAT-IO-VIEW "28.2.13. pg_stat_io") view to track I/O statistics (Melanie Plageman) [§](https://postgr.es/c/a9c70b46d) [§](https://postgr.es/c/8aaa04b32) [§](https://postgr.es/c/ac8d53dae) [§](https://postgr.es/c/0ecb87e1f) [§](https://postgr.es/c/093e5c57d)

  * Record statistics on the last sequential and index scans on tables (Dave Page) [§](https://postgr.es/c/c03747183)

This information appears in [`pg_stat_*_tables`](monitoring-stats.html#PG-
STAT-ALL-TABLES-VIEW "Table 28.28. pg_stat_all_tables View") and
[`pg_stat_*_indexes`](monitoring-stats.html#MONITORING-PG-STAT-ALL-INDEXES-
VIEW "28.2.19. pg_stat_all_indexes").

  * Record statistics on the occurrence of updated rows moving to new pages (Corey Huinker) [§](https://postgr.es/c/ae4fdde13)

The `pg_stat_*_tables` column is [`n_tup_newpage_upd`](monitoring-
stats.html#MONITORING-PG-STAT-ALL-TABLES-VIEW "28.2.18. pg_stat_all_tables").

  * Add speculative lock information to the [`pg_locks`](view-pg-locks.html "54.12. pg_locks") system view (Masahiko Sawada, Noriyoshi Shinoda) [§](https://postgr.es/c/f74573969)

The transaction id is displayed in the `transactionid` column and the
speculative insertion token is displayed in the `objid` column.

  * Add the display of prepared statement result types to the [`pg_prepared_statements`](view-pg-prepared-statements.html "54.15. pg_prepared_statements") view (Dagfinn Ilmari Mannsåker) [§](https://postgr.es/c/84ad713cf) [§](https://postgr.es/c/6ffff0fd2)

  * Create subscription statistics entries at subscription creation time so [`stats_reset`](monitoring-stats.html#PG-STAT-DATABASE-VIEW "Table 28.26. pg_stat_database View") is accurate (Andres Freund) [§](https://postgr.es/c/e0b014295)

Previously entries were created only when the first statistics were reported.

  * Correct the I/O accounting for temp relation writes shown in [`pg_stat_database`](monitoring-stats.html#PG-STAT-DATABASE-VIEW "Table 28.26. pg_stat_database View") (Melanie Plageman) [§](https://postgr.es/c/704261ecc)

  * Add function [`pg_stat_get_backend_subxact()`](monitoring-stats.html#MONITORING-STATS-BACKEND-FUNCS-TABLE "Table 28.36. Per-Backend Statistics Functions") to report on a session's subtransaction cache (Dilip Kumar) [§](https://postgr.es/c/10ea0f924)

  * Have [`pg_stat_get_backend_idset()`](monitoring-stats.html#MONITORING-STATS-BACKEND-FUNCS-TABLE "Table 28.36. Per-Backend Statistics Functions"), `pg_stat_get_backend_activity()`, and related functions use the unchanging backend id (Nathan Bossart) [§](https://postgr.es/c/d7e39d72c)

Previously the index values might change during the lifetime of the session.

  * Report stand-alone backends with a special backend type (Melanie Plageman) [§](https://postgr.es/c/0c679464a)

  * Add wait event [`SpinDelay`](monitoring-stats.html#WAIT-EVENT-TIMEOUT-TABLE "Table 28.13. Wait Events of Type Timeout") to report spinlock sleep delays (Andres Freund) [§](https://postgr.es/c/92daeca45)

  * Create new wait event [`DSMAllocate`](monitoring-stats.html#WAIT-EVENT-IO-TABLE "Table 28.9. Wait Events of Type IO") to indicate waiting for dynamic shared memory allocation (Thomas Munro) [§](https://postgr.es/c/7bae3bbf6)

Previously this type of wait was reported as `DSMFillZeroWrite`, which was
also used by `mmap()` allocations.

  * Add the database name to the [process title](runtime-config-logging.html#GUC-UPDATE-PROCESS-TITLE) of logical WAL senders (Tatsuhiro Nakamori) [§](https://postgr.es/c/af205152e)

Physical WAL senders do not display a database name.

  * Add checkpoint and `REDO LSN` information to [`log_checkpoints`](runtime-config-logging.html#GUC-LOG-CHECKPOINTS) messages (Bharath Rupireddy, Kyotaro Horiguchi) [§](https://postgr.es/c/62c46eee2)

  * Provide additional details during client certificate failures (Jacob Champion) [§](https://postgr.es/c/3a0e38504)

##### E.10.3.1.4. Privileges #

  * Add predefined role [`pg_create_subscription`](predefined-roles.html "22.5. Predefined Roles") with permission to create subscriptions (Robert Haas) [§](https://postgr.es/c/c3afe8cf5)

  * Allow subscriptions to not require passwords (Robert Haas) [§](https://postgr.es/c/c3afe8cf5) [§](https://postgr.es/c/c1cc4e688) [§](https://postgr.es/c/19e65dff3)

This is accomplished with the option [`password_required=false`](sql-
createsubscription.html "CREATE SUBSCRIPTION").

  * Simplify permissions for [`LOCK TABLE`](sql-lock.html "LOCK") (Jeff Davis) [§](https://postgr.es/c/c44f6334c)

Previously a user's ability to perform `LOCK TABLE` at various lock levels was
limited to the lock levels required by the commands they had permission to
execute on the table. For example, someone with [`UPDATE`](sql-update.html
"UPDATE") permission could perform all lock levels except `ACCESS SHARE`, even
though it was a lesser lock level. Now users can issue lesser lock levels if
they already have permission for greater lock levels.

  * Allow [`ALTER GROUP group_name ADD USER user_name`](sql-altergroup.html "ALTER GROUP") to be performed with `ADMIN OPTION` (Robert Haas) [§](https://postgr.es/c/ce6b672e4)

Previously `CREATEROLE` permission was required.

  * Allow [`GRANT`](sql-grant.html "GRANT") to use `WITH ADMIN TRUE`/`FALSE` syntax (Robert Haas) [§](https://postgr.es/c/e3ce2de09)

Previously only the `WITH ADMIN OPTION` syntax was supported.

  * Allow roles that create other roles to automatically inherit the new role's rights or the ability to [`SET ROLE`](sql-set-role.html "SET ROLE") to the new role (Robert Haas, Shi Yu) [§](https://postgr.es/c/e5b8a4c09) [§](https://postgr.es/c/e00bc6c92)

This is controlled by server variable [`createrole_self_grant`](runtime-
config-client.html#GUC-CREATEROLE-SELF-GRANT).

  * Prevent users from changing the default privileges of non-inherited roles (Robert Haas) [§](https://postgr.es/c/48a257d44)

This is now only allowed for inherited roles.

  * When granting role membership, require the granted-by role to be a role that has appropriate permissions (Robert Haas) [§](https://postgr.es/c/ce6b672e4)

This is a requirement even when a non-bootstrap superuser is granting role
membership.

  * Allow non-superusers to grant permissions using a granted-by user that is not the current user (Robert Haas) [§](https://postgr.es/c/ce6b672e4)

The current user still must have sufficient permissions given by the specified
granted-by user.

  * Add [`GRANT`](sql-grant.html "GRANT") to control permission to use [`SET ROLE`](sql-set-role.html "SET ROLE") (Robert Haas) [§](https://postgr.es/c/3d14e171e)

This is controlled by a new `GRANT ... SET` option.

  * Add dependency tracking to roles which have granted privileges (Robert Haas) [§](https://postgr.es/c/ce6b672e4)

For example, removing `ADMIN OPTION` will fail if there are privileges using
that option; `CASCADE` must be used to revoke dependent permissions.

  * Add dependency tracking of grantors for [`GRANT`](sql-grant.html "GRANT") records (Robert Haas) [§](https://postgr.es/c/6566133c5)

This guarantees that [`pg_auth_members`](catalog-pg-auth-members.html
"53.9. pg_auth_members").`grantor` values are always valid.

  * Allow multiple role membership records (Robert Haas) [§](https://postgr.es/c/ce6b672e4) [§](https://postgr.es/c/0101f770a)

Previously a new membership grant would remove a previous matching membership
grant, even if other aspects of the grant did not match.

  * Prevent removal of superuser privileges for the bootstrap user (Robert Haas) [§](https://postgr.es/c/e530be2c5)

Restoring such users could lead to errors.

  * Allow [`makeaclitem()`](functions-info.html#FUNCTIONS-ACLITEM-FN-TABLE "Table 9.70. aclitem Functions") to accept multiple privilege names (Robins Tharakan) [§](https://postgr.es/c/b762bbde3)

Previously only a single privilege name, like [`SELECT`](sql-select.html
"SELECT"), was accepted.

##### E.10.3.1.5. Server Configuration #

  * Add support for Kerberos credential delegation (Stephen Frost) [§](https://postgr.es/c/6633cfb21) [§](https://postgr.es/c/9c0a0e2ed) [§](https://postgr.es/c/f4001a553) [§](https://postgr.es/c/a2eb99a01)

This is enabled with server variable [`gss_accept_delegation`](runtime-config-
connection.html#GUC-GSS-ACCEPT-DELEGATION) and libpq connection parameter
[`gssdelegation`](libpq-connect.html#LIBPQ-CONNECT-GSSDELEGATION).

  * Allow the SCRAM iteration count to be set with server variable [`scram_iterations`](runtime-config-connection.html#GUC-SCRAM-ITERATIONS) (Daniel Gustafsson) [§](https://postgr.es/c/b57774300)

  * Improve performance of server variable management (Tom Lane) [§](https://postgr.es/c/3057465ac) [§](https://postgr.es/c/f13b2088f)

  * Tighten restrictions on which server variables can be reset (Masahiko Sawada) [§](https://postgr.es/c/385366426)

Previously, while certain variables, like [`transaction_isolation`](runtime-
config-client.html#GUC-DEFAULT-TRANSACTION-ISOLATION), were not affected by
[`RESET ALL`](sql-reset.html "RESET"), they could be individually reset in
inappropriate situations.

  * Move various [`postgresql.conf`](config-setting.html#CONFIG-SETTING-CONFIGURATION-FILE "20.1.2. Parameter Interaction via the Configuration File") items into new categories (Shinya Kato) [§](https://postgr.es/c/0b039e3a8)

This also affects the categories displayed in the [`pg_settings`](view-pg-
settings.html "54.24. pg_settings") view.

  * Prevent configuration file recursion beyond 10 levels (Julien Rouhaud) [§](https://postgr.es/c/d13b68411)

  * Allow [autovacuum](routine-vacuuming.html#AUTOVACUUM "25.1.6. The Autovacuum Daemon") to more frequently honor changes to delay settings (Melanie Plageman) [§](https://postgr.es/c/7d71d3dd0) [§](https://postgr.es/c/a9781ae11)

Rather than honor changes only at the start of each relation, honor them at
the start of each block.

  * Remove restrictions that archive files be durably renamed (Nathan Bossart) [§](https://postgr.es/c/756e221db) [§](https://postgr.es/c/3cabe45a8)

The [`archive_command`](runtime-config-wal.html#GUC-ARCHIVE-COMMAND) command
is now more likely to be called with already-archived files after a crash.

  * Prevent [`archive_library`](runtime-config-wal.html#GUC-ARCHIVE-LIBRARY) and [`archive_command`](runtime-config-wal.html#GUC-ARCHIVE-COMMAND) from being set at the same time (Nathan Bossart) [§](https://postgr.es/c/d627ce3b7)

Previously `archive_library` would override `archive_command`.

  * Allow the postmaster to terminate children with an abort signal (Tom Lane) [§](https://postgr.es/c/51b5834cd)

This allows collection of a core dump for a stuck child process. This is
controlled by [`send_abort_for_crash`](runtime-config-developer.html#GUC-SEND-
ABORT-FOR-CRASH) and [`send_abort_for_kill`](runtime-config-
developer.html#GUC-SEND-ABORT-FOR-KILL). The postmaster's `-T` switch is now
the same as setting `send_abort_for_crash`.

  * Remove the non-functional postmaster `-n` option (Tom Lane) [§](https://postgr.es/c/51b5834cd)

  * Allow the server to reserve backend slots for roles with [`pg_use_reserved_connections`](predefined-roles.html "22.5. Predefined Roles") membership (Nathan Bossart) [§](https://postgr.es/c/6e2775e4d)

The number of reserved slots is set by server variable
[`reserved_connections`](runtime-config-connection.html#GUC-RESERVED-
CONNECTIONS).

  * Allow [huge pages](runtime-config-resource.html#GUC-HUGE-PAGES) to work on newer versions of Windows 10 (Thomas Munro) [§](https://postgr.es/c/fdd8937c0)

This adds the special handling required to enable huge pages on newer versions
of Windows 10.

  * Add [`debug_io_direct`](runtime-config-developer.html#GUC-DEBUG-IO-DIRECT) setting for developer usage (Thomas Munro, Andres Freund, Bharath Rupireddy) [§](https://postgr.es/c/d4e71df6d) [§](https://postgr.es/c/319bae9a8)

While primarily for developers, [`wal_sync_method=open_sync`](runtime-config-
wal.html#GUC-WAL-SYNC-METHOD)/`open_datasync` has been modified to not use
direct I/O with `wal_level=minimal`; this is now enabled with
`debug_io_direct=wal`.

  * Add function [`pg_split_walfile_name()`](functions-admin.html#FUNCTIONS-ADMIN-BACKUP-TABLE "Table 9.91. Backup Control Functions") to report the segment and timeline values of WAL file names (Bharath Rupireddy) [§](https://postgr.es/c/cca186348) [§](https://postgr.es/c/13e0d7a60)

##### E.10.3.1.6. [pg_hba.conf](auth-pg-hba-conf.html "21.1. The pg_hba.conf
File") #

  * Add support for regular expression matching on database and role entries in `pg_hba.conf` (Bertrand Drouvot) [§](https://postgr.es/c/8fea86830)

Regular expression patterns are prefixed with a slash. Database and role names
that begin with slashes need to be double-quoted if referenced in
`pg_hba.conf`.

  * Improve user-column handling of [`pg_ident.conf`](runtime-config-file-locations.html "20.2. File Locations") to match `pg_hba.conf` (Jelte Fennema) [§](https://postgr.es/c/efb6f4a4f)

Specifically, add support for `all`, role membership with `+`, and regular
expressions with a leading slash. Any user name that matches these patterns
must be double-quoted.

  * Allow include files in `pg_hba.conf` and `pg_ident.conf` (Julien Rouhaud) [§](https://postgr.es/c/a54b658ce)

These are controlled by `include`, `include_if_exists`, and `include_dir`.
System views [`pg_hba_file_rules`](view-pg-hba-file-rules.html
"54.9. pg_hba_file_rules") and [`pg_ident_file_mappings`](view-pg-ident-file-
mappings.html "54.10. pg_ident_file_mappings") now display the file name.

  * Allow `pg_hba.conf` tokens to be of unlimited length (Tom Lane) [§](https://postgr.es/c/de3f0e3fe)

  * Add rule and map numbers to the system view [`pg_hba_file_rules`](view-pg-hba-file-rules.html "54.9. pg_hba_file_rules") (Julien Rouhaud) [§](https://postgr.es/c/c591300a8)

##### E.10.3.1.7. [Localization](charset.html "Chapter 24. Localization") #

  * Determine the default encoding from the locale when using ICU (Jeff Davis) [§](https://postgr.es/c/c45dc7ffb)

Previously the default was always `UTF-8`.

  * Have [`CREATE DATABASE`](sql-createdatabase.html "CREATE DATABASE") and [`CREATE COLLATION`](sql-createcollation.html "CREATE COLLATION")'s `LOCALE` options, and [initdb](app-initdb.html "initdb") and [createdb](app-createdb.html "createdb") `--locale` options, control non-libc collation providers (Jeff Davis)

Previously they only controlled libc providers.

  * Add predefined collations `unicode` and `ucs_basic` (Peter Eisentraut) [§](https://postgr.es/c/0d21d4b9b)

This only works if ICU support is enabled.

  * Allow custom ICU collation rules to be created (Peter Eisentraut) [§](https://postgr.es/c/30a53b792)

This is done using [`CREATE COLLATION`](sql-createcollation.html "CREATE
COLLATION")'s new `RULES` clause, as well as new options for [`CREATE
DATABASE`](sql-createdatabase.html "CREATE DATABASE"), [createdb](app-
createdb.html "createdb"), and [initdb](app-initdb.html "initdb").

  * Allow Windows to import system locales automatically (Juan José Santamaría Flecha) [§](https://postgr.es/c/bf03cfd16)

Previously, only ICU locales could be imported on Windows.

#### E.10.3.2. [Logical Replication](logical-replication.html
"Chapter 31. Logical Replication") #

  * Allow [logical decoding](logicaldecoding.html "Chapter 49. Logical Decoding") on standbys (Bertrand Drouvot, Andres Freund, Amit Khandekar) [§](https://postgr.es/c/0fdab27ad) [§](https://postgr.es/c/be87200ef) [§](https://postgr.es/c/26669757b)

Snapshot WAL records are required for logical slot creation but cannot be
created on standbys. To avoid delays, the new function
[`pg_log_standby_snapshot()`](functions-admin.html#FUNCTIONS-SNAPSHOT-
SYNCHRONIZATION-TABLE "Table 9.94. Snapshot Synchronization Functions") allows
creation of such records.

  * Add server variable to control how logical decoding publishers transfer changes and how subscribers apply them (Shi Yu) [§](https://postgr.es/c/5de94a041) [§](https://postgr.es/c/1e8b61735) [§](https://postgr.es/c/9f2213a7c)

The variable is [`debug_logical_replication_streaming`](runtime-config-
developer.html#GUC-DEBUG-LOGICAL-REPLICATION-STREAMING).

  * Allow logical replication initial table synchronization to copy rows in binary format (Melih Mutlu) [§](https://postgr.es/c/ecb696527)

This is only possible for subscriptions marked as binary.

  * Allow parallel application of logical replication (Hou Zhijie, Wang Wei, Amit Kapila) [§](https://postgr.es/c/216a78482) [§](https://postgr.es/c/cd06ccd78) [§](https://postgr.es/c/fce003cfd)

The [`CREATE SUBSCRIPTION`](sql-createsubscription.html "CREATE SUBSCRIPTION")
`STREAMING` option now supports `parallel` to enable application of large
transactions by parallel workers. The number of parallel workers is controlled
by the new server variable
[`max_parallel_apply_workers_per_subscription`](runtime-config-
replication.html#GUC-MAX-PARALLEL-APPLY-WORKERS-PER-SUBSCRIPTION). Wait events
[`LogicalParallelApplyMain`](monitoring-stats.html#WAIT-EVENT-ACTIVITY-TABLE
"Table 28.5. Wait Events of Type Activity"),
`LogicalParallelApplyStateChange`, and `LogicalApplySendData` were also added.
Column `leader_pid` was added to system view
[`pg_stat_subscription`](monitoring-stats.html#MONITORING-PG-STAT-SUBSCRIPTION
"28.2.8. pg_stat_subscription") to track parallel activity.

  * Improve performance for [logical replication apply](logical-replication-architecture.html "31.7. Architecture") without a primary key (Onder Kalaci, Amit Kapila) [§](https://postgr.es/c/89e46da5e)

Specifically, `REPLICA IDENTITY FULL` can now use btree indexes rather than
sequentially scanning the table to find matches.

  * Allow logical replication subscribers to process only changes that have no origin (Vignesh C, Amit Kapila) [§](https://postgr.es/c/366283961) [§](https://postgr.es/c/875693019)

This can be used to avoid replication loops. This is controlled by the new
`CREATE SUBSCRIPTION ... ORIGIN` option.

  * Perform logical replication [`SELECT`](sql-select.html "SELECT") and DML actions as the table owner (Robert Haas) [§](https://postgr.es/c/1e10d49b6) [§](https://postgr.es/c/482675987)

This improves security and now requires subscription owners to be either
superusers or to have [`SET ROLE`](sql-set-role.html "SET ROLE") permission on
all roles owning tables in the replication set. The previous behavior of
performing all operations as the subscription owner can be enabled with the
subscription [`run_as_owner`](sql-createsubscription.html "CREATE
SUBSCRIPTION") option.

  * Have [`wal_retrieve_retry_interval`](runtime-config-replication.html#GUC-WAL-RETRIEVE-RETRY-INTERVAL) operate on a per-subscription basis (Nathan Bossart) [§](https://postgr.es/c/5a3a95385)

Previously the retry time was applied globally. This also adds wait events
[>`LogicalRepLauncherDSA`](monitoring-stats.html#WAIT-EVENT-LWLOCK-TABLE
"Table 28.12. Wait Events of Type LWLock") and `LogicalRepLauncherHash`.

#### E.10.3.3. Utility Commands #

  * Add [`EXPLAIN`](sql-explain.html "EXPLAIN") option `GENERIC_PLAN` to display the generic plan for a parameterized query (Laurenz Albe) [§](https://postgr.es/c/3c05284d8)

  * Allow a [`COPY FROM`](sql-copy.html "COPY") value to map to a column's `DEFAULT` (Israel Barth Rubio) [§](https://postgr.es/c/9f8377f7a)

  * Allow [`COPY`](sql-copy.html "COPY") into foreign tables to add rows in batches (Andrey Lepikhov, Etsuro Fujita) [§](https://postgr.es/c/97da48246)

This is controlled by the [postgres_fdw](postgres-fdw.html "F.38. postgres_fdw
— access data stored in external PostgreSQL servers") option
[`batch_size`](postgres-fdw.html#POSTGRES-FDW-OPTIONS-COST-ESTIMATION
"F.38.1.3. Cost Estimation Options").

  * Allow the `STORAGE` type to be specified by [`CREATE TABLE`](sql-createtable.html "CREATE TABLE") (Teodor Sigaev, Aleksander Alekseev) [§](https://postgr.es/c/784cedda0) [§](https://postgr.es/c/b9424d014)

Previously only [`ALTER TABLE`](sql-altertable.html "ALTER TABLE") could
control this.

  * Allow [truncate triggers](sql-createtrigger.html "CREATE TRIGGER") on foreign tables (Yugo Nagata) [§](https://postgr.es/c/3b00a944a)

  * Allow [`VACUUM`](sql-vacuum.html "VACUUM") and [vacuumdb](app-vacuumdb.html "vacuumdb") to only process [`TOAST`](storage-toast.html "73.2. TOAST") tables (Nathan Bossart) [§](https://postgr.es/c/4211fbd84)

This is accomplished by having [`VACUUM`](sql-vacuum.html "VACUUM") turn off
`PROCESS_MAIN` or by [vacuumdb](app-vacuumdb.html "vacuumdb") using the `--no-
process-main` option.

  * Add [`VACUUM`](sql-vacuum.html "VACUUM") options to skip or update all [frozen](routine-vacuuming.html#VACUUM-FOR-WRAPAROUND "25.1.5. Preventing Transaction ID Wraparound Failures") statistics (Tom Lane, Nathan Bossart) [§](https://postgr.es/c/a46a7011b)

The options are `SKIP_DATABASE_STATS` and `ONLY_DATABASE_STATS`.

  * Change [`REINDEX DATABASE`](sql-reindex.html "REINDEX") and [`REINDEX SYSTEM`](sql-reindex.html "REINDEX") to no longer require an argument (Simon Riggs) [§](https://postgr.es/c/2cbc3c17a) [§](https://postgr.es/c/0a5f06b84)

Previously the database name had to be specified.

  * Allow [`CREATE STATISTICS`](sql-createstatistics.html "CREATE STATISTICS") to generate a statistics name if none is specified (Simon Riggs) [§](https://postgr.es/c/624aa2a13)

#### E.10.3.4. Data Types #

  * Allow non-decimal [integer literals](sql-syntax-lexical.html#SQL-SYNTAX-BIT-STRINGS "4.1.2.5. Bit-String Constants") (Peter Eisentraut) [§](https://postgr.es/c/6fcda9aba)

For example, `0x42F`, `0o273`, and `0b100101`.

  * Allow [`NUMERIC`](datatype-numeric.html "8.1. Numeric Types") to process hexadecimal, octal, and binary integers of any size (Dean Rasheed) [§](https://postgr.es/c/6dfacbf72)

Previously only unquoted eight-byte integers were supported with these non-
decimal bases.

  * Allow underscores in integer and numeric [constants](sql-syntax-lexical.html#SQL-SYNTAX-BIT-STRINGS "4.1.2.5. Bit-String Constants") (Peter Eisentraut, Dean Rasheed) [§](https://postgr.es/c/faff8f8e4)

This can improve readability for long strings of digits.

  * Accept the spelling `+infinity` in datetime input (Vik Fearing) [§](https://postgr.es/c/2ceea5adb)

  * Prevent the specification of `epoch` and `infinity` together with other fields in datetime strings (Joseph Koshakow) [§](https://postgr.es/c/bcc704b52)

  * Remove undocumented support for date input in the form `Y _`year`_ M _`month`_ D _`day`_` (Joseph Koshakow) [§](https://postgr.es/c/5b3c59535)

  * Add functions [`pg_input_is_valid()`](functions-info.html#FUNCTIONS-INFO-VALIDITY-TABLE "Table 9.79. Data Validity Checking Functions") and `pg_input_error_info()` to check for type conversion errors (Tom Lane) [§](https://postgr.es/c/1939d2628) [§](https://postgr.es/c/b8da37b3a)

#### E.10.3.5. General Queries #

  * Allow subqueries in the `FROM` clause to omit aliases (Dean Rasheed) [§](https://postgr.es/c/bcedd8f5f)

  * Add support for enhanced numeric literals in SQL/JSON paths (Peter Eisentraut) [§](https://postgr.es/c/102a5c164)

For example, allow hexadecimal, octal, and binary integers and underscores
between digits.

#### E.10.3.6. Functions #

  * Add SQL/JSON constructors (Nikita Glukhov, Teodor Sigaev, Oleg Bartunov, Alexander Korotkov, Amit Langote) [§](https://postgr.es/c/7081ac46a)

The new functions [`JSON_ARRAY()`](functions-json.html#FUNCTIONS-JSON-
CREATION-TABLE "Table 9.47. JSON Creation Functions"),
[`JSON_ARRAYAGG()`](functions-aggregate.html#FUNCTIONS-AGGREGATE-TABLE
"Table 9.59. General-Purpose Aggregate Functions"), `JSON_OBJECT()`, and
`JSON_OBJECTAGG()` are part of the SQL standard.

  * Add SQL/JSON object checks (Nikita Glukhov, Teodor Sigaev, Oleg Bartunov, Alexander Korotkov, Amit Langote, Andrew Dunstan) [§](https://postgr.es/c/6ee30209a)

The [`IS JSON`](functions-json.html#FUNCTIONS-SQLJSON-MISC
"Table 9.48. SQL/JSON Testing Functions") checks include checks for values,
arrays, objects, scalars, and unique keys.

  * Allow JSON string parsing to use vector operations (John Naylor) [§](https://postgr.es/c/0a8de93a4)

  * Improve the handling of full text highlighting function [`ts_headline()`](functions-textsearch.html#TEXTSEARCH-FUNCTIONS-TABLE "Table 9.43. Text Search Functions") for `OR` and `NOT` expressions (Tom Lane) [§](https://postgr.es/c/5a617d75d)

  * Add functions to add, subtract, and generate `timestamptz` values in a specified time zone (Przemyslaw Sztoch, Gurjeet Singh) [§](https://postgr.es/c/75bd846b6)

The functions are [`date_add()`](functions-datetime.html#FUNCTIONS-DATETIME-
TABLE "Table 9.33. Date/Time Functions"), `date_subtract()`, and
[`generate_series()`](functions-srf.html#FUNCTIONS-SRF-SERIES
"Table 9.65. Series Generating Functions").

  * Change [`date_trunc(unit, timestamptz, time_zone)`](functions-datetime.html#FUNCTIONS-DATETIME-TABLE "Table 9.33. Date/Time Functions") to be an immutable function (Przemyslaw Sztoch) [§](https://postgr.es/c/533e02e92)

This allows the creation of expression indexes using this function.

  * Add server variable [`SYSTEM_USER`](functions-info.html#FUNCTIONS-INFO-SESSION-TABLE "Table 9.67. Session Information Functions") (Bertrand Drouvot) [§](https://postgr.es/c/0823d061b)

This reports the authentication method and its authenticated user.

  * Add functions [`array_sample()`](functions-array.html#ARRAY-FUNCTIONS-TABLE "Table 9.54. Array Functions") and `array_shuffle()` (Martin Kalcher) [§](https://postgr.es/c/888f2ea0a)

  * Add aggregate function [`ANY_VALUE()`](functions-aggregate.html#FUNCTIONS-AGGREGATE-TABLE "Table 9.59. General-Purpose Aggregate Functions") which returns any value from a set (Vik Fearing) [§](https://postgr.es/c/2ddab010c)

  * Add function [`random_normal()`](functions-math.html#FUNCTIONS-MATH-RANDOM-TABLE "Table 9.6. Random Functions") to supply normally-distributed random numbers (Paul Ramsey) [§](https://postgr.es/c/38d81760c)

  * Add error function [`erf()`](functions-math.html#FUNCTIONS-MATH-FUNC-TABLE "Table 9.5. Mathematical Functions") and its complement `erfc()` (Dean Rasheed) [§](https://postgr.es/c/d5d574146)

  * Improve the accuracy of numeric [`power()`](functions-math.html#FUNCTIONS-MATH-FUNC-TABLE "Table 9.5. Mathematical Functions") for integer exponents (Dean Rasheed) [§](https://postgr.es/c/40c7fcbbe)

  * Add [`XMLSERIALIZE()`](datatype-xml.html#DATATYPE-XML-CREATING "8.13.1. Creating XML Values") option `INDENT` to pretty-print its output (Jim Jones) [§](https://postgr.es/c/483bdb2af)

  * Change [`pg_collation_actual_version()`](functions-admin.html#FUNCTIONS-ADMIN-COLLATION "Table 9.98. Collation Management Functions") to return a reasonable value for the default collation (Jeff Davis) [§](https://postgr.es/c/10932ed5e)

Previously it returned `NULL`.

  * Allow [`pg_read_file()`](functions-admin.html#FUNCTIONS-ADMIN-GENFILE-TABLE "Table 9.101. Generic File Access Functions") and `pg_read_binary_file()` to ignore missing files (Kyotaro Horiguchi) [§](https://postgr.es/c/283129e32)

  * Add byte specification (`B`) to [`pg_size_bytes()`](functions-admin.html#FUNCTIONS-ADMIN-DBSIZE "Table 9.96. Database Object Size Functions") (Peter Eisentraut) [§](https://postgr.es/c/ce1215d9b)

  * Allow [`to_reg`](functions-info.html#FUNCTIONS-INFO-CATALOG-TABLE "Table 9.72. System Catalog Information Functions")* functions to accept numeric OIDs as input (Tom Lane) [§](https://postgr.es/c/3ea7329c9)

#### E.10.3.7. [PL/pgSQL](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural
Language") #

  * Add the ability to get the current function's OID in PL/pgSQL (Pavel Stehule) [§](https://postgr.es/c/d3d53f955)

This is accomplished with [`GET DIAGNOSTICS variable =
PG_ROUTINE_OID`](plpgsql-statements.html#PLPGSQL-STATEMENTS-DIAGNOSTICS
"43.5.5. Obtaining the Result Status").

#### E.10.3.8. [libpq](libpq.html "Chapter 34. libpq — C Library") #

  * Add libpq connection option [`require_auth`](libpq-connect.html#LIBPQ-CONNECT-REQUIRE-AUTH) to specify a list of acceptable authentication methods (Jacob Champion) [§](https://postgr.es/c/3a465cc67)

This can also be used to disallow certain authentication methods.

  * Allow multiple libpq-specified hosts to be randomly selected (Jelte Fennema) [§](https://postgr.es/c/7f5b19817) [§](https://postgr.es/c/0a16512d4)

This is enabled with [`load_balance_hosts=random`](libpq-connect.html#LIBPQ-
CONNECT-LOAD-BALANCE-HOSTS) and can be used for load balancing.

  * Add libpq option [`sslcertmode`](libpq-connect.html#LIBPQ-CONNECT-SSLCERTMODE) to control transmission of the client certificate (Jacob Champion) [§](https://postgr.es/c/36f40ce2d)

The option values are `disable`, `allow`, and `require`.

  * Allow libpq to use the system certificate pool for certificate verification (Jacob Champion, Thomas Habets) [§](https://postgr.es/c/8eda73146)

This is enabled with [`sslrootcert=system`](libpq-connect.html#LIBPQ-CONNECT-
SSLROOTCERT), which also enables [`sslmode=verify-full`](libpq-
connect.html#LIBPQ-CONNECT-SSLMODE).

#### E.10.3.9. Client Applications #

  * Allow [`ECPG`](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") variable declarations to use typedef names that match unreserved SQL keywords (Tom Lane) [§](https://postgr.es/c/83f1c7b74)

This change does prevent keywords which match C typedef names from being
processed as keywords in later `EXEC SQL` blocks.

##### E.10.3.9.1. [psql](app-psql.html "psql") #

  * Allow psql to control the maximum width of header lines in expanded format (Platon Pronko) [§](https://postgr.es/c/a45388d6e)

This is controlled by [`xheader_width`](app-psql.html#APP-PSQL-META-COMMAND-
PSET-XHEADER-WIDTH).

  * Add psql command [`\drg`](app-psql.html#APP-PSQL-META-COMMAND-DRG) to show role membership details (Pavel Luzanov) [§](https://postgr.es/c/d913928c9) [§](https://postgr.es/c/d65ddaca9)

The `Member of` output column has been removed from `\du` and `\dg` because
this new command displays this information in more detail.

  * Allow psql's access privilege commands to show system objects (Nathan Bossart) [§](https://postgr.es/c/d913928c9) [§](https://postgr.es/c/d65ddaca9)

The options are [`\dpS`](app-psql.html#APP-PSQL-META-COMMAND-DP-LC) and
[`\zS`](app-psql.html#APP-PSQL-META-COMMAND-Z).

  * Add `FOREIGN` designation to psql [`\d+`](app-psql.html#APP-PSQL-META-COMMAND-D) for foreign table children and partitions (Ian Lawrence Barwick) [§](https://postgr.es/c/bd95816f7)

  * Prevent [`\df+`](app-psql.html#APP-PSQL-META-COMMAND-DF-UC) from showing function source code (Isaac Morland) [§](https://postgr.es/c/3dfae91f7)

Function bodies are more easily viewed with [`\sf`](app-psql.html#APP-PSQL-
META-COMMAND-SF).

  * Allow psql to submit queries using the extended query protocol (Peter Eisentraut) [§](https://postgr.es/c/5b66de343)

Passing arguments to such queries is done using the new psql [`\bind`](app-
psql.html#APP-PSQL-META-COMMAND-BIND) command.

  * Allow psql [`\watch`](app-psql.html#APP-PSQL-META-COMMAND-WATCH) to limit the number of executions (Andrey Borodin) [§](https://postgr.es/c/00beecfe8)

The `\watch` options can now be named when specified.

  * Detect invalid values for psql [`\watch`](app-psql.html#APP-PSQL-META-COMMAND-WATCH), and allow zero to specify no delay (Andrey Borodin) [§](https://postgr.es/c/6f9ee74d4)

  * Allow psql scripts to obtain the exit status of shell commands and queries (Corey Huinker, Tom Lane) [§](https://postgr.es/c/b0d8f2d98) [§](https://postgr.es/c/31ae2aa9d)

The new psql control variables are [`SHELL_ERROR`](app-psql.html#APP-PSQL-
VARIABLES-SHELL-ERROR) and [`SHELL_EXIT_CODE`](app-psql.html#APP-PSQL-
VARIABLES-SHELL-EXIT-CODE).

  * Various psql tab completion improvements (Vignesh C, Aleksander Alekseev, Dagfinn Ilmari Mannsåker, Shi Yu, Michael Paquier, Ken Kato, Peter Smith) [§](https://postgr.es/c/f6c750d31) [§](https://postgr.es/c/4cbe57974) [§](https://postgr.es/c/6afcab6ac) [§](https://postgr.es/c/9aa58d48f) [§](https://postgr.es/c/3cf2f7af7) [§](https://postgr.es/c/2ea5de296) [§](https://postgr.es/c/07f7237c2) [§](https://postgr.es/c/9d0cf5749) [§](https://postgr.es/c/a3bc631ea) [§](https://postgr.es/c/2ff5ca86e) [§](https://postgr.es/c/9e1e9d656) [§](https://postgr.es/c/96c498d2f)

##### E.10.3.9.2. [pg_dump](app-pgdump.html "pg_dump") #

  * Add pg_dump control of dumping child tables and partitions (Gilles Darold) [§](https://postgr.es/c/a563c24c9)

The new options are `--table-and-children`, `--exclude-table-and-children`,
and `--exclude-table-data-and-children`.

  * Add LZ4 and Zstandard compression to pg_dump (Georgios Kokolatos, Justin Pryzby)

  * Allow pg_dump and [pg_basebackup](app-pgbasebackup.html "pg_basebackup") to use `long` mode for compression (Justin Pryzby) [§](https://postgr.es/c/0da243fed) [§](https://postgr.es/c/0070b66fe) [§](https://postgr.es/c/84adc8e20) [§](https://postgr.es/c/2820adf77)

  * Improve pg_dump to accept a more consistent compression syntax (Georgios Kokolatos) [§](https://postgr.es/c/5e73a6048)

Options like `--compress=gzip:5`.

#### E.10.3.10. Server Applications #

  * Add [initdb](app-initdb.html "initdb") option to set server variables for the duration of initdb and all future server starts (Tom Lane) [§](https://postgr.es/c/3e51b278d)

The option is `-c name=value`.

  * Add options to [createuser](app-createuser.html "createuser") to control more user options (Shinya Kato) [§](https://postgr.es/c/08951a7c9) [§](https://postgr.es/c/2dcd1578c)

Specifically, the new options control the valid-until date, bypassing of row-
level security, and role membership.

  * Deprecate [createuser](app-createuser.html "createuser") option `--role` (Nathan Bossart) [§](https://postgr.es/c/2dcd1578c) [§](https://postgr.es/c/381d19b3e)

This option could be easily confused with new createuser role membership
options, so option `--member-of` has been added with the same functionality.
The `--role` option can still be used.

  * Allow control of [vacuumdb](app-vacuumdb.html "vacuumdb") schema processing (Gilles Darold) [§](https://postgr.es/c/7781f4e3e)

These are controlled by options `--schema` and `--exclude-schema`.

  * Use new [`VACUUM`](sql-vacuum.html "VACUUM") options to improve the performance of [vacuumdb](app-vacuumdb.html "vacuumdb") (Tom Lane, Nathan Bossart) [§](https://postgr.es/c/a46a7011b)

  * Have [pg_upgrade](pgupgrade.html "pg_upgrade") set the new cluster's locale and encoding (Jeff Davis) [§](https://postgr.es/c/9637badd9)

This removes the requirement that the new cluster be created with the same
locale and encoding settings.

  * Add [pg_upgrade](pgupgrade.html "pg_upgrade") option to specify the default transfer mode (Peter Eisentraut) [§](https://postgr.es/c/746915c68)

The option is `--copy`.

  * Improve [pg_basebackup](app-pgbasebackup.html "pg_basebackup") to accept numeric compression options (Georgios Kokolatos, Michael Paquier) [§](https://postgr.es/c/d18655cc0)

Options like `--compress=server-5` are now supported.

  * Fix [pg_basebackup](app-pgbasebackup.html "pg_basebackup") to handle tablespaces stored in the `PGDATA` directory (Robert Haas) [§](https://postgr.es/c/363e8f911)

  * Add [pg_waldump](pgwaldump.html "pg_waldump") option `--save-fullpage` to dump full page images (David Christensen) [§](https://postgr.es/c/d497093cb)

  * Allow [pg_waldump](pgwaldump.html "pg_waldump") options `-t`/`--timeline` to accept hexadecimal values (Peter Eisentraut) [§](https://postgr.es/c/4c8044c04)

  * Add support for progress reporting to [pg_verifybackup](app-pgverifybackup.html "pg_verifybackup") (Masahiko Sawada) [§](https://postgr.es/c/d07c2948b)

  * Allow [pg_rewind](app-pgrewind.html "pg_rewind") to properly track timeline changes (Heikki Linnakangas) [§](https://postgr.es/c/009eeee74) [§](https://postgr.es/c/0a0500207)

Previously if pg_rewind was run after a timeline switch but before a
checkpoint was issued, it might incorrectly determine that a rewind was
unnecessary.

  * Have [pg_receivewal](app-pgreceivewal.html "pg_receivewal") and [pg_recvlogical](app-pgrecvlogical.html "pg_recvlogical") cleanly exit on `SIGTERM` (Christoph Berg) [§](https://postgr.es/c/8b60db774)

This signal is often used by systemd.

#### E.10.3.11. Source Code #

  * Build ICU support by default (Jeff Davis) [§](https://postgr.es/c/fcb21b3ac)

This removes [build flag](installation.html "Chapter 17. Installation from
Source Code") `--with-icu` and adds flag `--without-icu`.

  * Add support for SSE2 (Streaming SIMD Extensions 2) vector operations on x86-64 architectures (John Naylor) [§](https://postgr.es/c/56f2c7b58)

  * Add support for Advanced SIMD (Single Instruction Multiple Data) (NEON) instructions on ARM architectures (Nathan Bossart) [§](https://postgr.es/c/82739d4a8)

  * Have Windows binaries built with MSVC use `RandomizedBaseAddress` (ASLR) (Michael Paquier) [§](https://postgr.es/c/36389a060)

This was already enabled on MinGW builds.

  * Prevent extension libraries from exporting their symbols by default (Andres Freund, Tom Lane) [§](https://postgr.es/c/089480c07) [§](https://postgr.es/c/8cf64d35e)

Functions that need to be called from the core backend or other extensions
must now be explicitly marked `PGDLLEXPORT`.

  * Require Windows 10 or newer versions (Michael Paquier, Juan José Santamaría Flecha) [§](https://postgr.es/c/495ed0ef2)

Previously Windows Vista and Windows XP were supported.

  * Require Perl version 5.14 or later (John Naylor) [§](https://postgr.es/c/4c1532763)

  * Require Bison version 2.3 or later (John Naylor) [§](https://postgr.es/c/b086a47a2)

  * Require Flex version 2.5.35 or later (John Naylor) [§](https://postgr.es/c/8b878bffa)

  * Require MIT Kerberos for GSSAPI support (Stephen Frost) [§](https://postgr.es/c/f7431bca8)

  * Remove support for Visual Studio 2013 (Michael Paquier) [§](https://postgr.es/c/6203583b7)

  * Remove support for HP-UX (Thomas Munro) [§](https://postgr.es/c/9db300ce6)

  * Remove support for HP/Intel Itanium (Thomas Munro) [§](https://postgr.es/c/0ad5b48e5)

  * Remove support for M68K, M88K, M32R, and SuperH CPU architectures (Thomas Munro) [§](https://postgr.es/c/718aa43a4) [§](https://postgr.es/c/14168d3c6)

  * Remove [libpq](libpq.html "Chapter 34. libpq — C Library") support for SCM credential authentication (Michael Paquier) [§](https://postgr.es/c/98ae2c84a)

Backend support for this authentication method was removed in PostgresSQL 9.1.

  * Add [meson](install-meson.html "17.4. Building and Installation with Meson") build system (Andres Freund, Nazir Bilal Yavuz, Peter Eisentraut) [§](https://postgr.es/c/e6927270c)

This eventually will replace the Autoconf and Windows-based MSVC build
systems.

  * Allow control of the location of the openssl binary used by the build system (Peter Eisentraut) [§](https://postgr.es/c/c8e4030d1)

Make finding openssl program a configure or meson option

  * Add build option to allow testing of small table segment sizes (Andres Freund) [§](https://postgr.es/c/d3b111e32)

The build options are [`--with-segsize-blocks`](install-make.html#CONFIGURE-
OPTION-WITH-SEGSIZE) and `-Dsegsize_blocks`.

  * Add [pgindent](source.html "Chapter 56. PostgreSQL Coding Conventions") options (Andrew Dunstan) [§](https://postgr.es/c/b90f0b574) [§](https://postgr.es/c/62e1e28bf) [§](https://postgr.es/c/124937163) [§](https://postgr.es/c/a1c4cd6f2) [§](https://postgr.es/c/068a243b7) [§](https://postgr.es/c/dab07e8c6) [§](https://postgr.es/c/b16259b3c)

The new options are `--show-diff`, `--silent-diff`, `--commit`, and `--help`,
and allow multiple `--exclude` options. Also require the typedef file to be
explicitly specified. Options `--code-base` and `--build` were also removed.

  * Add [pg_bsd_indent](source.html "Chapter 56. PostgreSQL Coding Conventions") source code to the main tree (Tom Lane) [§](https://postgr.es/c/4e831f4ce)

  * Improve make_ctags and make_etags (Yugo Nagata) [§](https://postgr.es/c/d1e2a380c)

  * Adjust [`pg_attribute`](catalog-pg-attribute.html "53.7. pg_attribute") columns for efficiency (Peter Eisentraut) [§](https://postgr.es/c/90189eefc)

#### E.10.3.12. Additional Modules #

  * Improve use of extension-based indexes on boolean columns (Zongliang Quan, Tom Lane) [§](https://postgr.es/c/ff720a597)

  * Add support for Daitch-Mokotoff Soundex to [fuzzystrmatch](fuzzystrmatch.html "F.17. fuzzystrmatch — determine string similarities and distance") (Dag Lem) [§](https://postgr.es/c/a290378a3)

  * Allow [auto_explain](auto-explain.html "F.4. auto_explain — log execution plans of slow queries") to log values passed to parameterized statements (Dagfinn Ilmari Mannsåker) [§](https://postgr.es/c/d4bfe4128)

This affects queries using server-side [`PREPARE`](sql-prepare.html
"PREPARE")/[`EXECUTE`](sql-execute.html "EXECUTE") and client-side parse/bind.
Logging is controlled by [`auto_explain.log_parameter_max_length`](auto-
explain.html#AUTO-EXPLAIN-CONFIGURATION-PARAMETERS-LOG-PARAMETER-MAX-LENGTH);
by default query parameters will be logged with no length restriction.

  * Have [auto_explain](auto-explain.html "F.4. auto_explain — log execution plans of slow queries")'s `log_verbose` mode honor the value of [`compute_query_id`](runtime-config-statistics.html#GUC-COMPUTE-QUERY-ID) (Atsushi Torikoshi) [§](https://postgr.es/c/9d2d9728b)

Previously even if `compute_query_id` was enabled, [`log_verbose`](auto-
explain.html#AUTO-EXPLAIN-CONFIGURATION-PARAMETERS-LOG-VERBOSE) was not
showing the query identifier.

  * Change the maximum length of [ltree](ltree.html "F.23. ltree — hierarchical tree-like data type") labels from 256 to 1000 and allow hyphens (Garen Torikian) [§](https://postgr.es/c/b1665bf01)

  * Have [`pg_stat_statements`](pgstatstatements.html "F.32. pg_stat_statements — track statistics of SQL planning and execution") normalize constants used in utility commands (Michael Paquier) [§](https://postgr.es/c/daa8365a9)

Previously constants appeared instead of placeholders, e.g., `$1`.

  * Add [pg_walinspect](pgwalinspect.html "F.37. pg_walinspect — low-level WAL inspection") function [`pg_get_wal_block_info()`](pgwalinspect.html#PGWALINSPECT-FUNCS-PG-GET-WAL-BLOCK-INFO) to report WAL block information (Michael Paquier, Melanie Plageman, Bharath Rupireddy) [§](https://postgr.es/c/c31cf1c03) [§](https://postgr.es/c/9ecb134a9) [§](https://postgr.es/c/122376f02) [§](https://postgr.es/c/df4f3ab51)

  * Change how [pg_walinspect](pgwalinspect.html "F.37. pg_walinspect — low-level WAL inspection") functions [`pg_get_wal_records_info()`](pgwalinspect.html#PGWALINSPECT-FUNCS-PG-GET-WAL-RECORDS-INFO) and [`pg_get_wal_stats()`](pgwalinspect.html#PGWALINSPECT-FUNCS-PG-GET-WAL-STATS) interpret ending LSNs (Bharath Rupireddy) [§](https://postgr.es/c/5c1b66280)

Previously ending LSNs which represent nonexistent WAL locations would
generate an error, while they will now be interpreted as the end of the WAL.

  * Add detailed descriptions of WAL records in [pg_walinspect](pgwalinspect.html "F.37. pg_walinspect — low-level WAL inspection") and [pg_waldump](pgwaldump.html "pg_waldump") (Melanie Plageman, Peter Geoghegan) [§](https://postgr.es/c/7d8219a44) [§](https://postgr.es/c/1c453cfd8) [§](https://postgr.es/c/96149a180) [§](https://postgr.es/c/50547a3fa)

  * Add [pageinspect](pageinspect.html "F.25. pageinspect — low-level inspection of database pages") function [`bt_multi_page_stats()`](pageinspect.html#PAGEINSPECT-B-TREE-FUNCS "F.25.3. B-Tree Functions") to report statistics on multiple pages (Hamid Akhtar) [§](https://postgr.es/c/1fd3dd204)

This is similar to `bt_page_stats()` except it can report on a range of pages.

  * Add empty range output column to [pageinspect](pageinspect.html "F.25. pageinspect — low-level inspection of database pages") function [`brin_page_items()`](pageinspect.html#PAGEINSPECT-BRIN-FUNCS "F.25.4. BRIN Functions") (Tomas Vondra) [§](https://postgr.es/c/1fd3dd204)

  * Redesign archive modules to be more flexible (Nathan Bossart) [§](https://postgr.es/c/35739b87d)

Initialization changes will require modules written for older versions of
Postgres to be updated.

  * Correct inaccurate [pg_stat_statements](pgstatstatements.html "F.32. pg_stat_statements — track statistics of SQL planning and execution") row tracking extended query protocol statements (Sami Imseih) [§](https://postgr.es/c/1d477a907)

  * Add [pg_buffercache](pgbuffercache.html "F.27. pg_buffercache — inspect PostgreSQL buffer cache state") function `pg_buffercache_usage_counts()` to report usage totals (Nathan Bossart) [§](https://postgr.es/c/f3fa31327)

  * Add [pg_buffercache](pgbuffercache.html "F.27. pg_buffercache — inspect PostgreSQL buffer cache state") function `pg_buffercache_summary()` to report summarized buffer statistics (Melih Mutlu) [§](https://postgr.es/c/2589434ae)

  * Allow the schemas of required extensions to be referenced in extension scripts using the new syntax `@extschema:referenced_extension_name@` (Regina Obe) [§](https://postgr.es/c/72a5b1fc8)

  * Allow required extensions to be marked as non-relocatable using [`no_relocate`](extend-extensions.html#EXTEND-EXTENSIONS-FILES-NO-RELOCATE) (Regina Obe) [§](https://postgr.es/c/72a5b1fc8)

This allows `@extschema:referenced_extension_name@` to be treated as a
constant for the lifetime of the extension.

##### E.10.3.12.1. [postgres_fdw](postgres-fdw.html "F.38. postgres_fdw —
access data stored in external PostgreSQL servers") #

  * Allow postgres_fdw to do aborts in parallel (Etsuro Fujita) [§](https://postgr.es/c/983ec2300)

This is enabled with postgres_fdw option [`parallel_abort`](postgres-
fdw.html#POSTGRES-FDW-OPTIONS-TRANSACTION-MANAGEMENT "F.38.1.6. Transaction
Management Options").

  * Make [`ANALYZE`](sql-analyze.html "ANALYZE") on foreign postgres_fdw tables more efficient (Tomas Vondra) [§](https://postgr.es/c/8ad51b5f4)

The postgres_fdw option [`analyze_sampling`](postgres-fdw.html#POSTGRES-FDW-
OPTIONS-COST-ESTIMATION "F.38.1.3. Cost Estimation Options") controls the
sampling method.

  * Restrict shipment of [`reg`](datatype-oid.html "8.19. Object Identifier Types")* type constants in postgres_fdw to those referencing built-in objects or extensions marked as shippable (Tom Lane) [§](https://postgr.es/c/31e5b5029)

  * Have postgres_fdw and [dblink](dblink.html "F.12. dblink — connect to other PostgreSQL databases") handle interrupts during connection establishment (Andres Freund) [§](https://postgr.es/c/e4602483e)

### E.10.4. Acknowledgments #

The following individuals (in alphabetical order) have contributed to this
release as patch authors, committers, reviewers, testers, or reporters of
issues.

Abhijit Menon-Sen  
---  
Adam Mackler  
Adrian Klaver  
Ahsan Hadi  
Ajin Cherian  
Ajit Awekar  
Alan Hodgson  
Aleksander Alekseev  
Alex Denman  
Alex Kozhemyakin  
Alexander Korolev  
Alexander Korotkov  
Alexander Lakhin  
Alexander Pyhalov  
Alexey Borzov  
Alexey Ermakov  
Alexey Makhmutov  
Álvaro Herrera  
Amit Kapila  
Amit Khandekar  
Amit Langote  
Amul Sul  
Anastasia Lubennikova  
Anban Company  
Andreas Dijkman  
Andreas Karlsson  
Andreas Scherbaum  
Andrei Zubkov  
Andres Freund  
Andrew Alsup  
Andrew Bille  
Andrew Dunstan  
Andrew Gierth  
Andrew Kesper  
Andrey Borodin  
Andrey Lepikhov  
Andrey Sokolov  
Ankit Kumar Pandey  
Ante Kresic  
Anton Melnikov  
Anton Sidyakin  
Anton Voloshin  
Antonin Houska  
Arne Roland  
Artem Anisimov  
Arthur Zakirov  
Ashutosh Bapat  
Ashutosh Sharma  
Asim Praveen  
Atsushi Torikoshi  
Ayaki Tachikake  
Balazs Szilfai  
Benoit Lobréau  
Bernd Helmle  
Bertrand Drouvot  
Bharath Rupireddy  
Bilva Sanaba  
Bob Krier  
Boris Zentner  
Brad Nicholson  
Brar Piening  
Bruce Momjian  
Bruno da Silva  
Carl Sopchak  
Cary Huang  
Changhong Fei  
Chris Travers  
Christoph Berg  
Christophe Pettus  
Corey Huinker  
Craig Ringer  
Curt Kolovson  
Dag Lem  
Dagfinn Ilmari Mannsåker  
Daniel Gustafsson  
Daniel Vérité  
Daniel Watzinger  
Daniel Westermann  
Daniele Varrazzo  
Daniil Anisimov  
Danny Shemesh  
Dave Page  
David Christensen  
David G. Johnston  
David Geier  
David Gilman  
David Kimura  
David Rowley  
David Steele  
David Turon  
David Zhang  
Davinder Singh  
Dean Rasheed  
Denis Laxalde  
Dilip Kumar  
Dimos Stamatakis  
Dmitriy Kuzmin  
Dmitry Astapov  
Dmitry Dolgov  
Dmitry Koval  
Dong Wook Lee  
Dongming Liu  
Drew DeVault  
Duncan Sands  
Ed Maste  
Egor Chindyaskin  
Ekaterina Kiryanova  
Elena Indrupskaya  
Emmanuel Quincerot  
Eric Mutta  
Erik Rijkers  
Erki Eessaar  
Erwin Brandstetter  
Etsuro Fujita  
Eugeny Zhuzhnev  
Euler Taveira  
Evan Jones  
Evgeny Morozov  
Fabrízio de Royes Mello  
Farias de Oliveira  
Florin Irion  
Franz-Josef Färber  
Garen Torikian  
Georgios Kokolatos  
Gilles Darold  
Greg Stark  
Guillaume Lelarge  
Gunnar Bluth  
Gunnar Morling  
Gurjeet Singh  
Haiyang Wang  
Haiying Tang  
Hamid Akhtar  
Hans Buschmann  
Hao Wu  
Hayato Kuroda  
Heath Lord  
Heikki Linnakangas  
Himanshu Upadhyaya  
Hisahiro Kauchi  
Hongyu Song  
Hubert Lubaczewski  
Hung Nguyen  
Ian Barwick  
Ibrar Ahmed  
Ilya Gladyshev  
Ilya Nenashev  
Isaac Morland  
Israel Barth Rubio  
Jacob Champion  
Jacob Speidel  
Jaime Casanova  
Jakub Wartak  
James Coleman  
James Inform  
James Vanns  
Jan Wieck  
Japin Li  
Jeevan Ladhe  
Jeff Davis  
Jeff Janes  
Jehan-Guillaume de Rorthais  
Jelte Fennema  
Jian He  
Jim Jones  
Jinbao Chen  
Joe Conway  
Joel Jacobson  
John Naylor  
Jonathan Katz  
Josef Simanek  
Joseph Koshakow  
Juan José Santamaría Flecha  
Julien Rouhaud  
Julien Roze  
Junwang Zhao  
Justin Pryzby  
Justin Zhang  
Karina Litskevich  
Karl O. Pinc  
Keisuke Kuroda  
Ken Kato  
Kevin McKibbin  
Kieran McCusker  
Kirk Wolak  
Konstantin Knizhnik  
Koshi Shibagaki  
Kotaro Kawamoto  
Kui Liu  
Kyotaro Horiguchi  
Lakshmi Narayanan Sreethar  
Laurence Parry  
Laurenz Albe  
Luca Ferrari  
Lukas Fittl  
Maciek Sakrejda  
Magnus Hagander  
Maja Zaloznik  
Marcel Hofstetter  
Marina Polyakova  
Mark Dilger  
Marko Tiikkaja  
Markus Winand  
Martijn van Oosterhout  
Martin Jurca  
Martin Kalcher  
Mary Xu  
Masahiko Sawada  
Masahiro Ikeda  
Masao Fujii  
Mason Sharp  
Matheus Alcantara  
Mats Kindahl  
Matthias van de Meent  
Matthijs van der Vleuten  
Maxim Orlov  
Maxim Yablokov  
Mehmet Emin Karakas  
Melanie Plageman  
Melih Mutlu  
Micah Gates  
Michael Banck  
Michael Paquier  
Michail Nikolaev  
Michel Pelletier  
Mike Oh  
Mikhail Gribkov  
Mingli Zhang  
Miroslav Bendik  
Mitsuru Hinata  
Myo Wai Thant  
Naeem Akhter  
Naoki Okano  
Nathan Bossart  
Nazir Bilal Yavuz  
Neha Sharma  
Nick Babadzhanian  
Nicola Contu  
Nikhil Shetty  
Nikita Glukhov  
Nikolay Samokhvalov  
Nikolay Shaplov  
Nishant Sharma  
Nitin Jadhav  
Noah Misch  
Noboru Saito  
Noriyoshi Shinoda  
Nuko Yokohama  
Oleg Bartunov  
Oleg Tselebrovskiy  
Olly Betts  
Onder Kalaci  
Onur Tirtir  
Pablo Federico  
Palle Girgensohn  
Paul Guo  
Paul Jungwirth  
Paul Ramsey  
Pavel Borisov  
Pavel Kulakov  
Pavel Luzanov  
Pavel Stehule  
Peifeng Qiu  
Peter Eisentraut  
Peter Geoghegan  
Peter Smith  
Phil Florent  
Philippe Godfrin  
Platon Pronko  
Przemyslaw Sztoch  
Rachel Heaton  
Ranier Vilela  
Regina Obe  
Reid Thompson  
Reiner Peterke  
Richard Guo  
Riivo Kolka  
Rishu Bagga  
Robert Haas  
Robert Sjöblom  
Robert Treat  
Roberto Mello  
Robins Tharakan  
Roman Zharkov  
Ronan Dunklau  
Rushabh Lathia  
Ryo Matsumura  
Samay Sharma  
Sami Imseih  
Sandeep Thakkar  
Sandro Santilli  
Sebastien Flaesch  
Sébastien Lardière  
Sehrope Sarkuni  
Sergey Belyashov  
Sergey Pankov  
Sergey Shinderuk  
Shi Yu  
Shinya Kato  
Sho Kato  
Shruthi Gowda  
Shveta Mallik  
Simon Riggs  
Sindy Senorita  
Sirisha Chamarthi  
Sravan Kumar  
Stéphane Tachoires  
Stephen Frost  
Steve Chavez  
Stone Tickle  
Sven Klemm  
Takamichi Osumi  
Takeshi Ideriha  
Tatsuhiro Nakamori  
Tatsuo Ishii  
Teja Mupparti  
Tender Wang  
Teodor Sigaev  
Thiago Nunes  
Thom Brown  
Thomas Habets  
Thomas Mc Kay  
Thomas Munro  
Tim Carey-Smith  
Tim Field  
Timo Stolz  
Tom Lane  
Tomas Vondra  
Tor Erik Linnerud  
Torsten Förtsch  
Tristan Partin  
Troy Frericks  
Tushar Ahuja  
Valerie Woolard  
Vibhor Kumar  
Victor Spirin  
Victoria Shepard  
Vignesh C  
Vik Fearing  
Vitaly Burovoy  
Vitaly Davydov  
Wang Wei  
Wenjing Zeng  
Whale Song  
Will Mortensen  
Wolfgang Walther  
Xin Wen  
Xing Guo  
Xingwang Xu  
XueJing Zhao  
Yanliang Lei  
Youmiu Mo  
Yugo Nagata  
Yura Sokolov  
Yuta Katsuragi  
Zhen Mingyang  
Zheng Li  
Zhihong Yu  
Zhijie Hou  
Zongliang Quan  
Zuming Jiang  
  
* * *

[Prev](release-16-1.html "E.9. Release 16.1")  | [Up](release.html "Appendix E. Release Notes") |  [Next](release-prior.html "E.11. Prior Releases")  
---|---|---  
E.9. Release 16.1  | [Home](index.html "PostgreSQL 16.9 Documentation") |  E.11. Prior Releases  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/release-16.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

