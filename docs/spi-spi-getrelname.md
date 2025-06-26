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

Supported Versions: [Current](/docs/current/spi-spi-getrelname.html
"PostgreSQL 17 - SPI_getrelname") ([17](/docs/17/spi-spi-getrelname.html
"PostgreSQL 17 - SPI_getrelname")) / [16](/docs/16/spi-spi-getrelname.html
"PostgreSQL 16 - SPI_getrelname") / [15](/docs/15/spi-spi-getrelname.html
"PostgreSQL 15 - SPI_getrelname") / [14](/docs/14/spi-spi-getrelname.html
"PostgreSQL 14 - SPI_getrelname") / [13](/docs/13/spi-spi-getrelname.html
"PostgreSQL 13 - SPI_getrelname")

Development Versions: [18](/docs/18/spi-spi-getrelname.html "PostgreSQL 18 -
SPI_getrelname") / [devel](/docs/devel/spi-spi-getrelname.html "PostgreSQL
devel - SPI_getrelname")

Unsupported versions: [12](/docs/12/spi-spi-getrelname.html "PostgreSQL 12 -
SPI_getrelname") / [11](/docs/11/spi-spi-getrelname.html "PostgreSQL 11 -
SPI_getrelname") / [10](/docs/10/spi-spi-getrelname.html "PostgreSQL 10 -
SPI_getrelname") / [9.6](/docs/9.6/spi-spi-getrelname.html "PostgreSQL 9.6 -
SPI_getrelname") / [9.5](/docs/9.5/spi-spi-getrelname.html "PostgreSQL 9.5 -
SPI_getrelname") / [9.4](/docs/9.4/spi-spi-getrelname.html "PostgreSQL 9.4 -
SPI_getrelname") / [9.3](/docs/9.3/spi-spi-getrelname.html "PostgreSQL 9.3 -
SPI_getrelname") / [9.2](/docs/9.2/spi-spi-getrelname.html "PostgreSQL 9.2 -
SPI_getrelname") / [9.1](/docs/9.1/spi-spi-getrelname.html "PostgreSQL 9.1 -
SPI_getrelname") / [9.0](/docs/9.0/spi-spi-getrelname.html "PostgreSQL 9.0 -
SPI_getrelname") / [8.4](/docs/8.4/spi-spi-getrelname.html "PostgreSQL 8.4 -
SPI_getrelname") / [8.3](/docs/8.3/spi-spi-getrelname.html "PostgreSQL 8.3 -
SPI_getrelname") / [8.2](/docs/8.2/spi-spi-getrelname.html "PostgreSQL 8.2 -
SPI_getrelname") / [8.1](/docs/8.1/spi-spi-getrelname.html "PostgreSQL 8.1 -
SPI_getrelname") / [8.0](/docs/8.0/spi-spi-getrelname.html "PostgreSQL 8.0 -
SPI_getrelname") / [7.4](/docs/7.4/spi-spi-getrelname.html "PostgreSQL 7.4 -
SPI_getrelname")

__

SPI_getrelname  
---  
[Prev](spi-spi-gettypeid.html "SPI_gettypeid")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") | 47.2. Interface Support Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-getnspname.html "SPI_getnspname")  
  
* * *

## SPI_getrelname

SPI_getrelname — return the name of the specified relation

## Synopsis

    
    
    char * SPI_getrelname(Relation _rel_)
    

## Description

`SPI_getrelname` returns a copy of the name of the specified relation. (You
can use `pfree` to release the copy of the name when you don't need it
anymore.)

## Arguments

`Relation _`rel`_`

    

input relation

## Return Value

The name of the specified relation.

* * *

[Prev](spi-spi-gettypeid.html "SPI_gettypeid")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") |  [Next](spi-spi-getnspname.html "SPI_getnspname")  
---|---|---  
SPI_gettypeid  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_getnspname  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-getrelname.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

