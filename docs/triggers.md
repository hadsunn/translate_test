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

Supported Versions: [Current](/docs/current/triggers.html "PostgreSQL 17 -
Chapter 39. Triggers") ([17](/docs/17/triggers.html "PostgreSQL 17 -
Chapter 39. Triggers")) / [16](/docs/16/triggers.html "PostgreSQL 16 -
Chapter 39. Triggers") / [15](/docs/15/triggers.html "PostgreSQL 15 -
Chapter 39. Triggers") / [14](/docs/14/triggers.html "PostgreSQL 14 -
Chapter 39. Triggers") / [13](/docs/13/triggers.html "PostgreSQL 13 -
Chapter 39. Triggers")

Development Versions: [18](/docs/18/triggers.html "PostgreSQL 18 -
Chapter 39. Triggers") / [devel](/docs/devel/triggers.html "PostgreSQL devel -
Chapter 39. Triggers")

Unsupported versions: [12](/docs/12/triggers.html "PostgreSQL 12 -
Chapter 39. Triggers") / [11](/docs/11/triggers.html "PostgreSQL 11 -
Chapter 39. Triggers") / [10](/docs/10/triggers.html "PostgreSQL 10 -
Chapter 39. Triggers") / [9.6](/docs/9.6/triggers.html "PostgreSQL 9.6 -
Chapter 39. Triggers") / [9.5](/docs/9.5/triggers.html "PostgreSQL 9.5 -
Chapter 39. Triggers") / [9.4](/docs/9.4/triggers.html "PostgreSQL 9.4 -
Chapter 39. Triggers") / [9.3](/docs/9.3/triggers.html "PostgreSQL 9.3 -
Chapter 39. Triggers") / [9.2](/docs/9.2/triggers.html "PostgreSQL 9.2 -
Chapter 39. Triggers") / [9.1](/docs/9.1/triggers.html "PostgreSQL 9.1 -
Chapter 39. Triggers") / [9.0](/docs/9.0/triggers.html "PostgreSQL 9.0 -
Chapter 39. Triggers") / [8.4](/docs/8.4/triggers.html "PostgreSQL 8.4 -
Chapter 39. Triggers") / [8.3](/docs/8.3/triggers.html "PostgreSQL 8.3 -
Chapter 39. Triggers") / [8.2](/docs/8.2/triggers.html "PostgreSQL 8.2 -
Chapter 39. Triggers") / [8.1](/docs/8.1/triggers.html "PostgreSQL 8.1 -
Chapter 39. Triggers") / [8.0](/docs/8.0/triggers.html "PostgreSQL 8.0 -
Chapter 39. Triggers") / [7.4](/docs/7.4/triggers.html "PostgreSQL 7.4 -
Chapter 39. Triggers") / [7.3](/docs/7.3/triggers.html "PostgreSQL 7.3 -
Chapter 39. Triggers") / [7.2](/docs/7.2/triggers.html "PostgreSQL 7.2 -
Chapter 39. Triggers") / [7.1](/docs/7.1/triggers.html "PostgreSQL 7.1 -
Chapter 39. Triggers")

__

Chapter 39. Triggers  
---  
[Prev](extend-pgxs.html "38.18. Extension Building Infrastructure")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](trigger-definition.html "39.1. Overview of Trigger Behavior")  
  
* * *

## Chapter 39. Triggers

**Table of Contents**

[39.1. Overview of Trigger Behavior](trigger-definition.html)

[39.2. Visibility of Data Changes](trigger-datachanges.html)

[39.3. Writing Trigger Functions in C](trigger-interface.html)

[39.4. A Complete Trigger Example](trigger-example.html)

This chapter provides general information about writing trigger functions.
Trigger functions can be written in most of the available procedural
languages, including PL/pgSQL ([Chapter 43](plpgsql.html "Chapter 43. PL/pgSQL
— SQL Procedural Language")), PL/Tcl ([Chapter 44](pltcl.html
"Chapter 44. PL/Tcl — Tcl Procedural Language")), PL/Perl ([Chapter
45](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language")), and
PL/Python ([Chapter 46](plpython.html "Chapter 46. PL/Python — Python
Procedural Language")). After reading this chapter, you should consult the
chapter for your favorite procedural language to find out the language-
specific details of writing a trigger in it.

It is also possible to write a trigger function in C, although most people
find it easier to use one of the procedural languages. It is not currently
possible to write a trigger function in the plain SQL function language.

* * *

[Prev](extend-pgxs.html "38.18. Extension Building Infrastructure")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](trigger-definition.html "39.1. Overview of Trigger Behavior")  
---|---|---  
38.18. Extension Building Infrastructure  | [Home](index.html "PostgreSQL 16.9 Documentation") |  39.1. Overview of Trigger Behavior  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/triggers.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

