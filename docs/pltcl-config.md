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

Supported Versions: [Current](/docs/current/pltcl-config.html "PostgreSQL 17 -
44.11. PL/Tcl Configuration") ([17](/docs/17/pltcl-config.html "PostgreSQL 17
- 44.11. PL/Tcl Configuration")) / [16](/docs/16/pltcl-config.html "PostgreSQL
16 - 44.11. PL/Tcl Configuration") / [15](/docs/15/pltcl-config.html
"PostgreSQL 15 - 44.11. PL/Tcl Configuration") / [14](/docs/14/pltcl-
config.html "PostgreSQL 14 - 44.11. PL/Tcl Configuration") /
[13](/docs/13/pltcl-config.html "PostgreSQL 13 - 44.11. PL/Tcl Configuration")

Development Versions: [18](/docs/18/pltcl-config.html "PostgreSQL 18 -
44.11. PL/Tcl Configuration") / [devel](/docs/devel/pltcl-config.html
"PostgreSQL devel - 44.11. PL/Tcl Configuration")

Unsupported versions: [12](/docs/12/pltcl-config.html "PostgreSQL 12 -
44.11. PL/Tcl Configuration") / [11](/docs/11/pltcl-config.html "PostgreSQL 11
- 44.11. PL/Tcl Configuration") / [10](/docs/10/pltcl-config.html "PostgreSQL
10 - 44.11. PL/Tcl Configuration")

__

44.11. PL/Tcl Configuration  
---  
[Prev](pltcl-transactions.html "44.10. Transaction Management")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-procnames.html "44.12. Tcl Procedure Names")  
  
* * *

## 44.11. PL/Tcl Configuration #

This section lists configuration parameters that affect PL/Tcl.

`pltcl.start_proc` (`string`)  #

    

This parameter, if set to a nonempty string, specifies the name (possibly
schema-qualified) of a parameterless PL/Tcl function that is to be executed
whenever a new Tcl interpreter is created for PL/Tcl. Such a function can
perform per-session initialization, such as loading additional Tcl code. A new
Tcl interpreter is created when a PL/Tcl function is first executed in a
database session, or when an additional interpreter has to be created because
a PL/Tcl function is called by a new SQL role.

The referenced function must be written in the `pltcl` language, and must not
be marked `SECURITY DEFINER`. (These restrictions ensure that it runs in the
interpreter it's supposed to initialize.) The current user must have
permission to call it, too.

If the function fails with an error it will abort the function call that
caused the new interpreter to be created and propagate out to the calling
query, causing the current transaction or subtransaction to be aborted. Any
actions already done within Tcl won't be undone; however, that interpreter
won't be used again. If the language is used again the initialization will be
attempted again within a fresh Tcl interpreter.

Only superusers can change this setting. Although this setting can be changed
within a session, such changes will not affect Tcl interpreters that have
already been created.

`pltclu.start_proc` (`string`)  #

    

This parameter is exactly like `pltcl.start_proc`, except that it applies to
PL/TclU. The referenced function must be written in the `pltclu` language.

* * *

[Prev](pltcl-transactions.html "44.10. Transaction Management")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-procnames.html "44.12. Tcl Procedure Names")  
---|---|---  
44.10. Transaction Management  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.12. Tcl Procedure Names  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-config.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

