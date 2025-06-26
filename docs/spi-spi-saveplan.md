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

Supported Versions: [Current](/docs/current/spi-spi-saveplan.html "PostgreSQL
17 - SPI_saveplan") ([17](/docs/17/spi-spi-saveplan.html "PostgreSQL 17 -
SPI_saveplan")) / [16](/docs/16/spi-spi-saveplan.html "PostgreSQL 16 -
SPI_saveplan") / [15](/docs/15/spi-spi-saveplan.html "PostgreSQL 15 -
SPI_saveplan") / [14](/docs/14/spi-spi-saveplan.html "PostgreSQL 14 -
SPI_saveplan") / [13](/docs/13/spi-spi-saveplan.html "PostgreSQL 13 -
SPI_saveplan")

Development Versions: [18](/docs/18/spi-spi-saveplan.html "PostgreSQL 18 -
SPI_saveplan") / [devel](/docs/devel/spi-spi-saveplan.html "PostgreSQL devel -
SPI_saveplan")

Unsupported versions: [12](/docs/12/spi-spi-saveplan.html "PostgreSQL 12 -
SPI_saveplan") / [11](/docs/11/spi-spi-saveplan.html "PostgreSQL 11 -
SPI_saveplan") / [10](/docs/10/spi-spi-saveplan.html "PostgreSQL 10 -
SPI_saveplan") / [9.6](/docs/9.6/spi-spi-saveplan.html "PostgreSQL 9.6 -
SPI_saveplan") / [9.5](/docs/9.5/spi-spi-saveplan.html "PostgreSQL 9.5 -
SPI_saveplan") / [9.4](/docs/9.4/spi-spi-saveplan.html "PostgreSQL 9.4 -
SPI_saveplan") / [9.3](/docs/9.3/spi-spi-saveplan.html "PostgreSQL 9.3 -
SPI_saveplan") / [9.2](/docs/9.2/spi-spi-saveplan.html "PostgreSQL 9.2 -
SPI_saveplan") / [9.1](/docs/9.1/spi-spi-saveplan.html "PostgreSQL 9.1 -
SPI_saveplan") / [9.0](/docs/9.0/spi-spi-saveplan.html "PostgreSQL 9.0 -
SPI_saveplan") / [8.4](/docs/8.4/spi-spi-saveplan.html "PostgreSQL 8.4 -
SPI_saveplan") / [8.3](/docs/8.3/spi-spi-saveplan.html "PostgreSQL 8.3 -
SPI_saveplan") / [8.2](/docs/8.2/spi-spi-saveplan.html "PostgreSQL 8.2 -
SPI_saveplan") / [8.1](/docs/8.1/spi-spi-saveplan.html "PostgreSQL 8.1 -
SPI_saveplan") / [8.0](/docs/8.0/spi-spi-saveplan.html "PostgreSQL 8.0 -
SPI_saveplan") / [7.4](/docs/7.4/spi-spi-saveplan.html "PostgreSQL 7.4 -
SPI_saveplan")

__

SPI_saveplan  
---  
[Prev](spi-spi-keepplan.html "SPI_keepplan")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-register-relation.html "SPI_register_relation")  
  
* * *

## SPI_saveplan

SPI_saveplan — save a prepared statement

## Synopsis

    
    
    SPIPlanPtr SPI_saveplan(SPIPlanPtr _plan_)
    

## Description

`SPI_saveplan` copies a passed statement (prepared by `SPI_prepare`) into
memory that will not be freed by `SPI_finish` nor by the transaction manager,
and returns a pointer to the copied statement. This gives you the ability to
reuse prepared statements in the subsequent invocations of your C function in
the current session.

## Arguments

`SPIPlanPtr _`plan`_`

    

the prepared statement to be saved

## Return Value

Pointer to the copied statement; or `NULL` if unsuccessful. On error,
`SPI_result` is set thus:

`SPI_ERROR_ARGUMENT`

    

if _`plan`_ is `NULL` or invalid

`SPI_ERROR_UNCONNECTED`

    

if called from an unconnected C function

## Notes

The originally passed-in statement is not freed, so you might wish to do
`SPI_freeplan` on it to avoid leaking memory until `SPI_finish`.

In most cases, `SPI_keepplan` is preferred to this function, since it
accomplishes largely the same result without needing to physically copy the
prepared statement's data structures.

* * *

[Prev](spi-spi-keepplan.html "SPI_keepplan")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-register-relation.html "SPI_register_relation")  
---|---|---  
SPI_keepplan  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_register_relation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-saveplan.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

