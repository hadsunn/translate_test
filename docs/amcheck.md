[Documentation](/docs/ "Documentation") -> [PostgreSQL
16](index.md)

Supported Versions: [Current](/docs/current/amcheck.md "PostgreSQL 17 -
F.2. amcheck — tools to verify table and index consistency")
([17](/docs/17/amcheck.md "PostgreSQL 17 - F.2. amcheck — tools to verify
table and index consistency")) / [16](/docs/16/amcheck.md "PostgreSQL 16 -
F.2. amcheck — tools to verify table and index consistency") /
[15](/docs/15/amcheck.md "PostgreSQL 15 - F.2. amcheck — tools to verify
table and index consistency") / [14](/docs/14/amcheck.md "PostgreSQL 14 -
F.2. amcheck — tools to verify table and index consistency") /
[13](/docs/13/amcheck.md "PostgreSQL 13 - F.2. amcheck — tools to verify
table and index consistency")

Development Versions: [18](/docs/18/amcheck.md "PostgreSQL 18 - F.2. amcheck
— tools to verify table and index consistency") /
[devel](/docs/devel/amcheck.md "PostgreSQL devel - F.2. amcheck — tools to
verify table and index consistency")

Unsupported versions: [12](/docs/12/amcheck.md "PostgreSQL 12 - F.2. amcheck
— tools to verify table and index consistency") / [11](/docs/11/amcheck.md
"PostgreSQL 11 - F.2. amcheck — tools to verify table and index consistency")
/ [10](/docs/10/amcheck.md "PostgreSQL 10 - F.2. amcheck — tools to verify
table and index consistency")

__

F.2. amcheck — tools to verify table and index consistency  
---  
[Prev](adminpack.md "F.1. adminpack — pgAdmin support toolpack")  | [Up](contrib.md "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.md "PostgreSQL 16.9 Documentation") |  [Next](auth-delay.md "F.3. auth_delay — pause on authentication failure")  
  
* * *

## F.2. amcheck — tools to verify table and index consistency #

[F.2.1. Functions](amcheck.md#AMCHECK-FUNCTIONS)

[F.2.2. Optional _`heapallindexed`_ Verification](amcheck.md#AMCHECK-
OPTIONAL-HEAPALLINDEXED-VERIFICATION)

[F.2.3. Using `amcheck` Effectively](amcheck.md#AMCHECK-USING-AMCHECK-
EFFECTIVELY)

[F.2.4. Repairing Corruption](amcheck.md#AMCHECK-REPAIRING-CORRUPTION)

The `amcheck` module provides functions that allow you to verify the logical
consistency of the structure of relations.

The B-Tree checking functions verify various _invariants_ in the structure of
the representation of particular relations. The correctness of the access
method functions behind index scans and other important operations relies on
these invariants always holding. For example, certain functions verify, among
other things, that all B-Tree pages have items in “logical” order (e.g., for
B-Tree indexes on `text`, index tuples should be in collated lexical order).
If that particular invariant somehow fails to hold, we can expect binary
searches on the affected page to incorrectly guide index scans, resulting in
wrong answers to SQL queries. If the structure appears to be valid, no error
is raised.

Verification is performed using the same procedures as those used by index
scans themselves, which may be user-defined operator class code. For example,
B-Tree index verification relies on comparisons made with one or more B-Tree
support function 1 routines. See [Section 38.16.3](xindex.md#XINDEX-SUPPORT
"38.16.3. Index Method Support Routines") for details of operator class
support functions.

Unlike the B-Tree checking functions which report corruption by raising
errors, the heap checking function `verify_heapam` checks a table and attempts
to return a set of rows, one row per corruption detected. Despite this, if
facilities that `verify_heapam` relies upon are themselves corrupted, the
function may be unable to continue and may instead raise an error.

Permission to execute `amcheck` functions may be granted to non-superusers,
but before granting such permissions careful consideration should be given to
data security and privacy concerns. Although the corruption reports generated
by these functions do not focus on the contents of the corrupted data so much
as on the structure of that data and the nature of the corruptions found, an
attacker who gains permission to execute these functions, particularly if the
attacker can also induce corruption, might be able to infer something of the
data itself from such messages.

### F.2.1. Functions #

`bt_index_check(index regclass, heapallindexed boolean) returns void`

    

`bt_index_check` tests that its target, a B-Tree index, respects a variety of
invariants. Example usage:

    
    
    test=# SELECT bt_index_check(index => c.oid, heapallindexed => i.indisunique),
                   c.relname,
                   c.relpages
    FROM pg_index i
    JOIN pg_opclass op ON i.indclass[0] = op.oid
    JOIN pg_am am ON op.opcmethod = am.oid
    JOIN pg_class c ON i.indexrelid = c.oid
    JOIN pg_namespace n ON c.relnamespace = n.oid
    WHERE am.amname = 'btree' AND n.nspname = 'pg_catalog'
    -- Don't check temp tables, which may be from another session:
    AND c.relpersistence != 't'
    -- Function may throw an error when this is omitted:
    AND c.relkind = 'i' AND i.indisready AND i.indisvalid
    ORDER BY c.relpages DESC LIMIT 10;
     bt_index_check |             relname             | relpages
    ----------------+---------------------------------+----------
                    | pg_depend_reference_index       |       43
                    | pg_depend_depender_index        |       40
                    | pg_proc_proname_args_nsp_index  |       31
                    | pg_description_o_c_o_index      |       21
                    | pg_attribute_relid_attnam_index |       14
                    | pg_proc_oid_index               |       10
                    | pg_attribute_relid_attnum_index |        9
                    | pg_amproc_fam_proc_index        |        5
                    | pg_amop_opr_fam_index           |        5
                    | pg_amop_fam_strat_index         |        5
    (10 rows)
    

This example shows a session that performs verification of the 10 largest
catalog indexes in the database “test”. Verification of the presence of heap
tuples as index tuples is requested for the subset that are unique indexes.
Since no error is raised, all indexes tested appear to be logically
consistent. Naturally, this query could easily be changed to call
`bt_index_check` for every index in the database where verification is
supported.

`bt_index_check` acquires an `AccessShareLock` on the target index and the
heap relation it belongs to. This lock mode is the same lock mode acquired on
relations by simple `SELECT` statements. `bt_index_check` does not verify
invariants that span child/parent relationships, but will verify the presence
of all heap tuples as index tuples within the index when _`heapallindexed`_ is
`true`. When a routine, lightweight test for corruption is required in a live
production environment, using `bt_index_check` often provides the best trade-
off between thoroughness of verification and limiting the impact on
application performance and availability.

`bt_index_parent_check(index regclass, heapallindexed boolean, rootdescend
boolean) returns void`

    

`bt_index_parent_check` tests that its target, a B-Tree index, respects a
variety of invariants. Optionally, when the _`heapallindexed`_ argument is
`true`, the function verifies the presence of all heap tuples that should be
found within the index. When the optional _`rootdescend`_ argument is `true`,
verification re-finds tuples on the leaf level by performing a new search from
the root page for each tuple. The checks that can be performed by
`bt_index_parent_check` are a superset of the checks that can be performed by
`bt_index_check`. `bt_index_parent_check` can be thought of as a more thorough
variant of `bt_index_check`: unlike `bt_index_check`, `bt_index_parent_check`
also checks invariants that span parent/child relationships, including
checking that there are no missing downlinks in the index structure.
`bt_index_parent_check` follows the general convention of raising an error if
it finds a logical inconsistency or other problem.

A `ShareLock` is required on the target index by `bt_index_parent_check` (a
`ShareLock` is also acquired on the heap relation). These locks prevent
concurrent data modification from `INSERT`, `UPDATE`, and `DELETE` commands.
The locks also prevent the underlying relation from being concurrently
processed by `VACUUM`, as well as all other utility commands. Note that the
function holds locks only while running, not for the entire transaction.

`bt_index_parent_check`'s additional verification is more likely to detect
various pathological cases. These cases may involve an incorrectly implemented
B-Tree operator class used by the index that is checked, or, hypothetically,
undiscovered bugs in the underlying B-Tree index access method code. Note that
`bt_index_parent_check` cannot be used when hot standby mode is enabled (i.e.,
on read-only physical replicas), unlike `bt_index_check`.

### Tip

`bt_index_check` and `bt_index_parent_check` both output log messages about
the verification process at `DEBUG1` and `DEBUG2` severity levels. These
messages provide detailed information about the verification process that may
be of interest to PostgreSQL developers. Advanced users may also find this
information helpful, since it provides additional context should verification
actually detect an inconsistency. Running:

    
    
    SET client_min_messages = DEBUG1;
    

in an interactive psql session before running a verification query will
display messages about the progress of verification with a manageable level of
detail.

`verify_heapam(relation regclass, on_error_stop boolean, check_toast boolean,
skip text, startblock bigint, endblock bigint, blkno OUT bigint, offnum OUT
integer, attnum OUT integer, msg OUT text) returns setof record`

    

Checks a table, sequence, or materialized view for structural corruption,
where pages in the relation contain data that is invalidly formatted, and for
logical corruption, where pages are structurally valid but inconsistent with
the rest of the database cluster.

The following optional arguments are recognized:

`on_error_stop`

    

If true, corruption checking stops at the end of the first block in which any
corruptions are found.

Defaults to false.

`check_toast`

    

If true, toasted values are checked against the target relation's TOAST table.

This option is known to be slow. Also, if the toast table or its index is
corrupt, checking it against toast values could conceivably crash the server,
although in many cases this would just produce an error.

Defaults to false.

`skip`

    

If not `none`, corruption checking skips blocks that are marked as all-visible
or all-frozen, as specified. Valid options are `all-visible`, `all-frozen` and
`none`.

Defaults to `none`.

`startblock`

    

If specified, corruption checking begins at the specified block, skipping all
previous blocks. It is an error to specify a _`startblock`_ outside the range
of blocks in the target table.

By default, checking begins at the first block.

`endblock`

    

If specified, corruption checking ends at the specified block, skipping all
remaining blocks. It is an error to specify an _`endblock`_ outside the range
of blocks in the target table.

By default, all blocks are checked.

For each corruption detected, `verify_heapam` returns a row with the following
columns:

`blkno`

    

The number of the block containing the corrupt page.

`offnum`

    

The OffsetNumber of the corrupt tuple.

`attnum`

    

The attribute number of the corrupt column in the tuple, if the corruption is
specific to a column and not the tuple as a whole.

`msg`

    

A message describing the problem detected.

### F.2.2. Optional _`heapallindexed`_ Verification #

When the _`heapallindexed`_ argument to B-Tree verification functions is
`true`, an additional phase of verification is performed against the table
associated with the target index relation. This consists of a “dummy” `CREATE
INDEX` operation, which checks for the presence of all hypothetical new index
tuples against a temporary, in-memory summarizing structure (this is built
when needed during the basic first phase of verification). The summarizing
structure “fingerprints” every tuple found within the target index. The high
level principle behind _`heapallindexed`_ verification is that a new index
that is equivalent to the existing, target index must only have entries that
can be found in the existing structure.

The additional _`heapallindexed`_ phase adds significant overhead:
verification will typically take several times longer. However, there is no
change to the relation-level locks acquired when _`heapallindexed`_
verification is performed.

The summarizing structure is bound in size by `maintenance_work_mem`. In order
to ensure that there is no more than a 2% probability of failure to detect an
inconsistency for each heap tuple that should be represented in the index,
approximately 2 bytes of memory are needed per tuple. As less memory is made
available per tuple, the probability of missing an inconsistency slowly
increases. This approach limits the overhead of verification significantly,
while only slightly reducing the probability of detecting a problem,
especially for installations where verification is treated as a routine
maintenance task. Any single absent or malformed tuple has a new opportunity
to be detected with each new verification attempt.

### F.2.3. Using `amcheck` Effectively #

`amcheck` can be effective at detecting various types of failure modes that
[data checksums](app-initdb.md#APP-INITDB-DATA-CHECKSUMS) will fail to
catch. These include:

  * Structural inconsistencies caused by incorrect operator class implementations.

This includes issues caused by the comparison rules of operating system
collations changing. Comparisons of datums of a collatable type like `text`
must be immutable (just as all comparisons used for B-Tree index scans must be
immutable), which implies that operating system collation rules must never
change. Though rare, updates to operating system collation rules can cause
these issues. More commonly, an inconsistency in the collation order between a
primary server and a standby server is implicated, possibly because the
_major_ operating system version in use is inconsistent. Such inconsistencies
will generally only arise on standby servers, and so can generally only be
detected on standby servers.

If a problem like this arises, it may not affect each individual index that is
ordered using an affected collation, simply because _indexed_ values might
happen to have the same absolute ordering regardless of the behavioral
inconsistency. See [Section 24.1](locale.md "24.1. Locale Support") and
[Section 24.2](collation.md "24.2. Collation Support") for further details
about how PostgreSQL uses operating system locales and collations.

  * Structural inconsistencies between indexes and the heap relations that are indexed (when _`heapallindexed`_ verification is performed).

There is no cross-checking of indexes against their heap relation during
normal operation. Symptoms of heap corruption can be subtle.

  * Corruption caused by hypothetical undiscovered bugs in the underlying PostgreSQL access method code, sort code, or transaction management code.

Automatic verification of the structural integrity of indexes plays a role in
the general testing of new or proposed PostgreSQL features that could
plausibly allow a logical inconsistency to be introduced. Verification of
table structure and associated visibility and transaction status information
plays a similar role. One obvious testing strategy is to call `amcheck`
functions continuously when running the standard regression tests. See
[Section 33.1](regress-run.md "33.1. Running the Tests") for details on
running the tests.

  * File system or storage subsystem faults where checksums happen to simply not be enabled.

Note that `amcheck` examines a page as represented in some shared memory
buffer at the time of verification if there is only a shared buffer hit when
accessing the block. Consequently, `amcheck` does not necessarily examine data
read from the file system at the time of verification. Note that when
checksums are enabled, `amcheck` may raise an error due to a checksum failure
when a corrupt block is read into a buffer.

  * Corruption caused by faulty RAM, or the broader memory subsystem.

PostgreSQL does not protect against correctable memory errors and it is
assumed you will operate using RAM that uses industry standard Error
Correcting Codes (ECC) or better protection. However, ECC memory is typically
only immune to single-bit errors, and should not be assumed to provide
_absolute_ protection against failures that result in memory corruption.

When _`heapallindexed`_ verification is performed, there is generally a
greatly increased chance of detecting single-bit errors, since strict binary
equality is tested, and the indexed attributes within the heap are tested.

Structural corruption can happen due to faulty storage hardware, or relation
files being overwritten or modified by unrelated software. This kind of
corruption can also be detected with [data page checksums](checksums.md
"30.2. Data Checksums").

Relation pages which are correctly formatted, internally consistent, and
correct relative to their own internal checksums may still contain logical
corruption. As such, this kind of corruption cannot be detected with
checksums. Examples include toasted values in the main table which lack a
corresponding entry in the toast table, and tuples in the main table with a
Transaction ID that is older than the oldest valid Transaction ID in the
database or cluster.

Multiple causes of logical corruption have been observed in production
systems, including bugs in the PostgreSQL server software, faulty and ill-
conceived backup and restore tools, and user error.

Corrupt relations are most concerning in live production environments,
precisely the same environments where high risk activities are least welcome.
For this reason, `verify_heapam` has been designed to diagnose corruption
without undue risk. It cannot guard against all causes of backend crashes, as
even executing the calling query could be unsafe on a badly corrupted system.
Access to [catalog tables](catalogs-overview.md "53.1. Overview") is
performed and could be problematic if the catalogs themselves are corrupted.

In general, `amcheck` can only prove the presence of corruption; it cannot
prove its absence.

### F.2.4. Repairing Corruption #

No error concerning corruption raised by `amcheck` should ever be a false
positive. `amcheck` raises errors in the event of conditions that, by
definition, should never happen, and so careful analysis of `amcheck` errors
is often required.

There is no general method of repairing problems that `amcheck` detects. An
explanation for the root cause of an invariant violation should be sought.
[pageinspect](pageinspect.md "F.25. pageinspect — low-level inspection of
database pages") may play a useful role in diagnosing corruption that
`amcheck` detects. A `REINDEX` may not be effective in repairing corruption.

* * *

[Prev](adminpack.md "F.1. adminpack — pgAdmin support toolpack")  | [Up](contrib.md "Appendix F. Additional Supplied Modules and Extensions") |  [Next](auth-delay.md "F.3. auth_delay — pause on authentication failure")  
---|---|---  
F.1. adminpack — pgAdmin support toolpack  | [Home](index.md "PostgreSQL 16.9 Documentation") |  F.3. auth_delay — pause on authentication failure  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/amcheck.md/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

