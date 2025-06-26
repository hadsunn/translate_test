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

Supported Versions: [Current](/docs/current/plperl-data.html "PostgreSQL 17 -
45.2. Data Values in PL/Perl") ([17](/docs/17/plperl-data.html "PostgreSQL 17
- 45.2. Data Values in PL/Perl")) / [16](/docs/16/plperl-data.html "PostgreSQL
16 - 45.2. Data Values in PL/Perl") / [15](/docs/15/plperl-data.html
"PostgreSQL 15 - 45.2. Data Values in PL/Perl") / [14](/docs/14/plperl-
data.html "PostgreSQL 14 - 45.2. Data Values in PL/Perl") /
[13](/docs/13/plperl-data.html "PostgreSQL 13 - 45.2. Data Values in PL/Perl")

Development Versions: [18](/docs/18/plperl-data.html "PostgreSQL 18 -
45.2. Data Values in PL/Perl") / [devel](/docs/devel/plperl-data.html
"PostgreSQL devel - 45.2. Data Values in PL/Perl")

Unsupported versions: [12](/docs/12/plperl-data.html "PostgreSQL 12 -
45.2. Data Values in PL/Perl") / [11](/docs/11/plperl-data.html "PostgreSQL 11
- 45.2. Data Values in PL/Perl") / [10](/docs/10/plperl-data.html "PostgreSQL
10 - 45.2. Data Values in PL/Perl") / [9.6](/docs/9.6/plperl-data.html
"PostgreSQL 9.6 - 45.2. Data Values in PL/Perl") / [9.5](/docs/9.5/plperl-
data.html "PostgreSQL 9.5 - 45.2. Data Values in PL/Perl") /
[9.4](/docs/9.4/plperl-data.html "PostgreSQL 9.4 - 45.2. Data Values in
PL/Perl") / [9.3](/docs/9.3/plperl-data.html "PostgreSQL 9.3 - 45.2. Data
Values in PL/Perl") / [9.2](/docs/9.2/plperl-data.html "PostgreSQL 9.2 -
45.2. Data Values in PL/Perl") / [9.1](/docs/9.1/plperl-data.html "PostgreSQL
9.1 - 45.2. Data Values in PL/Perl") / [9.0](/docs/9.0/plperl-data.html
"PostgreSQL 9.0 - 45.2. Data Values in PL/Perl") / [8.4](/docs/8.4/plperl-
data.html "PostgreSQL 8.4 - 45.2. Data Values in PL/Perl") /
[8.3](/docs/8.3/plperl-data.html "PostgreSQL 8.3 - 45.2. Data Values in
PL/Perl") / [8.2](/docs/8.2/plperl-data.html "PostgreSQL 8.2 - 45.2. Data
Values in PL/Perl") / [8.1](/docs/8.1/plperl-data.html "PostgreSQL 8.1 -
45.2. Data Values in PL/Perl") / [8.0](/docs/8.0/plperl-data.html "PostgreSQL
8.0 - 45.2. Data Values in PL/Perl") / [7.4](/docs/7.4/plperl-data.html
"PostgreSQL 7.4 - 45.2. Data Values in PL/Perl") / [7.3](/docs/7.3/plperl-
data.html "PostgreSQL 7.3 - 45.2. Data Values in PL/Perl")

__

45.2. Data Values in PL/Perl  
---  
[Prev](plperl-funcs.html "45.1. PL/Perl Functions and Arguments")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") | Chapter 45. PL/Perl — Perl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-builtins.html "45.3. Built-in Functions")  
  
* * *

## 45.2. Data Values in PL/Perl #

The argument values supplied to a PL/Perl function's code are simply the input
arguments converted to text form (just as if they had been displayed by a
`SELECT` statement). Conversely, the `return` and `return_next` commands will
accept any string that is acceptable input format for the function's declared
return type.

If this behavior is inconvenient for a particular case, it can be improved by
using a transform, as already illustrated for `bool` values. Several examples
of transform modules are included in the PostgreSQL distribution.

* * *

[Prev](plperl-funcs.html "45.1. PL/Perl Functions and Arguments")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") |  [Next](plperl-builtins.html "45.3. Built-in Functions")  
---|---|---  
45.1. PL/Perl Functions and Arguments  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.3. Built-in Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl-data.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

