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

Supported Versions: [Current](/docs/current/spi-spi-gettype.html "PostgreSQL
17 - SPI_gettype") ([17](/docs/17/spi-spi-gettype.html "PostgreSQL 17 -
SPI_gettype")) / [16](/docs/16/spi-spi-gettype.html "PostgreSQL 16 -
SPI_gettype") / [15](/docs/15/spi-spi-gettype.html "PostgreSQL 15 -
SPI_gettype") / [14](/docs/14/spi-spi-gettype.html "PostgreSQL 14 -
SPI_gettype") / [13](/docs/13/spi-spi-gettype.html "PostgreSQL 13 -
SPI_gettype")

Development Versions: [18](/docs/18/spi-spi-gettype.html "PostgreSQL 18 -
SPI_gettype") / [devel](/docs/devel/spi-spi-gettype.html "PostgreSQL devel -
SPI_gettype")

Unsupported versions: [12](/docs/12/spi-spi-gettype.html "PostgreSQL 12 -
SPI_gettype") / [11](/docs/11/spi-spi-gettype.html "PostgreSQL 11 -
SPI_gettype") / [10](/docs/10/spi-spi-gettype.html "PostgreSQL 10 -
SPI_gettype") / [9.6](/docs/9.6/spi-spi-gettype.html "PostgreSQL 9.6 -
SPI_gettype") / [9.5](/docs/9.5/spi-spi-gettype.html "PostgreSQL 9.5 -
SPI_gettype") / [9.4](/docs/9.4/spi-spi-gettype.html "PostgreSQL 9.4 -
SPI_gettype") / [9.3](/docs/9.3/spi-spi-gettype.html "PostgreSQL 9.3 -
SPI_gettype") / [9.2](/docs/9.2/spi-spi-gettype.html "PostgreSQL 9.2 -
SPI_gettype") / [9.1](/docs/9.1/spi-spi-gettype.html "PostgreSQL 9.1 -
SPI_gettype") / [9.0](/docs/9.0/spi-spi-gettype.html "PostgreSQL 9.0 -
SPI_gettype") / [8.4](/docs/8.4/spi-spi-gettype.html "PostgreSQL 8.4 -
SPI_gettype") / [8.3](/docs/8.3/spi-spi-gettype.html "PostgreSQL 8.3 -
SPI_gettype") / [8.2](/docs/8.2/spi-spi-gettype.html "PostgreSQL 8.2 -
SPI_gettype") / [8.1](/docs/8.1/spi-spi-gettype.html "PostgreSQL 8.1 -
SPI_gettype") / [8.0](/docs/8.0/spi-spi-gettype.html "PostgreSQL 8.0 -
SPI_gettype") / [7.4](/docs/7.4/spi-spi-gettype.html "PostgreSQL 7.4 -
SPI_gettype")

__

SPI_gettype  
---  
[Prev](spi-spi-getbinval.html "SPI_getbinval")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") | 47.2. Interface Support Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-gettypeid.html "SPI_gettypeid")  
  
* * *

## SPI_gettype

SPI_gettype — return the data type name of the specified column

## Synopsis

    
    
    char * SPI_gettype(TupleDesc _rowdesc_ , int _colnumber_)
    

## Description

`SPI_gettype` returns a copy of the data type name of the specified column.
(You can use `pfree` to release the copy of the name when you don't need it
anymore.)

## Arguments

`TupleDesc _`rowdesc`_`

    

input row description

`int _`colnumber`_`

    

column number (count starts at 1)

## Return Value

The data type name of the specified column, or `NULL` on error. `SPI_result`
is set to `SPI_ERROR_NOATTRIBUTE` on error.

* * *

[Prev](spi-spi-getbinval.html "SPI_getbinval")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") |  [Next](spi-spi-gettypeid.html "SPI_gettypeid")  
---|---|---  
SPI_getbinval  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_gettypeid  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-gettype.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

