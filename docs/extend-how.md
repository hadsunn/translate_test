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

Supported Versions: [Current](/docs/current/extend-how.html "PostgreSQL 17 -
38.1. How Extensibility Works") ([17](/docs/17/extend-how.html "PostgreSQL 17
- 38.1. How Extensibility Works")) / [16](/docs/16/extend-how.html "PostgreSQL
16 - 38.1. How Extensibility Works") / [15](/docs/15/extend-how.html
"PostgreSQL 15 - 38.1. How Extensibility Works") / [14](/docs/14/extend-
how.html "PostgreSQL 14 - 38.1. How Extensibility Works") /
[13](/docs/13/extend-how.html "PostgreSQL 13 - 38.1. How Extensibility Works")

Development Versions: [18](/docs/18/extend-how.html "PostgreSQL 18 - 38.1. How
Extensibility Works") / [devel](/docs/devel/extend-how.html "PostgreSQL devel
- 38.1. How Extensibility Works")

Unsupported versions: [12](/docs/12/extend-how.html "PostgreSQL 12 - 38.1. How
Extensibility Works") / [11](/docs/11/extend-how.html "PostgreSQL 11 -
38.1. How Extensibility Works") / [10](/docs/10/extend-how.html "PostgreSQL 10
- 38.1. How Extensibility Works") / [9.6](/docs/9.6/extend-how.html
"PostgreSQL 9.6 - 38.1. How Extensibility Works") / [9.5](/docs/9.5/extend-
how.html "PostgreSQL 9.5 - 38.1. How Extensibility Works") /
[9.4](/docs/9.4/extend-how.html "PostgreSQL 9.4 - 38.1. How Extensibility
Works") / [9.3](/docs/9.3/extend-how.html "PostgreSQL 9.3 - 38.1. How
Extensibility Works") / [9.2](/docs/9.2/extend-how.html "PostgreSQL 9.2 -
38.1. How Extensibility Works") / [9.1](/docs/9.1/extend-how.html "PostgreSQL
9.1 - 38.1. How Extensibility Works") / [9.0](/docs/9.0/extend-how.html
"PostgreSQL 9.0 - 38.1. How Extensibility Works") / [8.4](/docs/8.4/extend-
how.html "PostgreSQL 8.4 - 38.1. How Extensibility Works") /
[8.3](/docs/8.3/extend-how.html "PostgreSQL 8.3 - 38.1. How Extensibility
Works") / [8.2](/docs/8.2/extend-how.html "PostgreSQL 8.2 - 38.1. How
Extensibility Works")

__

38.1. How Extensibility Works  
---  
[Prev](extend.html "Chapter 38. Extending SQL")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](extend-type-system.html "38.2. The PostgreSQL Type System")  
  
* * *

## 38.1. How Extensibility Works #

PostgreSQL is extensible because its operation is catalog-driven. If you are
familiar with standard relational database systems, you know that they store
information about databases, tables, columns, etc., in what are commonly known
as system catalogs. (Some systems call this the data dictionary.) The catalogs
appear to the user as tables like any other, but the DBMS stores its internal
bookkeeping in them. One key difference between PostgreSQL and standard
relational database systems is that PostgreSQL stores much more information in
its catalogs: not only information about tables and columns, but also
information about data types, functions, access methods, and so on. These
tables can be modified by the user, and since PostgreSQL bases its operation
on these tables, this means that PostgreSQL can be extended by users. By
comparison, conventional database systems can only be extended by changing
hardcoded procedures in the source code or by loading modules specially
written by the DBMS vendor.

The PostgreSQL server can moreover incorporate user-written code into itself
through dynamic loading. That is, the user can specify an object code file
(e.g., a shared library) that implements a new type or function, and
PostgreSQL will load it as required. Code written in SQL is even more trivial
to add to the server. This ability to modify its operation “on the fly” makes
PostgreSQL uniquely suited for rapid prototyping of new applications and
storage structures.

* * *

[Prev](extend.html "Chapter 38. Extending SQL")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](extend-type-system.html "38.2. The PostgreSQL Type System")  
---|---|---  
Chapter 38. Extending SQL  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.2. The PostgreSQL Type System  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/extend-how.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

