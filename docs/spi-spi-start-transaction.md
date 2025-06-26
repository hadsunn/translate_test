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

Supported Versions: [Current](/docs/current/spi-spi-start-transaction.html
"PostgreSQL 17 - SPI_start_transaction") ([17](/docs/17/spi-spi-start-
transaction.html "PostgreSQL 17 - SPI_start_transaction")) /
[16](/docs/16/spi-spi-start-transaction.html "PostgreSQL 16 -
SPI_start_transaction") / [15](/docs/15/spi-spi-start-transaction.html
"PostgreSQL 15 - SPI_start_transaction") / [14](/docs/14/spi-spi-start-
transaction.html "PostgreSQL 14 - SPI_start_transaction") / [13](/docs/13/spi-
spi-start-transaction.html "PostgreSQL 13 - SPI_start_transaction")

Development Versions: [18](/docs/18/spi-spi-start-transaction.html "PostgreSQL
18 - SPI_start_transaction") / [devel](/docs/devel/spi-spi-start-
transaction.html "PostgreSQL devel - SPI_start_transaction")

Unsupported versions: [12](/docs/12/spi-spi-start-transaction.html "PostgreSQL
12 - SPI_start_transaction") / [11](/docs/11/spi-spi-start-transaction.html
"PostgreSQL 11 - SPI_start_transaction")

__

SPI_start_transaction  
---  
[Prev](spi-spi-rollback.html "SPI_rollback")  | [Up](spi-transaction.html "47.4. Transaction Management") | 47.4. Transaction Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-visibility.html "47.5. Visibility of Data Changes")  
  
* * *

## SPI_start_transaction

SPI_start_transaction — obsolete function

## Synopsis

    
    
    void SPI_start_transaction(void)
    

## Description

`SPI_start_transaction` does nothing, and exists only for code compatibility
with earlier PostgreSQL releases. It used to be required after calling
`SPI_commit` or `SPI_rollback`, but now those functions start a new
transaction automatically.

* * *

[Prev](spi-spi-rollback.html "SPI_rollback")  | [Up](spi-transaction.html "47.4. Transaction Management") |  [Next](spi-visibility.html "47.5. Visibility of Data Changes")  
---|---|---  
SPI_rollback  | [Home](index.html "PostgreSQL 16.9 Documentation") |  47.5. Visibility of Data Changes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-start-
transaction.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

