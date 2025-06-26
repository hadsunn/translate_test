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

Supported Versions: [Current](/docs/current/spi-spi-result-code-string.html
"PostgreSQL 17 - SPI_result_code_string") ([17](/docs/17/spi-spi-result-code-
string.html "PostgreSQL 17 - SPI_result_code_string")) / [16](/docs/16/spi-
spi-result-code-string.html "PostgreSQL 16 - SPI_result_code_string") /
[15](/docs/15/spi-spi-result-code-string.html "PostgreSQL 15 -
SPI_result_code_string") / [14](/docs/14/spi-spi-result-code-string.html
"PostgreSQL 14 - SPI_result_code_string") / [13](/docs/13/spi-spi-result-code-
string.html "PostgreSQL 13 - SPI_result_code_string")

Development Versions: [18](/docs/18/spi-spi-result-code-string.html
"PostgreSQL 18 - SPI_result_code_string") / [devel](/docs/devel/spi-spi-
result-code-string.html "PostgreSQL devel - SPI_result_code_string")

Unsupported versions: [12](/docs/12/spi-spi-result-code-string.html
"PostgreSQL 12 - SPI_result_code_string") / [11](/docs/11/spi-spi-result-code-
string.html "PostgreSQL 11 - SPI_result_code_string")

__

SPI_result_code_string  
---  
[Prev](spi-spi-getnspname.html "SPI_getnspname")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") | 47.2. Interface Support Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-memory.html "47.3. Memory Management")  
  
* * *

## SPI_result_code_string

SPI_result_code_string — return error code as string

## Synopsis

    
    
    const char * SPI_result_code_string(int _code_);
    

## Description

`SPI_result_code_string` returns a string representation of the result code
returned by various SPI functions or stored in `SPI_result`.

## Arguments

`int _`code`_`

    

result code

## Return Value

A string representation of the result code.

* * *

[Prev](spi-spi-getnspname.html "SPI_getnspname")  | [Up](spi-interface-support.html "47.2. Interface Support Functions") |  [Next](spi-memory.html "47.3. Memory Management")  
---|---|---  
SPI_getnspname  | [Home](index.html "PostgreSQL 16.9 Documentation") |  47.3. Memory Management  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-result-code-
string.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

