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

Supported Versions: [Current](/docs/current/spi-spi-register-relation.html
"PostgreSQL 17 - SPI_register_relation") ([17](/docs/17/spi-spi-register-
relation.html "PostgreSQL 17 - SPI_register_relation")) / [16](/docs/16/spi-
spi-register-relation.html "PostgreSQL 16 - SPI_register_relation") /
[15](/docs/15/spi-spi-register-relation.html "PostgreSQL 15 -
SPI_register_relation") / [14](/docs/14/spi-spi-register-relation.html
"PostgreSQL 14 - SPI_register_relation") / [13](/docs/13/spi-spi-register-
relation.html "PostgreSQL 13 - SPI_register_relation")

Development Versions: [18](/docs/18/spi-spi-register-relation.html "PostgreSQL
18 - SPI_register_relation") / [devel](/docs/devel/spi-spi-register-
relation.html "PostgreSQL devel - SPI_register_relation")

Unsupported versions: [12](/docs/12/spi-spi-register-relation.html "PostgreSQL
12 - SPI_register_relation") / [11](/docs/11/spi-spi-register-relation.html
"PostgreSQL 11 - SPI_register_relation") / [10](/docs/10/spi-spi-register-
relation.html "PostgreSQL 10 - SPI_register_relation")

__

SPI_register_relation  
---  
[Prev](spi-spi-saveplan.html "SPI_saveplan")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-unregister-relation.html "SPI_unregister_relation")  
  
* * *

## SPI_register_relation

SPI_register_relation — make an ephemeral named relation available by name in
SPI queries

## Synopsis

    
    
    int SPI_register_relation(EphemeralNamedRelation _enr_)
    

## Description

`SPI_register_relation` makes an ephemeral named relation, with associated
information, available to queries planned and executed through the current SPI
connection.

## Arguments

`EphemeralNamedRelation _`enr`_`

    

the ephemeral named relation registry entry

## Return Value

If the execution of the command was successful then the following
(nonnegative) value will be returned:

`SPI_OK_REL_REGISTER`

    

if the relation has been successfully registered by name

On error, one of the following negative values is returned:

`SPI_ERROR_ARGUMENT`

    

if _`enr`_ is `NULL` or its `name` field is `NULL`

`SPI_ERROR_UNCONNECTED`

    

if called from an unconnected C function

`SPI_ERROR_REL_DUPLICATE`

    

if the name specified in the `name` field of _`enr`_ is already registered for
this connection

* * *

[Prev](spi-spi-saveplan.html "SPI_saveplan")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-unregister-relation.html "SPI_unregister_relation")  
---|---|---  
SPI_saveplan  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_unregister_relation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-register-
relation.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

