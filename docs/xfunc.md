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

Supported Versions: [Current](/docs/current/xfunc.html "PostgreSQL 17 -
38.3. User-Defined Functions") ([17](/docs/17/xfunc.html "PostgreSQL 17 -
38.3. User-Defined Functions")) / [16](/docs/16/xfunc.html "PostgreSQL 16 -
38.3. User-Defined Functions") / [15](/docs/15/xfunc.html "PostgreSQL 15 -
38.3. User-Defined Functions") / [14](/docs/14/xfunc.html "PostgreSQL 14 -
38.3. User-Defined Functions") / [13](/docs/13/xfunc.html "PostgreSQL 13 -
38.3. User-Defined Functions")

Development Versions: [18](/docs/18/xfunc.html "PostgreSQL 18 - 38.3. User-
Defined Functions") / [devel](/docs/devel/xfunc.html "PostgreSQL devel -
38.3. User-Defined Functions")

Unsupported versions: [12](/docs/12/xfunc.html "PostgreSQL 12 - 38.3. User-
Defined Functions") / [11](/docs/11/xfunc.html "PostgreSQL 11 - 38.3. User-
Defined Functions") / [10](/docs/10/xfunc.html "PostgreSQL 10 - 38.3. User-
Defined Functions") / [9.6](/docs/9.6/xfunc.html "PostgreSQL 9.6 - 38.3. User-
Defined Functions") / [9.5](/docs/9.5/xfunc.html "PostgreSQL 9.5 - 38.3. User-
Defined Functions") / [9.4](/docs/9.4/xfunc.html "PostgreSQL 9.4 - 38.3. User-
Defined Functions") / [9.3](/docs/9.3/xfunc.html "PostgreSQL 9.3 - 38.3. User-
Defined Functions") / [9.2](/docs/9.2/xfunc.html "PostgreSQL 9.2 - 38.3. User-
Defined Functions") / [9.1](/docs/9.1/xfunc.html "PostgreSQL 9.1 - 38.3. User-
Defined Functions") / [9.0](/docs/9.0/xfunc.html "PostgreSQL 9.0 - 38.3. User-
Defined Functions") / [8.4](/docs/8.4/xfunc.html "PostgreSQL 8.4 - 38.3. User-
Defined Functions") / [8.3](/docs/8.3/xfunc.html "PostgreSQL 8.3 - 38.3. User-
Defined Functions") / [8.2](/docs/8.2/xfunc.html "PostgreSQL 8.2 - 38.3. User-
Defined Functions") / [8.1](/docs/8.1/xfunc.html "PostgreSQL 8.1 - 38.3. User-
Defined Functions") / [8.0](/docs/8.0/xfunc.html "PostgreSQL 8.0 - 38.3. User-
Defined Functions") / [7.4](/docs/7.4/xfunc.html "PostgreSQL 7.4 - 38.3. User-
Defined Functions") / [7.3](/docs/7.3/xfunc.html "PostgreSQL 7.3 - 38.3. User-
Defined Functions") / [7.2](/docs/7.2/xfunc.html "PostgreSQL 7.2 - 38.3. User-
Defined Functions") / [7.1](/docs/7.1/xfunc.html "PostgreSQL 7.1 - 38.3. User-
Defined Functions")

__

38.3. User-Defined Functions  
---  
[Prev](extend-type-system.html "38.2. The PostgreSQL Type System")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xproc.html "38.4. User-Defined Procedures")  
  
* * *

## 38.3. User-Defined Functions #

PostgreSQL provides four kinds of functions:

  * query language functions (functions written in SQL) ([Section 38.5](xfunc-sql.html "38.5. Query Language \(SQL\) Functions"))

  * procedural language functions (functions written in, for example, PL/pgSQL or PL/Tcl) ([Section 38.8](xfunc-pl.html "38.8. Procedural Language Functions"))

  * internal functions ([Section 38.9](xfunc-internal.html "38.9. Internal Functions"))

  * C-language functions ([Section 38.10](xfunc-c.html "38.10. C-Language Functions"))

Every kind of function can take base types, composite types, or combinations
of these as arguments (parameters). In addition, every kind of function can
return a base type or a composite type. Functions can also be defined to
return sets of base or composite values.

Many kinds of functions can take or return certain pseudo-types (such as
polymorphic types), but the available facilities vary. Consult the description
of each kind of function for more details.

It's easiest to define SQL functions, so we'll start by discussing those. Most
of the concepts presented for SQL functions will carry over to the other types
of functions.

Throughout this chapter, it can be useful to look at the reference page of the
[`CREATE FUNCTION`](sql-createfunction.html "CREATE FUNCTION") command to
understand the examples better. Some examples from this chapter can be found
in `funcs.sql` and `funcs.c` in the `src/tutorial` directory in the PostgreSQL
source distribution.

* * *

[Prev](extend-type-system.html "38.2. The PostgreSQL Type System")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xproc.html "38.4. User-Defined Procedures")  
---|---|---  
38.2. The PostgreSQL Type System  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.4. User-Defined Procedures  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xfunc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

