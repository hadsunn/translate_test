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

Supported Versions: [Current](/docs/current/spi-spi-fnumber.html "PostgreSQL
17 - SPI_fnumber") ([17](/docs/17/spi-spi-fnumber.html "PostgreSQL 17 -
SPI_fnumber")) / [16](/docs/16/spi-spi-fnumber.html "PostgreSQL 16 -
SPI_fnumber") / [15](/docs/15/spi-spi-fnumber.html "PostgreSQL 15 -
SPI_fnumber") / [14](/docs/14/spi-spi-fnumber.html "PostgreSQL 14 -
SPI_fnumber") / [13](/docs/13/spi-spi-fnumber.html "PostgreSQL 13 -
SPI_fnumber")

Development Versions: [18](/docs/18/spi-spi-fnumber.html "PostgreSQL 18 -
SPI_fnumber") / [devel](/docs/devel/spi-spi-fnumber.html "PostgreSQL devel -
SPI_fnumber")

Unsupported versions: [12](/docs/12/spi-spi-fnumber.html "PostgreSQL 12 -
SPI_fnumber") / [11](/docs/11/spi-spi-fnumber.html "PostgreSQL 11 -
SPI_fnumber") / [10](/docs/10/spi-spi-fnumber.html "PostgreSQL 10 -
SPI_fnumber") / [9.6](/docs/9.6/spi-spi-fnumber.html "PostgreSQL 9.6 -
SPI_fnumber") / [9.5](/docs/9.5/spi-spi-fnumber.html "PostgreSQL 9.5 -
SPI_fnumber") / [9.4](/docs/9.4/spi-spi-fnumber.html "PostgreSQL 9.4 -
SPI_fnumber") / [9.3](/docs/9.3/spi-spi-fnumber.html "PostgreSQL 9.3 -
SPI_fnumber") / [9.2](/docs/9.2/spi-spi-fnumber.html "PostgreSQL 9.2 -
SPI_fnumber") / [9.1](/docs/9.1/spi-spi-fnumber.html "PostgreSQL 9.1 -
SPI_fnumber") / [9.0](/docs/9.0/spi-spi-fnumber.html "PostgreSQL 9.0 -
SPI_fnumber") / [8.4](/docs/8.4/spi-spi-fnumber.html "PostgreSQL 8.4 -
SPI_fnumber") / [8.3](/docs/8.3/spi-spi-fnumber.html "PostgreSQL 8.3 -
SPI_fnumber") / [8.2](/docs/8.2/spi-spi-fnumber.html "PostgreSQL 8.2 -
SPI_fnumber") / [8.1](/docs/8.1/spi-spi-fnumber.html "PostgreSQL 8.1 -
SPI_fnumber") / [8.0](/docs/8.0/spi-spi-fnumber.html "PostgreSQL 8.0 -
SPI_fnumber") / [7.4](/docs/7.4/spi-spi-fnumber.html "PostgreSQL 7.4 -
SPI_fnumber")

__

SPI_fnumber  
---  
[Prev](spi-spi-fname.html "SPI_fname")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") | 47.2. Interface Support Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-getvalue.html "SPI_getvalue")  
  
* * *

## SPI_fnumber

SPI_fnumber — determine the column number for the specified column name

## Synopsis

    
    
    int SPI_fnumber(TupleDesc _rowdesc_ , const char * _colname_)
    

## Description

`SPI_fnumber` returns the column number for the column with the specified
name.

If _`colname`_ refers to a system column (e.g., `ctid`) then the appropriate
negative column number will be returned. The caller should be careful to test
the return value for exact equality to `SPI_ERROR_NOATTRIBUTE` to detect an
error; testing the result for less than or equal to 0 is not correct unless
system columns should be rejected.

## Arguments

`TupleDesc _`rowdesc`_`

    

input row description

`const char * _`colname`_`

    

column name

## Return Value

Column number (count starts at 1 for user-defined columns), or
`SPI_ERROR_NOATTRIBUTE` if the named column was not found.

* * *

[Prev](spi-spi-fname.html "SPI_fname")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") |  [Next](spi-spi-getvalue.html "SPI_getvalue")  
---|---|---  
SPI_fname  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_getvalue  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-fnumber.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

