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

Supported Versions: [Current](/docs/current/spi-spi-rollback.html "PostgreSQL
17 - SPI_rollback") ([17](/docs/17/spi-spi-rollback.html "PostgreSQL 17 -
SPI_rollback")) / [16](/docs/16/spi-spi-rollback.html "PostgreSQL 16 -
SPI_rollback") / [15](/docs/15/spi-spi-rollback.html "PostgreSQL 15 -
SPI_rollback") / [14](/docs/14/spi-spi-rollback.html "PostgreSQL 14 -
SPI_rollback") / [13](/docs/13/spi-spi-rollback.html "PostgreSQL 13 -
SPI_rollback")

Development Versions: [18](/docs/18/spi-spi-rollback.html "PostgreSQL 18 -
SPI_rollback") / [devel](/docs/devel/spi-spi-rollback.html "PostgreSQL devel -
SPI_rollback")

Unsupported versions: [12](/docs/12/spi-spi-rollback.html "PostgreSQL 12 -
SPI_rollback") / [11](/docs/11/spi-spi-rollback.html "PostgreSQL 11 -
SPI_rollback")

__

SPI_rollback  
---  
[Prev](spi-spi-commit.html "SPI_commit")  | [Up](spi-transaction.html "47.4. Transaction Management") | 47.4. Transaction Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-start-transaction.html "SPI_start_transaction")  
  
* * *

## SPI_rollback

SPI_rollback, SPI_rollback_and_chain — abort the current transaction

## Synopsis

    
    
    void SPI_rollback(void)
    
    
    
    void SPI_rollback_and_chain(void)
    

## Description

`SPI_rollback` rolls back the current transaction. It is approximately
equivalent to running the SQL command `ROLLBACK`. After the transaction is
rolled back, a new transaction is automatically started using default
transaction characteristics, so that the caller can continue using SPI
facilities.

`SPI_rollback_and_chain` is the same, but the new transaction is started with
the same transaction characteristics as the just finished one, like with the
SQL command `ROLLBACK AND CHAIN`.

These functions can only be executed if the SPI connection has been set as
nonatomic in the call to `SPI_connect_ext`.

* * *

[Prev](spi-spi-commit.html "SPI_commit")  | [Up](spi-transaction.html "47.4. Transaction Management") |  [Next](spi-spi-start-transaction.html "SPI_start_transaction")  
---|---|---  
SPI_commit  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_start_transaction  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-rollback.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

