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

Supported Versions: [Current](/docs/current/catalog-pg-ts-dict.html
"PostgreSQL 17 - 53.61. pg_ts_dict") ([17](/docs/17/catalog-pg-ts-dict.html
"PostgreSQL 17 - 53.61. pg_ts_dict")) / [16](/docs/16/catalog-pg-ts-dict.html
"PostgreSQL 16 - 53.61. pg_ts_dict") / [15](/docs/15/catalog-pg-ts-dict.html
"PostgreSQL 15 - 53.61. pg_ts_dict") / [14](/docs/14/catalog-pg-ts-dict.html
"PostgreSQL 14 - 53.61. pg_ts_dict") / [13](/docs/13/catalog-pg-ts-dict.html
"PostgreSQL 13 - 53.61. pg_ts_dict")

Development Versions: [18](/docs/18/catalog-pg-ts-dict.html "PostgreSQL 18 -
53.61. pg_ts_dict") / [devel](/docs/devel/catalog-pg-ts-dict.html "PostgreSQL
devel - 53.61. pg_ts_dict")

Unsupported versions: [12](/docs/12/catalog-pg-ts-dict.html "PostgreSQL 12 -
53.61. pg_ts_dict") / [11](/docs/11/catalog-pg-ts-dict.html "PostgreSQL 11 -
53.61. pg_ts_dict") / [10](/docs/10/catalog-pg-ts-dict.html "PostgreSQL 10 -
53.61. pg_ts_dict") / [9.6](/docs/9.6/catalog-pg-ts-dict.html "PostgreSQL 9.6
- 53.61. pg_ts_dict") / [9.5](/docs/9.5/catalog-pg-ts-dict.html "PostgreSQL
9.5 - 53.61. pg_ts_dict") / [9.4](/docs/9.4/catalog-pg-ts-dict.html
"PostgreSQL 9.4 - 53.61. pg_ts_dict") / [9.3](/docs/9.3/catalog-pg-ts-
dict.html "PostgreSQL 9.3 - 53.61. pg_ts_dict") / [9.2](/docs/9.2/catalog-pg-
ts-dict.html "PostgreSQL 9.2 - 53.61. pg_ts_dict") / [9.1](/docs/9.1/catalog-
pg-ts-dict.html "PostgreSQL 9.1 - 53.61. pg_ts_dict") /
[9.0](/docs/9.0/catalog-pg-ts-dict.html "PostgreSQL 9.0 - 53.61. pg_ts_dict")
/ [8.4](/docs/8.4/catalog-pg-ts-dict.html "PostgreSQL 8.4 -
53.61. pg_ts_dict") / [8.3](/docs/8.3/catalog-pg-ts-dict.html "PostgreSQL 8.3
- 53.61. pg_ts_dict")

__

53.61. `pg_ts_dict`  
---  
[Prev](catalog-pg-ts-config-map.html "53.60. pg_ts_config_map")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-ts-parser.html "53.62. pg_ts_parser")  
  
* * *

## 53.61. `pg_ts_dict` #

The `pg_ts_dict` catalog contains entries defining text search dictionaries. A
dictionary depends on a text search template, which specifies all the
implementation functions needed; the dictionary itself provides values for the
user-settable parameters supported by the template. This division of labor
allows dictionaries to be created by unprivileged users. The parameters are
specified by a text string `dictinitoption`, whose format and meaning vary
depending on the template.

PostgreSQL's text search features are described at length in [Chapter
12](textsearch.html "Chapter 12. Full Text Search").

**Table  53.61. `pg_ts_dict` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`dictname` `name` Text search dictionary name  
`dictnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
dictionary  
`dictowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the dictionary  
`dicttemplate` `oid` (references [`pg_ts_template`](catalog-pg-ts-
template.html "53.63. pg_ts_template").`oid`) The OID of the text search
template for this dictionary  
`dictinitoption` `text` Initialization option string for the template  
  
  

* * *

[Prev](catalog-pg-ts-config-map.html "53.60. pg_ts_config_map")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-ts-parser.html "53.62. pg_ts_parser")  
---|---|---  
53.60. `pg_ts_config_map`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.62. `pg_ts_parser`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-ts-dict.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

