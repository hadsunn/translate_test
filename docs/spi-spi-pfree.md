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

Supported Versions: [Current](/docs/current/spi-spi-pfree.html "PostgreSQL 17
- SPI_pfree") ([17](/docs/17/spi-spi-pfree.html "PostgreSQL 17 - SPI_pfree"))
/ [16](/docs/16/spi-spi-pfree.html "PostgreSQL 16 - SPI_pfree") /
[15](/docs/15/spi-spi-pfree.html "PostgreSQL 15 - SPI_pfree") /
[14](/docs/14/spi-spi-pfree.html "PostgreSQL 14 - SPI_pfree") /
[13](/docs/13/spi-spi-pfree.html "PostgreSQL 13 - SPI_pfree")

Development Versions: [18](/docs/18/spi-spi-pfree.html "PostgreSQL 18 -
SPI_pfree") / [devel](/docs/devel/spi-spi-pfree.html "PostgreSQL devel -
SPI_pfree")

Unsupported versions: [12](/docs/12/spi-spi-pfree.html "PostgreSQL 12 -
SPI_pfree") / [11](/docs/11/spi-spi-pfree.html "PostgreSQL 11 - SPI_pfree") /
[10](/docs/10/spi-spi-pfree.html "PostgreSQL 10 - SPI_pfree") /
[9.6](/docs/9.6/spi-spi-pfree.html "PostgreSQL 9.6 - SPI_pfree") /
[9.5](/docs/9.5/spi-spi-pfree.html "PostgreSQL 9.5 - SPI_pfree") /
[9.4](/docs/9.4/spi-spi-pfree.html "PostgreSQL 9.4 - SPI_pfree") /
[9.3](/docs/9.3/spi-spi-pfree.html "PostgreSQL 9.3 - SPI_pfree") /
[9.2](/docs/9.2/spi-spi-pfree.html "PostgreSQL 9.2 - SPI_pfree") /
[9.1](/docs/9.1/spi-spi-pfree.html "PostgreSQL 9.1 - SPI_pfree") /
[9.0](/docs/9.0/spi-spi-pfree.html "PostgreSQL 9.0 - SPI_pfree") /
[8.4](/docs/8.4/spi-spi-pfree.html "PostgreSQL 8.4 - SPI_pfree") /
[8.3](/docs/8.3/spi-spi-pfree.html "PostgreSQL 8.3 - SPI_pfree") /
[8.2](/docs/8.2/spi-spi-pfree.html "PostgreSQL 8.2 - SPI_pfree") /
[8.1](/docs/8.1/spi-spi-pfree.html "PostgreSQL 8.1 - SPI_pfree") /
[8.0](/docs/8.0/spi-spi-pfree.html "PostgreSQL 8.0 - SPI_pfree") /
[7.4](/docs/7.4/spi-spi-pfree.html "PostgreSQL 7.4 - SPI_pfree")

__

SPI_pfree  
---  
[Prev](spi-realloc.html "SPI_repalloc")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-copytuple.html "SPI_copytuple")  
  
* * *

## SPI_pfree

SPI_pfree — free memory in the upper executor context

## Synopsis

    
    
    void SPI_pfree(void * _pointer_)
    

## Description

`SPI_pfree` frees memory previously allocated using `SPI_palloc` or
`SPI_repalloc`.

This function is no longer different from plain `pfree`. It's kept just for
backward compatibility of existing code.

## Arguments

`void * _`pointer`_`

    

pointer to existing storage to free

* * *

[Prev](spi-realloc.html "SPI_repalloc")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-copytuple.html "SPI_copytuple")  
---|---|---  
SPI_repalloc  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_copytuple  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-pfree.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

