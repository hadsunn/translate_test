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

Supported Versions: [Current](/docs/current/pltcl-global.html "PostgreSQL 17 -
44.4. Global Data in PL/Tcl") ([17](/docs/17/pltcl-global.html "PostgreSQL 17
- 44.4. Global Data in PL/Tcl")) / [16](/docs/16/pltcl-global.html "PostgreSQL
16 - 44.4. Global Data in PL/Tcl") / [15](/docs/15/pltcl-global.html
"PostgreSQL 15 - 44.4. Global Data in PL/Tcl") / [14](/docs/14/pltcl-
global.html "PostgreSQL 14 - 44.4. Global Data in PL/Tcl") /
[13](/docs/13/pltcl-global.html "PostgreSQL 13 - 44.4. Global Data in PL/Tcl")

Development Versions: [18](/docs/18/pltcl-global.html "PostgreSQL 18 -
44.4. Global Data in PL/Tcl") / [devel](/docs/devel/pltcl-global.html
"PostgreSQL devel - 44.4. Global Data in PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-global.html "PostgreSQL 12 -
44.4. Global Data in PL/Tcl") / [11](/docs/11/pltcl-global.html "PostgreSQL 11
- 44.4. Global Data in PL/Tcl") / [10](/docs/10/pltcl-global.html "PostgreSQL
10 - 44.4. Global Data in PL/Tcl") / [9.6](/docs/9.6/pltcl-global.html
"PostgreSQL 9.6 - 44.4. Global Data in PL/Tcl") / [9.5](/docs/9.5/pltcl-
global.html "PostgreSQL 9.5 - 44.4. Global Data in PL/Tcl") /
[9.4](/docs/9.4/pltcl-global.html "PostgreSQL 9.4 - 44.4. Global Data in
PL/Tcl") / [9.3](/docs/9.3/pltcl-global.html "PostgreSQL 9.3 - 44.4. Global
Data in PL/Tcl") / [9.2](/docs/9.2/pltcl-global.html "PostgreSQL 9.2 -
44.4. Global Data in PL/Tcl") / [9.1](/docs/9.1/pltcl-global.html "PostgreSQL
9.1 - 44.4. Global Data in PL/Tcl") / [9.0](/docs/9.0/pltcl-global.html
"PostgreSQL 9.0 - 44.4. Global Data in PL/Tcl") / [8.4](/docs/8.4/pltcl-
global.html "PostgreSQL 8.4 - 44.4. Global Data in PL/Tcl") /
[8.3](/docs/8.3/pltcl-global.html "PostgreSQL 8.3 - 44.4. Global Data in
PL/Tcl") / [8.2](/docs/8.2/pltcl-global.html "PostgreSQL 8.2 - 44.4. Global
Data in PL/Tcl") / [8.1](/docs/8.1/pltcl-global.html "PostgreSQL 8.1 -
44.4. Global Data in PL/Tcl") / [8.0](/docs/8.0/pltcl-global.html "PostgreSQL
8.0 - 44.4. Global Data in PL/Tcl") / [7.4](/docs/7.4/pltcl-global.html
"PostgreSQL 7.4 - 44.4. Global Data in PL/Tcl")

__

44.4. Global Data in PL/Tcl  
---  
[Prev](pltcl-data.html "44.3. Data Values in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-dbaccess.html "44.5. Database Access from PL/Tcl")  
  
* * *

## 44.4. Global Data in PL/Tcl #

Sometimes it is useful to have some global data that is held between two calls
to a function or is shared between different functions. This is easily done in
PL/Tcl, but there are some restrictions that must be understood.

For security reasons, PL/Tcl executes functions called by any one SQL role in
a separate Tcl interpreter for that role. This prevents accidental or
malicious interference by one user with the behavior of another user's PL/Tcl
functions. Each such interpreter will have its own values for any “global” Tcl
variables. Thus, two PL/Tcl functions will share the same global variables if
and only if they are executed by the same SQL role. In an application wherein
a single session executes code under multiple SQL roles (via `SECURITY
DEFINER` functions, use of `SET ROLE`, etc.) you may need to take explicit
steps to ensure that PL/Tcl functions can share data. To do that, make sure
that functions that should communicate are owned by the same user, and mark
them `SECURITY DEFINER`. You must of course take care that such functions
can't be used to do anything unintended.

All PL/TclU functions used in a session execute in the same Tcl interpreter,
which of course is distinct from the interpreter(s) used for PL/Tcl functions.
So global data is automatically shared between PL/TclU functions. This is not
considered a security risk because all PL/TclU functions execute at the same
trust level, namely that of a database superuser.

To help protect PL/Tcl functions from unintentionally interfering with each
other, a global array is made available to each function via the `upvar`
command. The global name of this variable is the function's internal name, and
the local name is `GD`. It is recommended that `GD` be used for persistent
private data of a function. Use regular Tcl global variables only for values
that you specifically intend to be shared among multiple functions. (Note that
the `GD` arrays are only global within a particular interpreter, so they do
not bypass the security restrictions mentioned above.)

An example of using `GD` appears in the `spi_execp` example below.

* * *

[Prev](pltcl-data.html "44.3. Data Values in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-dbaccess.html "44.5. Database Access from PL/Tcl")  
---|---|---  
44.3. Data Values in PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.5. Database Access from PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-global.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

