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

Supported Versions: [Current](/docs/current/view-pg-shmem-allocations.html
"PostgreSQL 17 - 54.26. pg_shmem_allocations") ([17](/docs/17/view-pg-shmem-
allocations.html "PostgreSQL 17 - 54.26. pg_shmem_allocations")) /
[16](/docs/16/view-pg-shmem-allocations.html "PostgreSQL 16 -
54.26. pg_shmem_allocations") / [15](/docs/15/view-pg-shmem-allocations.html
"PostgreSQL 15 - 54.26. pg_shmem_allocations") / [14](/docs/14/view-pg-shmem-
allocations.html "PostgreSQL 14 - 54.26. pg_shmem_allocations") /
[13](/docs/13/view-pg-shmem-allocations.html "PostgreSQL 13 -
54.26. pg_shmem_allocations")

Development Versions: [18](/docs/18/view-pg-shmem-allocations.html "PostgreSQL
18 - 54.26. pg_shmem_allocations") / [devel](/docs/devel/view-pg-shmem-
allocations.html "PostgreSQL devel - 54.26. pg_shmem_allocations")

__

54.26. `pg_shmem_allocations`  
---  
[Prev](view-pg-shadow.html "54.25. pg_shadow")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-stats.html "54.27. pg_stats")  
  
* * *

## 54.26. `pg_shmem_allocations` #

The `pg_shmem_allocations` view shows allocations made from the server's main
shared memory segment. This includes both memory allocated by PostgreSQL
itself and memory allocated by extensions using the mechanisms detailed in
[Section 38.10.10](xfunc-c.html#XFUNC-SHARED-ADDIN "38.10.10. Shared Memory
and LWLocks").

Note that this view does not include memory allocated using the dynamic shared
memory infrastructure.

**Table  54.26. `pg_shmem_allocations` Columns**

Column Type Description  
---  
`name` `text` The name of the shared memory allocation. NULL for unused memory
and `<anonymous>` for anonymous allocations.  
`off` `int8` The offset at which the allocation starts. NULL for anonymous
allocations, since details related to them are not known.  
`size` `int8` Size of the allocation in bytes  
`allocated_size` `int8` Size of the allocation in bytes including padding. For
anonymous allocations, no information about padding is available, so the
`size` and `allocated_size` columns will always be equal. Padding is not
meaningful for free memory, so the columns will be equal in that case also.  
  
  

Anonymous allocations are allocations that have been made with `ShmemAlloc()`
directly, rather than via `ShmemInitStruct()` or `ShmemInitHash()`.

By default, the `pg_shmem_allocations` view can be read only by superusers or
roles with privileges of the `pg_read_all_stats` role.

* * *

[Prev](view-pg-shadow.html "54.25. pg_shadow")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-stats.html "54.27. pg_stats")  
---|---|---  
54.25. `pg_shadow`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.27. `pg_stats`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-shmem-
allocations.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

