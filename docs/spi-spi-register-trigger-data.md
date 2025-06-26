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

Supported Versions: [Current](/docs/current/spi-spi-register-trigger-data.html
"PostgreSQL 17 - SPI_register_trigger_data") ([17](/docs/17/spi-spi-register-
trigger-data.html "PostgreSQL 17 - SPI_register_trigger_data")) /
[16](/docs/16/spi-spi-register-trigger-data.html "PostgreSQL 16 -
SPI_register_trigger_data") / [15](/docs/15/spi-spi-register-trigger-data.html
"PostgreSQL 15 - SPI_register_trigger_data") / [14](/docs/14/spi-spi-register-
trigger-data.html "PostgreSQL 14 - SPI_register_trigger_data") /
[13](/docs/13/spi-spi-register-trigger-data.html "PostgreSQL 13 -
SPI_register_trigger_data")

Development Versions: [18](/docs/18/spi-spi-register-trigger-data.html
"PostgreSQL 18 - SPI_register_trigger_data") / [devel](/docs/devel/spi-spi-
register-trigger-data.html "PostgreSQL devel - SPI_register_trigger_data")

Unsupported versions: [12](/docs/12/spi-spi-register-trigger-data.html
"PostgreSQL 12 - SPI_register_trigger_data") / [11](/docs/11/spi-spi-register-
trigger-data.html "PostgreSQL 11 - SPI_register_trigger_data") /
[10](/docs/10/spi-spi-register-trigger-data.html "PostgreSQL 10 -
SPI_register_trigger_data")

__

SPI_register_trigger_data  
---  
[Prev](spi-spi-unregister-relation.html "SPI_unregister_relation")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-interface-support.html "47.2. Interface Support Functions")  
  
* * *

## SPI_register_trigger_data

SPI_register_trigger_data — make ephemeral trigger data available in SPI
queries

## Synopsis

    
    
    int SPI_register_trigger_data(TriggerData *_tdata_)
    

## Description

`SPI_register_trigger_data` makes any ephemeral relations captured by a
trigger available to queries planned and executed through the current SPI
connection. Currently, this means the transition tables captured by an `AFTER`
trigger defined with a `REFERENCING OLD/NEW TABLE AS` ... clause. This
function should be called by a PL trigger handler function after connecting.

## Arguments

`TriggerData *_`tdata`_`

    

the `TriggerData` object passed to a trigger handler function as
`fcinfo->context`

## Return Value

If the execution of the command was successful then the following
(nonnegative) value will be returned:

`SPI_OK_TD_REGISTER`

    

if the captured trigger data (if any) has been successfully registered

On error, one of the following negative values is returned:

`SPI_ERROR_ARGUMENT`

    

if _`tdata`_ is `NULL`

`SPI_ERROR_UNCONNECTED`

    

if called from an unconnected C function

`SPI_ERROR_REL_DUPLICATE`

    

if the name of any trigger data transient relation is already registered for
this connection

* * *

[Prev](spi-spi-unregister-relation.html "SPI_unregister_relation")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-interface-support.html "47.2. Interface Support Functions")  
---|---|---  
SPI_unregister_relation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  47.2. Interface Support Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-register-trigger-
data.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

