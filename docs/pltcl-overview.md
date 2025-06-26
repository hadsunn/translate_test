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

Supported Versions: [Current](/docs/current/pltcl-overview.html "PostgreSQL 17
- 44.1. Overview") ([17](/docs/17/pltcl-overview.html "PostgreSQL 17 -
44.1. Overview")) / [16](/docs/16/pltcl-overview.html "PostgreSQL 16 -
44.1. Overview") / [15](/docs/15/pltcl-overview.html "PostgreSQL 15 -
44.1. Overview") / [14](/docs/14/pltcl-overview.html "PostgreSQL 14 -
44.1. Overview") / [13](/docs/13/pltcl-overview.html "PostgreSQL 13 -
44.1. Overview")

Development Versions: [18](/docs/18/pltcl-overview.html "PostgreSQL 18 -
44.1. Overview") / [devel](/docs/devel/pltcl-overview.html "PostgreSQL devel -
44.1. Overview")

Unsupported versions: [12](/docs/12/pltcl-overview.html "PostgreSQL 12 -
44.1. Overview") / [11](/docs/11/pltcl-overview.html "PostgreSQL 11 -
44.1. Overview") / [10](/docs/10/pltcl-overview.html "PostgreSQL 10 -
44.1. Overview") / [9.6](/docs/9.6/pltcl-overview.html "PostgreSQL 9.6 -
44.1. Overview") / [9.5](/docs/9.5/pltcl-overview.html "PostgreSQL 9.5 -
44.1. Overview") / [9.4](/docs/9.4/pltcl-overview.html "PostgreSQL 9.4 -
44.1. Overview") / [9.3](/docs/9.3/pltcl-overview.html "PostgreSQL 9.3 -
44.1. Overview") / [9.2](/docs/9.2/pltcl-overview.html "PostgreSQL 9.2 -
44.1. Overview") / [9.1](/docs/9.1/pltcl-overview.html "PostgreSQL 9.1 -
44.1. Overview") / [9.0](/docs/9.0/pltcl-overview.html "PostgreSQL 9.0 -
44.1. Overview") / [8.4](/docs/8.4/pltcl-overview.html "PostgreSQL 8.4 -
44.1. Overview") / [8.3](/docs/8.3/pltcl-overview.html "PostgreSQL 8.3 -
44.1. Overview") / [8.2](/docs/8.2/pltcl-overview.html "PostgreSQL 8.2 -
44.1. Overview")

__

44.1. Overview  
---  
[Prev](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-functions.html "44.2. PL/Tcl Functions and Arguments")  
  
* * *

## 44.1. Overview #

PL/Tcl offers most of the capabilities a function writer has in the C
language, with a few restrictions, and with the addition of the powerful
string processing libraries that are available for Tcl.

One compelling _good_ restriction is that everything is executed from within
the safety of the context of a Tcl interpreter. In addition to the limited
command set of safe Tcl, only a few commands are available to access the
database via SPI and to raise messages via `elog()`. PL/Tcl provides no way to
access internals of the database server or to gain OS-level access under the
permissions of the PostgreSQL server process, as a C function can do. Thus,
unprivileged database users can be trusted to use this language; it does not
give them unlimited authority.

The other notable implementation restriction is that Tcl functions cannot be
used to create input/output functions for new data types.

Sometimes it is desirable to write Tcl functions that are not restricted to
safe Tcl. For example, one might want a Tcl function that sends email. To
handle these cases, there is a variant of PL/Tcl called `PL/TclU` (for
untrusted Tcl). This is exactly the same language except that a full Tcl
interpreter is used. _If PL/TclU is used, it must be installed as an untrusted
procedural language_ so that only database superusers can create functions in
it. The writer of a PL/TclU function must take care that the function cannot
be used to do anything unwanted, since it will be able to do anything that
could be done by a user logged in as the database administrator.

The shared object code for the PL/Tcl and PL/TclU call handlers is
automatically built and installed in the PostgreSQL library directory if Tcl
support is specified in the configuration step of the installation procedure.
To install PL/Tcl and/or PL/TclU in a particular database, use the `CREATE
EXTENSION` command, for example `CREATE EXTENSION pltcl` or `CREATE EXTENSION
pltclu`.

* * *

[Prev](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-functions.html "44.2. PL/Tcl Functions and Arguments")  
---|---|---  
Chapter 44. PL/Tcl — Tcl Procedural Language  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.2. PL/Tcl Functions and Arguments  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-overview.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

