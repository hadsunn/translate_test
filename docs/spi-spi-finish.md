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

Supported Versions: [Current](/docs/current/spi-spi-finish.html "PostgreSQL 17
- SPI_finish") ([17](/docs/17/spi-spi-finish.html "PostgreSQL 17 -
SPI_finish")) / [16](/docs/16/spi-spi-finish.html "PostgreSQL 16 -
SPI_finish") / [15](/docs/15/spi-spi-finish.html "PostgreSQL 15 - SPI_finish")
/ [14](/docs/14/spi-spi-finish.html "PostgreSQL 14 - SPI_finish") /
[13](/docs/13/spi-spi-finish.html "PostgreSQL 13 - SPI_finish")

Development Versions: [18](/docs/18/spi-spi-finish.html "PostgreSQL 18 -
SPI_finish") / [devel](/docs/devel/spi-spi-finish.html "PostgreSQL devel -
SPI_finish")

Unsupported versions: [12](/docs/12/spi-spi-finish.html "PostgreSQL 12 -
SPI_finish") / [11](/docs/11/spi-spi-finish.html "PostgreSQL 11 - SPI_finish")
/ [10](/docs/10/spi-spi-finish.html "PostgreSQL 10 - SPI_finish") /
[9.6](/docs/9.6/spi-spi-finish.html "PostgreSQL 9.6 - SPI_finish") /
[9.5](/docs/9.5/spi-spi-finish.html "PostgreSQL 9.5 - SPI_finish") /
[9.4](/docs/9.4/spi-spi-finish.html "PostgreSQL 9.4 - SPI_finish") /
[9.3](/docs/9.3/spi-spi-finish.html "PostgreSQL 9.3 - SPI_finish") /
[9.2](/docs/9.2/spi-spi-finish.html "PostgreSQL 9.2 - SPI_finish") /
[9.1](/docs/9.1/spi-spi-finish.html "PostgreSQL 9.1 - SPI_finish") /
[9.0](/docs/9.0/spi-spi-finish.html "PostgreSQL 9.0 - SPI_finish") /
[8.4](/docs/8.4/spi-spi-finish.html "PostgreSQL 8.4 - SPI_finish") /
[8.3](/docs/8.3/spi-spi-finish.html "PostgreSQL 8.3 - SPI_finish") /
[8.2](/docs/8.2/spi-spi-finish.html "PostgreSQL 8.2 - SPI_finish") /
[8.1](/docs/8.1/spi-spi-finish.html "PostgreSQL 8.1 - SPI_finish") /
[8.0](/docs/8.0/spi-spi-finish.html "PostgreSQL 8.0 - SPI_finish") /
[7.4](/docs/7.4/spi-spi-finish.html "PostgreSQL 7.4 - SPI_finish")

__

SPI_finish  
---  
[Prev](spi-spi-connect.html "SPI_connect")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-execute.html "SPI_execute")  
  
* * *

## SPI_finish

SPI_finish — disconnect a C function from the SPI manager

## Synopsis

    
    
    int SPI_finish(void)
    

## Description

`SPI_finish` closes an existing connection to the SPI manager. You must call
this function after completing the SPI operations needed during your C
function's current invocation. You do not need to worry about making this
happen, however, if you abort the transaction via `elog(ERROR)`. In that case
SPI will clean itself up automatically.

## Return Value

`SPI_OK_FINISH`

    

if properly disconnected

`SPI_ERROR_UNCONNECTED`

    

if called from an unconnected C function

* * *

[Prev](spi-spi-connect.html "SPI_connect")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-execute.html "SPI_execute")  
---|---|---  
SPI_connect  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_execute  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-finish.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

