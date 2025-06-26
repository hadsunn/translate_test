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

Supported Versions: [Current](/docs/current/storage-fsm.html "PostgreSQL 17 -
73.3. Free Space Map") ([17](/docs/17/storage-fsm.html "PostgreSQL 17 -
73.3. Free Space Map")) / [16](/docs/16/storage-fsm.html "PostgreSQL 16 -
73.3. Free Space Map") / [15](/docs/15/storage-fsm.html "PostgreSQL 15 -
73.3. Free Space Map") / [14](/docs/14/storage-fsm.html "PostgreSQL 14 -
73.3. Free Space Map") / [13](/docs/13/storage-fsm.html "PostgreSQL 13 -
73.3. Free Space Map")

Development Versions: [18](/docs/18/storage-fsm.html "PostgreSQL 18 -
73.3. Free Space Map") / [devel](/docs/devel/storage-fsm.html "PostgreSQL
devel - 73.3. Free Space Map")

Unsupported versions: [12](/docs/12/storage-fsm.html "PostgreSQL 12 -
73.3. Free Space Map") / [11](/docs/11/storage-fsm.html "PostgreSQL 11 -
73.3. Free Space Map") / [10](/docs/10/storage-fsm.html "PostgreSQL 10 -
73.3. Free Space Map") / [9.6](/docs/9.6/storage-fsm.html "PostgreSQL 9.6 -
73.3. Free Space Map") / [9.5](/docs/9.5/storage-fsm.html "PostgreSQL 9.5 -
73.3. Free Space Map") / [9.4](/docs/9.4/storage-fsm.html "PostgreSQL 9.4 -
73.3. Free Space Map") / [9.3](/docs/9.3/storage-fsm.html "PostgreSQL 9.3 -
73.3. Free Space Map") / [9.2](/docs/9.2/storage-fsm.html "PostgreSQL 9.2 -
73.3. Free Space Map") / [9.1](/docs/9.1/storage-fsm.html "PostgreSQL 9.1 -
73.3. Free Space Map") / [9.0](/docs/9.0/storage-fsm.html "PostgreSQL 9.0 -
73.3. Free Space Map") / [8.4](/docs/8.4/storage-fsm.html "PostgreSQL 8.4 -
73.3. Free Space Map")

__

73.3. Free Space Map  
---  
[Prev](storage-toast.html "73.2. TOAST")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage-vm.html "73.4. Visibility Map")  
  
* * *

## 73.3. Free Space Map #

Each heap and index relation, except for hash indexes, has a Free Space Map
(FSM) to keep track of available space in the relation. It's stored alongside
the main relation data in a separate relation fork, named after the filenode
number of the relation, plus a `_fsm` suffix. For example, if the filenode of
a relation is 12345, the FSM is stored in a file called `12345_fsm`, in the
same directory as the main relation file.

The Free Space Map is organized as a tree of FSM pages. The bottom level FSM
pages store the free space available on each heap (or index) page, using one
byte to represent each such page. The upper levels aggregate information from
the lower levels.

Within each FSM page is a binary tree, stored in an array with one byte per
node. Each leaf node represents a heap page, or a lower level FSM page. In
each non-leaf node, the higher of its children's values is stored. The maximum
value in the leaf nodes is therefore stored at the root.

See `src/backend/storage/freespace/README` for more details on how the FSM is
structured, and how it's updated and searched. The
[pg_freespacemap](pgfreespacemap.html "F.29. pg_freespacemap — examine the
free space map") module can be used to examine the information stored in free
space maps.

* * *

[Prev](storage-toast.html "73.2. TOAST")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](storage-vm.html "73.4. Visibility Map")  
---|---|---  
73.2. TOAST  | [Home](index.html "PostgreSQL 16.9 Documentation") |  73.4. Visibility Map  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-fsm.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

