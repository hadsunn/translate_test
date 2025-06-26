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

Supported Versions: [Current](/docs/current/lo-implementation.html "PostgreSQL
17 - 35.2. Implementation Features") ([17](/docs/17/lo-implementation.html
"PostgreSQL 17 - 35.2. Implementation Features")) / [16](/docs/16/lo-
implementation.html "PostgreSQL 16 - 35.2. Implementation Features") /
[15](/docs/15/lo-implementation.html "PostgreSQL 15 - 35.2. Implementation
Features") / [14](/docs/14/lo-implementation.html "PostgreSQL 14 -
35.2. Implementation Features") / [13](/docs/13/lo-implementation.html
"PostgreSQL 13 - 35.2. Implementation Features")

Development Versions: [18](/docs/18/lo-implementation.html "PostgreSQL 18 -
35.2. Implementation Features") / [devel](/docs/devel/lo-implementation.html
"PostgreSQL devel - 35.2. Implementation Features")

Unsupported versions: [12](/docs/12/lo-implementation.html "PostgreSQL 12 -
35.2. Implementation Features") / [11](/docs/11/lo-implementation.html
"PostgreSQL 11 - 35.2. Implementation Features") / [10](/docs/10/lo-
implementation.html "PostgreSQL 10 - 35.2. Implementation Features") /
[9.6](/docs/9.6/lo-implementation.html "PostgreSQL 9.6 - 35.2. Implementation
Features") / [9.5](/docs/9.5/lo-implementation.html "PostgreSQL 9.5 -
35.2. Implementation Features") / [9.4](/docs/9.4/lo-implementation.html
"PostgreSQL 9.4 - 35.2. Implementation Features") / [9.3](/docs/9.3/lo-
implementation.html "PostgreSQL 9.3 - 35.2. Implementation Features") /
[9.2](/docs/9.2/lo-implementation.html "PostgreSQL 9.2 - 35.2. Implementation
Features") / [9.1](/docs/9.1/lo-implementation.html "PostgreSQL 9.1 -
35.2. Implementation Features") / [9.0](/docs/9.0/lo-implementation.html
"PostgreSQL 9.0 - 35.2. Implementation Features") / [8.4](/docs/8.4/lo-
implementation.html "PostgreSQL 8.4 - 35.2. Implementation Features") /
[8.3](/docs/8.3/lo-implementation.html "PostgreSQL 8.3 - 35.2. Implementation
Features") / [8.2](/docs/8.2/lo-implementation.html "PostgreSQL 8.2 -
35.2. Implementation Features") / [8.1](/docs/8.1/lo-implementation.html
"PostgreSQL 8.1 - 35.2. Implementation Features") / [8.0](/docs/8.0/lo-
implementation.html "PostgreSQL 8.0 - 35.2. Implementation Features") /
[7.4](/docs/7.4/lo-implementation.html "PostgreSQL 7.4 - 35.2. Implementation
Features") / [7.3](/docs/7.3/lo-implementation.html "PostgreSQL 7.3 -
35.2. Implementation Features") / [7.2](/docs/7.2/lo-implementation.html
"PostgreSQL 7.2 - 35.2. Implementation Features") / [7.1](/docs/7.1/lo-
implementation.html "PostgreSQL 7.1 - 35.2. Implementation Features")

__

35.2. Implementation Features  
---  
[Prev](lo-intro.html "35.1. Introduction")  | [Up](largeobjects.html "Chapter 35. Large Objects") | Chapter 35. Large Objects | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](lo-interfaces.html "35.3. Client Interfaces")  
  
* * *

## 35.2. Implementation Features #

The large object implementation breaks large objects up into “chunks” and
stores the chunks in rows in the database. A B-tree index guarantees fast
searches for the correct chunk number when doing random access reads and
writes.

The chunks stored for a large object do not have to be contiguous. For
example, if an application opens a new large object, seeks to offset 1000000,
and writes a few bytes there, this does not result in allocation of 1000000
bytes worth of storage; only of chunks covering the range of data bytes
actually written. A read operation will, however, read out zeroes for any
unallocated locations preceding the last existing chunk. This corresponds to
the common behavior of “sparsely allocated” files in Unix file systems.

As of PostgreSQL 9.0, large objects have an owner and a set of access
permissions, which can be managed using [GRANT](sql-grant.html "GRANT") and
[REVOKE](sql-revoke.html "REVOKE"). `SELECT` privileges are required to read a
large object, and `UPDATE` privileges are required to write or truncate it.
Only the large object's owner (or a database superuser) can delete, comment
on, or change the owner of a large object. To adjust this behavior for
compatibility with prior releases, see the [lo_compat_privileges](runtime-
config-compatible.html#GUC-LO-COMPAT-PRIVILEGES) run-time parameter.

* * *

[Prev](lo-intro.html "35.1. Introduction")  | [Up](largeobjects.html "Chapter 35. Large Objects") |  [Next](lo-interfaces.html "35.3. Client Interfaces")  
---|---|---  
35.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  35.3. Client Interfaces  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/lo-implementation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

