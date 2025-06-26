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

Supported Versions: [Current](/docs/current/bki-structure.html "PostgreSQL 17
- 75.5. Structure of the Bootstrap BKI File") ([17](/docs/17/bki-
structure.html "PostgreSQL 17 - 75.5. Structure of the Bootstrap BKI File")) /
[16](/docs/16/bki-structure.html "PostgreSQL 16 - 75.5. Structure of the
Bootstrap BKI File") / [15](/docs/15/bki-structure.html "PostgreSQL 15 -
75.5. Structure of the Bootstrap BKI File") / [14](/docs/14/bki-structure.html
"PostgreSQL 14 - 75.5. Structure of the Bootstrap BKI File") /
[13](/docs/13/bki-structure.html "PostgreSQL 13 - 75.5. Structure of the
Bootstrap BKI File")

Development Versions: [18](/docs/18/bki-structure.html "PostgreSQL 18 -
75.5. Structure of the Bootstrap BKI File") / [devel](/docs/devel/bki-
structure.html "PostgreSQL devel - 75.5. Structure of the Bootstrap BKI File")

Unsupported versions: [12](/docs/12/bki-structure.html "PostgreSQL 12 -
75.5. Structure of the Bootstrap BKI File") / [11](/docs/11/bki-structure.html
"PostgreSQL 11 - 75.5. Structure of the Bootstrap BKI File") /
[10](/docs/10/bki-structure.html "PostgreSQL 10 - 75.5. Structure of the
Bootstrap BKI File") / [9.6](/docs/9.6/bki-structure.html "PostgreSQL 9.6 -
75.5. Structure of the Bootstrap BKI File") / [9.5](/docs/9.5/bki-
structure.html "PostgreSQL 9.5 - 75.5. Structure of the Bootstrap BKI File") /
[9.4](/docs/9.4/bki-structure.html "PostgreSQL 9.4 - 75.5. Structure of the
Bootstrap BKI File") / [9.3](/docs/9.3/bki-structure.html "PostgreSQL 9.3 -
75.5. Structure of the Bootstrap BKI File") / [9.2](/docs/9.2/bki-
structure.html "PostgreSQL 9.2 - 75.5. Structure of the Bootstrap BKI File") /
[9.1](/docs/9.1/bki-structure.html "PostgreSQL 9.1 - 75.5. Structure of the
Bootstrap BKI File") / [9.0](/docs/9.0/bki-structure.html "PostgreSQL 9.0 -
75.5. Structure of the Bootstrap BKI File") / [8.4](/docs/8.4/bki-
structure.html "PostgreSQL 8.4 - 75.5. Structure of the Bootstrap BKI File") /
[8.3](/docs/8.3/bki-structure.html "PostgreSQL 8.3 - 75.5. Structure of the
Bootstrap BKI File") / [8.2](/docs/8.2/bki-structure.html "PostgreSQL 8.2 -
75.5. Structure of the Bootstrap BKI File") / [8.1](/docs/8.1/bki-
structure.html "PostgreSQL 8.1 - 75.5. Structure of the Bootstrap BKI File")

__

75.5. Structure of the Bootstrap BKI File  
---  
[Prev](bki-commands.html "75.4. BKI Commands")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") | Chapter 75. System Catalog Declarations and Initial Contents | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](bki-example.html "75.6. BKI Example")  
  
* * *

## 75.5. Structure of the Bootstrap BKI File #

The `open` command cannot be used until the tables it uses exist and have
entries for the table that is to be opened. (These minimum tables are
`pg_class`, `pg_attribute`, `pg_proc`, and `pg_type`.) To allow those tables
themselves to be filled, `create` with the `bootstrap` option implicitly opens
the created table for data insertion.

Also, the `declare index` and `declare toast` commands cannot be used until
the system catalogs they need have been created and filled in.

Thus, the structure of the `postgres.bki` file has to be:

  1. `create bootstrap` one of the critical tables

  2. `insert` data describing at least the critical tables

  3. `close`

  4. Repeat for the other critical tables.

  5. `create` (without `bootstrap`) a noncritical table

  6. `open`

  7. `insert` desired data

  8. `close`

  9. Repeat for the other noncritical tables.

  10. Define indexes and toast tables.

  11. `build indices`

There are doubtless other, undocumented ordering dependencies.

* * *

[Prev](bki-commands.html "75.4. BKI Commands")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") |  [Next](bki-example.html "75.6. BKI Example")  
---|---|---  
75.4. BKI Commands  | [Home](index.html "PostgreSQL 16.9 Documentation") |  75.6. BKI Example  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/bki-structure.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

