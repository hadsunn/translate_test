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

Supported Versions: [Current](/docs/current/spi-interface-support.html
"PostgreSQL 17 - 47.2. Interface Support Functions") ([17](/docs/17/spi-
interface-support.html "PostgreSQL 17 - 47.2. Interface Support Functions")) /
[16](/docs/16/spi-interface-support.html "PostgreSQL 16 - 47.2. Interface
Support Functions") / [15](/docs/15/spi-interface-support.html "PostgreSQL 15
- 47.2. Interface Support Functions") / [14](/docs/14/spi-interface-
support.html "PostgreSQL 14 - 47.2. Interface Support Functions") /
[13](/docs/13/spi-interface-support.html "PostgreSQL 13 - 47.2. Interface
Support Functions")

Development Versions: [18](/docs/18/spi-interface-support.html "PostgreSQL 18
- 47.2. Interface Support Functions") / [devel](/docs/devel/spi-interface-
support.html "PostgreSQL devel - 47.2. Interface Support Functions")

Unsupported versions: [12](/docs/12/spi-interface-support.html "PostgreSQL 12
- 47.2. Interface Support Functions") / [11](/docs/11/spi-interface-
support.html "PostgreSQL 11 - 47.2. Interface Support Functions") /
[10](/docs/10/spi-interface-support.html "PostgreSQL 10 - 47.2. Interface
Support Functions") / [9.6](/docs/9.6/spi-interface-support.html "PostgreSQL
9.6 - 47.2. Interface Support Functions") / [9.5](/docs/9.5/spi-interface-
support.html "PostgreSQL 9.5 - 47.2. Interface Support Functions") /
[9.4](/docs/9.4/spi-interface-support.html "PostgreSQL 9.4 - 47.2. Interface
Support Functions") / [9.3](/docs/9.3/spi-interface-support.html "PostgreSQL
9.3 - 47.2. Interface Support Functions") / [9.2](/docs/9.2/spi-interface-
support.html "PostgreSQL 9.2 - 47.2. Interface Support Functions") /
[9.1](/docs/9.1/spi-interface-support.html "PostgreSQL 9.1 - 47.2. Interface
Support Functions") / [9.0](/docs/9.0/spi-interface-support.html "PostgreSQL
9.0 - 47.2. Interface Support Functions") / [8.4](/docs/8.4/spi-interface-
support.html "PostgreSQL 8.4 - 47.2. Interface Support Functions") /
[8.3](/docs/8.3/spi-interface-support.html "PostgreSQL 8.3 - 47.2. Interface
Support Functions") / [8.2](/docs/8.2/spi-interface-support.html "PostgreSQL
8.2 - 47.2. Interface Support Functions") / [8.1](/docs/8.1/spi-interface-
support.html "PostgreSQL 8.1 - 47.2. Interface Support Functions") /
[8.0](/docs/8.0/spi-interface-support.html "PostgreSQL 8.0 - 47.2. Interface
Support Functions") / [7.4](/docs/7.4/spi-interface-support.html "PostgreSQL
7.4 - 47.2. Interface Support Functions") / [7.3](/docs/7.3/spi-interface-
support.html "PostgreSQL 7.3 - 47.2. Interface Support Functions") /
[7.2](/docs/7.2/spi-interface-support.html "PostgreSQL 7.2 - 47.2. Interface
Support Functions") / [7.1](/docs/7.1/spi-interface-support.html "PostgreSQL
7.1 - 47.2. Interface Support Functions")

__

47.2. Interface Support Functions  
---  
[Prev](spi-spi-register-trigger-data.html "SPI_register_trigger_data")  | [Up](spi.html "Chapter 47. Server Programming Interface") | Chapter 47. Server Programming Interface | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-fname.html "SPI_fname")  
  
* * *

## 47.2. Interface Support Functions #

[SPI_fname](spi-spi-fname.html) — determine the column name for the specified
column number

[SPI_fnumber](spi-spi-fnumber.html) — determine the column number for the
specified column name

[SPI_getvalue](spi-spi-getvalue.html) — return the string value of the
specified column

[SPI_getbinval](spi-spi-getbinval.html) — return the binary value of the
specified column

[SPI_gettype](spi-spi-gettype.html) — return the data type name of the
specified column

[SPI_gettypeid](spi-spi-gettypeid.html) — return the data type OID of the
specified column

[SPI_getrelname](spi-spi-getrelname.html) — return the name of the specified
relation

[SPI_getnspname](spi-spi-getnspname.html) — return the namespace of the
specified relation

[SPI_result_code_string](spi-spi-result-code-string.html) — return error code
as string

The functions described here provide an interface for extracting information
from result sets returned by `SPI_execute` and other SPI functions.

All functions described in this section can be used by both connected and
unconnected C functions.

* * *

[Prev](spi-spi-register-trigger-data.html "SPI_register_trigger_data")  | [Up](spi.html "Chapter 47. Server Programming Interface") |  [Next](spi-spi-fname.html "SPI_fname")  
---|---|---  
SPI_register_trigger_data  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_fname  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-interface-support.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

