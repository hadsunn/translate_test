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

Supported Versions: [Current](/docs/current/ecpg-oracle-compat.html
"PostgreSQL 17 - 36.16. Oracle Compatibility Mode") ([17](/docs/17/ecpg-
oracle-compat.html "PostgreSQL 17 - 36.16. Oracle Compatibility Mode")) /
[16](/docs/16/ecpg-oracle-compat.html "PostgreSQL 16 - 36.16. Oracle
Compatibility Mode") / [15](/docs/15/ecpg-oracle-compat.html "PostgreSQL 15 -
36.16. Oracle Compatibility Mode") / [14](/docs/14/ecpg-oracle-compat.html
"PostgreSQL 14 - 36.16. Oracle Compatibility Mode") / [13](/docs/13/ecpg-
oracle-compat.html "PostgreSQL 13 - 36.16. Oracle Compatibility Mode")

Development Versions: [18](/docs/18/ecpg-oracle-compat.html "PostgreSQL 18 -
36.16. Oracle Compatibility Mode") / [devel](/docs/devel/ecpg-oracle-
compat.html "PostgreSQL devel - 36.16. Oracle Compatibility Mode")

Unsupported versions: [12](/docs/12/ecpg-oracle-compat.html "PostgreSQL 12 -
36.16. Oracle Compatibility Mode") / [11](/docs/11/ecpg-oracle-compat.html
"PostgreSQL 11 - 36.16. Oracle Compatibility Mode")

__

36.16. Oracle Compatibility Mode  
---  
[Prev](ecpg-informix-compat.html "36.15. Informix Compatibility Mode")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-develop.html "36.17. Internals")  
  
* * *

## 36.16. Oracle Compatibility Mode #

`ecpg` can be run in a so-called _Oracle compatibility mode_. If this mode is
active, it tries to behave as if it were Oracle Pro*C.

Specifically, this mode changes `ecpg` in three ways:

  * Pad character arrays receiving character string types with trailing spaces to the specified length

  * Zero byte terminate these character arrays, and set the indicator variable if truncation occurs

  * Set the null indicator to `-1` when character arrays receive empty character string types

* * *

[Prev](ecpg-informix-compat.html "36.15. Informix Compatibility Mode")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-develop.html "36.17. Internals")  
---|---|---  
36.15. Informix Compatibility Mode  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.17. Internals  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-oracle-compat.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

