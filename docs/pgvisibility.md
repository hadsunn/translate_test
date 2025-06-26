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

Supported Versions: [Current](/docs/current/pgvisibility.html "PostgreSQL 17 -
F.36. pg_visibility — visibility map information and utilities")
([17](/docs/17/pgvisibility.html "PostgreSQL 17 - F.36. pg_visibility —
visibility map information and utilities")) / [16](/docs/16/pgvisibility.html
"PostgreSQL 16 - F.36. pg_visibility — visibility map information and
utilities") / [15](/docs/15/pgvisibility.html "PostgreSQL 15 -
F.36. pg_visibility — visibility map information and utilities") /
[14](/docs/14/pgvisibility.html "PostgreSQL 14 - F.36. pg_visibility —
visibility map information and utilities") / [13](/docs/13/pgvisibility.html
"PostgreSQL 13 - F.36. pg_visibility — visibility map information and
utilities")

Development Versions: [18](/docs/18/pgvisibility.html "PostgreSQL 18 -
F.36. pg_visibility — visibility map information and utilities") /
[devel](/docs/devel/pgvisibility.html "PostgreSQL devel - F.36. pg_visibility
— visibility map information and utilities")

Unsupported versions: [12](/docs/12/pgvisibility.html "PostgreSQL 12 -
F.36. pg_visibility — visibility map information and utilities") /
[11](/docs/11/pgvisibility.html "PostgreSQL 11 - F.36. pg_visibility —
visibility map information and utilities") / [10](/docs/10/pgvisibility.html
"PostgreSQL 10 - F.36. pg_visibility — visibility map information and
utilities") / [9.6](/docs/9.6/pgvisibility.html "PostgreSQL 9.6 -
F.36. pg_visibility — visibility map information and utilities")

__

F.36. pg_visibility — visibility map information and utilities  
---  
[Prev](pgtrgm.html "F.35. pg_trgm —  support for similarity of text using trigram matching")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgwalinspect.html "F.37. pg_walinspect — low-level WAL inspection")  
  
* * *

## F.36. pg_visibility — visibility map information and utilities #

[F.36.1. Functions](pgvisibility.html#PGVISIBILITY-FUNCS)

[F.36.2. Author](pgvisibility.html#PGVISIBILITY-AUTHOR)

The `pg_visibility` module provides a means for examining the visibility map
(VM) and page-level visibility information of a table. It also provides
functions to check the integrity of a visibility map and to force it to be
rebuilt.

Three different bits are used to store information about page-level
visibility. The all-visible bit in the visibility map indicates that every
tuple in the corresponding page of the relation is visible to every current
and future transaction. The all-frozen bit in the visibility map indicates
that every tuple in the page is frozen; that is, no future vacuum will need to
modify the page until such time as a tuple is inserted, updated, deleted, or
locked on that page. The page header's `PD_ALL_VISIBLE` bit has the same
meaning as the all-visible bit in the visibility map, but is stored within the
data page itself rather than in a separate data structure. These two bits will
normally agree, but the page's all-visible bit can sometimes be set while the
visibility map bit is clear after a crash recovery. The reported values can
also disagree because of a change that occurs after `pg_visibility` examines
the visibility map and before it examines the data page. Any event that causes
data corruption can also cause these bits to disagree.

Functions that display information about `PD_ALL_VISIBLE` bits are much more
costly than those that only consult the visibility map, because they must read
the relation's data blocks rather than only the (much smaller) visibility map.
Functions that check the relation's data blocks are similarly expensive.

### F.36.1. Functions #

`pg_visibility_map(relation regclass, blkno bigint, all_visible OUT boolean,
all_frozen OUT boolean) returns record`

    

Returns the all-visible and all-frozen bits in the visibility map for the
given block of the given relation.

`pg_visibility(relation regclass, blkno bigint, all_visible OUT boolean,
all_frozen OUT boolean, pd_all_visible OUT boolean) returns record`

    

Returns the all-visible and all-frozen bits in the visibility map for the
given block of the given relation, plus the `PD_ALL_VISIBLE` bit of that
block.

`pg_visibility_map(relation regclass, blkno OUT bigint, all_visible OUT
boolean, all_frozen OUT boolean) returns setof record`

    

Returns the all-visible and all-frozen bits in the visibility map for each
block of the given relation.

`pg_visibility(relation regclass, blkno OUT bigint, all_visible OUT boolean,
all_frozen OUT boolean, pd_all_visible OUT boolean) returns setof record`

    

Returns the all-visible and all-frozen bits in the visibility map for each
block of the given relation, plus the `PD_ALL_VISIBLE` bit of each block.

`pg_visibility_map_summary(relation regclass, all_visible OUT bigint,
all_frozen OUT bigint) returns record`

    

Returns the number of all-visible pages and the number of all-frozen pages in
the relation according to the visibility map.

`pg_check_frozen(relation regclass, t_ctid OUT tid) returns setof tid`

    

Returns the TIDs of non-frozen tuples stored in pages marked all-frozen in the
visibility map. If this function returns a non-empty set of TIDs, the
visibility map is corrupt.

`pg_check_visible(relation regclass, t_ctid OUT tid) returns setof tid`

    

Returns the TIDs of non-all-visible tuples stored in pages marked all-visible
in the visibility map. If this function returns a non-empty set of TIDs, the
visibility map is corrupt.

`pg_truncate_visibility_map(relation regclass) returns void`

    

Truncates the visibility map for the given relation. This function is useful
if you believe that the visibility map for the relation is corrupt and wish to
force rebuilding it. The first `VACUUM` executed on the given relation after
this function is executed will scan every page in the relation and rebuild the
visibility map. (Until that is done, queries will treat the visibility map as
containing all zeroes.)

By default, these functions are executable only by superusers and roles with
privileges of the `pg_stat_scan_tables` role, with the exception of
`pg_truncate_visibility_map(relation regclass)` which can only be executed by
superusers.

### F.36.2. Author #

Robert Haas `<[rhaas@postgresql.org](mailto:rhaas@postgresql.org)>`

* * *

[Prev](pgtrgm.html "F.35. pg_trgm —  support for similarity of text using trigram matching")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pgwalinspect.html "F.37. pg_walinspect — low-level WAL inspection")  
---|---|---  
F.35. pg_trgm — support for similarity of text using trigram matching  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.37. pg_walinspect — low-level WAL inspection  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgvisibility.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

