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

Supported Versions: [Current](/docs/current/spi-memory.html "PostgreSQL 17 -
47.3. Memory Management") ([17](/docs/17/spi-memory.html "PostgreSQL 17 -
47.3. Memory Management")) / [16](/docs/16/spi-memory.html "PostgreSQL 16 -
47.3. Memory Management") / [15](/docs/15/spi-memory.html "PostgreSQL 15 -
47.3. Memory Management") / [14](/docs/14/spi-memory.html "PostgreSQL 14 -
47.3. Memory Management") / [13](/docs/13/spi-memory.html "PostgreSQL 13 -
47.3. Memory Management")

Development Versions: [18](/docs/18/spi-memory.html "PostgreSQL 18 -
47.3. Memory Management") / [devel](/docs/devel/spi-memory.html "PostgreSQL
devel - 47.3. Memory Management")

Unsupported versions: [12](/docs/12/spi-memory.html "PostgreSQL 12 -
47.3. Memory Management") / [11](/docs/11/spi-memory.html "PostgreSQL 11 -
47.3. Memory Management") / [10](/docs/10/spi-memory.html "PostgreSQL 10 -
47.3. Memory Management") / [9.6](/docs/9.6/spi-memory.html "PostgreSQL 9.6 -
47.3. Memory Management") / [9.5](/docs/9.5/spi-memory.html "PostgreSQL 9.5 -
47.3. Memory Management") / [9.4](/docs/9.4/spi-memory.html "PostgreSQL 9.4 -
47.3. Memory Management") / [9.3](/docs/9.3/spi-memory.html "PostgreSQL 9.3 -
47.3. Memory Management") / [9.2](/docs/9.2/spi-memory.html "PostgreSQL 9.2 -
47.3. Memory Management") / [9.1](/docs/9.1/spi-memory.html "PostgreSQL 9.1 -
47.3. Memory Management") / [9.0](/docs/9.0/spi-memory.html "PostgreSQL 9.0 -
47.3. Memory Management") / [8.4](/docs/8.4/spi-memory.html "PostgreSQL 8.4 -
47.3. Memory Management") / [8.3](/docs/8.3/spi-memory.html "PostgreSQL 8.3 -
47.3. Memory Management") / [8.2](/docs/8.2/spi-memory.html "PostgreSQL 8.2 -
47.3. Memory Management") / [8.1](/docs/8.1/spi-memory.html "PostgreSQL 8.1 -
47.3. Memory Management") / [8.0](/docs/8.0/spi-memory.html "PostgreSQL 8.0 -
47.3. Memory Management") / [7.4](/docs/7.4/spi-memory.html "PostgreSQL 7.4 -
47.3. Memory Management") / [7.3](/docs/7.3/spi-memory.html "PostgreSQL 7.3 -
47.3. Memory Management") / [7.2](/docs/7.2/spi-memory.html "PostgreSQL 7.2 -
47.3. Memory Management") / [7.1](/docs/7.1/spi-memory.html "PostgreSQL 7.1 -
47.3. Memory Management")

__

47.3. Memory Management  
---  
[Prev](spi-spi-result-code-string.html "SPI_result_code_string")  | [Up](spi.html "Chapter 47. Server Programming Interface") | Chapter 47. Server Programming Interface | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-palloc.html "SPI_palloc")  
  
* * *

## 47.3. Memory Management #

[SPI_palloc](spi-spi-palloc.html) — allocate memory in the upper executor
context

[SPI_repalloc](spi-realloc.html) — reallocate memory in the upper executor
context

[SPI_pfree](spi-spi-pfree.html) — free memory in the upper executor context

[SPI_copytuple](spi-spi-copytuple.html) — make a copy of a row in the upper
executor context

[SPI_returntuple](spi-spi-returntuple.html) — prepare to return a tuple as a
Datum

[SPI_modifytuple](spi-spi-modifytuple.html) — create a row by replacing
selected fields of a given row

[SPI_freetuple](spi-spi-freetuple.html) — free a row allocated in the upper
executor context

[SPI_freetuptable](spi-spi-freetupletable.html) — free a row set created by
`SPI_execute` or a similar function

[SPI_freeplan](spi-spi-freeplan.html) — free a previously saved prepared
statement

PostgreSQL allocates memory within _memory contexts_ , which provide a
convenient method of managing allocations made in many different places that
need to live for differing amounts of time. Destroying a context releases all
the memory that was allocated in it. Thus, it is not necessary to keep track
of individual objects to avoid memory leaks; instead only a relatively small
number of contexts have to be managed. `palloc` and related functions allocate
memory from the “current” context.

`SPI_connect` creates a new memory context and makes it current. `SPI_finish`
restores the previous current memory context and destroys the context created
by `SPI_connect`. These actions ensure that transient memory allocations made
inside your C function are reclaimed at C function exit, avoiding memory
leakage.

However, if your C function needs to return an object in allocated memory
(such as a value of a pass-by-reference data type), you cannot allocate that
memory using `palloc`, at least not while you are connected to SPI. If you
try, the object will be deallocated by `SPI_finish`, and your C function will
not work reliably. To solve this problem, use `SPI_palloc` to allocate memory
for your return object. `SPI_palloc` allocates memory in the “upper executor
context”, that is, the memory context that was current when `SPI_connect` was
called, which is precisely the right context for a value returned from your C
function. Several of the other utility functions described in this section
also return objects created in the upper executor context.

When `SPI_connect` is called, the private context of the C function, which is
created by `SPI_connect`, is made the current context. All allocations made by
`palloc`, `repalloc`, or SPI utility functions (except as described in this
section) are made in this context. When a C function disconnects from the SPI
manager (via `SPI_finish`) the current context is restored to the upper
executor context, and all allocations made in the C function memory context
are freed and cannot be used any more.

* * *

[Prev](spi-spi-result-code-string.html "SPI_result_code_string")  | [Up](spi.html "Chapter 47. Server Programming Interface") |  [Next](spi-spi-palloc.html "SPI_palloc")  
---|---|---  
SPI_result_code_string  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_palloc  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-memory.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

