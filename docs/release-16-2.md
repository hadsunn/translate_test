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

Supported Versions: [16](/docs/16/release-16-2.html "PostgreSQL 16 -
E.8. Release 16.2")

__

E.8. Release 16.2  
---  
[Prev](release-16-3.html "E.7. Release 16.3")  | [Up](release.html "Appendix E. Release Notes") | Appendix E. Release Notes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](release-16-1.html "E.9. Release 16.1")  
  
* * *

## E.8. Release 16.2 #

[E.8.1. Migration to Version 16.2](release-16-2.html#RELEASE-16-2-MIGRATION)

[E.8.2. Changes](release-16-2.html#RELEASE-16-2-CHANGES)

**Release date:  **2024-02-08

This release contains a variety of fixes from 16.1. For information about new
features in major release 16, see [Section E.10](release-16.html
"E.10. Release 16").

### E.8.1. Migration to Version 16.2 #

A dump/restore is not required for those running 16.X.

However, one bug was fixed that could have resulted in corruption of GIN
indexes during concurrent updates. If you suspect such corruption, reindex
affected indexes after installing this update.

Also, if you are upgrading from a version earlier than 16.1, see [Section
E.9](release-16-1.html "E.9. Release 16.1").

### E.8.2. Changes #

  * Tighten security restrictions within `REFRESH MATERIALIZED VIEW CONCURRENTLY` (Heikki Linnakangas) [§](https://postgr.es/c/d6a61cb3b) [§](https://postgr.es/c/fb3836855)

One step of a concurrent refresh command was run under weak security
restrictions. If a materialized view's owner could persuade a superuser or
other high-privileged user to perform a concurrent refresh on that view, the
view's owner could control code executed with the privileges of the user
running `REFRESH`. Fix things so that all user-determined code is run as the
view's owner, as expected.

The only known exploit for this error does not work in PostgreSQL 16.0 and
later, so it may be that v16 is not vulnerable in practice.

The PostgreSQL Project thanks Pedro Gallegos for reporting this problem.
(CVE-2024-0985)

  * Fix memory leak when performing JIT inlining (Andres Freund, Daniel Gustafsson) [§](https://postgr.es/c/2cf50585e)

There have been multiple reports of backend processes suffering out-of-memory
conditions after sufficiently many JIT compilations. This fix should resolve
that.

  * Avoid generating incorrect partitioned-join plans (Richard Guo) [§](https://postgr.es/c/62f120203)

Some uncommon situations involving lateral references could create incorrect
plans. Affected queries could produce wrong answers, or odd failures such as
“variable not found in subplan target list”, or executor crashes.

  * Fix incorrect wrapping of subquery output expressions in PlaceHolderVars (Tom Lane) [§](https://postgr.es/c/80bece312)

This fixes incorrect results when a subquery is underneath an outer join and
has an output column that laterally references something outside the outer
join's scope. The output column might not appear as NULL when it should do so
due to the action of the outer join.

  * Fix misprocessing of window function run conditions (Richard Guo) [§](https://postgr.es/c/ee9553218)

This oversight could lead to “WindowFunc not found in subplan target lists”
errors.

  * Fix detection of inner-side uniqueness for Memoize plans (Richard Guo) [§](https://postgr.es/c/74f770ef2)

This mistake could lead to “cache entry already complete” errors.

  * Fix computation of nullingrels when constant-folding field selection (Richard Guo) [§](https://postgr.es/c/6bf2efb38)

Failure to do this led to errors like “wrong varnullingrels (b) (expected (b
3)) for Var 2/2”.

  * Skip inappropriate actions when `MERGE` causes a cross-partition update (Dean Rasheed) [§](https://postgr.es/c/06a546382)

When executing a `MERGE UPDATE` action on a partitioned table, if the `UPDATE`
is turned into a `DELETE` and `INSERT` due to changing a partition key column,
skip firing `AFTER UPDATE ROW` triggers, as well as other post-update actions
such as RLS checks. These actions would typically fail, which is why a regular
`UPDATE` doesn't do them in such cases; `MERGE` shouldn't either.

  * Cope with `BEFORE ROW DELETE` triggers in cross-partition `MERGE` updates (Dean Rasheed) [§](https://postgr.es/c/7f07384dc)

If such a trigger attempted to prevent the update by returning NULL, `MERGE`
would suffer an error or assertion failure.

  * Prevent access to a no-longer-pinned buffer in `BEFORE ROW UPDATE` triggers (Alexander Lakhin, Tom Lane) [§](https://postgr.es/c/23e0ba59c)

If the tuple being updated had just been updated and moved to another page by
another session, there was a narrow window where we would attempt to fetch
data from the new tuple version without any pin on its buffer. In principle
this could result in garbage data appearing in non-updated columns of the
proposed new tuple. The odds of problems in practice seem rather low, however.

  * Avoid requesting an oversize shared-memory area in parallel hash join (Thomas Munro, Andrei Lepikhov, Alexander Korotkov) [§](https://postgr.es/c/714a987bc) [§](https://postgr.es/c/20a566cd4)

The limiting value was too large, allowing “invalid DSA memory alloc request
size” errors to occur with sufficiently large expected hash table sizes.

  * Fix corruption of local buffer state when an error occurs while trying to extend a temporary table (Tender Wang) [§](https://postgr.es/c/37c551663)

  * Fix use of wrong tuple slot while evaluating `DISTINCT` aggregates that have multiple arguments (David Rowley) [§](https://postgr.es/c/6298673f4)

This mistake could lead to errors such as “attribute 1 of type record has
wrong type”.

  * Avoid assertion failures in `heap_update()` and `heap_delete()` when a tuple to be updated by a foreign-key enforcement trigger fails the extra visibility crosscheck (Alexander Lakhin) [§](https://postgr.es/c/9fee3232a)

This error had no impact in non-assert builds.

  * Fix overly tight assertion about `false_positive_rate` parameter of BRIN bloom operator classes (Alexander Lakhin) [§](https://postgr.es/c/4dccf9575)

This error had no impact in non-assert builds, either.

  * Fix possible failure during `ALTER TABLE ADD COLUMN` on a complex inheritance tree (Tender Wang) [§](https://postgr.es/c/51193e7a7)

If a grandchild table would inherit the new column via multiple intermediate
parents, the command failed with “tuple already updated by self”.

  * Fix problems with duplicate token names in `ALTER TEXT SEARCH CONFIGURATION ... MAPPING` commands (Tender Wang, Michael Paquier) [§](https://postgr.es/c/f33e83285)

  * Fix `DROP ROLE` with duplicate role names (Michael Paquier) [§](https://postgr.es/c/f57a580fd)

Previously this led to a “tuple already updated by self” failure. Instead,
ignore the duplicate.

  * Properly lock the associated table during `DROP STATISTICS` (Tomas Vondra) [§](https://postgr.es/c/ee32b824d)

Failure to acquire the lock could result in “tuple concurrently deleted”
errors if the `DROP` executes concurrently with `ANALYZE`.

  * Fix function volatility checking for `GENERATED` and `DEFAULT` expressions (Tom Lane) [§](https://postgr.es/c/f07a3039c)

These places could fail to detect insertion of a volatile function default-
argument expression, or decide that a polymorphic function is volatile
although it is actually immutable on the datatype of interest. This could lead
to improperly rejecting or accepting a `GENERATED` clause, or to mistakenly
applying the constant-default-value optimization in `ALTER TABLE ADD COLUMN`.

  * Detect that a new catalog cache entry became stale while detoasting its fields (Tom Lane) [§](https://postgr.es/c/7e2561e1a) [§](https://postgr.es/c/56dcd71de)

We expand any out-of-line fields in a catalog tuple before inserting it into
the catalog caches. That involves database access which might cause
invalidation of catalog cache entries — but the new entry isn't in the cache
yet, so we would miss noticing that it should get invalidated. The result is a
race condition in which an already-stale cache entry could get made, and then
persist indefinitely. This would lead to hard-to-predict misbehavior. Fix by
rechecking the tuple's visibility after detoasting.

  * Fix edge-case integer overflow detection bug on some platforms (Dean Rasheed) [§](https://postgr.es/c/c396aca2b)

Computing `0 - INT64_MIN` should result in an overflow error, and did on most
platforms. However, platforms with neither integer overflow builtins nor
128-bit integers would fail to spot the overflow, instead returning
`INT64_MIN`.

  * Detect Julian-date overflow when adding or subtracting an `interval` to/from a `timestamp` (Tom Lane) [§](https://postgr.es/c/7204aea83)

Some cases that should cause an out-of-range error produced an incorrect
result instead.

  * Add more checks for overflow in `interval_mul()` and `interval_div()` (Dean Rasheed) [§](https://postgr.es/c/72d0c135b)

Some cases that should cause an out-of-range error produced an incorrect
result instead.

  * Allow `scram_SaltedPassword()` to be interrupted (Bowen Shi) [§](https://postgr.es/c/07cb7bc1c)

With large `scram_iterations` values, this function could take a long time to
run. Allow it to be interrupted by query cancel requests.

  * Ensure cached statistics are discarded after a change to `stats_fetch_consistency` (Shinya Kato) [§](https://postgr.es/c/781bc121d)

In some code paths, it was possible for stale statistics to be returned.

  * Make the `pg_file_settings` view check validity of unapplied values for settings with `backend` or `superuser-backend` context (Tom Lane) [§](https://postgr.es/c/e87252ceb)

Invalid values were not noted in the view as intended. This escaped detection
because there are very few settings in these groups.

  * Match collation too when matching an existing index to a new partitioned index (Peter Eisentraut) [§](https://postgr.es/c/267f33f68)

Previously we could accept an index that has a different collation from the
corresponding element of the partition key, possibly leading to misbehavior.

  * Avoid failure if a child index is dropped concurrently with `REINDEX INDEX` on a partitioned index (Fei Changhong) [§](https://postgr.es/c/c030e263e) [§](https://postgr.es/c/7ce65c6f7)

  * Fix insufficient locking when cleaning up an incomplete split of a GIN index's internal page (Fei Changhong, Heikki Linnakangas) [§](https://postgr.es/c/b899e00e7)

The code tried to do this with shared rather than exclusive lock on the
buffer. This could lead to index corruption if two processes attempted the
cleanup concurrently.

  * Avoid premature release of buffer pin in GIN index insertion (Tom Lane) [§](https://postgr.es/c/f76b975d5)

If an index root page split occurs concurrently with our own insertion, the
code could fail with “buffer NNNN is not owned by resource owner”.

  * Avoid failure with partitioned SP-GiST indexes (Tom Lane) [§](https://postgr.es/c/0977bd64e)

Trying to use an index of this kind could lead to “No such file or directory”
errors.

  * Fix ownership tests for large objects (Tom Lane) [§](https://postgr.es/c/152bfc0af)

Operations on large objects that require ownership privilege failed with
“unrecognized class ID: 2613”, unless run by a superuser.

  * Fix ownership change reporting for large objects (Tom Lane) [§](https://postgr.es/c/152bfc0af)

A no-op `ALTER LARGE OBJECT OWNER` command (that is, one selecting the
existing owner) passed the wrong class ID to the `PostAlterHook`, probably
confusing any extension using that hook.

  * Fix reporting of I/O timing data in `EXPLAIN (BUFFERS)` (Michael Paquier) [§](https://postgr.es/c/db69101a1)

The numbers labeled as “shared/local” actually refer only to shared buffers,
so change that label to “shared”.

  * Ensure durability of `CREATE DATABASE` (Noah Misch) [§](https://postgr.es/c/6d423e9ff) [§](https://postgr.es/c/48a6bf5c4)

If an operating system crash occurred during or shortly after `CREATE
DATABASE`, recovery could fail, or subsequent connections to the new database
could fail. If a base backup was taken in that window, similar problems could
be observed when trying to use the backup. The symptom would be that the
database directory, `PG_VERSION` file, or `pg_filenode.map` file was missing
or empty.

  * Add more `LOG` messages when starting and ending recovery from a backup (Andres Freund) [§](https://postgr.es/c/edbd1b41a)

This change provides additional information in the postmaster log that may be
useful for diagnosing recovery problems.

  * Prevent standby servers from incorrectly processing dead index tuples during subtransactions (Fei Changhong) [§](https://postgr.es/c/0e2c05af9)

The `startedInRecovery` flag was not correctly set for a subtransaction. This
affects only processing of dead index tuples. It could allow a query in a
subtransaction to ignore index entries that it should return (if they are
already dead on the primary server, but not dead to the standby transaction),
or to prematurely mark index entries as dead that are not yet dead on the
primary. It is not clear that the latter case has any serious consequences,
but it's not the intended behavior.

  * Fix signal handling in walreceiver processes (Heikki Linnakangas) [§](https://postgr.es/c/c5a6d5337)

Revert a change that made walreceivers non-responsive to SIGTERM while waiting
for the replication connection to be established.

  * Fix integer overflow hazard in checking whether a record will fit into the WAL decoding buffer (Thomas Munro) [§](https://postgr.es/c/8ca56620c)

This bug appears to be only latent except when running a 32-bit PostgreSQL
build on a 64-bit platform.

  * Fix deadlock between a logical replication apply worker, its tablesync worker, and a session process trying to alter the subscription (Shlok Kyal) [§](https://postgr.es/c/01cc92fa6)

One edge of the deadlock loop did not involve a lock wait, so the deadlock
went undetected and would persist until manual intervention.

  * Ensure that column default values are correctly transmitted by the pgoutput logical replication plugin (Nikhil Benesch) [§](https://postgr.es/c/d7ca9209c)

`ALTER TABLE ADD COLUMN` with a constant default value for the new column
avoids rewriting existing tuples, instead expecting that reading code will
insert the correct default into a tuple that lacks that column. If replication
was subsequently initiated on the table, pgoutput would transmit NULL instead
of the correct default for such a column, causing incorrect replication on the
subscriber.

  * Fix failure of logical replication's initial sync for a table with no columns (Vignesh C) [§](https://postgr.es/c/1b6da28e0)

This case generated an improperly-formatted `COPY` command.

  * Re-validate a subscription's connection string before use (Vignesh C) [§](https://postgr.es/c/4c03ac7e2) [§](https://postgr.es/c/5b5318c38)

This is meant to detect cases where a subscription was created without a
password (which is allowed to superusers) but then the subscription owner is
changed to a non-superuser.

  * Return the correct status code when a new client disconnects without responding to the server's password challenge (Liu Lang, Tom Lane) [§](https://postgr.es/c/fb464a1ae)

In some cases we'd treat this as a loggable error, which was not the intention
and tends to create log spam, since common clients like psql frequently do
this. It may also confuse extensions that use `ClientAuthentication_hook`.

  * Fix incompatibility with OpenSSL 3.2 (Tristan Partin, Bo Andreson) [§](https://postgr.es/c/efa8f6064)

Use the BIO “app_data” field for our private storage, instead of assuming it's
okay to use the “data” field. This mistake didn't cause problems before, but
with 3.2 it leads to crashes and complaints about double frees.

  * Be more wary about OpenSSL not setting `errno` on error (Tom Lane) [§](https://postgr.es/c/ebbd499d4)

If `errno` isn't set, assume the cause of the reported failure is read EOF.
This fixes rare cases of strange error reports like “could not accept SSL
connection: Success”.

  * Fix file descriptor leakage when a foreign data wrapper's `ForeignAsyncRequest` function fails (Heikki Linnakangas) [§](https://postgr.es/c/501cfd07d)

  * Fix minor memory leak in connection string validation for `CREATE SUBSCRIPTION` (Jeff Davis) [§](https://postgr.es/c/41820e640)

  * Report ENOMEM errors from file-related system calls as `ERRCODE_OUT_OF_MEMORY`, not `ERRCODE_INTERNAL_ERROR` (Alexander Kuzmenkov) [§](https://postgr.es/c/a15378100)

  * In PL/pgSQL, support SQL commands that are `CREATE FUNCTION`/`CREATE PROCEDURE` with SQL-standard bodies (Tom Lane) [§](https://postgr.es/c/00f941356)

Previously, such cases failed with parsing errors due to the semicolon(s)
appearing in the function body.

  * Fix libpq's handling of errors in pipelines (Álvaro Herrera) [§](https://postgr.es/c/878aa41f8) [§](https://postgr.es/c/39aab1108)

The pipeline state could get out of sync if an error is returned for reasons
other than a query problem (for example, if the connection is lost).
Potentially this would lead to a busy-loop in the calling application.

  * Make libpq's `PQsendFlushRequest()` function flush the client output buffer under the same rules as other `PQsend` functions (Jelte Fennema-Nio) [§](https://postgr.es/c/42f832685)

In pipeline mode, it may still be necessary to call `PQflush()` as well; but
this change removes some inconsistency.

  * Avoid race condition when libpq initializes OpenSSL support concurrently in two different threads (Willi Mann, Michael Paquier) [§](https://postgr.es/c/8984480b5)

  * Fix timing-dependent failure in GSSAPI data transmission (Tom Lane) [§](https://postgr.es/c/85eb77185)

When using GSSAPI encryption in non-blocking mode, libpq sometimes failed with
“GSSAPI caller failed to retransmit all data needing to be retried”.

  * Change initdb to always un-comment the `postgresql.conf` entries for the `lc__`xxx`_` parameters (Kyotaro Horiguchi) [§](https://postgr.es/c/ba33775fd)

initdb used to work this way before v16, and now it does again. The change
caused initdb's `--no-locale` option to not have the intended effect on
`lc_messages`.

  * In pg_dump, don't dump RLS policies or security labels for extension member objects (Tom Lane, Jacob Champion) [§](https://postgr.es/c/64d2467fc) [§](https://postgr.es/c/f1674ac6b)

Previously, commands would be included in the dump to set these properties,
which is really incorrect since they should be considered as internal affairs
of the extension. Moreover, the restoring user might not have adequate
privilege to set them, and indeed the dumping user might not have enough
privilege to dump them (since dumping RLS policies requires acquiring lock on
their table).

  * In pg_dump, don't dump an extended statistics object if its underlying table isn't being dumped (Rian McGuire, Tom Lane) [§](https://postgr.es/c/b2c9936a7)

This conforms to the behavior for other dependent objects such as indexes.

  * Properly detect out-of-memory in one code path in pg_dump (Daniel Gustafsson) [§](https://postgr.es/c/5b5db413d)

  * Make it an error for a pgbench script to end with an open pipeline (Anthonin Bonnefoy) [§](https://postgr.es/c/07b53de70)

Previously, pgbench would behave oddly if a `\startpipeline` command lacked a
matching `\endpipeline`. This seems like a scripting mistake rather than a
case that pgbench needs to handle nicely, so throw an error.

  * Fix crash in `contrib/intarray` if an array with an element equal to `INT_MAX` is inserted into a `gist__int_ops` index (Alexander Lakhin, Tom Lane) [§](https://postgr.es/c/cf6f802bf)

  * Report a better error when `contrib/pageinspect`'s `hash_bitmap_info()` function is applied to a partitioned hash index (Alexander Lakhin, Michael Paquier) [§](https://postgr.es/c/7f68b1462)

  * Report a better error when `contrib/pgstattuple`'s `pgstathashindex()` function is applied to a partitioned hash index (Alexander Lakhin) [§](https://postgr.es/c/b4948ed66)

  * On Windows, suppress autorun options when launching subprocesses in pg_ctl and pg_regress (Kyotaro Horiguchi) [§](https://postgr.es/c/714bfb781) [§](https://postgr.es/c/506c77f9b)

When launching a child process via `cmd.exe`, pass the `/D` flag to prevent
executing any autorun commands specified in the registry. This avoids
possibly-surprising side effects.

  * Move `is_valid_ascii()` from `mb/pg_wchar.h` to `utils/ascii.h` (Jubilee Young) [§](https://postgr.es/c/1b924a86e)

This change avoids the need to include `<simd.h>` in `pg_wchar.h`, which was
causing problems for some third-party code.

  * Fix compilation failures with libxml2 version 2.12.0 and later (Tom Lane) [§](https://postgr.es/c/e02fea093)

  * Fix compilation failure of `WAL_DEBUG` code on Windows (Bharath Rupireddy) [§](https://postgr.es/c/6248a2bb9)

  * Suppress compiler warnings from Python's header files (Peter Eisentraut, Tom Lane) [§](https://postgr.es/c/b0115e7e2) [§](https://postgr.es/c/c72049dbc)

Our preferred compiler options provoke warnings about constructs appearing in
recent versions of Python's header files. When using gcc, we can suppress
these warnings with a pragma.

  * Avoid deprecation warning when compiling with LLVM 18 (Thomas Munro) [§](https://postgr.es/c/60ba7cae7)

  * Update time zone data files to tzdata release 2024a for DST law changes in Greenland, Kazakhstan, and Palestine, plus corrections for the Antarctic stations Casey and Vostok. Also historical corrections for Vietnam, Toronto, and Miquelon. (Tom Lane) [§](https://postgr.es/c/b4fb76fb5)

* * *

[Prev](release-16-3.html "E.7. Release 16.3")  | [Up](release.html "Appendix E. Release Notes") |  [Next](release-16-1.html "E.9. Release 16.1")  
---|---|---  
E.7. Release 16.3  | [Home](index.html "PostgreSQL 16.9 Documentation") |  E.9. Release 16.1  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/release-16-2.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

