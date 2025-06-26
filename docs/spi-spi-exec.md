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

Supported Versions: [Current](/docs/current/spi-spi-exec.html "PostgreSQL 17 -
SPI_exec") ([17](/docs/17/spi-spi-exec.html "PostgreSQL 17 - SPI_exec")) /
[16](/docs/16/spi-spi-exec.html "PostgreSQL 16 - SPI_exec") /
[15](/docs/15/spi-spi-exec.html "PostgreSQL 15 - SPI_exec") /
[14](/docs/14/spi-spi-exec.html "PostgreSQL 14 - SPI_exec") /
[13](/docs/13/spi-spi-exec.html "PostgreSQL 13 - SPI_exec")

Development Versions: [18](/docs/18/spi-spi-exec.html "PostgreSQL 18 -
SPI_exec") / [devel](/docs/devel/spi-spi-exec.html "PostgreSQL devel -
SPI_exec")

Unsupported versions: [12](/docs/12/spi-spi-exec.html "PostgreSQL 12 -
SPI_exec") / [11](/docs/11/spi-spi-exec.html "PostgreSQL 11 - SPI_exec") /
[10](/docs/10/spi-spi-exec.html "PostgreSQL 10 - SPI_exec") /
[9.6](/docs/9.6/spi-spi-exec.html "PostgreSQL 9.6 - SPI_exec") /
[9.5](/docs/9.5/spi-spi-exec.html "PostgreSQL 9.5 - SPI_exec") /
[9.4](/docs/9.4/spi-spi-exec.html "PostgreSQL 9.4 - SPI_exec") /
[9.3](/docs/9.3/spi-spi-exec.html "PostgreSQL 9.3 - SPI_exec") /
[9.2](/docs/9.2/spi-spi-exec.html "PostgreSQL 9.2 - SPI_exec") /
[9.1](/docs/9.1/spi-spi-exec.html "PostgreSQL 9.1 - SPI_exec") /
[9.0](/docs/9.0/spi-spi-exec.html "PostgreSQL 9.0 - SPI_exec") /
[8.4](/docs/8.4/spi-spi-exec.html "PostgreSQL 8.4 - SPI_exec") /
[8.3](/docs/8.3/spi-spi-exec.html "PostgreSQL 8.3 - SPI_exec") /
[8.2](/docs/8.2/spi-spi-exec.html "PostgreSQL 8.2 - SPI_exec") /
[8.1](/docs/8.1/spi-spi-exec.html "PostgreSQL 8.1 - SPI_exec") /
[8.0](/docs/8.0/spi-spi-exec.html "PostgreSQL 8.0 - SPI_exec") /
[7.4](/docs/7.4/spi-spi-exec.html "PostgreSQL 7.4 - SPI_exec")

__

SPI_exec  
---  
[Prev](spi-spi-execute.html "SPI_execute")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-execute-extended.html "SPI_execute_extended")  
  
* * *

## SPI_exec

SPI_exec — execute a read/write command

## Synopsis

    
    
    int SPI_exec(const char * _command_ , long _count_)
    

## Description

`SPI_exec` is the same as `SPI_execute`, with the latter's _`read_only`_
parameter always taken as `false`.

## Arguments

`const char * _`command`_`

    

string containing command to execute

`long _`count`_`

    

maximum number of rows to return, or `0` for no limit

## Return Value

See `SPI_execute`.

* * *

[Prev](spi-spi-execute.html "SPI_execute")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-execute-extended.html "SPI_execute_extended")  
---|---|---  
SPI_execute  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_execute_extended  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-exec.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

