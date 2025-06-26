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

Supported Versions: [16](/docs/16/release-16-7.html "PostgreSQL 16 -
E.3. Release 16.7")

__

E.3. Release 16.7  
---  
[Prev](release-16-8.html "E.2. Release 16.8")  | [Up](release.html "Appendix E. Release Notes") | Appendix E. Release Notes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](release-16-6.html "E.4. Release 16.6")  
  
* * *

## E.3. Release 16.7 #

[E.3.1. Migration to Version 16.7](release-16-7.html#RELEASE-16-7-MIGRATION)

[E.3.2. Changes](release-16-7.html#RELEASE-16-7-CHANGES)

**Release date:  **2025-02-13

This release contains a variety of fixes from 16.6. For information about new
features in major release 16, see [Section E.10](release-16.html
"E.10. Release 16").

### E.3.1. Migration to Version 16.7 #

A dump/restore is not required for those running 16.X.

However, if you are upgrading from a version earlier than 16.5, see [Section
E.5](release-16-5.html "E.5. Release 16.5").

### E.3.2. Changes #

  * Harden `PQescapeString` and allied functions against invalidly-encoded input strings (Andres Freund, Noah Misch) [§](https://postgr.es/c/92e4170f4) [§](https://postgr.es/c/6e05b195d) [§](https://postgr.es/c/56aa2dcdd) [§](https://postgr.es/c/01784793f) [§](https://postgr.es/c/41343f840) [§](https://postgr.es/c/0075a5c6c)

Data-quoting functions supplied by libpq now fully check the encoding validity
of their input. If invalid characters are detected, they report an error if
possible. For the ones that lack an error return convention, the output string
is adjusted to ensure that the server will report invalid encoding and no
intervening processing will be fooled by bytes that might happen to match
single quote, backslash, etc.

The purpose of this change is to guard against SQL-injection attacks that are
possible if one of these functions is used to quote crafted input. There is no
hazard when the resulting string is sent directly to a PostgreSQL server
(which would check its encoding anyway), but there is a risk when it is passed
through psql or other client-side code. Historically such code has not
carefully vetted encoding, and in many cases it's not clear what it should do
if it did detect such a problem.

This fix is effective only if the data-quoting function, the server, and any
intermediate processing agree on the character encoding that's being used.
Applications that insert untrusted input into SQL commands should take special
care to ensure that that's true.

Applications and drivers that quote untrusted input without using these libpq
functions may be at risk of similar problems. They should first confirm the
data is valid in the encoding expected by the server.

The PostgreSQL Project thanks Stephen Fewer for reporting this problem.
(CVE-2025-1094)

  * Exclude parallel workers from connection privilege checks and limits (Tom Lane) [§](https://postgr.es/c/41a252c2c)

Do not check `datallowconn`, `rolcanlogin`, and `ACL_CONNECT` privileges when
starting a parallel worker, instead assuming that it's enough for the leader
process to have passed similar checks originally. This avoids, for example,
unexpected failures of parallelized queries when the leader is running as a
role that lacks login privilege. In the same vein, enforce
`ReservedConnections`, `datconnlimit`, and `rolconnlimit` limits only against
regular backends, and count only regular backends while checking if the limits
were already reached. Those limits are meant to prevent excessive consumption
of process slots for regular backends --- but parallel workers and other
special processes have their own pools of process slots with their own limit
checks.

  * Fix possible re-use of stale results in window aggregates (David Rowley) [§](https://postgr.es/c/c1d6506ac)

A window aggregate with a “run condition” optimization and a pass-by-reference
result type might incorrectly return the result from the previous partition
instead of performing a fresh calculation.

  * Keep `TransactionXmin` in sync with `MyProc->xmin` (Heikki Linnakangas) [§](https://postgr.es/c/9d8ab2c46)

This oversight could permit a process to try to access data that had already
been vacuumed away. One known consequence is transient “could not access
status of transaction” errors.

  * Fix race condition that could cause failure to add a newly-inserted catalog entry to a catalog cache list (Heikki Linnakangas) [§](https://postgr.es/c/91fc447c2)

This could result, for example, in failure to use a newly-created function
within an existing session.

  * Prevent possible catalog corruption when a system catalog is vacuumed concurrently with an update (Noah Misch) [§](https://postgr.es/c/9311fcb86)

  * Fix data corruption when relation truncation fails (Thomas Munro) [§](https://postgr.es/c/ba02d24ba) [§](https://postgr.es/c/c957d7444) [§](https://postgr.es/c/9defaaa1d)

The filesystem calls needed to perform relation truncation could fail, leaving
inconsistent state on disk (for example, effectively reviving deleted data).
We can't really prevent that, but we can recover by dint of making such
failures into PANICs, so that consistency is restored by replaying from WAL up
to just before the attempted truncation. This isn't a hugely desirable
behavior, but such failures are rare enough that it seems an acceptable
solution.

  * Prevent checkpoints from starting during relation truncation (Robert Haas) [§](https://postgr.es/c/ad5aa7bfd)

This avoids a race condition wherein the modified file might not get fsync'd
before completing the checkpoint, creating a risk of data corruption if the
operating system crashes soon after.

  * Avoid possibly losing an update of `pg_database`.`datfrozenxid` when `VACUUM` runs concurrently with a `REASSIGN OWNED` that changes that database's owner (Kirill Reshke) [§](https://postgr.es/c/5d94aa4dc)

  * Fix incorrect `tg_updatedcols` values passed to `AFTER UPDATE` triggers (Tom Lane) [§](https://postgr.es/c/8c57f5485)

In some cases the `tg_updatedcols` bitmap could describe the set of columns
updated by an earlier command in the same transaction, fooling the trigger
into doing the wrong thing.

Also, prevent memory bloat caused by making too many copies of the
`tg_updatedcols` bitmap.

  * Fix detach of a partition that has its own foreign-key constraint referencing a partitioned table (Amul Sul) [§](https://postgr.es/c/ddab512eb)

In common cases, foreign keys are defined on a partitioned table's top level;
but if instead one is defined on a partition and references a partitioned
table, and the referencing partition is detached, the relevant `pg_constraint`
entries were updated incorrectly. This led to errors like “could not find ON
INSERT check triggers of foreign key constraint”.

  * Fix mis-processing of `to_timestamp`'s `FF _`n`_` format codes (Tom Lane) [§](https://postgr.es/c/26c233b8b)

An integer format code immediately preceding `FF _`n`_` would consume all
available digits, leaving none for `FF _`n`_`.

  * When deparsing an `XMLTABLE()` expression, ensure that XML namespace names are double-quoted when necessary (Dean Rasheed) [§](https://postgr.es/c/77763f3be)

  * Include the `ldapscheme` option in `pg_hba_file_rules()` output (Laurenz Albe) [§](https://postgr.es/c/c35bbdfbc) [§](https://postgr.es/c/116036d81)

  * Don't merge `UNION` operations if their column collations aren't consistent (Tom Lane) [§](https://postgr.es/c/f286f64bc)

Previously we ignored collations when deciding if it's safe to merge `UNION`
steps into a single N-way `UNION` operation. This was arguably valid before
the introduction of nondeterministic collations, but it's not anymore, since
the collation in use can affect the definition of uniqueness.

  * Prevent “wrong varnullingrels” planner errors after pulling up a subquery that's underneath an outer join (Tom Lane) [§](https://postgr.es/c/85990e2fd) [§](https://postgr.es/c/7b456f040)

  * Ignore nulling-relation marker bits when looking up statistics (Richard Guo) [§](https://postgr.es/c/a1a9120c7)

This oversight could lead to failure to use relevant statistics about
expressions, or to “corrupt MVNDistinct entry” errors.

  * Fix missed expression processing for partition pruning steps (Tom Lane) [§](https://postgr.es/c/94c02bd33)

This oversight could lead to “unrecognized node type” errors, and perhaps
other problems, in queries accessing partitioned tables.

  * Allow dshash tables to grow past 1GB (Matthias van de Meent) [§](https://postgr.es/c/2a7402322)

This avoids errors like “invalid DSA memory alloc request size”. The case can
occur for example in transactions that process several million tables.

  * Avoid possible integer overflow in `bringetbitmap()` (James Hunter, Evgeniy Gorbanyov) [§](https://postgr.es/c/bfda7d8dd)

Since the result is only used for statistical purposes, the effects of this
error were mostly cosmetic.

  * Ensure that an already-set process latch doesn't prevent the postmaster from noticing socket events (Thomas Munro) [§](https://postgr.es/c/b4b52c911)

An extremely heavy workload of backends launching workers and workers exiting
could prevent the postmaster from responding to incoming client connections in
a timely fashion.

  * Prevent streaming standby servers from looping infinitely when reading a WAL record that crosses pages (Kyotaro Horiguchi, Alexander Kukushkin) [§](https://postgr.es/c/2c2e1d4f4)

This would happen when the record's continuation is on a page that needs to be
read from a different WAL source.

  * Fix unintended promotion of FATAL errors to PANIC during early process startup (Noah Misch) [§](https://postgr.es/c/ac4a2b403)

This fixes some unlikely cases that would result in “PANIC: proc_exit() called
in child process”.

  * Fix cases where an operator family member operator or support procedure could become a dangling reference (Tom Lane) [§](https://postgr.es/c/be5db08ed) [§](https://postgr.es/c/faad01835)

In some cases a data type could be dropped while references to its OID still
remain in `pg_amop` or `pg_amproc`. While that caused no immediate issues, an
attempt to drop the owning operator family would fail, and pg_dump would
produce bogus output when dumping the operator family. This fix causes
creation and modification of operator families/classes to add needed
dependency entries so that dropping a data type will also drop any dependent
operator family elements. That does not help vulnerable pre-existing operator
families, though, so a band-aid has also been added to `DROP OPERATOR FAMILY`
to prevent failure when dropping a family that has dangling members.

  * Fix multiple memory leaks in logical decoding output (Vignesh C, Masahiko Sawada, Boyu Yang) [§](https://postgr.es/c/e3a27fd06) [§](https://postgr.es/c/4d45e7490) [§](https://postgr.es/c/e749eaf46)

  * Fix small memory leak when updating the `application_name` or `cluster_name` settings (Tofig Aliev) [§](https://postgr.es/c/be9dac9af)

  * Avoid integer overflow while testing `wal_skip_threshold` condition (Tom Lane) [§](https://postgr.es/c/f7a08b6e9)

A transaction that created a very large relation could mistakenly decide to
ensure durability by copying the relation into WAL instead of fsync'ing it,
thereby negating the point of `wal_skip_threshold`. (This only matters when
`wal_level` is set to `minimal`, else a WAL copy is required anyway.)

  * Fix unsafe order of operations during cache lookups (Noah Misch) [§](https://postgr.es/c/c1285bbeb)

The only known consequence was a usually-harmless “you don't own a lock of
type ExclusiveLock” warning during `GRANT TABLESPACE`.

  * Fix possible “failed to resolve name” failures when using JIT on older ARM platforms (Thomas Munro) [§](https://postgr.es/c/6de14dbb3)

This could occur as a consequence of inconsistency about the default setting
of `-moutline-atomics` between gcc and clang. At least Debian and Ubuntu are
known to ship gcc and clang compilers that target armv8-a but differ on the
use of outline atomics by default.

  * Fix assertion failure in `WITH RECURSIVE ... UNION` queries (David Rowley) [§](https://postgr.es/c/093fc156b)

  * Avoid assertion failure in rule deparsing if a set operation leaf query contains set operations (Man Zeng, Tom Lane) [§](https://postgr.es/c/fe084039e)

  * Avoid edge-case assertion failure in parallel query startup (Tom Lane) [§](https://postgr.es/c/bb649b553)

  * Fix assertion failure at shutdown when writing out the statistics file (Michael Paquier) [§](https://postgr.es/c/ae77bcc3a)

  * In `NULLIF()`, avoid passing a read-write expanded object pointer to the data type's equality function (Tom Lane) [§](https://postgr.es/c/4aba56adc)

The equality function could modify or delete the object if it's given a read-
write pointer, which would be bad if we decide to return it as the `NULLIF()`
result. There is probably no problem with any built-in equality function, but
it's easy to demonstrate a failure with one coded in PL/pgSQL.

  * Ensure that expression preprocessing is applied to a default null value in `INSERT` (Tom Lane) [§](https://postgr.es/c/6655d931c)

If the target column is of a domain type, the planner must insert a coerce-to-
domain step not just a null constant, and this expression missed going through
some required processing steps. There is no known consequence with domains
based on core data types, but in theory an error could occur with domains
based on extension types.

  * Repair memory leaks in PL/Python (Mat Arye, Tom Lane) [§](https://postgr.es/c/33a4e656d)

Repeated use of `PLyPlan.execute` or `plpy.cursor` resulted in memory leakage
for the duration of the calling PL/Python function.

  * Fix PL/Tcl to compile with Tcl 9 (Peter Eisentraut) [§](https://postgr.es/c/07c77803c)

  * In the ecpg preprocessor, fix possible misprocessing of cursors that reference out-of-scope variables (Tom Lane) [§](https://postgr.es/c/cca34f68c)

  * In ecpg, fix compile-time warnings about unsupported use of `COPY ... FROM STDIN` (Ryo Kanbayashi) [§](https://postgr.es/c/5c7c34db2)

Previously, the intended warning was not issued due to a typo.

  * Fix psql to safely handle file path names that are encoded in SJIS (Tom Lane) [§](https://postgr.es/c/998c4fc7c)

Some two-byte characters in SJIS have a second byte that is equal to ASCII
backslash (`\`). These characters were corrupted by path name normalization,
preventing access to files whose names include such characters.

  * Fix use of wrong version of `pqsignal()` in pgbench and psql (Fujii Masao, Tom Lane) [§](https://postgr.es/c/b935691b8)

This error could lead to misbehavior when using the `-T` option in pgbench or
the `\watch` command in psql, due to interrupted system calls not being
resumed as expected.

  * Fix misexecution of some nested `\if` constructs in pgbench (Michail Nikolaev) [§](https://postgr.es/c/076b09123)

An `\if` command appearing within a false (not-being-executed) `\if` branch
was incorrectly treated the same as `\elif`.

  * In pgbench, fix possible misdisplay of progress messages during table initialization (Yushi Ogiwara, Tatsuo Ishii, Fujii Masao) [§](https://postgr.es/c/1cf646957) [§](https://postgr.es/c/21b815f92)

  * Make pg_controldata more robust against corrupted `pg_control` files (Ilyasov Ian, Anton Voloshin) [§](https://postgr.es/c/d54d5668b)

Since pg_controldata will attempt to print the contents of `pg_control` even
if the CRC check fails, it must take care not to misbehave for invalid field
values. This patch fixes some issues triggered by invalid timestamps and
apparently-negative WAL segment sizes.

  * Fix possible crash in pg_dump with identity sequences attached to tables that are extension members (Tom Lane) [§](https://postgr.es/c/782cc1aa3)

  * Fix memory leak in pg_restore with zstd-compressed data (Tom Lane) [§](https://postgr.es/c/8cfff087b)

The leak was per-decompression-operation, so would be most noticeable with a
dump containing many tables or large objects.

  * Fix pg_basebackup to correctly handle `pg_wal.tar` files exceeding 2GB on Windows (Davinder Singh, Thomas Munro) [§](https://postgr.es/c/be7489662) [§](https://postgr.es/c/0bff6f1da)

  * Use SQL-standard function bodies in the declarations of `contrib/earthdistance`'s SQL-language functions (Tom Lane, Ronan Dunklau) [§](https://postgr.es/c/31daa10fa)

This change allows their references to `contrib/cube` to be resolved during
extension creation, reducing the risk of search-path-based failures and
possible attacks.

In particular, this restores their usability in contexts like generated
columns, for which PostgreSQL v17 restricts the search path on security
grounds. We have received reports of databases failing to be upgraded to v17
because of that. This patch has been included in v16 to provide a workaround:
updating the `earthdistance` extension to this version beforehand should allow
an upgrade to succeed.

  * Update configuration probes that determine the compiler switches needed to access ARM CRC instructions (Tom Lane) [§](https://postgr.es/c/1f4aadec4)

On ARM platforms where the baseline CPU target lacks CRC instructions, we need
to supply a `-march` switch to persuade the compiler to compile such
instructions. Recent versions of gcc reject the value we were trying, leading
to silently falling back to software CRC.

  * Fix meson build system to support old OpenSSL libraries on Windows (Darek Slusarczyk) [§](https://postgr.es/c/60516fc8b)

Add support for the legacy library names `ssleay32` and `libeay32`.

  * In Windows builds using meson, ensure all libcommon and libpgport functions are exported (Vladlen Popolitov, Heikki Linnakangas) [§](https://postgr.es/c/4e0d71ff2) [§](https://postgr.es/c/643efb18b)

This fixes “unresolved external symbol” build errors for extensions.

  * Fix meson configuration process to correctly detect OSSP's `uuid.h` header file under MSVC (Andrew Dunstan) [§](https://postgr.es/c/1250adfdf)

  * When building with meson, install `pgevent` in _`pkglibdir`_ not _`bindir`_ (Peter Eisentraut) [§](https://postgr.es/c/766b0b40a)

This matches the behavior of the make-based build system and the old MSVC
build system.

  * When building with meson, install `sepgsql.sql` under `share/contrib/` not `share/extension/` (Peter Eisentraut) [§](https://postgr.es/c/155d6162e)

This matches what the make-based build system does.

  * Update time zone data files to tzdata release 2025a for DST law changes in Paraguay, plus historical corrections for the Philippines (Tom Lane) [§](https://postgr.es/c/d62403c51)

* * *

[Prev](release-16-8.html "E.2. Release 16.8")  | [Up](release.html "Appendix E. Release Notes") |  [Next](release-16-6.html "E.4. Release 16.6")  
---|---|---  
E.2. Release 16.8  | [Home](index.html "PostgreSQL 16.9 Documentation") |  E.4. Release 16.6  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/release-16-7.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

