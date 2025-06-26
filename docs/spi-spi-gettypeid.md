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

Supported Versions: [Current](/docs/current/spi-spi-gettypeid.html "PostgreSQL
17 - SPI_gettypeid") ([17](/docs/17/spi-spi-gettypeid.html "PostgreSQL 17 -
SPI_gettypeid")) / [16](/docs/16/spi-spi-gettypeid.html "PostgreSQL 16 -
SPI_gettypeid") / [15](/docs/15/spi-spi-gettypeid.html "PostgreSQL 15 -
SPI_gettypeid") / [14](/docs/14/spi-spi-gettypeid.html "PostgreSQL 14 -
SPI_gettypeid") / [13](/docs/13/spi-spi-gettypeid.html "PostgreSQL 13 -
SPI_gettypeid")

Development Versions: [18](/docs/18/spi-spi-gettypeid.html "PostgreSQL 18 -
SPI_gettypeid") / [devel](/docs/devel/spi-spi-gettypeid.html "PostgreSQL devel
- SPI_gettypeid")

Unsupported versions: [12](/docs/12/spi-spi-gettypeid.html "PostgreSQL 12 -
SPI_gettypeid") / [11](/docs/11/spi-spi-gettypeid.html "PostgreSQL 11 -
SPI_gettypeid") / [10](/docs/10/spi-spi-gettypeid.html "PostgreSQL 10 -
SPI_gettypeid") / [9.6](/docs/9.6/spi-spi-gettypeid.html "PostgreSQL 9.6 -
SPI_gettypeid") / [9.5](/docs/9.5/spi-spi-gettypeid.html "PostgreSQL 9.5 -
SPI_gettypeid") / [9.4](/docs/9.4/spi-spi-gettypeid.html "PostgreSQL 9.4 -
SPI_gettypeid") / [9.3](/docs/9.3/spi-spi-gettypeid.html "PostgreSQL 9.3 -
SPI_gettypeid") / [9.2](/docs/9.2/spi-spi-gettypeid.html "PostgreSQL 9.2 -
SPI_gettypeid") / [9.1](/docs/9.1/spi-spi-gettypeid.html "PostgreSQL 9.1 -
SPI_gettypeid") / [9.0](/docs/9.0/spi-spi-gettypeid.html "PostgreSQL 9.0 -
SPI_gettypeid") / [8.4](/docs/8.4/spi-spi-gettypeid.html "PostgreSQL 8.4 -
SPI_gettypeid") / [8.3](/docs/8.3/spi-spi-gettypeid.html "PostgreSQL 8.3 -
SPI_gettypeid") / [8.2](/docs/8.2/spi-spi-gettypeid.html "PostgreSQL 8.2 -
SPI_gettypeid") / [8.1](/docs/8.1/spi-spi-gettypeid.html "PostgreSQL 8.1 -
SPI_gettypeid") / [8.0](/docs/8.0/spi-spi-gettypeid.html "PostgreSQL 8.0 -
SPI_gettypeid") / [7.4](/docs/7.4/spi-spi-gettypeid.html "PostgreSQL 7.4 -
SPI_gettypeid")

__

SPI_gettypeid  
---  
[Prev](spi-spi-gettype.html "SPI_gettype")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") | 47.2. Interface Support Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-getrelname.html "SPI_getrelname")  
  
* * *

## SPI_gettypeid

SPI_gettypeid — return the data type OID of the specified column

## Synopsis

    
    
    Oid SPI_gettypeid(TupleDesc _rowdesc_ , int _colnumber_)
    

## Description

`SPI_gettypeid` returns the OID of the data type of the specified column.

## Arguments

`TupleDesc _`rowdesc`_`

    

input row description

`int _`colnumber`_`

    

column number (count starts at 1)

## Return Value

The OID of the data type of the specified column or `InvalidOid` on error. On
error, `SPI_result` is set to `SPI_ERROR_NOATTRIBUTE`.

* * *

[Prev](spi-spi-gettype.html "SPI_gettype")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") |  [Next](spi-spi-getrelname.html "SPI_getrelname")  
---|---|---  
SPI_gettype  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_getrelname  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-gettypeid.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

