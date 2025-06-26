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

Supported Versions: [Current](/docs/current/spi-spi-palloc.html "PostgreSQL 17
- SPI_palloc") ([17](/docs/17/spi-spi-palloc.html "PostgreSQL 17 -
SPI_palloc")) / [16](/docs/16/spi-spi-palloc.html "PostgreSQL 16 -
SPI_palloc") / [15](/docs/15/spi-spi-palloc.html "PostgreSQL 15 - SPI_palloc")
/ [14](/docs/14/spi-spi-palloc.html "PostgreSQL 14 - SPI_palloc") /
[13](/docs/13/spi-spi-palloc.html "PostgreSQL 13 - SPI_palloc")

Development Versions: [18](/docs/18/spi-spi-palloc.html "PostgreSQL 18 -
SPI_palloc") / [devel](/docs/devel/spi-spi-palloc.html "PostgreSQL devel -
SPI_palloc")

Unsupported versions: [12](/docs/12/spi-spi-palloc.html "PostgreSQL 12 -
SPI_palloc") / [11](/docs/11/spi-spi-palloc.html "PostgreSQL 11 - SPI_palloc")
/ [10](/docs/10/spi-spi-palloc.html "PostgreSQL 10 - SPI_palloc") /
[9.6](/docs/9.6/spi-spi-palloc.html "PostgreSQL 9.6 - SPI_palloc") /
[9.5](/docs/9.5/spi-spi-palloc.html "PostgreSQL 9.5 - SPI_palloc") /
[9.4](/docs/9.4/spi-spi-palloc.html "PostgreSQL 9.4 - SPI_palloc") /
[9.3](/docs/9.3/spi-spi-palloc.html "PostgreSQL 9.3 - SPI_palloc") /
[9.2](/docs/9.2/spi-spi-palloc.html "PostgreSQL 9.2 - SPI_palloc") /
[9.1](/docs/9.1/spi-spi-palloc.html "PostgreSQL 9.1 - SPI_palloc") /
[9.0](/docs/9.0/spi-spi-palloc.html "PostgreSQL 9.0 - SPI_palloc") /
[8.4](/docs/8.4/spi-spi-palloc.html "PostgreSQL 8.4 - SPI_palloc") /
[8.3](/docs/8.3/spi-spi-palloc.html "PostgreSQL 8.3 - SPI_palloc") /
[8.2](/docs/8.2/spi-spi-palloc.html "PostgreSQL 8.2 - SPI_palloc") /
[8.1](/docs/8.1/spi-spi-palloc.html "PostgreSQL 8.1 - SPI_palloc") /
[8.0](/docs/8.0/spi-spi-palloc.html "PostgreSQL 8.0 - SPI_palloc") /
[7.4](/docs/7.4/spi-spi-palloc.html "PostgreSQL 7.4 - SPI_palloc")

__

SPI_palloc  
---  
[Prev](spi-memory.html "47.3. Memory Management")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-realloc.html "SPI_repalloc")  
  
* * *

## SPI_palloc

SPI_palloc — allocate memory in the upper executor context

## Synopsis

    
    
    void * SPI_palloc(Size _size_)
    

## Description

`SPI_palloc` allocates memory in the upper executor context.

This function can only be used while connected to SPI. Otherwise, it throws an
error.

## Arguments

`Size _`size`_`

    

size in bytes of storage to allocate

## Return Value

pointer to new storage space of the specified size

* * *

[Prev](spi-memory.html "47.3. Memory Management")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-realloc.html "SPI_repalloc")  
---|---|---  
47.3. Memory Management  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_repalloc  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-palloc.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

