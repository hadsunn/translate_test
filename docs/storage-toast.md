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

Supported Versions: [Current](/docs/current/storage-toast.html "PostgreSQL 17
- 73.2. TOAST") ([17](/docs/17/storage-toast.html "PostgreSQL 17 -
73.2. TOAST")) / [16](/docs/16/storage-toast.html "PostgreSQL 16 -
73.2. TOAST") / [15](/docs/15/storage-toast.html "PostgreSQL 15 -
73.2. TOAST") / [14](/docs/14/storage-toast.html "PostgreSQL 14 -
73.2. TOAST") / [13](/docs/13/storage-toast.html "PostgreSQL 13 -
73.2. TOAST")

Development Versions: [18](/docs/18/storage-toast.html "PostgreSQL 18 -
73.2. TOAST") / [devel](/docs/devel/storage-toast.html "PostgreSQL devel -
73.2. TOAST")

Unsupported versions: [12](/docs/12/storage-toast.html "PostgreSQL 12 -
73.2. TOAST") / [11](/docs/11/storage-toast.html "PostgreSQL 11 -
73.2. TOAST") / [10](/docs/10/storage-toast.html "PostgreSQL 10 -
73.2. TOAST") / [9.6](/docs/9.6/storage-toast.html "PostgreSQL 9.6 -
73.2. TOAST") / [9.5](/docs/9.5/storage-toast.html "PostgreSQL 9.5 -
73.2. TOAST") / [9.4](/docs/9.4/storage-toast.html "PostgreSQL 9.4 -
73.2. TOAST") / [9.3](/docs/9.3/storage-toast.html "PostgreSQL 9.3 -
73.2. TOAST") / [9.2](/docs/9.2/storage-toast.html "PostgreSQL 9.2 -
73.2. TOAST") / [9.1](/docs/9.1/storage-toast.html "PostgreSQL 9.1 -
73.2. TOAST") / [9.0](/docs/9.0/storage-toast.html "PostgreSQL 9.0 -
73.2. TOAST") / [8.4](/docs/8.4/storage-toast.html "PostgreSQL 8.4 -
73.2. TOAST") / [8.3](/docs/8.3/storage-toast.html "PostgreSQL 8.3 -
73.2. TOAST") / [8.2](/docs/8.2/storage-toast.html "PostgreSQL 8.2 -
73.2. TOAST") / [8.1](/docs/8.1/storage-toast.html "PostgreSQL 8.1 -
73.2. TOAST") / [8.0](/docs/8.0/storage-toast.html "PostgreSQL 8.0 -
73.2. TOAST")

__

73.2. TOAST  
---  
[Prev](storage-file-layout.html "73.1. Database File Layout")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage-fsm.html "73.3. Free Space Map")  
  
* * *

## 73.2. TOAST #

[73.2.1. Out-of-Line, On-Disk TOAST Storage](storage-toast.html#STORAGE-TOAST-
ONDISK)

[73.2.2. Out-of-Line, In-Memory TOAST Storage](storage-toast.html#STORAGE-
TOAST-INMEMORY)

This section provides an overview of TOAST (The Oversized-Attribute Storage
Technique).

PostgreSQL uses a fixed page size (commonly 8 kB), and does not allow tuples
to span multiple pages. Therefore, it is not possible to store very large
field values directly. To overcome this limitation, large field values are
compressed and/or broken up into multiple physical rows. This happens
transparently to the user, with only small impact on most of the backend code.
The technique is affectionately known as TOAST (or “the best thing since
sliced bread”). The TOAST infrastructure is also used to improve handling of
large data values in-memory.

Only certain data types support TOAST — there is no need to impose the
overhead on data types that cannot produce large field values. To support
TOAST, a data type must have a variable-length (_varlena_) representation, in
which, ordinarily, the first four-byte word of any stored value contains the
total length of the value in bytes (including itself). TOAST does not
constrain the rest of the data type's representation. The special
representations collectively called _TOAST ed values_ work by modifying or
reinterpreting this initial length word. Therefore, the C-level functions
supporting a TOAST-able data type must be careful about how they handle
potentially TOASTed input values: an input might not actually consist of a
four-byte length word and contents until after it's been _detoasted_. (This is
normally done by invoking `PG_DETOAST_DATUM` before doing anything with an
input value, but in some cases more efficient approaches are possible. See
[Section 38.13.1](xtypes.html#XTYPES-TOAST "38.13.1. TOAST Considerations")
for more detail.)

TOAST usurps two bits of the varlena length word (the high-order bits on big-
endian machines, the low-order bits on little-endian machines), thereby
limiting the logical size of any value of a TOAST-able data type to 1 GB (230
\- 1 bytes). When both bits are zero, the value is an ordinary un-TOASTed
value of the data type, and the remaining bits of the length word give the
total datum size (including length word) in bytes. When the highest-order or
lowest-order bit is set, the value has only a single-byte header instead of
the normal four-byte header, and the remaining bits of that byte give the
total datum size (including length byte) in bytes. This alternative supports
space-efficient storage of values shorter than 127 bytes, while still allowing
the data type to grow to 1 GB at need. Values with single-byte headers aren't
aligned on any particular boundary, whereas values with four-byte headers are
aligned on at least a four-byte boundary; this omission of alignment padding
provides additional space savings that is significant compared to short
values. As a special case, if the remaining bits of a single-byte header are
all zero (which would be impossible for a self-inclusive length), the value is
a pointer to out-of-line data, with several possible alternatives as described
below. The type and size of such a _TOAST pointer_ are determined by a code
stored in the second byte of the datum. Lastly, when the highest-order or
lowest-order bit is clear but the adjacent bit is set, the content of the
datum has been compressed and must be decompressed before use. In this case
the remaining bits of the four-byte length word give the total size of the
compressed datum, not the original data. Note that compression is also
possible for out-of-line data but the varlena header does not tell whether it
has occurred — the content of the TOAST pointer tells that, instead.

The compression technique used for either in-line or out-of-line compressed
data can be selected for each column by setting the `COMPRESSION` column
option in `CREATE TABLE` or `ALTER TABLE`. The default for columns with no
explicit setting is to consult the [default_toast_compression](runtime-config-
client.html#GUC-DEFAULT-TOAST-COMPRESSION) parameter at the time data is
inserted.

As mentioned, there are multiple types of TOAST pointer datums. The oldest and
most common type is a pointer to out-of-line data stored in a _TOAST table_
that is separate from, but associated with, the table containing the TOAST
pointer datum itself. These _on-disk_ pointer datums are created by the TOAST
management code (in `access/common/toast_internals.c`) when a tuple to be
stored on disk is too large to be stored as-is. Further details appear in
[Section 73.2.1](storage-toast.html#STORAGE-TOAST-ONDISK "73.2.1. Out-of-Line,
On-Disk TOAST Storage"). Alternatively, a TOAST pointer datum can contain a
pointer to out-of-line data that appears elsewhere in memory. Such datums are
necessarily short-lived, and will never appear on-disk, but they are very
useful for avoiding copying and redundant processing of large data values.
Further details appear in [Section 73.2.2](storage-toast.html#STORAGE-TOAST-
INMEMORY "73.2.2. Out-of-Line, In-Memory TOAST Storage").

### 73.2.1. Out-of-Line, On-Disk TOAST Storage #

If any of the columns of a table are TOAST-able, the table will have an
associated TOAST table, whose OID is stored in the table's
`pg_class`.`reltoastrelid` entry. On-disk TOASTed values are kept in the TOAST
table, as described in more detail below.

Out-of-line values are divided (after compression if used) into chunks of at
most `TOAST_MAX_CHUNK_SIZE` bytes (by default this value is chosen so that
four chunk rows will fit on a page, making it about 2000 bytes). Each chunk is
stored as a separate row in the TOAST table belonging to the owning table.
Every TOAST table has the columns `chunk_id` (an OID identifying the
particular TOASTed value), `chunk_seq` (a sequence number for the chunk within
its value), and `chunk_data` (the actual data of the chunk). A unique index on
`chunk_id` and `chunk_seq` provides fast retrieval of the values. A pointer
datum representing an out-of-line on-disk TOASTed value therefore needs to
store the OID of the TOAST table in which to look and the OID of the specific
value (its `chunk_id`). For convenience, pointer datums also store the logical
datum size (original uncompressed data length), physical stored size
(different if compression was applied), and the compression method used, if
any. Allowing for the varlena header bytes, the total size of an on-disk TOAST
pointer datum is therefore 18 bytes regardless of the actual size of the
represented value.

The TOAST management code is triggered only when a row value to be stored in a
table is wider than `TOAST_TUPLE_THRESHOLD` bytes (normally 2 kB). The TOAST
code will compress and/or move field values out-of-line until the row value is
shorter than `TOAST_TUPLE_TARGET` bytes (also normally 2 kB, adjustable) or no
more gains can be had. During an UPDATE operation, values of unchanged fields
are normally preserved as-is; so an UPDATE of a row with out-of-line values
incurs no TOAST costs if none of the out-of-line values change.

The TOAST management code recognizes four different strategies for storing
TOAST-able columns on disk:

  * `PLAIN` prevents either compression or out-of-line storage. This is the only possible strategy for columns of non-TOAST-able data types.

  * `EXTENDED` allows both compression and out-of-line storage. This is the default for most TOAST-able data types. Compression will be attempted first, then out-of-line storage if the row is still too big.

  * `EXTERNAL` allows out-of-line storage but not compression. Use of `EXTERNAL` will make substring operations on wide `text` and `bytea` columns faster (at the penalty of increased storage space) because these operations are optimized to fetch only the required parts of the out-of-line value when it is not compressed.

  * `MAIN` allows compression but not out-of-line storage. (Actually, out-of-line storage will still be performed for such columns, but only as a last resort when there is no other way to make the row small enough to fit on a page.)

Each TOAST-able data type specifies a default strategy for columns of that
data type, but the strategy for a given table column can be altered with
[`ALTER TABLE ... SET STORAGE`](sql-altertable.html "ALTER TABLE").

`TOAST_TUPLE_TARGET` can be adjusted for each table using [`ALTER TABLE ...
SET (toast_tuple_target = N)`](sql-altertable.html "ALTER TABLE")

This scheme has a number of advantages compared to a more straightforward
approach such as allowing row values to span pages. Assuming that queries are
usually qualified by comparisons against relatively small key values, most of
the work of the executor will be done using the main row entry. The big values
of TOASTed attributes will only be pulled out (if selected at all) at the time
the result set is sent to the client. Thus, the main table is much smaller and
more of its rows fit in the shared buffer cache than would be the case without
any out-of-line storage. Sort sets shrink also, and sorts will more often be
done entirely in memory. A little test showed that a table containing typical
HTML pages and their URLs was stored in about half of the raw data size
including the TOAST table, and that the main table contained only about 10% of
the entire data (the URLs and some small HTML pages). There was no run time
difference compared to an un-TOASTed comparison table, in which all the HTML
pages were cut down to 7 kB to fit.

### 73.2.2. Out-of-Line, In-Memory TOAST Storage #

TOAST pointers can point to data that is not on disk, but is elsewhere in the
memory of the current server process. Such pointers obviously cannot be long-
lived, but they are nonetheless useful. There are currently two sub-cases:
pointers to _indirect_ data and pointers to _expanded_ data.

Indirect TOAST pointers simply point at a non-indirect varlena value stored
somewhere in memory. This case was originally created merely as a proof of
concept, but it is currently used during logical decoding to avoid possibly
having to create physical tuples exceeding 1 GB (as pulling all out-of-line
field values into the tuple might do). The case is of limited use since the
creator of the pointer datum is entirely responsible that the referenced data
survives for as long as the pointer could exist, and there is no
infrastructure to help with this.

Expanded TOAST pointers are useful for complex data types whose on-disk
representation is not especially suited for computational purposes. As an
example, the standard varlena representation of a PostgreSQL array includes
dimensionality information, a nulls bitmap if there are any null elements,
then the values of all the elements in order. When the element type itself is
variable-length, the only way to find the _`N`_ 'th element is to scan through
all the preceding elements. This representation is appropriate for on-disk
storage because of its compactness, but for computations with the array it's
much nicer to have an “expanded” or “deconstructed” representation in which
all the element starting locations have been identified. The TOAST pointer
mechanism supports this need by allowing a pass-by-reference Datum to point to
either a standard varlena value (the on-disk representation) or a TOAST
pointer that points to an expanded representation somewhere in memory. The
details of this expanded representation are up to the data type, though it
must have a standard header and meet the other API requirements given in
`src/include/utils/expandeddatum.h`. C-level functions working with the data
type can choose to handle either representation. Functions that do not know
about the expanded representation, but simply apply `PG_DETOAST_DATUM` to
their inputs, will automatically receive the traditional varlena
representation; so support for an expanded representation can be introduced
incrementally, one function at a time.

TOAST pointers to expanded values are further broken down into _read-write_
and _read-only_ pointers. The pointed-to representation is the same either
way, but a function that receives a read-write pointer is allowed to modify
the referenced value in-place, whereas one that receives a read-only pointer
must not; it must first create a copy if it wants to make a modified version
of the value. This distinction and some associated conventions make it
possible to avoid unnecessary copying of expanded values during query
execution.

For all types of in-memory TOAST pointer, the TOAST management code ensures
that no such pointer datum can accidentally get stored on disk. In-memory
TOAST pointers are automatically expanded to normal in-line varlena values
before storage — and then possibly converted to on-disk TOAST pointers, if the
containing tuple would otherwise be too big.

* * *

[Prev](storage-file-layout.html "73.1. Database File Layout")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](storage-fsm.html "73.3. Free Space Map")  
---|---|---  
73.1. Database File Layout  | [Home](index.html "PostgreSQL 16.9 Documentation") |  73.3. Free Space Map  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-toast.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

