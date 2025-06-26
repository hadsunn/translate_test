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

Supported Versions: [Current](/docs/current/xplang.html "PostgreSQL 17 -
Chapter 42. Procedural Languages") ([17](/docs/17/xplang.html "PostgreSQL 17 -
Chapter 42. Procedural Languages")) / [16](/docs/16/xplang.html "PostgreSQL 16
- Chapter 42. Procedural Languages") / [15](/docs/15/xplang.html "PostgreSQL
15 - Chapter 42. Procedural Languages") / [14](/docs/14/xplang.html
"PostgreSQL 14 - Chapter 42. Procedural Languages") /
[13](/docs/13/xplang.html "PostgreSQL 13 - Chapter 42. Procedural Languages")

Development Versions: [18](/docs/18/xplang.html "PostgreSQL 18 -
Chapter 42. Procedural Languages") / [devel](/docs/devel/xplang.html
"PostgreSQL devel - Chapter 42. Procedural Languages")

Unsupported versions: [12](/docs/12/xplang.html "PostgreSQL 12 -
Chapter 42. Procedural Languages") / [11](/docs/11/xplang.html "PostgreSQL 11
- Chapter 42. Procedural Languages") / [10](/docs/10/xplang.html "PostgreSQL
10 - Chapter 42. Procedural Languages") / [9.6](/docs/9.6/xplang.html
"PostgreSQL 9.6 - Chapter 42. Procedural Languages") /
[9.5](/docs/9.5/xplang.html "PostgreSQL 9.5 - Chapter 42. Procedural
Languages") / [9.4](/docs/9.4/xplang.html "PostgreSQL 9.4 -
Chapter 42. Procedural Languages") / [9.3](/docs/9.3/xplang.html "PostgreSQL
9.3 - Chapter 42. Procedural Languages") / [9.2](/docs/9.2/xplang.html
"PostgreSQL 9.2 - Chapter 42. Procedural Languages") /
[9.1](/docs/9.1/xplang.html "PostgreSQL 9.1 - Chapter 42. Procedural
Languages") / [9.0](/docs/9.0/xplang.html "PostgreSQL 9.0 -
Chapter 42. Procedural Languages") / [8.4](/docs/8.4/xplang.html "PostgreSQL
8.4 - Chapter 42. Procedural Languages") / [8.3](/docs/8.3/xplang.html
"PostgreSQL 8.3 - Chapter 42. Procedural Languages") /
[8.2](/docs/8.2/xplang.html "PostgreSQL 8.2 - Chapter 42. Procedural
Languages") / [8.1](/docs/8.1/xplang.html "PostgreSQL 8.1 -
Chapter 42. Procedural Languages") / [8.0](/docs/8.0/xplang.html "PostgreSQL
8.0 - Chapter 42. Procedural Languages") / [7.4](/docs/7.4/xplang.html
"PostgreSQL 7.4 - Chapter 42. Procedural Languages") /
[7.3](/docs/7.3/xplang.html "PostgreSQL 7.3 - Chapter 42. Procedural
Languages") / [7.2](/docs/7.2/xplang.html "PostgreSQL 7.2 -
Chapter 42. Procedural Languages") / [7.1](/docs/7.1/xplang.html "PostgreSQL
7.1 - Chapter 42. Procedural Languages")

__

Chapter 42. Procedural Languages  
---  
[Prev](rules-triggers.html "41.7. Rules Versus Triggers")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xplang-install.html "42.1. Installing Procedural Languages")  
  
* * *

## Chapter 42. Procedural Languages

**Table of Contents**

[42.1. Installing Procedural Languages](xplang-install.html)

PostgreSQL allows user-defined functions to be written in other languages
besides SQL and C. These other languages are generically called _procedural
languages_ (PLs). For a function written in a procedural language, the
database server has no built-in knowledge about how to interpret the
function's source text. Instead, the task is passed to a special handler that
knows the details of the language. The handler could either do all the work of
parsing, syntax analysis, execution, etc. itself, or it could serve as “glue”
between PostgreSQL and an existing implementation of a programming language.
The handler itself is a C language function compiled into a shared object and
loaded on demand, just like any other C function.

There are currently four procedural languages available in the standard
PostgreSQL distribution: PL/pgSQL ([Chapter 43](plpgsql.html
"Chapter 43. PL/pgSQL — SQL Procedural Language")), PL/Tcl ([Chapter
44](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language")), PL/Perl
([Chapter 45](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language")),
and PL/Python ([Chapter 46](plpython.html "Chapter 46. PL/Python — Python
Procedural Language")). There are additional procedural languages available
that are not included in the core distribution. [Appendix H](external-
projects.html "Appendix H. External Projects") has information about finding
them. In addition other languages can be defined by users; the basics of
developing a new procedural language are covered in [Chapter
58](plhandler.html "Chapter 58. Writing a Procedural Language Handler").

* * *

[Prev](rules-triggers.html "41.7. Rules Versus Triggers")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](xplang-install.html "42.1. Installing Procedural Languages")  
---|---|---  
41.7. Rules Versus Triggers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  42.1. Installing Procedural Languages  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xplang.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

