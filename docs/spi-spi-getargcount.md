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

Supported Versions: [Current](/docs/current/spi-spi-getargcount.html
"PostgreSQL 17 - SPI_getargcount") ([17](/docs/17/spi-spi-getargcount.html
"PostgreSQL 17 - SPI_getargcount")) / [16](/docs/16/spi-spi-getargcount.html
"PostgreSQL 16 - SPI_getargcount") / [15](/docs/15/spi-spi-getargcount.html
"PostgreSQL 15 - SPI_getargcount") / [14](/docs/14/spi-spi-getargcount.html
"PostgreSQL 14 - SPI_getargcount") / [13](/docs/13/spi-spi-getargcount.html
"PostgreSQL 13 - SPI_getargcount")

Development Versions: [18](/docs/18/spi-spi-getargcount.html "PostgreSQL 18 -
SPI_getargcount") / [devel](/docs/devel/spi-spi-getargcount.html "PostgreSQL
devel - SPI_getargcount")

Unsupported versions: [12](/docs/12/spi-spi-getargcount.html "PostgreSQL 12 -
SPI_getargcount") / [11](/docs/11/spi-spi-getargcount.html "PostgreSQL 11 -
SPI_getargcount") / [10](/docs/10/spi-spi-getargcount.html "PostgreSQL 10 -
SPI_getargcount") / [9.6](/docs/9.6/spi-spi-getargcount.html "PostgreSQL 9.6 -
SPI_getargcount") / [9.5](/docs/9.5/spi-spi-getargcount.html "PostgreSQL 9.5 -
SPI_getargcount") / [9.4](/docs/9.4/spi-spi-getargcount.html "PostgreSQL 9.4 -
SPI_getargcount") / [9.3](/docs/9.3/spi-spi-getargcount.html "PostgreSQL 9.3 -
SPI_getargcount") / [9.2](/docs/9.2/spi-spi-getargcount.html "PostgreSQL 9.2 -
SPI_getargcount") / [9.1](/docs/9.1/spi-spi-getargcount.html "PostgreSQL 9.1 -
SPI_getargcount") / [9.0](/docs/9.0/spi-spi-getargcount.html "PostgreSQL 9.0 -
SPI_getargcount") / [8.4](/docs/8.4/spi-spi-getargcount.html "PostgreSQL 8.4 -
SPI_getargcount") / [8.3](/docs/8.3/spi-spi-getargcount.html "PostgreSQL 8.3 -
SPI_getargcount") / [8.2](/docs/8.2/spi-spi-getargcount.html "PostgreSQL 8.2 -
SPI_getargcount") / [8.1](/docs/8.1/spi-spi-getargcount.html "PostgreSQL 8.1 -
SPI_getargcount") / [8.0](/docs/8.0/spi-spi-getargcount.html "PostgreSQL 8.0 -
SPI_getargcount")

__

SPI_getargcount  
---  
[Prev](spi-spi-prepare-params.html "SPI_prepare_params")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-getargtypeid.html "SPI_getargtypeid")  
  
* * *

## SPI_getargcount

SPI_getargcount — return the number of arguments needed by a statement
prepared by `SPI_prepare`

## Synopsis

    
    
    int SPI_getargcount(SPIPlanPtr _plan_)
    

## Description

`SPI_getargcount` returns the number of arguments needed to execute a
statement prepared by `SPI_prepare`.

## Arguments

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

## Return Value

The count of expected arguments for the _`plan`_. If the _`plan`_ is `NULL` or
invalid, `SPI_result` is set to `SPI_ERROR_ARGUMENT` and -1 is returned.

* * *

[Prev](spi-spi-prepare-params.html "SPI_prepare_params")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-getargtypeid.html "SPI_getargtypeid")  
---|---|---  
SPI_prepare_params  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_getargtypeid  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-getargcount.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

