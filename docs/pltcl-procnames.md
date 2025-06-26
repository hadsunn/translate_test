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

Supported Versions: [Current](/docs/current/pltcl-procnames.html "PostgreSQL
17 - 44.12. Tcl Procedure Names") ([17](/docs/17/pltcl-procnames.html
"PostgreSQL 17 - 44.12. Tcl Procedure Names")) / [16](/docs/16/pltcl-
procnames.html "PostgreSQL 16 - 44.12. Tcl Procedure Names") /
[15](/docs/15/pltcl-procnames.html "PostgreSQL 15 - 44.12. Tcl Procedure
Names") / [14](/docs/14/pltcl-procnames.html "PostgreSQL 14 - 44.12. Tcl
Procedure Names") / [13](/docs/13/pltcl-procnames.html "PostgreSQL 13 -
44.12. Tcl Procedure Names")

Development Versions: [18](/docs/18/pltcl-procnames.html "PostgreSQL 18 -
44.12. Tcl Procedure Names") / [devel](/docs/devel/pltcl-procnames.html
"PostgreSQL devel - 44.12. Tcl Procedure Names")

Unsupported versions: [12](/docs/12/pltcl-procnames.html "PostgreSQL 12 -
44.12. Tcl Procedure Names") / [11](/docs/11/pltcl-procnames.html "PostgreSQL
11 - 44.12. Tcl Procedure Names") / [10](/docs/10/pltcl-procnames.html
"PostgreSQL 10 - 44.12. Tcl Procedure Names") / [9.6](/docs/9.6/pltcl-
procnames.html "PostgreSQL 9.6 - 44.12. Tcl Procedure Names") /
[9.5](/docs/9.5/pltcl-procnames.html "PostgreSQL 9.5 - 44.12. Tcl Procedure
Names") / [9.4](/docs/9.4/pltcl-procnames.html "PostgreSQL 9.4 - 44.12. Tcl
Procedure Names") / [9.3](/docs/9.3/pltcl-procnames.html "PostgreSQL 9.3 -
44.12. Tcl Procedure Names") / [9.2](/docs/9.2/pltcl-procnames.html
"PostgreSQL 9.2 - 44.12. Tcl Procedure Names") / [9.1](/docs/9.1/pltcl-
procnames.html "PostgreSQL 9.1 - 44.12. Tcl Procedure Names") /
[9.0](/docs/9.0/pltcl-procnames.html "PostgreSQL 9.0 - 44.12. Tcl Procedure
Names") / [8.4](/docs/8.4/pltcl-procnames.html "PostgreSQL 8.4 - 44.12. Tcl
Procedure Names") / [8.3](/docs/8.3/pltcl-procnames.html "PostgreSQL 8.3 -
44.12. Tcl Procedure Names") / [8.2](/docs/8.2/pltcl-procnames.html
"PostgreSQL 8.2 - 44.12. Tcl Procedure Names") / [8.1](/docs/8.1/pltcl-
procnames.html "PostgreSQL 8.1 - 44.12. Tcl Procedure Names") /
[8.0](/docs/8.0/pltcl-procnames.html "PostgreSQL 8.0 - 44.12. Tcl Procedure
Names") / [7.4](/docs/7.4/pltcl-procnames.html "PostgreSQL 7.4 - 44.12. Tcl
Procedure Names")

__

44.12. Tcl Procedure Names  
---  
[Prev](pltcl-config.html "44.11. PL/Tcl Configuration")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language")  
  
* * *

## 44.12. Tcl Procedure Names #

In PostgreSQL, the same function name can be used for different function
definitions as long as the number of arguments or their types differ. Tcl,
however, requires all procedure names to be distinct. PL/Tcl deals with this
by making the internal Tcl procedure names contain the object ID of the
function from the system table `pg_proc` as part of their name. Thus,
PostgreSQL functions with the same name and different argument types will be
different Tcl procedures, too. This is not normally a concern for a PL/Tcl
programmer, but it might be visible when debugging.

* * *

[Prev](pltcl-config.html "44.11. PL/Tcl Configuration")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language")  
---|---|---  
44.11. PL/Tcl Configuration  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 45. PL/Perl — Perl Procedural Language  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-procnames.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

