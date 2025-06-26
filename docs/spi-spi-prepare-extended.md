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

Supported Versions: [Current](/docs/current/spi-spi-prepare-extended.html
"PostgreSQL 17 - SPI_prepare_extended") ([17](/docs/17/spi-spi-prepare-
extended.html "PostgreSQL 17 - SPI_prepare_extended")) / [16](/docs/16/spi-
spi-prepare-extended.html "PostgreSQL 16 - SPI_prepare_extended") /
[15](/docs/15/spi-spi-prepare-extended.html "PostgreSQL 15 -
SPI_prepare_extended") / [14](/docs/14/spi-spi-prepare-extended.html
"PostgreSQL 14 - SPI_prepare_extended")

Development Versions: [18](/docs/18/spi-spi-prepare-extended.html "PostgreSQL
18 - SPI_prepare_extended") / [devel](/docs/devel/spi-spi-prepare-
extended.html "PostgreSQL devel - SPI_prepare_extended")

__

SPI_prepare_extended  
---  
[Prev](spi-spi-prepare-cursor.html "SPI_prepare_cursor")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-prepare-params.html "SPI_prepare_params")  
  
* * *

## SPI_prepare_extended

SPI_prepare_extended — prepare a statement, without executing it yet

## Synopsis

    
    
    SPIPlanPtr SPI_prepare_extended(const char * _command_ ,
                                    const SPIPrepareOptions * _options_)
    

## Description

`SPI_prepare_extended` creates and returns a prepared statement for the
specified command, but doesn't execute the command. This function is
equivalent to `SPI_prepare`, with the addition that the caller can specify
options to control the parsing of external parameter references, as well as
other facets of query parsing and planning.

## Arguments

`const char * _`command`_`

    

command string

`const SPIPrepareOptions * _`options`_`

    

struct containing optional arguments

Callers should always zero out the entire _`options`_ struct, then fill
whichever fields they want to set. This ensures forward compatibility of code,
since any fields that are added to the struct in future will be defined to
behave backwards-compatibly if they are zero. The currently available
_`options`_ fields are:

`ParserSetupHook _`parserSetup`_`

    

Parser hook setup function

`void * _`parserSetupArg`_`

    

pass-through argument for _`parserSetup`_

`RawParseMode _`parseMode`_`

    

mode for raw parsing; `RAW_PARSE_DEFAULT` (zero) produces default behavior

`int _`cursorOptions`_`

    

integer bit mask of cursor options; zero produces default behavior

## Return Value

`SPI_prepare_extended` has the same return conventions as `SPI_prepare`.

* * *

[Prev](spi-spi-prepare-cursor.html "SPI_prepare_cursor")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-prepare-params.html "SPI_prepare_params")  
---|---|---  
SPI_prepare_cursor  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_prepare_params  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-prepare-
extended.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

