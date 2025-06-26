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

Supported Versions: [Current](/docs/current/storage-init.html "PostgreSQL 17 -
73.5. The Initialization Fork") ([17](/docs/17/storage-init.html "PostgreSQL
17 - 73.5. The Initialization Fork")) / [16](/docs/16/storage-init.html
"PostgreSQL 16 - 73.5. The Initialization Fork") / [15](/docs/15/storage-
init.html "PostgreSQL 15 - 73.5. The Initialization Fork") /
[14](/docs/14/storage-init.html "PostgreSQL 14 - 73.5. The Initialization
Fork") / [13](/docs/13/storage-init.html "PostgreSQL 13 - 73.5. The
Initialization Fork")

Development Versions: [18](/docs/18/storage-init.html "PostgreSQL 18 -
73.5. The Initialization Fork") / [devel](/docs/devel/storage-init.html
"PostgreSQL devel - 73.5. The Initialization Fork")

Unsupported versions: [12](/docs/12/storage-init.html "PostgreSQL 12 -
73.5. The Initialization Fork") / [11](/docs/11/storage-init.html "PostgreSQL
11 - 73.5. The Initialization Fork") / [10](/docs/10/storage-init.html
"PostgreSQL 10 - 73.5. The Initialization Fork") / [9.6](/docs/9.6/storage-
init.html "PostgreSQL 9.6 - 73.5. The Initialization Fork") /
[9.5](/docs/9.5/storage-init.html "PostgreSQL 9.5 - 73.5. The Initialization
Fork") / [9.4](/docs/9.4/storage-init.html "PostgreSQL 9.4 - 73.5. The
Initialization Fork") / [9.3](/docs/9.3/storage-init.html "PostgreSQL 9.3 -
73.5. The Initialization Fork") / [9.2](/docs/9.2/storage-init.html
"PostgreSQL 9.2 - 73.5. The Initialization Fork") / [9.1](/docs/9.1/storage-
init.html "PostgreSQL 9.1 - 73.5. The Initialization Fork")

__

73.5. The Initialization Fork  
---  
[Prev](storage-vm.html "73.4. Visibility Map")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage-page-layout.html "73.6. Database Page Layout")  
  
* * *

## 73.5. The Initialization Fork #

Each unlogged table, and each index on an unlogged table, has an
initialization fork. The initialization fork is an empty table or index of the
appropriate type. When an unlogged table must be reset to empty due to a
crash, the initialization fork is copied over the main fork, and any other
forks are erased (they will be recreated automatically as needed).

* * *

[Prev](storage-vm.html "73.4. Visibility Map")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](storage-page-layout.html "73.6. Database Page Layout")  
---|---|---  
73.4. Visibility Map  | [Home](index.html "PostgreSQL 16.9 Documentation") |  73.6. Database Page Layout  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-init.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

