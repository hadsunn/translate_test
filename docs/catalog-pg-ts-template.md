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

Supported Versions: [Current](/docs/current/catalog-pg-ts-template.html
"PostgreSQL 17 - 53.63. pg_ts_template") ([17](/docs/17/catalog-pg-ts-
template.html "PostgreSQL 17 - 53.63. pg_ts_template")) /
[16](/docs/16/catalog-pg-ts-template.html "PostgreSQL 16 -
53.63. pg_ts_template") / [15](/docs/15/catalog-pg-ts-template.html
"PostgreSQL 15 - 53.63. pg_ts_template") / [14](/docs/14/catalog-pg-ts-
template.html "PostgreSQL 14 - 53.63. pg_ts_template") /
[13](/docs/13/catalog-pg-ts-template.html "PostgreSQL 13 -
53.63. pg_ts_template")

Development Versions: [18](/docs/18/catalog-pg-ts-template.html "PostgreSQL 18
- 53.63. pg_ts_template") / [devel](/docs/devel/catalog-pg-ts-template.html
"PostgreSQL devel - 53.63. pg_ts_template")

Unsupported versions: [12](/docs/12/catalog-pg-ts-template.html "PostgreSQL 12
- 53.63. pg_ts_template") / [11](/docs/11/catalog-pg-ts-template.html
"PostgreSQL 11 - 53.63. pg_ts_template") / [10](/docs/10/catalog-pg-ts-
template.html "PostgreSQL 10 - 53.63. pg_ts_template") /
[9.6](/docs/9.6/catalog-pg-ts-template.html "PostgreSQL 9.6 -
53.63. pg_ts_template") / [9.5](/docs/9.5/catalog-pg-ts-template.html
"PostgreSQL 9.5 - 53.63. pg_ts_template") / [9.4](/docs/9.4/catalog-pg-ts-
template.html "PostgreSQL 9.4 - 53.63. pg_ts_template") /
[9.3](/docs/9.3/catalog-pg-ts-template.html "PostgreSQL 9.3 -
53.63. pg_ts_template") / [9.2](/docs/9.2/catalog-pg-ts-template.html
"PostgreSQL 9.2 - 53.63. pg_ts_template") / [9.1](/docs/9.1/catalog-pg-ts-
template.html "PostgreSQL 9.1 - 53.63. pg_ts_template") /
[9.0](/docs/9.0/catalog-pg-ts-template.html "PostgreSQL 9.0 -
53.63. pg_ts_template") / [8.4](/docs/8.4/catalog-pg-ts-template.html
"PostgreSQL 8.4 - 53.63. pg_ts_template") / [8.3](/docs/8.3/catalog-pg-ts-
template.html "PostgreSQL 8.3 - 53.63. pg_ts_template")

__

53.63. `pg_ts_template`  
---  
[Prev](catalog-pg-ts-parser.html "53.62. pg_ts_parser")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-type.html "53.64. pg_type")  
  
* * *

## 53.63. `pg_ts_template` #

The `pg_ts_template` catalog contains entries defining text search templates.
A template is the implementation skeleton for a class of text search
dictionaries. Since a template must be implemented by C-language-level
functions, creation of new templates is restricted to database superusers.

PostgreSQL's text search features are described at length in [Chapter
12](textsearch.html "Chapter 12. Full Text Search").

**Table  53.63. `pg_ts_template` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`tmplname` `name` Text search template name  
`tmplnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
template  
`tmplinit` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) OID of the template's initialization function (zero
if none)  
`tmpllexize` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) OID of the template's lexize function  
  
  

* * *

[Prev](catalog-pg-ts-parser.html "53.62. pg_ts_parser")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-type.html "53.64. pg_type")  
---|---|---  
53.62. `pg_ts_parser`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.64. `pg_type`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-ts-template.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

