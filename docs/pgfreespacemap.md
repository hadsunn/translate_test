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

Supported Versions: [Current](/docs/current/pgfreespacemap.html "PostgreSQL 17
- F.29. pg_freespacemap — examine the free space map")
([17](/docs/17/pgfreespacemap.html "PostgreSQL 17 - F.29. pg_freespacemap —
examine the free space map")) / [16](/docs/16/pgfreespacemap.html "PostgreSQL
16 - F.29. pg_freespacemap — examine the free space map") /
[15](/docs/15/pgfreespacemap.html "PostgreSQL 15 - F.29. pg_freespacemap —
examine the free space map") / [14](/docs/14/pgfreespacemap.html "PostgreSQL
14 - F.29. pg_freespacemap — examine the free space map") /
[13](/docs/13/pgfreespacemap.html "PostgreSQL 13 - F.29. pg_freespacemap —
examine the free space map")

Development Versions: [18](/docs/18/pgfreespacemap.html "PostgreSQL 18 -
F.29. pg_freespacemap — examine the free space map") /
[devel](/docs/devel/pgfreespacemap.html "PostgreSQL devel -
F.29. pg_freespacemap — examine the free space map")

Unsupported versions: [12](/docs/12/pgfreespacemap.html "PostgreSQL 12 -
F.29. pg_freespacemap — examine the free space map") /
[11](/docs/11/pgfreespacemap.html "PostgreSQL 11 - F.29. pg_freespacemap —
examine the free space map") / [10](/docs/10/pgfreespacemap.html "PostgreSQL
10 - F.29. pg_freespacemap — examine the free space map") /
[9.6](/docs/9.6/pgfreespacemap.html "PostgreSQL 9.6 - F.29. pg_freespacemap —
examine the free space map") / [9.5](/docs/9.5/pgfreespacemap.html "PostgreSQL
9.5 - F.29. pg_freespacemap — examine the free space map") /
[9.4](/docs/9.4/pgfreespacemap.html "PostgreSQL 9.4 - F.29. pg_freespacemap —
examine the free space map") / [9.3](/docs/9.3/pgfreespacemap.html "PostgreSQL
9.3 - F.29. pg_freespacemap — examine the free space map") /
[9.2](/docs/9.2/pgfreespacemap.html "PostgreSQL 9.2 - F.29. pg_freespacemap —
examine the free space map") / [9.1](/docs/9.1/pgfreespacemap.html "PostgreSQL
9.1 - F.29. pg_freespacemap — examine the free space map") /
[9.0](/docs/9.0/pgfreespacemap.html "PostgreSQL 9.0 - F.29. pg_freespacemap —
examine the free space map") / [8.4](/docs/8.4/pgfreespacemap.html "PostgreSQL
8.4 - F.29. pg_freespacemap — examine the free space map") /
[8.3](/docs/8.3/pgfreespacemap.html "PostgreSQL 8.3 - F.29. pg_freespacemap —
examine the free space map")

__

F.29. pg_freespacemap — examine the free space map  
---  
[Prev](pgcrypto.html "F.28. pgcrypto — cryptographic functions")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgprewarm.html "F.30. pg_prewarm — preload relation data into buffer caches")  
  
* * *

## F.29. pg_freespacemap — examine the free space map #

[F.29.1. Functions](pgfreespacemap.html#PGFREESPACEMAP-FUNCS)

[F.29.2. Sample Output](pgfreespacemap.html#PGFREESPACEMAP-SAMPLE-OUTPUT)

[F.29.3. Author](pgfreespacemap.html#PGFREESPACEMAP-AUTHOR)

The `pg_freespacemap` module provides a means for examining the [free space
map](storage-fsm.html "73.3. Free Space Map") (FSM). It provides a function
called `pg_freespace`, or two overloaded functions, to be precise. The
functions show the value recorded in the free space map for a given page, or
for all pages in the relation.

By default use is restricted to superusers and roles with privileges of the
`pg_stat_scan_tables` role. Access may be granted to others using `GRANT`.

### F.29.1. Functions #

`pg_freespace(rel regclass IN, blkno bigint IN) returns int2`

    

Returns the amount of free space on the page of the relation, specified by
`blkno`, according to the FSM.

`pg_freespace(rel regclass IN, blkno OUT bigint, avail OUT int2)`

    

Displays the amount of free space on each page of the relation, according to
the FSM. A set of `(blkno bigint, avail int2)` tuples is returned, one tuple
for each page in the relation.

The values stored in the free space map are not exact. They're rounded to
precision of 1/256th of `BLCKSZ` (32 bytes with default `BLCKSZ`), and they're
not kept fully up-to-date as tuples are inserted and updated.

For indexes, what is tracked is entirely-unused pages, rather than free space
within pages. Therefore, the values are not meaningful, just whether a page is
in-use or empty.

### F.29.2. Sample Output #

    
    
    postgres=# SELECT * FROM pg_freespace('foo');
     blkno | avail
    -------+-------
         0 |     0
         1 |     0
         2 |     0
         3 |    32
         4 |   704
         5 |   704
         6 |   704
         7 |  1216
         8 |   704
         9 |   704
        10 |   704
        11 |   704
        12 |   704
        13 |   704
        14 |   704
        15 |   704
        16 |   704
        17 |   704
        18 |   704
        19 |  3648
    (20 rows)
    
    postgres=# SELECT * FROM pg_freespace('foo', 7);
     pg_freespace
    --------------
             1216
    (1 row)
    

### F.29.3. Author #

Original version by Mark Kirkwood
`<[markir@paradise.net.nz](mailto:markir@paradise.net.nz)>`. Rewritten in
version 8.4 to suit new FSM implementation by Heikki Linnakangas
`<[heikki@enterprisedb.com](mailto:heikki@enterprisedb.com)>`

* * *

[Prev](pgcrypto.html "F.28. pgcrypto — cryptographic functions")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pgprewarm.html "F.30. pg_prewarm — preload relation data into buffer caches")  
---|---|---  
F.28. pgcrypto — cryptographic functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.30. pg_prewarm — preload relation data into buffer caches  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgfreespacemap.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

