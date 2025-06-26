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

Supported Versions: [Current](/docs/current/catalog-pg-extension.html
"PostgreSQL 17 - 53.22. pg_extension") ([17](/docs/17/catalog-pg-
extension.html "PostgreSQL 17 - 53.22. pg_extension")) /
[16](/docs/16/catalog-pg-extension.html "PostgreSQL 16 - 53.22. pg_extension")
/ [15](/docs/15/catalog-pg-extension.html "PostgreSQL 15 -
53.22. pg_extension") / [14](/docs/14/catalog-pg-extension.html "PostgreSQL 14
- 53.22. pg_extension") / [13](/docs/13/catalog-pg-extension.html "PostgreSQL
13 - 53.22. pg_extension")

Development Versions: [18](/docs/18/catalog-pg-extension.html "PostgreSQL 18 -
53.22. pg_extension") / [devel](/docs/devel/catalog-pg-extension.html
"PostgreSQL devel - 53.22. pg_extension")

Unsupported versions: [12](/docs/12/catalog-pg-extension.html "PostgreSQL 12 -
53.22. pg_extension") / [11](/docs/11/catalog-pg-extension.html "PostgreSQL 11
- 53.22. pg_extension") / [10](/docs/10/catalog-pg-extension.html "PostgreSQL
10 - 53.22. pg_extension") / [9.6](/docs/9.6/catalog-pg-extension.html
"PostgreSQL 9.6 - 53.22. pg_extension") / [9.5](/docs/9.5/catalog-pg-
extension.html "PostgreSQL 9.5 - 53.22. pg_extension") /
[9.4](/docs/9.4/catalog-pg-extension.html "PostgreSQL 9.4 -
53.22. pg_extension") / [9.3](/docs/9.3/catalog-pg-extension.html "PostgreSQL
9.3 - 53.22. pg_extension") / [9.2](/docs/9.2/catalog-pg-extension.html
"PostgreSQL 9.2 - 53.22. pg_extension") / [9.1](/docs/9.1/catalog-pg-
extension.html "PostgreSQL 9.1 - 53.22. pg_extension")

__

53.22. `pg_extension`  
---  
[Prev](catalog-pg-event-trigger.html "53.21. pg_event_trigger")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-foreign-data-wrapper.html "53.23. pg_foreign_data_wrapper")  
  
* * *

## 53.22. `pg_extension` #

The catalog `pg_extension` stores information about the installed extensions.
See [Section 38.17](extend-extensions.html "38.17. Packaging Related Objects
into an Extension") for details about extensions.

**Table  53.22. `pg_extension` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`extname` `name` Name of the extension  
`extowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the extension  
`extnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) Schema containing the extension's exported
objects  
`extrelocatable` `bool` True if extension can be relocated to another schema  
`extversion` `text` Version name for the extension  
`extconfig` `oid[]` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) Array of `regclass` OIDs for the extension's
configuration table(s), or `NULL` if none  
`extcondition` `text[]` Array of `WHERE`-clause filter conditions for the
extension's configuration table(s), or `NULL` if none  
  
  

Note that unlike most catalogs with a “namespace” column, `extnamespace` is
not meant to imply that the extension belongs to that schema. Extension names
are never schema-qualified. Rather, `extnamespace` indicates the schema that
contains most or all of the extension's objects. If `extrelocatable` is true,
then this schema must in fact contain all schema-qualifiable objects belonging
to the extension.

* * *

[Prev](catalog-pg-event-trigger.html "53.21. pg_event_trigger")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-foreign-data-wrapper.html "53.23. pg_foreign_data_wrapper")  
---|---|---  
53.21. `pg_event_trigger`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.23. `pg_foreign_data_wrapper`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-extension.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

