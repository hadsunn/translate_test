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

Supported Versions: [Current](/docs/current/catalog-pg-ts-config-map.html
"PostgreSQL 17 - 53.60. pg_ts_config_map") ([17](/docs/17/catalog-pg-ts-
config-map.html "PostgreSQL 17 - 53.60. pg_ts_config_map")) /
[16](/docs/16/catalog-pg-ts-config-map.html "PostgreSQL 16 -
53.60. pg_ts_config_map") / [15](/docs/15/catalog-pg-ts-config-map.html
"PostgreSQL 15 - 53.60. pg_ts_config_map") / [14](/docs/14/catalog-pg-ts-
config-map.html "PostgreSQL 14 - 53.60. pg_ts_config_map") /
[13](/docs/13/catalog-pg-ts-config-map.html "PostgreSQL 13 -
53.60. pg_ts_config_map")

Development Versions: [18](/docs/18/catalog-pg-ts-config-map.html "PostgreSQL
18 - 53.60. pg_ts_config_map") / [devel](/docs/devel/catalog-pg-ts-config-
map.html "PostgreSQL devel - 53.60. pg_ts_config_map")

Unsupported versions: [12](/docs/12/catalog-pg-ts-config-map.html "PostgreSQL
12 - 53.60. pg_ts_config_map") / [11](/docs/11/catalog-pg-ts-config-map.html
"PostgreSQL 11 - 53.60. pg_ts_config_map") / [10](/docs/10/catalog-pg-ts-
config-map.html "PostgreSQL 10 - 53.60. pg_ts_config_map") /
[9.6](/docs/9.6/catalog-pg-ts-config-map.html "PostgreSQL 9.6 -
53.60. pg_ts_config_map") / [9.5](/docs/9.5/catalog-pg-ts-config-map.html
"PostgreSQL 9.5 - 53.60. pg_ts_config_map") / [9.4](/docs/9.4/catalog-pg-ts-
config-map.html "PostgreSQL 9.4 - 53.60. pg_ts_config_map") /
[9.3](/docs/9.3/catalog-pg-ts-config-map.html "PostgreSQL 9.3 -
53.60. pg_ts_config_map") / [9.2](/docs/9.2/catalog-pg-ts-config-map.html
"PostgreSQL 9.2 - 53.60. pg_ts_config_map") / [9.1](/docs/9.1/catalog-pg-ts-
config-map.html "PostgreSQL 9.1 - 53.60. pg_ts_config_map") /
[9.0](/docs/9.0/catalog-pg-ts-config-map.html "PostgreSQL 9.0 -
53.60. pg_ts_config_map") / [8.4](/docs/8.4/catalog-pg-ts-config-map.html
"PostgreSQL 8.4 - 53.60. pg_ts_config_map") / [8.3](/docs/8.3/catalog-pg-ts-
config-map.html "PostgreSQL 8.3 - 53.60. pg_ts_config_map")

__

53.60. `pg_ts_config_map`  
---  
[Prev](catalog-pg-ts-config.html "53.59. pg_ts_config")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-ts-dict.html "53.61. pg_ts_dict")  
  
* * *

## 53.60. `pg_ts_config_map` #

The `pg_ts_config_map` catalog contains entries showing which text search
dictionaries should be consulted, and in what order, for each output token
type of each text search configuration's parser.

PostgreSQL's text search features are described at length in [Chapter
12](textsearch.html "Chapter 12. Full Text Search").

**Table  53.60. `pg_ts_config_map` Columns**

Column Type Description  
---  
`mapcfg` `oid` (references [`pg_ts_config`](catalog-pg-ts-config.html
"53.59. pg_ts_config").`oid`) The OID of the [`pg_ts_config`](catalog-pg-ts-
config.html "53.59. pg_ts_config") entry owning this map entry  
`maptokentype` `int4` A token type emitted by the configuration's parser  
`mapseqno` `int4` Order in which to consult this entry (lower `mapseqno`s
first)  
`mapdict` `oid` (references [`pg_ts_dict`](catalog-pg-ts-dict.html
"53.61. pg_ts_dict").`oid`) The OID of the text search dictionary to consult  
  
  

* * *

[Prev](catalog-pg-ts-config.html "53.59. pg_ts_config")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-ts-dict.html "53.61. pg_ts_dict")  
---|---|---  
53.59. `pg_ts_config`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.61. `pg_ts_dict`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-ts-config-
map.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

