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

Supported Versions: [Current](/docs/current/catalog-pg-ts-config.html
"PostgreSQL 17 - 53.59. pg_ts_config") ([17](/docs/17/catalog-pg-ts-
config.html "PostgreSQL 17 - 53.59. pg_ts_config")) / [16](/docs/16/catalog-
pg-ts-config.html "PostgreSQL 16 - 53.59. pg_ts_config") /
[15](/docs/15/catalog-pg-ts-config.html "PostgreSQL 15 - 53.59. pg_ts_config")
/ [14](/docs/14/catalog-pg-ts-config.html "PostgreSQL 14 -
53.59. pg_ts_config") / [13](/docs/13/catalog-pg-ts-config.html "PostgreSQL 13
- 53.59. pg_ts_config")

Development Versions: [18](/docs/18/catalog-pg-ts-config.html "PostgreSQL 18 -
53.59. pg_ts_config") / [devel](/docs/devel/catalog-pg-ts-config.html
"PostgreSQL devel - 53.59. pg_ts_config")

Unsupported versions: [12](/docs/12/catalog-pg-ts-config.html "PostgreSQL 12 -
53.59. pg_ts_config") / [11](/docs/11/catalog-pg-ts-config.html "PostgreSQL 11
- 53.59. pg_ts_config") / [10](/docs/10/catalog-pg-ts-config.html "PostgreSQL
10 - 53.59. pg_ts_config") / [9.6](/docs/9.6/catalog-pg-ts-config.html
"PostgreSQL 9.6 - 53.59. pg_ts_config") / [9.5](/docs/9.5/catalog-pg-ts-
config.html "PostgreSQL 9.5 - 53.59. pg_ts_config") / [9.4](/docs/9.4/catalog-
pg-ts-config.html "PostgreSQL 9.4 - 53.59. pg_ts_config") /
[9.3](/docs/9.3/catalog-pg-ts-config.html "PostgreSQL 9.3 -
53.59. pg_ts_config") / [9.2](/docs/9.2/catalog-pg-ts-config.html "PostgreSQL
9.2 - 53.59. pg_ts_config") / [9.1](/docs/9.1/catalog-pg-ts-config.html
"PostgreSQL 9.1 - 53.59. pg_ts_config") / [9.0](/docs/9.0/catalog-pg-ts-
config.html "PostgreSQL 9.0 - 53.59. pg_ts_config") / [8.4](/docs/8.4/catalog-
pg-ts-config.html "PostgreSQL 8.4 - 53.59. pg_ts_config") /
[8.3](/docs/8.3/catalog-pg-ts-config.html "PostgreSQL 8.3 -
53.59. pg_ts_config")

__

53.59. `pg_ts_config`  
---  
[Prev](catalog-pg-trigger.html "53.58. pg_trigger")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-ts-config-map.html "53.60. pg_ts_config_map")  
  
* * *

## 53.59. `pg_ts_config` #

The `pg_ts_config` catalog contains entries representing text search
configurations. A configuration specifies a particular text search parser and
a list of dictionaries to use for each of the parser's output token types. The
parser is shown in the `pg_ts_config` entry, but the token-to-dictionary
mapping is defined by subsidiary entries in [`pg_ts_config_map`](catalog-pg-
ts-config-map.html "53.60. pg_ts_config_map").

PostgreSQL's text search features are described at length in [Chapter
12](textsearch.html "Chapter 12. Full Text Search").

**Table  53.59. `pg_ts_config` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`cfgname` `name` Text search configuration name  
`cfgnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
configuration  
`cfgowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the configuration  
`cfgparser` `oid` (references [`pg_ts_parser`](catalog-pg-ts-parser.html
"53.62. pg_ts_parser").`oid`) The OID of the text search parser for this
configuration  
  
  

* * *

[Prev](catalog-pg-trigger.html "53.58. pg_trigger")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-ts-config-map.html "53.60. pg_ts_config_map")  
---|---|---  
53.58. `pg_trigger`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.60. `pg_ts_config_map`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-ts-config.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

