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

Supported Versions: [Current](/docs/current/spi-visibility.html "PostgreSQL 17
- 47.5. Visibility of Data Changes") ([17](/docs/17/spi-visibility.html
"PostgreSQL 17 - 47.5. Visibility of Data Changes")) / [16](/docs/16/spi-
visibility.html "PostgreSQL 16 - 47.5. Visibility of Data Changes") /
[15](/docs/15/spi-visibility.html "PostgreSQL 15 - 47.5. Visibility of Data
Changes") / [14](/docs/14/spi-visibility.html "PostgreSQL 14 -
47.5. Visibility of Data Changes") / [13](/docs/13/spi-visibility.html
"PostgreSQL 13 - 47.5. Visibility of Data Changes")

Development Versions: [18](/docs/18/spi-visibility.html "PostgreSQL 18 -
47.5. Visibility of Data Changes") / [devel](/docs/devel/spi-visibility.html
"PostgreSQL devel - 47.5. Visibility of Data Changes")

Unsupported versions: [12](/docs/12/spi-visibility.html "PostgreSQL 12 -
47.5. Visibility of Data Changes") / [11](/docs/11/spi-visibility.html
"PostgreSQL 11 - 47.5. Visibility of Data Changes") / [10](/docs/10/spi-
visibility.html "PostgreSQL 10 - 47.5. Visibility of Data Changes") /
[9.6](/docs/9.6/spi-visibility.html "PostgreSQL 9.6 - 47.5. Visibility of Data
Changes") / [9.5](/docs/9.5/spi-visibility.html "PostgreSQL 9.5 -
47.5. Visibility of Data Changes") / [9.4](/docs/9.4/spi-visibility.html
"PostgreSQL 9.4 - 47.5. Visibility of Data Changes") / [9.3](/docs/9.3/spi-
visibility.html "PostgreSQL 9.3 - 47.5. Visibility of Data Changes") /
[9.2](/docs/9.2/spi-visibility.html "PostgreSQL 9.2 - 47.5. Visibility of Data
Changes") / [9.1](/docs/9.1/spi-visibility.html "PostgreSQL 9.1 -
47.5. Visibility of Data Changes") / [9.0](/docs/9.0/spi-visibility.html
"PostgreSQL 9.0 - 47.5. Visibility of Data Changes") / [8.4](/docs/8.4/spi-
visibility.html "PostgreSQL 8.4 - 47.5. Visibility of Data Changes") /
[8.3](/docs/8.3/spi-visibility.html "PostgreSQL 8.3 - 47.5. Visibility of Data
Changes") / [8.2](/docs/8.2/spi-visibility.html "PostgreSQL 8.2 -
47.5. Visibility of Data Changes") / [8.1](/docs/8.1/spi-visibility.html
"PostgreSQL 8.1 - 47.5. Visibility of Data Changes") / [8.0](/docs/8.0/spi-
visibility.html "PostgreSQL 8.0 - 47.5. Visibility of Data Changes") /
[7.4](/docs/7.4/spi-visibility.html "PostgreSQL 7.4 - 47.5. Visibility of Data
Changes") / [7.3](/docs/7.3/spi-visibility.html "PostgreSQL 7.3 -
47.5. Visibility of Data Changes") / [7.2](/docs/7.2/spi-visibility.html
"PostgreSQL 7.2 - 47.5. Visibility of Data Changes") / [7.1](/docs/7.1/spi-
visibility.html "PostgreSQL 7.1 - 47.5. Visibility of Data Changes")

__

47.5. Visibility of Data Changes  
---  
[Prev](spi-spi-start-transaction.html "SPI_start_transaction")  | [Up](spi.html "Chapter 47. Server Programming Interface") | Chapter 47. Server Programming Interface | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-examples.html "47.6. Examples")  
  
* * *

## 47.5. Visibility of Data Changes #

The following rules govern the visibility of data changes in functions that
use SPI (or any other C function):

  * During the execution of an SQL command, any data changes made by the command are invisible to the command itself. For example, in:
        
        INSERT INTO a SELECT * FROM a;
        

the inserted rows are invisible to the `SELECT` part.

  * Changes made by a command C are visible to all commands that are started after C, no matter whether they are started inside C (during the execution of C) or after C is done.

  * Commands executed via SPI inside a function called by an SQL command (either an ordinary function or a trigger) follow one or the other of the above rules depending on the read/write flag passed to SPI. Commands executed in read-only mode follow the first rule: they cannot see changes of the calling command. Commands executed in read-write mode follow the second rule: they can see all changes made so far.

  * All standard procedural languages set the SPI read-write mode depending on the volatility attribute of the function. Commands of `STABLE` and `IMMUTABLE` functions are done in read-only mode, while commands of `VOLATILE` functions are done in read-write mode. While authors of C functions are able to violate this convention, it's unlikely to be a good idea to do so.

The next section contains an example that illustrates the application of these
rules.

* * *

[Prev](spi-spi-start-transaction.html "SPI_start_transaction")  | [Up](spi.html "Chapter 47. Server Programming Interface") |  [Next](spi-examples.html "47.6. Examples")  
---|---|---  
SPI_start_transaction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  47.6. Examples  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-visibility.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

