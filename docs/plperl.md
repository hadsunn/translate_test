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

Supported Versions: [Current](/docs/current/plperl.html "PostgreSQL 17 -
Chapter 45. PL/Perl — Perl Procedural Language") ([17](/docs/17/plperl.html
"PostgreSQL 17 - Chapter 45. PL/Perl — Perl Procedural Language")) /
[16](/docs/16/plperl.html "PostgreSQL 16 - Chapter 45. PL/Perl — Perl
Procedural Language") / [15](/docs/15/plperl.html "PostgreSQL 15 -
Chapter 45. PL/Perl — Perl Procedural Language") / [14](/docs/14/plperl.html
"PostgreSQL 14 - Chapter 45. PL/Perl — Perl Procedural Language") /
[13](/docs/13/plperl.html "PostgreSQL 13 - Chapter 45. PL/Perl — Perl
Procedural Language")

Development Versions: [18](/docs/18/plperl.html "PostgreSQL 18 -
Chapter 45. PL/Perl — Perl Procedural Language") /
[devel](/docs/devel/plperl.html "PostgreSQL devel - Chapter 45. PL/Perl — Perl
Procedural Language")

Unsupported versions: [12](/docs/12/plperl.html "PostgreSQL 12 -
Chapter 45. PL/Perl — Perl Procedural Language") / [11](/docs/11/plperl.html
"PostgreSQL 11 - Chapter 45. PL/Perl — Perl Procedural Language") /
[10](/docs/10/plperl.html "PostgreSQL 10 - Chapter 45. PL/Perl — Perl
Procedural Language") / [9.6](/docs/9.6/plperl.html "PostgreSQL 9.6 -
Chapter 45. PL/Perl — Perl Procedural Language") / [9.5](/docs/9.5/plperl.html
"PostgreSQL 9.5 - Chapter 45. PL/Perl — Perl Procedural Language") /
[9.4](/docs/9.4/plperl.html "PostgreSQL 9.4 - Chapter 45. PL/Perl — Perl
Procedural Language") / [9.3](/docs/9.3/plperl.html "PostgreSQL 9.3 -
Chapter 45. PL/Perl — Perl Procedural Language") / [9.2](/docs/9.2/plperl.html
"PostgreSQL 9.2 - Chapter 45. PL/Perl — Perl Procedural Language") /
[9.1](/docs/9.1/plperl.html "PostgreSQL 9.1 - Chapter 45. PL/Perl — Perl
Procedural Language") / [9.0](/docs/9.0/plperl.html "PostgreSQL 9.0 -
Chapter 45. PL/Perl — Perl Procedural Language") / [8.4](/docs/8.4/plperl.html
"PostgreSQL 8.4 - Chapter 45. PL/Perl — Perl Procedural Language") /
[8.3](/docs/8.3/plperl.html "PostgreSQL 8.3 - Chapter 45. PL/Perl — Perl
Procedural Language") / [8.2](/docs/8.2/plperl.html "PostgreSQL 8.2 -
Chapter 45. PL/Perl — Perl Procedural Language") / [8.1](/docs/8.1/plperl.html
"PostgreSQL 8.1 - Chapter 45. PL/Perl — Perl Procedural Language") /
[8.0](/docs/8.0/plperl.html "PostgreSQL 8.0 - Chapter 45. PL/Perl — Perl
Procedural Language") / [7.4](/docs/7.4/plperl.html "PostgreSQL 7.4 -
Chapter 45. PL/Perl — Perl Procedural Language") / [7.3](/docs/7.3/plperl.html
"PostgreSQL 7.3 - Chapter 45. PL/Perl — Perl Procedural Language") /
[7.2](/docs/7.2/plperl.html "PostgreSQL 7.2 - Chapter 45. PL/Perl — Perl
Procedural Language") / [7.1](/docs/7.1/plperl.html "PostgreSQL 7.1 -
Chapter 45. PL/Perl — Perl Procedural Language")

__

Chapter 45. PL/Perl — Perl Procedural Language  
---  
[Prev](pltcl-procnames.html "44.12. Tcl Procedure Names")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-funcs.html "45.1. PL/Perl Functions and Arguments")  
  
* * *

## Chapter 45. PL/Perl — Perl Procedural Language

**Table of Contents**

[45.1. PL/Perl Functions and Arguments](plperl-funcs.html)

[45.2. Data Values in PL/Perl](plperl-data.html)

[45.3. Built-in Functions](plperl-builtins.html)

    

[45.3.1. Database Access from PL/Perl](plperl-builtins.html#PLPERL-DATABASE)

[45.3.2. Utility Functions in PL/Perl](plperl-builtins.html#PLPERL-UTILITY-
FUNCTIONS)

[45.4. Global Values in PL/Perl](plperl-global.html)

[45.5. Trusted and Untrusted PL/Perl](plperl-trusted.html)

[45.6. PL/Perl Triggers](plperl-triggers.html)

[45.7. PL/Perl Event Triggers](plperl-event-triggers.html)

[45.8. PL/Perl Under the Hood](plperl-under-the-hood.html)

    

[45.8.1. Configuration](plperl-under-the-hood.html#PLPERL-CONFIG)

[45.8.2. Limitations and Missing Features](plperl-under-the-hood.html#PLPERL-
MISSING)

PL/Perl is a loadable procedural language that enables you to write PostgreSQL
functions and procedures in the [Perl programming
language](https://www.perl.org).

The main advantage to using PL/Perl is that this allows use, within stored
functions and procedures, of the manyfold “string munging” operators and
functions available for Perl. Parsing complex strings might be easier using
Perl than it is with the string functions and control structures provided in
PL/pgSQL.

To install PL/Perl in a particular database, use `CREATE EXTENSION plperl`.

### Tip

If a language is installed into `template1`, all subsequently created
databases will have the language installed automatically.

### Note

Users of source packages must specially enable the build of PL/Perl during the
installation process. (Refer to [Chapter 17](installation.html
"Chapter 17. Installation from Source Code") for more information.) Users of
binary packages might find PL/Perl in a separate subpackage.

* * *

[Prev](pltcl-procnames.html "44.12. Tcl Procedure Names")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](plperl-funcs.html "45.1. PL/Perl Functions and Arguments")  
---|---|---  
44.12. Tcl Procedure Names  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.1. PL/Perl Functions and Arguments  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

