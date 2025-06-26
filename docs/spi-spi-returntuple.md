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

Supported Versions: [Current](/docs/current/spi-spi-returntuple.html
"PostgreSQL 17 - SPI_returntuple") ([17](/docs/17/spi-spi-returntuple.html
"PostgreSQL 17 - SPI_returntuple")) / [16](/docs/16/spi-spi-returntuple.html
"PostgreSQL 16 - SPI_returntuple") / [15](/docs/15/spi-spi-returntuple.html
"PostgreSQL 15 - SPI_returntuple") / [14](/docs/14/spi-spi-returntuple.html
"PostgreSQL 14 - SPI_returntuple") / [13](/docs/13/spi-spi-returntuple.html
"PostgreSQL 13 - SPI_returntuple")

Development Versions: [18](/docs/18/spi-spi-returntuple.html "PostgreSQL 18 -
SPI_returntuple") / [devel](/docs/devel/spi-spi-returntuple.html "PostgreSQL
devel - SPI_returntuple")

Unsupported versions: [12](/docs/12/spi-spi-returntuple.html "PostgreSQL 12 -
SPI_returntuple") / [11](/docs/11/spi-spi-returntuple.html "PostgreSQL 11 -
SPI_returntuple") / [10](/docs/10/spi-spi-returntuple.html "PostgreSQL 10 -
SPI_returntuple") / [9.6](/docs/9.6/spi-spi-returntuple.html "PostgreSQL 9.6 -
SPI_returntuple") / [9.5](/docs/9.5/spi-spi-returntuple.html "PostgreSQL 9.5 -
SPI_returntuple") / [9.4](/docs/9.4/spi-spi-returntuple.html "PostgreSQL 9.4 -
SPI_returntuple") / [9.3](/docs/9.3/spi-spi-returntuple.html "PostgreSQL 9.3 -
SPI_returntuple") / [9.2](/docs/9.2/spi-spi-returntuple.html "PostgreSQL 9.2 -
SPI_returntuple") / [9.1](/docs/9.1/spi-spi-returntuple.html "PostgreSQL 9.1 -
SPI_returntuple") / [9.0](/docs/9.0/spi-spi-returntuple.html "PostgreSQL 9.0 -
SPI_returntuple") / [8.4](/docs/8.4/spi-spi-returntuple.html "PostgreSQL 8.4 -
SPI_returntuple") / [8.3](/docs/8.3/spi-spi-returntuple.html "PostgreSQL 8.3 -
SPI_returntuple") / [8.2](/docs/8.2/spi-spi-returntuple.html "PostgreSQL 8.2 -
SPI_returntuple") / [8.1](/docs/8.1/spi-spi-returntuple.html "PostgreSQL 8.1 -
SPI_returntuple") / [8.0](/docs/8.0/spi-spi-returntuple.html "PostgreSQL 8.0 -
SPI_returntuple")

__

SPI_returntuple  
---  
[Prev](spi-spi-copytuple.html "SPI_copytuple")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-modifytuple.html "SPI_modifytuple")  
  
* * *

## SPI_returntuple

SPI_returntuple — prepare to return a tuple as a Datum

## Synopsis

    
    
    HeapTupleHeader SPI_returntuple(HeapTuple _row_ , TupleDesc _rowdesc_)
    

## Description

`SPI_returntuple` makes a copy of a row in the upper executor context,
returning it in the form of a row type `Datum`. The returned pointer need only
be converted to `Datum` via `PointerGetDatum` before returning.

This function can only be used while connected to SPI. Otherwise, it returns
NULL and sets `SPI_result` to `SPI_ERROR_UNCONNECTED`.

Note that this should be used for functions that are declared to return
composite types. It is not used for triggers; use `SPI_copytuple` for
returning a modified row in a trigger.

## Arguments

`HeapTuple _`row`_`

    

row to be copied

`TupleDesc _`rowdesc`_`

    

descriptor for row (pass the same descriptor each time for most effective
caching)

## Return Value

`HeapTupleHeader` pointing to copied row, or `NULL` on error (see `SPI_result`
for an error indication)

* * *

[Prev](spi-spi-copytuple.html "SPI_copytuple")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-modifytuple.html "SPI_modifytuple")  
---|---|---  
SPI_copytuple  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_modifytuple  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-returntuple.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

