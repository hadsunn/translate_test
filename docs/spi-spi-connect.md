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

Supported Versions: [Current](/docs/current/spi-spi-connect.html "PostgreSQL
17 - SPI_connect") ([17](/docs/17/spi-spi-connect.html "PostgreSQL 17 -
SPI_connect")) / [16](/docs/16/spi-spi-connect.html "PostgreSQL 16 -
SPI_connect") / [15](/docs/15/spi-spi-connect.html "PostgreSQL 15 -
SPI_connect") / [14](/docs/14/spi-spi-connect.html "PostgreSQL 14 -
SPI_connect") / [13](/docs/13/spi-spi-connect.html "PostgreSQL 13 -
SPI_connect")

Development Versions: [18](/docs/18/spi-spi-connect.html "PostgreSQL 18 -
SPI_connect") / [devel](/docs/devel/spi-spi-connect.html "PostgreSQL devel -
SPI_connect")

Unsupported versions: [12](/docs/12/spi-spi-connect.html "PostgreSQL 12 -
SPI_connect") / [11](/docs/11/spi-spi-connect.html "PostgreSQL 11 -
SPI_connect") / [10](/docs/10/spi-spi-connect.html "PostgreSQL 10 -
SPI_connect") / [9.6](/docs/9.6/spi-spi-connect.html "PostgreSQL 9.6 -
SPI_connect") / [9.5](/docs/9.5/spi-spi-connect.html "PostgreSQL 9.5 -
SPI_connect") / [9.4](/docs/9.4/spi-spi-connect.html "PostgreSQL 9.4 -
SPI_connect") / [9.3](/docs/9.3/spi-spi-connect.html "PostgreSQL 9.3 -
SPI_connect") / [9.2](/docs/9.2/spi-spi-connect.html "PostgreSQL 9.2 -
SPI_connect") / [9.1](/docs/9.1/spi-spi-connect.html "PostgreSQL 9.1 -
SPI_connect") / [9.0](/docs/9.0/spi-spi-connect.html "PostgreSQL 9.0 -
SPI_connect") / [8.4](/docs/8.4/spi-spi-connect.html "PostgreSQL 8.4 -
SPI_connect") / [8.3](/docs/8.3/spi-spi-connect.html "PostgreSQL 8.3 -
SPI_connect") / [8.2](/docs/8.2/spi-spi-connect.html "PostgreSQL 8.2 -
SPI_connect") / [8.1](/docs/8.1/spi-spi-connect.html "PostgreSQL 8.1 -
SPI_connect") / [8.0](/docs/8.0/spi-spi-connect.html "PostgreSQL 8.0 -
SPI_connect") / [7.4](/docs/7.4/spi-spi-connect.html "PostgreSQL 7.4 -
SPI_connect")

__

SPI_connect  
---  
[Prev](spi-interface.html "47.1. Interface Functions")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-finish.html "SPI_finish")  
  
* * *

## SPI_connect

SPI_connect, SPI_connect_ext — connect a C function to the SPI manager

## Synopsis

    
    
    int SPI_connect(void)
    
    
    
    int SPI_connect_ext(int _options_)
    

## Description

`SPI_connect` opens a connection from a C function invocation to the SPI
manager. You must call this function if you want to execute commands through
SPI. Some utility SPI functions can be called from unconnected C functions.

`SPI_connect_ext` does the same but has an argument that allows passing option
flags. Currently, the following option values are available:

`SPI_OPT_NONATOMIC`

    

Sets the SPI connection to be _nonatomic_ , which means that transaction
control calls (`SPI_commit`, `SPI_rollback`) are allowed. Otherwise, calling
those functions will result in an immediate error.

`SPI_connect()` is equivalent to `SPI_connect_ext(0)`.

## Return Value

`SPI_OK_CONNECT`

    

on success

`SPI_ERROR_CONNECT`

    

on error

* * *

[Prev](spi-interface.html "47.1. Interface Functions")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-finish.html "SPI_finish")  
---|---|---  
47.1. Interface Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_finish  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-connect.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

