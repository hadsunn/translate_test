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

Supported Versions: [Current](/docs/current/storage-page-layout.html
"PostgreSQL 17 - 73.6. Database Page Layout") ([17](/docs/17/storage-page-
layout.html "PostgreSQL 17 - 73.6. Database Page Layout")) /
[16](/docs/16/storage-page-layout.html "PostgreSQL 16 - 73.6. Database Page
Layout") / [15](/docs/15/storage-page-layout.html "PostgreSQL 15 -
73.6. Database Page Layout") / [14](/docs/14/storage-page-layout.html
"PostgreSQL 14 - 73.6. Database Page Layout") / [13](/docs/13/storage-page-
layout.html "PostgreSQL 13 - 73.6. Database Page Layout")

Development Versions: [18](/docs/18/storage-page-layout.html "PostgreSQL 18 -
73.6. Database Page Layout") / [devel](/docs/devel/storage-page-layout.html
"PostgreSQL devel - 73.6. Database Page Layout")

Unsupported versions: [12](/docs/12/storage-page-layout.html "PostgreSQL 12 -
73.6. Database Page Layout") / [11](/docs/11/storage-page-layout.html
"PostgreSQL 11 - 73.6. Database Page Layout") / [10](/docs/10/storage-page-
layout.html "PostgreSQL 10 - 73.6. Database Page Layout") /
[9.6](/docs/9.6/storage-page-layout.html "PostgreSQL 9.6 - 73.6. Database Page
Layout") / [9.5](/docs/9.5/storage-page-layout.html "PostgreSQL 9.5 -
73.6. Database Page Layout") / [9.4](/docs/9.4/storage-page-layout.html
"PostgreSQL 9.4 - 73.6. Database Page Layout") / [9.3](/docs/9.3/storage-page-
layout.html "PostgreSQL 9.3 - 73.6. Database Page Layout") /
[9.2](/docs/9.2/storage-page-layout.html "PostgreSQL 9.2 - 73.6. Database Page
Layout") / [9.1](/docs/9.1/storage-page-layout.html "PostgreSQL 9.1 -
73.6. Database Page Layout") / [9.0](/docs/9.0/storage-page-layout.html
"PostgreSQL 9.0 - 73.6. Database Page Layout") / [8.4](/docs/8.4/storage-page-
layout.html "PostgreSQL 8.4 - 73.6. Database Page Layout") /
[8.3](/docs/8.3/storage-page-layout.html "PostgreSQL 8.3 - 73.6. Database Page
Layout") / [8.2](/docs/8.2/storage-page-layout.html "PostgreSQL 8.2 -
73.6. Database Page Layout") / [8.1](/docs/8.1/storage-page-layout.html
"PostgreSQL 8.1 - 73.6. Database Page Layout") / [8.0](/docs/8.0/storage-page-
layout.html "PostgreSQL 8.0 - 73.6. Database Page Layout")

__

73.6. Database Page Layout  
---  
[Prev](storage-init.html "73.5. The Initialization Fork")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage-hot.html "73.7. Heap-Only Tuples \(HOT\)")  
  
* * *

## 73.6. Database Page Layout #

[73.6.1. Table Row Layout](storage-page-layout.html#STORAGE-TUPLE-LAYOUT)

This section provides an overview of the page format used within PostgreSQL
tables and indexes.[17] Sequences and TOAST tables are formatted just like a
regular table.

In the following explanation, a _byte_ is assumed to contain 8 bits. In
addition, the term _item_ refers to an individual data value that is stored on
a page. In a table, an item is a row; in an index, an item is an index entry.

Every table and index is stored as an array of _pages_ of a fixed size
(usually 8 kB, although a different page size can be selected when compiling
the server). In a table, all the pages are logically equivalent, so a
particular item (row) can be stored in any page. In indexes, the first page is
generally reserved as a _metapage_ holding control information, and there can
be different types of pages within the index, depending on the index access
method.

[Table 73.2](storage-page-layout.html#PAGE-TABLE "Table 73.2. Overall Page
Layout") shows the overall layout of a page. There are five parts to each
page.

**Table  73.2. Overall Page Layout**

Item | Description  
---|---  
PageHeaderData | 24 bytes long. Contains general information about the page, including free space pointers.  
ItemIdData | Array of item identifiers pointing to the actual items. Each entry is an (offset,length) pair. 4 bytes per item.  
Free space | The unallocated space. New item identifiers are allocated from the start of this area, new items from the end.  
Items | The actual items themselves.  
Special space | Index access method specific data. Different methods store different data. Empty in ordinary tables.  
  
  

The first 24 bytes of each page consists of a page header (`PageHeaderData`).
Its format is detailed in [Table 73.3](storage-page-
layout.html#PAGEHEADERDATA-TABLE "Table 73.3. PageHeaderData Layout"). The
first field tracks the most recent WAL entry related to this page. The second
field contains the page checksum if [data checksums](app-initdb.html#APP-
INITDB-DATA-CHECKSUMS) are enabled. Next is a 2-byte field containing flag
bits. This is followed by three 2-byte integer fields (`pd_lower`, `pd_upper`,
and `pd_special`). These contain byte offsets from the page start to the start
of unallocated space, to the end of unallocated space, and to the start of the
special space. The next 2 bytes of the page header, `pd_pagesize_version`,
store both the page size and a version indicator. Beginning with PostgreSQL
8.3 the version number is 4; PostgreSQL 8.1 and 8.2 used version number 3;
PostgreSQL 8.0 used version number 2; PostgreSQL 7.3 and 7.4 used version
number 1; prior releases used version number 0. (The basic page layout and
header format has not changed in most of these versions, but the layout of
heap row headers has.) The page size is basically only present as a cross-
check; there is no support for having more than one page size in an
installation. The last field is a hint that shows whether pruning the page is
likely to be profitable: it tracks the oldest un-pruned XMAX on the page.

**Table  73.3. PageHeaderData Layout**

Field | Type | Length | Description  
---|---|---|---  
pd_lsn | PageXLogRecPtr | 8 bytes | LSN: next byte after last byte of WAL record for last change to this page  
pd_checksum | uint16 | 2 bytes | Page checksum  
pd_flags | uint16 | 2 bytes | Flag bits  
pd_lower | LocationIndex | 2 bytes | Offset to start of free space  
pd_upper | LocationIndex | 2 bytes | Offset to end of free space  
pd_special | LocationIndex | 2 bytes | Offset to start of special space  
pd_pagesize_version | uint16 | 2 bytes | Page size and layout version number information  
pd_prune_xid | TransactionId | 4 bytes | Oldest unpruned XMAX on page, or zero if none  
  
  

All the details can be found in `src/include/storage/bufpage.h`.

Following the page header are item identifiers (`ItemIdData`), each requiring
four bytes. An item identifier contains a byte-offset to the start of an item,
its length in bytes, and a few attribute bits which affect its interpretation.
New item identifiers are allocated as needed from the beginning of the
unallocated space. The number of item identifiers present can be determined by
looking at `pd_lower`, which is increased to allocate a new identifier.
Because an item identifier is never moved until it is freed, its index can be
used on a long-term basis to reference an item, even when the item itself is
moved around on the page to compact free space. In fact, every pointer to an
item (`ItemPointer`, also known as `CTID`) created by PostgreSQL consists of a
page number and the index of an item identifier.

The items themselves are stored in space allocated backwards from the end of
unallocated space. The exact structure varies depending on what the table is
to contain. Tables and sequences both use a structure named
`HeapTupleHeaderData`, described below.

The final section is the “special section” which can contain anything the
access method wishes to store. For example, b-tree indexes store links to the
page's left and right siblings, as well as some other data relevant to the
index structure. Ordinary tables do not use a special section at all
(indicated by setting `pd_special` to equal the page size).

[Figure 73.1](storage-page-layout.html#STORAGE-PAGE-LAYOUT-FIGURE
"Figure 73.1. Page Layout") illustrates how these parts are laid out in a
page.

**Figure  73.1. Page Layout**

  

### 73.6.1. Table Row Layout #

All table rows are structured in the same way. There is a fixed-size header
(occupying 23 bytes on most machines), followed by an optional null bitmap, an
optional object ID field, and the user data. The header is detailed in [Table
73.4](storage-page-layout.html#HEAPTUPLEHEADERDATA-TABLE
"Table 73.4. HeapTupleHeaderData Layout"). The actual user data (columns of
the row) begins at the offset indicated by `t_hoff`, which must always be a
multiple of the MAXALIGN distance for the platform. The null bitmap is only
present if the _HEAP_HASNULL_ bit is set in `t_infomask`. If it is present it
begins just after the fixed header and occupies enough bytes to have one bit
per data column (that is, the number of bits that equals the attribute count
in `t_infomask2`). In this list of bits, a 1 bit indicates not-null, a 0 bit
is a null. When the bitmap is not present, all columns are assumed not-null.
The object ID is only present if the _HEAP_HASOID_OLD_ bit is set in
`t_infomask`. If present, it appears just before the `t_hoff` boundary. Any
padding needed to make `t_hoff` a MAXALIGN multiple will appear between the
null bitmap and the object ID. (This in turn ensures that the object ID is
suitably aligned.)

**Table  73.4. HeapTupleHeaderData Layout**

Field | Type | Length | Description  
---|---|---|---  
t_xmin | TransactionId | 4 bytes | insert XID stamp  
t_xmax | TransactionId | 4 bytes | delete XID stamp  
t_cid | CommandId | 4 bytes | insert and/or delete CID stamp (overlays with t_xvac)  
t_xvac | TransactionId | 4 bytes | XID for VACUUM operation moving a row version  
t_ctid | ItemPointerData | 6 bytes | current TID of this or newer row version  
t_infomask2 | uint16 | 2 bytes | number of attributes, plus various flag bits  
t_infomask | uint16 | 2 bytes | various flag bits  
t_hoff | uint8 | 1 byte | offset to user data  
  
  

All the details can be found in `src/include/access/htup_details.h`.

Interpreting the actual data can only be done with information obtained from
other tables, mostly `pg_attribute`. The key values needed to identify field
locations are `attlen` and `attalign`. There is no way to directly get a
particular attribute, except when there are only fixed width fields and no
null values. All this trickery is wrapped up in the functions _heap_getattr_ ,
_fastgetattr_ and _heap_getsysattr_.

To read the data you need to examine each attribute in turn. First check
whether the field is NULL according to the null bitmap. If it is, go to the
next. Then make sure you have the right alignment. If the field is a fixed
width field, then all the bytes are simply placed. If it's a variable length
field (attlen = -1) then it's a bit more complicated. All variable-length data
types share the common header structure `struct varlena`, which includes the
total length of the stored value and some flag bits. Depending on the flags,
the data can be either inline or in a TOAST table; it might be compressed, too
(see [Section 73.2](storage-toast.html "73.2. TOAST")).

  

* * *

[17] Actually, use of this page format is not required for either table or
index access methods. The `heap` table access method always uses this format.
All the existing index methods also use the basic format, but the data kept on
index metapages usually doesn't follow the item layout rules.

* * *

[Prev](storage-init.html "73.5. The Initialization Fork")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](storage-hot.html "73.7. Heap-Only Tuples \(HOT\)")  
---|---|---  
73.5. The Initialization Fork  | [Home](index.html "PostgreSQL 16.9 Documentation") |  73.7. Heap-Only Tuples (HOT)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-page-layout.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

