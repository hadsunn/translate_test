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

Supported Versions: [Current](/docs/current/spi-realloc.html "PostgreSQL 17 -
SPI_repalloc") ([17](/docs/17/spi-realloc.html "PostgreSQL 17 -
SPI_repalloc")) / [16](/docs/16/spi-realloc.html "PostgreSQL 16 -
SPI_repalloc") / [15](/docs/15/spi-realloc.html "PostgreSQL 15 -
SPI_repalloc") / [14](/docs/14/spi-realloc.html "PostgreSQL 14 -
SPI_repalloc") / [13](/docs/13/spi-realloc.html "PostgreSQL 13 -
SPI_repalloc")

Development Versions: [18](/docs/18/spi-realloc.html "PostgreSQL 18 -
SPI_repalloc") / [devel](/docs/devel/spi-realloc.html "PostgreSQL devel -
SPI_repalloc")

Unsupported versions: [12](/docs/12/spi-realloc.html "PostgreSQL 12 -
SPI_repalloc") / [11](/docs/11/spi-realloc.html "PostgreSQL 11 -
SPI_repalloc") / [10](/docs/10/spi-realloc.html "PostgreSQL 10 -
SPI_repalloc") / [9.6](/docs/9.6/spi-realloc.html "PostgreSQL 9.6 -
SPI_repalloc") / [9.5](/docs/9.5/spi-realloc.html "PostgreSQL 9.5 -
SPI_repalloc") / [9.4](/docs/9.4/spi-realloc.html "PostgreSQL 9.4 -
SPI_repalloc") / [9.3](/docs/9.3/spi-realloc.html "PostgreSQL 9.3 -
SPI_repalloc") / [9.2](/docs/9.2/spi-realloc.html "PostgreSQL 9.2 -
SPI_repalloc") / [9.1](/docs/9.1/spi-realloc.html "PostgreSQL 9.1 -
SPI_repalloc") / [9.0](/docs/9.0/spi-realloc.html "PostgreSQL 9.0 -
SPI_repalloc") / [8.4](/docs/8.4/spi-realloc.html "PostgreSQL 8.4 -
SPI_repalloc") / [8.3](/docs/8.3/spi-realloc.html "PostgreSQL 8.3 -
SPI_repalloc") / [8.2](/docs/8.2/spi-realloc.html "PostgreSQL 8.2 -
SPI_repalloc") / [8.1](/docs/8.1/spi-realloc.html "PostgreSQL 8.1 -
SPI_repalloc") / [8.0](/docs/8.0/spi-realloc.html "PostgreSQL 8.0 -
SPI_repalloc") / [7.4](/docs/7.4/spi-realloc.html "PostgreSQL 7.4 -
SPI_repalloc")

__

SPI_repalloc  
---  
[Prev](spi-spi-palloc.html "SPI_palloc")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-pfree.html "SPI_pfree")  
  
* * *

## SPI_repalloc

SPI_repalloc — reallocate memory in the upper executor context

## Synopsis

    
    
    void * SPI_repalloc(void * _pointer_ , Size _size_)
    

## Description

`SPI_repalloc` changes the size of a memory segment previously allocated using
`SPI_palloc`.

This function is no longer different from plain `repalloc`. It's kept just for
backward compatibility of existing code.

## Arguments

`void * _`pointer`_`

    

pointer to existing storage to change

`Size _`size`_`

    

size in bytes of storage to allocate

## Return Value

pointer to new storage space of specified size with the contents copied from
the existing area

* * *

[Prev](spi-spi-palloc.html "SPI_palloc")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-pfree.html "SPI_pfree")  
---|---|---  
SPI_palloc  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_pfree  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-realloc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

