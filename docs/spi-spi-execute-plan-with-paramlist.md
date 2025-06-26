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

Supported Versions: [Current](/docs/current/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 17 - SPI_execute_plan_with_paramlist")
([17](/docs/17/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 17 -
SPI_execute_plan_with_paramlist")) / [16](/docs/16/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 16 - SPI_execute_plan_with_paramlist") /
[15](/docs/15/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 15 -
SPI_execute_plan_with_paramlist") / [14](/docs/14/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 14 - SPI_execute_plan_with_paramlist") /
[13](/docs/13/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 13 -
SPI_execute_plan_with_paramlist")

Development Versions: [18](/docs/18/spi-spi-execute-plan-with-paramlist.html
"PostgreSQL 18 - SPI_execute_plan_with_paramlist") / [devel](/docs/devel/spi-
spi-execute-plan-with-paramlist.html "PostgreSQL devel -
SPI_execute_plan_with_paramlist")

Unsupported versions: [12](/docs/12/spi-spi-execute-plan-with-paramlist.html
"PostgreSQL 12 - SPI_execute_plan_with_paramlist") / [11](/docs/11/spi-spi-
execute-plan-with-paramlist.html "PostgreSQL 11 -
SPI_execute_plan_with_paramlist") / [10](/docs/10/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 10 - SPI_execute_plan_with_paramlist") /
[9.6](/docs/9.6/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 9.6 -
SPI_execute_plan_with_paramlist") / [9.5](/docs/9.5/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 9.5 - SPI_execute_plan_with_paramlist") /
[9.4](/docs/9.4/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 9.4 -
SPI_execute_plan_with_paramlist") / [9.3](/docs/9.3/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 9.3 - SPI_execute_plan_with_paramlist") /
[9.2](/docs/9.2/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 9.2 -
SPI_execute_plan_with_paramlist") / [9.1](/docs/9.1/spi-spi-execute-plan-with-
paramlist.html "PostgreSQL 9.1 - SPI_execute_plan_with_paramlist") /
[9.0](/docs/9.0/spi-spi-execute-plan-with-paramlist.html "PostgreSQL 9.0 -
SPI_execute_plan_with_paramlist")

__

SPI_execute_plan_with_paramlist  
---  
[Prev](spi-spi-execute-plan-extended.html "SPI_execute_plan_extended")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-execp.html "SPI_execp")  
  
* * *

## SPI_execute_plan_with_paramlist

SPI_execute_plan_with_paramlist — execute a statement prepared by
`SPI_prepare`

## Synopsis

    
    
    int SPI_execute_plan_with_paramlist(SPIPlanPtr _plan_ ,
                                        ParamListInfo _params_ ,
                                        bool _read_only_ ,
                                        long _count_)
    

## Description

`SPI_execute_plan_with_paramlist` executes a statement prepared by
`SPI_prepare`. This function is equivalent to `SPI_execute_plan` except that
information about the parameter values to be passed to the query is presented
differently. The `ParamListInfo` representation can be convenient for passing
down values that are already available in that format. It also supports use of
dynamic parameter sets via hook functions specified in `ParamListInfo`.

This function is now deprecated in favor of `SPI_execute_plan_extended`.

## Arguments

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

`ParamListInfo _`params`_`

    

data structure containing parameter types and values; NULL if none

`bool _`read_only`_`

    

`true` for read-only execution

`long _`count`_`

    

maximum number of rows to return, or `0` for no limit

## Return Value

The return value is the same as for `SPI_execute_plan`.

`SPI_processed` and `SPI_tuptable` are set as in `SPI_execute_plan` if
successful.

* * *

[Prev](spi-spi-execute-plan-extended.html "SPI_execute_plan_extended")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-execp.html "SPI_execp")  
---|---|---  
SPI_execute_plan_extended  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_execp  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-execute-plan-with-
paramlist.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

