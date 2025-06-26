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

Supported Versions: [Current](/docs/current/spi-spi-freetuple.html "PostgreSQL
17 - SPI_freetuple") ([17](/docs/17/spi-spi-freetuple.html "PostgreSQL 17 -
SPI_freetuple")) / [16](/docs/16/spi-spi-freetuple.html "PostgreSQL 16 -
SPI_freetuple") / [15](/docs/15/spi-spi-freetuple.html "PostgreSQL 15 -
SPI_freetuple") / [14](/docs/14/spi-spi-freetuple.html "PostgreSQL 14 -
SPI_freetuple") / [13](/docs/13/spi-spi-freetuple.html "PostgreSQL 13 -
SPI_freetuple")

Development Versions: [18](/docs/18/spi-spi-freetuple.html "PostgreSQL 18 -
SPI_freetuple") / [devel](/docs/devel/spi-spi-freetuple.html "PostgreSQL devel
- SPI_freetuple")

Unsupported versions: [12](/docs/12/spi-spi-freetuple.html "PostgreSQL 12 -
SPI_freetuple") / [11](/docs/11/spi-spi-freetuple.html "PostgreSQL 11 -
SPI_freetuple") / [10](/docs/10/spi-spi-freetuple.html "PostgreSQL 10 -
SPI_freetuple") / [9.6](/docs/9.6/spi-spi-freetuple.html "PostgreSQL 9.6 -
SPI_freetuple") / [9.5](/docs/9.5/spi-spi-freetuple.html "PostgreSQL 9.5 -
SPI_freetuple") / [9.4](/docs/9.4/spi-spi-freetuple.html "PostgreSQL 9.4 -
SPI_freetuple") / [9.3](/docs/9.3/spi-spi-freetuple.html "PostgreSQL 9.3 -
SPI_freetuple") / [9.2](/docs/9.2/spi-spi-freetuple.html "PostgreSQL 9.2 -
SPI_freetuple") / [9.1](/docs/9.1/spi-spi-freetuple.html "PostgreSQL 9.1 -
SPI_freetuple") / [9.0](/docs/9.0/spi-spi-freetuple.html "PostgreSQL 9.0 -
SPI_freetuple") / [8.4](/docs/8.4/spi-spi-freetuple.html "PostgreSQL 8.4 -
SPI_freetuple") / [8.3](/docs/8.3/spi-spi-freetuple.html "PostgreSQL 8.3 -
SPI_freetuple") / [8.2](/docs/8.2/spi-spi-freetuple.html "PostgreSQL 8.2 -
SPI_freetuple") / [8.1](/docs/8.1/spi-spi-freetuple.html "PostgreSQL 8.1 -
SPI_freetuple") / [8.0](/docs/8.0/spi-spi-freetuple.html "PostgreSQL 8.0 -
SPI_freetuple") / [7.4](/docs/7.4/spi-spi-freetuple.html "PostgreSQL 7.4 -
SPI_freetuple")

__

SPI_freetuple  
---  
[Prev](spi-spi-modifytuple.html "SPI_modifytuple")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-freetupletable.html "SPI_freetuptable")  
  
* * *

## SPI_freetuple

SPI_freetuple — free a row allocated in the upper executor context

## Synopsis

    
    
    void SPI_freetuple(HeapTuple _row_)
    

## Description

`SPI_freetuple` frees a row previously allocated in the upper executor
context.

This function is no longer different from plain `heap_freetuple`. It's kept
just for backward compatibility of existing code.

## Arguments

`HeapTuple _`row`_`

    

row to free

* * *

[Prev](spi-spi-modifytuple.html "SPI_modifytuple")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-freetupletable.html "SPI_freetuptable")  
---|---|---  
SPI_modifytuple  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_freetuptable  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-freetuple.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

