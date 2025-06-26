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

Supported Versions: [Current](/docs/current/spi-spi-freetupletable.html
"PostgreSQL 17 - SPI_freetuptable") ([17](/docs/17/spi-spi-freetupletable.html
"PostgreSQL 17 - SPI_freetuptable")) / [16](/docs/16/spi-spi-
freetupletable.html "PostgreSQL 16 - SPI_freetuptable") / [15](/docs/15/spi-
spi-freetupletable.html "PostgreSQL 15 - SPI_freetuptable") /
[14](/docs/14/spi-spi-freetupletable.html "PostgreSQL 14 - SPI_freetuptable")
/ [13](/docs/13/spi-spi-freetupletable.html "PostgreSQL 13 -
SPI_freetuptable")

Development Versions: [18](/docs/18/spi-spi-freetupletable.html "PostgreSQL 18
- SPI_freetuptable") / [devel](/docs/devel/spi-spi-freetupletable.html
"PostgreSQL devel - SPI_freetuptable")

Unsupported versions: [12](/docs/12/spi-spi-freetupletable.html "PostgreSQL 12
- SPI_freetuptable") / [11](/docs/11/spi-spi-freetupletable.html "PostgreSQL
11 - SPI_freetuptable") / [10](/docs/10/spi-spi-freetupletable.html
"PostgreSQL 10 - SPI_freetuptable") / [9.6](/docs/9.6/spi-spi-
freetupletable.html "PostgreSQL 9.6 - SPI_freetuptable") /
[9.5](/docs/9.5/spi-spi-freetupletable.html "PostgreSQL 9.5 -
SPI_freetuptable") / [9.4](/docs/9.4/spi-spi-freetupletable.html "PostgreSQL
9.4 - SPI_freetuptable") / [9.3](/docs/9.3/spi-spi-freetupletable.html
"PostgreSQL 9.3 - SPI_freetuptable") / [9.2](/docs/9.2/spi-spi-
freetupletable.html "PostgreSQL 9.2 - SPI_freetuptable") /
[9.1](/docs/9.1/spi-spi-freetupletable.html "PostgreSQL 9.1 -
SPI_freetuptable") / [9.0](/docs/9.0/spi-spi-freetupletable.html "PostgreSQL
9.0 - SPI_freetuptable") / [8.4](/docs/8.4/spi-spi-freetupletable.html
"PostgreSQL 8.4 - SPI_freetuptable") / [8.3](/docs/8.3/spi-spi-
freetupletable.html "PostgreSQL 8.3 - SPI_freetuptable") /
[8.2](/docs/8.2/spi-spi-freetupletable.html "PostgreSQL 8.2 -
SPI_freetuptable") / [8.1](/docs/8.1/spi-spi-freetupletable.html "PostgreSQL
8.1 - SPI_freetuptable") / [8.0](/docs/8.0/spi-spi-freetupletable.html
"PostgreSQL 8.0 - SPI_freetuptable") / [7.4](/docs/7.4/spi-spi-
freetupletable.html "PostgreSQL 7.4 - SPI_freetuptable")

__

SPI_freetuptable  
---  
[Prev](spi-spi-freetuple.html "SPI_freetuple")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-freeplan.html "SPI_freeplan")  
  
* * *

## SPI_freetuptable

SPI_freetuptable — free a row set created by `SPI_execute` or a similar
function

## Synopsis

    
    
    void SPI_freetuptable(SPITupleTable * _tuptable_)
    

## Description

`SPI_freetuptable` frees a row set created by a prior SPI command execution
function, such as `SPI_execute`. Therefore, this function is often called with
the global variable `SPI_tuptable` as argument.

This function is useful if an SPI-using C function needs to execute multiple
commands and does not want to keep the results of earlier commands around
until it ends. Note that any unfreed row sets will be freed anyway at
`SPI_finish`. Also, if a subtransaction is started and then aborted within
execution of an SPI-using C function, SPI automatically frees any row sets
created while the subtransaction was running.

Beginning in PostgreSQL 9.3, `SPI_freetuptable` contains guard logic to
protect against duplicate deletion requests for the same row set. In previous
releases, duplicate deletions would lead to crashes.

## Arguments

`SPITupleTable * _`tuptable`_`

    

pointer to row set to free, or NULL to do nothing

* * *

[Prev](spi-spi-freetuple.html "SPI_freetuple")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-freeplan.html "SPI_freeplan")  
---|---|---  
SPI_freetuple  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_freeplan  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-freetupletable.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

