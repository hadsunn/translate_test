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

Supported Versions: [Current](/docs/current/spi-spi-getbinval.html "PostgreSQL
17 - SPI_getbinval") ([17](/docs/17/spi-spi-getbinval.html "PostgreSQL 17 -
SPI_getbinval")) / [16](/docs/16/spi-spi-getbinval.html "PostgreSQL 16 -
SPI_getbinval") / [15](/docs/15/spi-spi-getbinval.html "PostgreSQL 15 -
SPI_getbinval") / [14](/docs/14/spi-spi-getbinval.html "PostgreSQL 14 -
SPI_getbinval") / [13](/docs/13/spi-spi-getbinval.html "PostgreSQL 13 -
SPI_getbinval")

Development Versions: [18](/docs/18/spi-spi-getbinval.html "PostgreSQL 18 -
SPI_getbinval") / [devel](/docs/devel/spi-spi-getbinval.html "PostgreSQL devel
- SPI_getbinval")

Unsupported versions: [12](/docs/12/spi-spi-getbinval.html "PostgreSQL 12 -
SPI_getbinval") / [11](/docs/11/spi-spi-getbinval.html "PostgreSQL 11 -
SPI_getbinval") / [10](/docs/10/spi-spi-getbinval.html "PostgreSQL 10 -
SPI_getbinval") / [9.6](/docs/9.6/spi-spi-getbinval.html "PostgreSQL 9.6 -
SPI_getbinval") / [9.5](/docs/9.5/spi-spi-getbinval.html "PostgreSQL 9.5 -
SPI_getbinval") / [9.4](/docs/9.4/spi-spi-getbinval.html "PostgreSQL 9.4 -
SPI_getbinval") / [9.3](/docs/9.3/spi-spi-getbinval.html "PostgreSQL 9.3 -
SPI_getbinval") / [9.2](/docs/9.2/spi-spi-getbinval.html "PostgreSQL 9.2 -
SPI_getbinval") / [9.1](/docs/9.1/spi-spi-getbinval.html "PostgreSQL 9.1 -
SPI_getbinval") / [9.0](/docs/9.0/spi-spi-getbinval.html "PostgreSQL 9.0 -
SPI_getbinval") / [8.4](/docs/8.4/spi-spi-getbinval.html "PostgreSQL 8.4 -
SPI_getbinval") / [8.3](/docs/8.3/spi-spi-getbinval.html "PostgreSQL 8.3 -
SPI_getbinval") / [8.2](/docs/8.2/spi-spi-getbinval.html "PostgreSQL 8.2 -
SPI_getbinval") / [8.1](/docs/8.1/spi-spi-getbinval.html "PostgreSQL 8.1 -
SPI_getbinval") / [8.0](/docs/8.0/spi-spi-getbinval.html "PostgreSQL 8.0 -
SPI_getbinval") / [7.4](/docs/7.4/spi-spi-getbinval.html "PostgreSQL 7.4 -
SPI_getbinval")

__

SPI_getbinval  
---  
[Prev](spi-spi-getvalue.html "SPI_getvalue")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") | 47.2. Interface Support Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-gettype.html "SPI_gettype")  
  
* * *

## SPI_getbinval

SPI_getbinval — return the binary value of the specified column

## Synopsis

    
    
    Datum SPI_getbinval(HeapTuple _row_ , TupleDesc _rowdesc_ , int _colnumber_ ,
                        bool * _isnull_)
    

## Description

`SPI_getbinval` returns the value of the specified column in the internal form
(as type `Datum`).

This function does not allocate new space for the datum. In the case of a
pass-by-reference data type, the return value will be a pointer into the
passed row.

## Arguments

`HeapTuple _`row`_`

    

input row to be examined

`TupleDesc _`rowdesc`_`

    

input row description

`int _`colnumber`_`

    

column number (count starts at 1)

`bool * _`isnull`_`

    

flag for a null value in the column

## Return Value

The binary value of the column is returned. The variable pointed to by
_`isnull`_ is set to true if the column is null, else to false.

`SPI_result` is set to `SPI_ERROR_NOATTRIBUTE` on error.

* * *

[Prev](spi-spi-getvalue.html "SPI_getvalue")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") |  [Next](spi-spi-gettype.html "SPI_gettype")  
---|---|---  
SPI_getvalue  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_gettype  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-getbinval.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

