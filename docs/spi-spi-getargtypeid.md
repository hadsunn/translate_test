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

Supported Versions: [Current](/docs/current/spi-spi-getargtypeid.html
"PostgreSQL 17 - SPI_getargtypeid") ([17](/docs/17/spi-spi-getargtypeid.html
"PostgreSQL 17 - SPI_getargtypeid")) / [16](/docs/16/spi-spi-getargtypeid.html
"PostgreSQL 16 - SPI_getargtypeid") / [15](/docs/15/spi-spi-getargtypeid.html
"PostgreSQL 15 - SPI_getargtypeid") / [14](/docs/14/spi-spi-getargtypeid.html
"PostgreSQL 14 - SPI_getargtypeid") / [13](/docs/13/spi-spi-getargtypeid.html
"PostgreSQL 13 - SPI_getargtypeid")

Development Versions: [18](/docs/18/spi-spi-getargtypeid.html "PostgreSQL 18 -
SPI_getargtypeid") / [devel](/docs/devel/spi-spi-getargtypeid.html "PostgreSQL
devel - SPI_getargtypeid")

Unsupported versions: [12](/docs/12/spi-spi-getargtypeid.html "PostgreSQL 12 -
SPI_getargtypeid") / [11](/docs/11/spi-spi-getargtypeid.html "PostgreSQL 11 -
SPI_getargtypeid") / [10](/docs/10/spi-spi-getargtypeid.html "PostgreSQL 10 -
SPI_getargtypeid") / [9.6](/docs/9.6/spi-spi-getargtypeid.html "PostgreSQL 9.6
- SPI_getargtypeid") / [9.5](/docs/9.5/spi-spi-getargtypeid.html "PostgreSQL
9.5 - SPI_getargtypeid") / [9.4](/docs/9.4/spi-spi-getargtypeid.html
"PostgreSQL 9.4 - SPI_getargtypeid") / [9.3](/docs/9.3/spi-spi-
getargtypeid.html "PostgreSQL 9.3 - SPI_getargtypeid") / [9.2](/docs/9.2/spi-
spi-getargtypeid.html "PostgreSQL 9.2 - SPI_getargtypeid") /
[9.1](/docs/9.1/spi-spi-getargtypeid.html "PostgreSQL 9.1 - SPI_getargtypeid")
/ [9.0](/docs/9.0/spi-spi-getargtypeid.html "PostgreSQL 9.0 -
SPI_getargtypeid") / [8.4](/docs/8.4/spi-spi-getargtypeid.html "PostgreSQL 8.4
- SPI_getargtypeid") / [8.3](/docs/8.3/spi-spi-getargtypeid.html "PostgreSQL
8.3 - SPI_getargtypeid") / [8.2](/docs/8.2/spi-spi-getargtypeid.html
"PostgreSQL 8.2 - SPI_getargtypeid") / [8.1](/docs/8.1/spi-spi-
getargtypeid.html "PostgreSQL 8.1 - SPI_getargtypeid") / [8.0](/docs/8.0/spi-
spi-getargtypeid.html "PostgreSQL 8.0 - SPI_getargtypeid")

__

SPI_getargtypeid  
---  
[Prev](spi-spi-getargcount.html "SPI_getargcount")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-is-cursor-plan.html "SPI_is_cursor_plan")  
  
* * *

## SPI_getargtypeid

SPI_getargtypeid — return the data type OID for an argument of a statement
prepared by `SPI_prepare`

## Synopsis

    
    
    Oid SPI_getargtypeid(SPIPlanPtr _plan_ , int _argIndex_)
    

## Description

`SPI_getargtypeid` returns the OID representing the type for the _`argIndex`_
'th argument of a statement prepared by `SPI_prepare`. First argument is at
index zero.

## Arguments

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

`int _`argIndex`_`

    

zero based index of the argument

## Return Value

The type OID of the argument at the given index. If the _`plan`_ is `NULL` or
invalid, or _`argIndex`_ is less than 0 or not less than the number of
arguments declared for the _`plan`_ , `SPI_result` is set to
`SPI_ERROR_ARGUMENT` and `InvalidOid` is returned.

* * *

[Prev](spi-spi-getargcount.html "SPI_getargcount")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-is-cursor-plan.html "SPI_is_cursor_plan")  
---|---|---  
SPI_getargcount  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_is_cursor_plan  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-getargtypeid.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

