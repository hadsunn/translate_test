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

Supported Versions: [Current](/docs/current/tableam.html "PostgreSQL 17 -
Chapter 63. Table Access Method Interface Definition")
([17](/docs/17/tableam.html "PostgreSQL 17 - Chapter 63. Table Access Method
Interface Definition")) / [16](/docs/16/tableam.html "PostgreSQL 16 -
Chapter 63. Table Access Method Interface Definition") /
[15](/docs/15/tableam.html "PostgreSQL 15 - Chapter 63. Table Access Method
Interface Definition") / [14](/docs/14/tableam.html "PostgreSQL 14 -
Chapter 63. Table Access Method Interface Definition") /
[13](/docs/13/tableam.html "PostgreSQL 13 - Chapter 63. Table Access Method
Interface Definition")

Development Versions: [18](/docs/18/tableam.html "PostgreSQL 18 -
Chapter 63. Table Access Method Interface Definition") /
[devel](/docs/devel/tableam.html "PostgreSQL devel - Chapter 63. Table Access
Method Interface Definition")

Unsupported versions: [12](/docs/12/tableam.html "PostgreSQL 12 -
Chapter 63. Table Access Method Interface Definition")

__

Chapter 63. Table Access Method Interface Definition  
---  
[Prev](geqo-biblio.html "62.4. Further Reading")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexam.html "Chapter 64. Index Access Method Interface Definition")  
  
* * *

## Chapter 63. Table Access Method Interface Definition

This chapter explains the interface between the core PostgreSQL system and
_table access methods_ , which manage the storage for tables. The core system
knows little about these access methods beyond what is specified here, so it
is possible to develop entirely new access method types by writing add-on
code.

Each table access method is described by a row in the [`pg_am`](catalog-pg-
am.html "53.3. pg_am") system catalog. The `pg_am` entry specifies a name and
a _handler function_ for the table access method. These entries can be created
and deleted using the [CREATE ACCESS METHOD](sql-create-access-method.html
"CREATE ACCESS METHOD") and [DROP ACCESS METHOD](sql-drop-access-method.html
"DROP ACCESS METHOD") SQL commands.

A table access method handler function must be declared to accept a single
argument of type `internal` and to return the pseudo-type `table_am_handler`.
The argument is a dummy value that simply serves to prevent handler functions
from being called directly from SQL commands. The result of the function must
be a pointer to a struct of type `TableAmRoutine`, which contains everything
that the core code needs to know to make use of the table access method. The
return value needs to be of server lifetime, which is typically achieved by
defining it as a `static const` variable in global scope. The `TableAmRoutine`
struct, also called the access method's _API struct_ , defines the behavior of
the access method using callbacks. These callbacks are pointers to plain C
functions and are not visible or callable at the SQL level. All the callbacks
and their behavior is defined in the `TableAmRoutine` structure (with comments
inside the struct defining the requirements for callbacks). Most callbacks
have wrapper functions, which are documented from the point of view of a user
(rather than an implementor) of the table access method. For details, please
refer to the
[`src/include/access/tableam.h`](https://git.postgresql.org/gitweb/?p=postgresql.git;a=blob;f=src/include/access/tableam.h;hb=HEAD)
file.

To implement an access method, an implementor will typically need to implement
an AM-specific type of tuple table slot (see
[`src/include/executor/tuptable.h`](https://git.postgresql.org/gitweb/?p=postgresql.git;a=blob;f=src/include/executor/tuptable.h;hb=HEAD)),
which allows code outside the access method to hold references to tuples of
the AM, and to access the columns of the tuple.

Currently, the way an AM actually stores data is fairly unconstrained. For
example, it's possible, but not required, to use postgres' shared buffer
cache. In case it is used, it likely makes sense to use PostgreSQL's standard
page layout as described in [Section 73.6](storage-page-layout.html
"73.6. Database Page Layout").

One fairly large constraint of the table access method API is that, currently,
if the AM wants to support modifications and/or indexes, it is necessary for
each tuple to have a tuple identifier (TID) consisting of a block number and
an item number (see also [Section 73.6](storage-page-layout.html
"73.6. Database Page Layout")). It is not strictly necessary that the sub-
parts of TIDs have the same meaning they e.g., have for `heap`, but if bitmap
scan support is desired (it is optional), the block number needs to provide
locality.

For crash safety, an AM can use postgres' [WAL](wal.html
"Chapter 30. Reliability and the Write-Ahead Log"), or a custom
implementation. If WAL is chosen, either [Generic WAL Records](generic-
wal.html "Chapter 65. Generic WAL Records") can be used, or a [Custom WAL
Resource Manager](custom-rmgr.html "Chapter 66. Custom WAL Resource Managers")
can be implemented.

To implement transactional support in a manner that allows different table
access methods be accessed within a single transaction, it likely is necessary
to closely integrate with the machinery in
`src/backend/access/transam/xlog.c`.

Any developer of a new `table access method` can refer to the existing `heap`
implementation present in `src/backend/access/heap/heapam_handler.c` for
details of its implementation.

* * *

[Prev](geqo-biblio.html "62.4. Further Reading")  | [Up](internals.html "Part VII. Internals") |  [Next](indexam.html "Chapter 64. Index Access Method Interface Definition")  
---|---|---  
62.4. Further Reading  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 64. Index Access Method Interface Definition  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tableam.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

