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

Supported Versions: [Current](/docs/current/pltcl-data.html "PostgreSQL 17 -
44.3. Data Values in PL/Tcl") ([17](/docs/17/pltcl-data.html "PostgreSQL 17 -
44.3. Data Values in PL/Tcl")) / [16](/docs/16/pltcl-data.html "PostgreSQL 16
- 44.3. Data Values in PL/Tcl") / [15](/docs/15/pltcl-data.html "PostgreSQL 15
- 44.3. Data Values in PL/Tcl") / [14](/docs/14/pltcl-data.html "PostgreSQL 14
- 44.3. Data Values in PL/Tcl") / [13](/docs/13/pltcl-data.html "PostgreSQL 13
- 44.3. Data Values in PL/Tcl")

Development Versions: [18](/docs/18/pltcl-data.html "PostgreSQL 18 -
44.3. Data Values in PL/Tcl") / [devel](/docs/devel/pltcl-data.html
"PostgreSQL devel - 44.3. Data Values in PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-data.html "PostgreSQL 12 -
44.3. Data Values in PL/Tcl") / [11](/docs/11/pltcl-data.html "PostgreSQL 11 -
44.3. Data Values in PL/Tcl") / [10](/docs/10/pltcl-data.html "PostgreSQL 10 -
44.3. Data Values in PL/Tcl") / [9.6](/docs/9.6/pltcl-data.html "PostgreSQL
9.6 - 44.3. Data Values in PL/Tcl") / [9.5](/docs/9.5/pltcl-data.html
"PostgreSQL 9.5 - 44.3. Data Values in PL/Tcl") / [9.4](/docs/9.4/pltcl-
data.html "PostgreSQL 9.4 - 44.3. Data Values in PL/Tcl") /
[9.3](/docs/9.3/pltcl-data.html "PostgreSQL 9.3 - 44.3. Data Values in
PL/Tcl") / [9.2](/docs/9.2/pltcl-data.html "PostgreSQL 9.2 - 44.3. Data Values
in PL/Tcl") / [9.1](/docs/9.1/pltcl-data.html "PostgreSQL 9.1 - 44.3. Data
Values in PL/Tcl") / [9.0](/docs/9.0/pltcl-data.html "PostgreSQL 9.0 -
44.3. Data Values in PL/Tcl") / [8.4](/docs/8.4/pltcl-data.html "PostgreSQL
8.4 - 44.3. Data Values in PL/Tcl") / [8.3](/docs/8.3/pltcl-data.html
"PostgreSQL 8.3 - 44.3. Data Values in PL/Tcl") / [8.2](/docs/8.2/pltcl-
data.html "PostgreSQL 8.2 - 44.3. Data Values in PL/Tcl") /
[8.1](/docs/8.1/pltcl-data.html "PostgreSQL 8.1 - 44.3. Data Values in
PL/Tcl") / [8.0](/docs/8.0/pltcl-data.html "PostgreSQL 8.0 - 44.3. Data Values
in PL/Tcl") / [7.4](/docs/7.4/pltcl-data.html "PostgreSQL 7.4 - 44.3. Data
Values in PL/Tcl")

__

44.3. Data Values in PL/Tcl  
---  
[Prev](pltcl-functions.html "44.2. PL/Tcl Functions and Arguments")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-global.html "44.4. Global Data in PL/Tcl")  
  
* * *

## 44.3. Data Values in PL/Tcl #

The argument values supplied to a PL/Tcl function's code are simply the input
arguments converted to text form (just as if they had been displayed by a
`SELECT` statement). Conversely, the `return` and `return_next` commands will
accept any string that is acceptable input format for the function's declared
result type, or for the specified column of a composite result type.

* * *

[Prev](pltcl-functions.html "44.2. PL/Tcl Functions and Arguments")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-global.html "44.4. Global Data in PL/Tcl")  
---|---|---  
44.2. PL/Tcl Functions and Arguments  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.4. Global Data in PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-data.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

