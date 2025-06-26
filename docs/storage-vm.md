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

Supported Versions: [Current](/docs/current/storage-vm.html "PostgreSQL 17 -
73.4. Visibility Map") ([17](/docs/17/storage-vm.html "PostgreSQL 17 -
73.4. Visibility Map")) / [16](/docs/16/storage-vm.html "PostgreSQL 16 -
73.4. Visibility Map") / [15](/docs/15/storage-vm.html "PostgreSQL 15 -
73.4. Visibility Map") / [14](/docs/14/storage-vm.html "PostgreSQL 14 -
73.4. Visibility Map") / [13](/docs/13/storage-vm.html "PostgreSQL 13 -
73.4. Visibility Map")

Development Versions: [18](/docs/18/storage-vm.html "PostgreSQL 18 -
73.4. Visibility Map") / [devel](/docs/devel/storage-vm.html "PostgreSQL devel
- 73.4. Visibility Map")

Unsupported versions: [12](/docs/12/storage-vm.html "PostgreSQL 12 -
73.4. Visibility Map") / [11](/docs/11/storage-vm.html "PostgreSQL 11 -
73.4. Visibility Map") / [10](/docs/10/storage-vm.html "PostgreSQL 10 -
73.4. Visibility Map") / [9.6](/docs/9.6/storage-vm.html "PostgreSQL 9.6 -
73.4. Visibility Map") / [9.5](/docs/9.5/storage-vm.html "PostgreSQL 9.5 -
73.4. Visibility Map") / [9.4](/docs/9.4/storage-vm.html "PostgreSQL 9.4 -
73.4. Visibility Map") / [9.3](/docs/9.3/storage-vm.html "PostgreSQL 9.3 -
73.4. Visibility Map") / [9.2](/docs/9.2/storage-vm.html "PostgreSQL 9.2 -
73.4. Visibility Map") / [9.1](/docs/9.1/storage-vm.html "PostgreSQL 9.1 -
73.4. Visibility Map") / [9.0](/docs/9.0/storage-vm.html "PostgreSQL 9.0 -
73.4. Visibility Map") / [8.4](/docs/8.4/storage-vm.html "PostgreSQL 8.4 -
73.4. Visibility Map")

__

73.4. Visibility Map  
---  
[Prev](storage-fsm.html "73.3. Free Space Map")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage-init.html "73.5. The Initialization Fork")  
  
* * *

## 73.4. Visibility Map #

Each heap relation has a Visibility Map (VM) to keep track of which pages
contain only tuples that are known to be visible to all active transactions;
it also keeps track of which pages contain only frozen tuples. It's stored
alongside the main relation data in a separate relation fork, named after the
filenode number of the relation, plus a `_vm` suffix. For example, if the
filenode of a relation is 12345, the VM is stored in a file called `12345_vm`,
in the same directory as the main relation file. Note that indexes do not have
VMs.

The visibility map stores two bits per heap page. The first bit, if set,
indicates that the page is all-visible, or in other words that the page does
not contain any tuples that need to be vacuumed. This information can also be
used by [_index-only scans_](indexes-index-only-scans.html "11.9. Index-Only
Scans and Covering Indexes") to answer queries using only the index tuple. The
second bit, if set, means that all tuples on the page have been frozen. That
means that even an anti-wraparound vacuum need not revisit the page.

The map is conservative in the sense that we make sure that whenever a bit is
set, we know the condition is true, but if a bit is not set, it might or might
not be true. Visibility map bits are only set by vacuum, but are cleared by
any data-modifying operations on a page.

The [pg_visibility](pgvisibility.html "F.36. pg_visibility — visibility map
information and utilities") module can be used to examine the information
stored in the visibility map.

* * *

[Prev](storage-fsm.html "73.3. Free Space Map")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](storage-init.html "73.5. The Initialization Fork")  
---|---|---  
73.3. Free Space Map  | [Home](index.html "PostgreSQL 16.9 Documentation") |  73.5. The Initialization Fork  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-vm.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

