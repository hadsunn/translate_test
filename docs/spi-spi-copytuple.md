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

Supported Versions: [Current](/docs/current/spi-spi-copytuple.html "PostgreSQL
17 - SPI_copytuple") ([17](/docs/17/spi-spi-copytuple.html "PostgreSQL 17 -
SPI_copytuple")) / [16](/docs/16/spi-spi-copytuple.html "PostgreSQL 16 -
SPI_copytuple") / [15](/docs/15/spi-spi-copytuple.html "PostgreSQL 15 -
SPI_copytuple") / [14](/docs/14/spi-spi-copytuple.html "PostgreSQL 14 -
SPI_copytuple") / [13](/docs/13/spi-spi-copytuple.html "PostgreSQL 13 -
SPI_copytuple")

Development Versions: [18](/docs/18/spi-spi-copytuple.html "PostgreSQL 18 -
SPI_copytuple") / [devel](/docs/devel/spi-spi-copytuple.html "PostgreSQL devel
- SPI_copytuple")

Unsupported versions: [12](/docs/12/spi-spi-copytuple.html "PostgreSQL 12 -
SPI_copytuple") / [11](/docs/11/spi-spi-copytuple.html "PostgreSQL 11 -
SPI_copytuple") / [10](/docs/10/spi-spi-copytuple.html "PostgreSQL 10 -
SPI_copytuple") / [9.6](/docs/9.6/spi-spi-copytuple.html "PostgreSQL 9.6 -
SPI_copytuple") / [9.5](/docs/9.5/spi-spi-copytuple.html "PostgreSQL 9.5 -
SPI_copytuple") / [9.4](/docs/9.4/spi-spi-copytuple.html "PostgreSQL 9.4 -
SPI_copytuple") / [9.3](/docs/9.3/spi-spi-copytuple.html "PostgreSQL 9.3 -
SPI_copytuple") / [9.2](/docs/9.2/spi-spi-copytuple.html "PostgreSQL 9.2 -
SPI_copytuple") / [9.1](/docs/9.1/spi-spi-copytuple.html "PostgreSQL 9.1 -
SPI_copytuple") / [9.0](/docs/9.0/spi-spi-copytuple.html "PostgreSQL 9.0 -
SPI_copytuple") / [8.4](/docs/8.4/spi-spi-copytuple.html "PostgreSQL 8.4 -
SPI_copytuple") / [8.3](/docs/8.3/spi-spi-copytuple.html "PostgreSQL 8.3 -
SPI_copytuple") / [8.2](/docs/8.2/spi-spi-copytuple.html "PostgreSQL 8.2 -
SPI_copytuple") / [8.1](/docs/8.1/spi-spi-copytuple.html "PostgreSQL 8.1 -
SPI_copytuple") / [8.0](/docs/8.0/spi-spi-copytuple.html "PostgreSQL 8.0 -
SPI_copytuple") / [7.4](/docs/7.4/spi-spi-copytuple.html "PostgreSQL 7.4 -
SPI_copytuple")

__

SPI_copytuple  
---  
[Prev](spi-spi-pfree.html "SPI_pfree")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-returntuple.html "SPI_returntuple")  
  
* * *

## SPI_copytuple

SPI_copytuple — make a copy of a row in the upper executor context

## Synopsis

    
    
    HeapTuple SPI_copytuple(HeapTuple _row_)
    

## Description

`SPI_copytuple` makes a copy of a row in the upper executor context. This is
normally used to return a modified row from a trigger. In a function declared
to return a composite type, use `SPI_returntuple` instead.

This function can only be used while connected to SPI. Otherwise, it returns
NULL and sets `SPI_result` to `SPI_ERROR_UNCONNECTED`.

## Arguments

`HeapTuple _`row`_`

    

row to be copied

## Return Value

the copied row, or `NULL` on error (see `SPI_result` for an error indication)

* * *

[Prev](spi-spi-pfree.html "SPI_pfree")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-returntuple.html "SPI_returntuple")  
---|---|---  
SPI_pfree  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_returntuple  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-copytuple.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

