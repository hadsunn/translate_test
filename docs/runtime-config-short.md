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

Supported Versions: [Current](/docs/current/runtime-config-short.html
"PostgreSQL 17 - 20.18. Short Options") ([17](/docs/17/runtime-config-
short.html "PostgreSQL 17 - 20.18. Short Options")) / [16](/docs/16/runtime-
config-short.html "PostgreSQL 16 - 20.18. Short Options") /
[15](/docs/15/runtime-config-short.html "PostgreSQL 15 - 20.18. Short
Options") / [14](/docs/14/runtime-config-short.html "PostgreSQL 14 -
20.18. Short Options") / [13](/docs/13/runtime-config-short.html "PostgreSQL
13 - 20.18. Short Options")

Development Versions: [18](/docs/18/runtime-config-short.html "PostgreSQL 18 -
20.18. Short Options") / [devel](/docs/devel/runtime-config-short.html
"PostgreSQL devel - 20.18. Short Options")

Unsupported versions: [12](/docs/12/runtime-config-short.html "PostgreSQL 12 -
20.18. Short Options") / [11](/docs/11/runtime-config-short.html "PostgreSQL
11 - 20.18. Short Options") / [10](/docs/10/runtime-config-short.html
"PostgreSQL 10 - 20.18. Short Options") / [9.6](/docs/9.6/runtime-config-
short.html "PostgreSQL 9.6 - 20.18. Short Options") / [9.5](/docs/9.5/runtime-
config-short.html "PostgreSQL 9.5 - 20.18. Short Options") /
[9.4](/docs/9.4/runtime-config-short.html "PostgreSQL 9.4 - 20.18. Short
Options") / [9.3](/docs/9.3/runtime-config-short.html "PostgreSQL 9.3 -
20.18. Short Options") / [9.2](/docs/9.2/runtime-config-short.html "PostgreSQL
9.2 - 20.18. Short Options") / [9.1](/docs/9.1/runtime-config-short.html
"PostgreSQL 9.1 - 20.18. Short Options") / [9.0](/docs/9.0/runtime-config-
short.html "PostgreSQL 9.0 - 20.18. Short Options") / [8.4](/docs/8.4/runtime-
config-short.html "PostgreSQL 8.4 - 20.18. Short Options") /
[8.3](/docs/8.3/runtime-config-short.html "PostgreSQL 8.3 - 20.18. Short
Options") / [8.2](/docs/8.2/runtime-config-short.html "PostgreSQL 8.2 -
20.18. Short Options") / [8.1](/docs/8.1/runtime-config-short.html "PostgreSQL
8.1 - 20.18. Short Options")

__

20.18. Short Options  
---  
[Prev](runtime-config-developer.html "20.17. Developer Options")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](client-authentication.html "Chapter 21. Client Authentication")  
  
* * *

## 20.18. Short Options #

For convenience there are also single letter command-line option switches
available for some parameters. They are described in [Table 20.4](runtime-
config-short.html#RUNTIME-CONFIG-SHORT-TABLE "Table 20.4. Short Option Key").
Some of these options exist for historical reasons, and their presence as a
single-letter option does not necessarily indicate an endorsement to use the
option heavily.

**Table  20.4. Short Option Key**

Short Option | Equivalent  
---|---  
`-B _`x`_` | `shared_buffers = _`x`_`  
`-d _`x`_` | `log_min_messages = DEBUG _`x`_`  
`-e` | `datestyle = euro`  
`-fb`, `-fh`, `-fi`, `-fm`, `-fn`, `-fo`, `-fs`, `-ft` | `enable_bitmapscan = off`, `enable_hashjoin = off`, `enable_indexscan = off`, `enable_mergejoin = off`, `enable_nestloop = off`, `enable_indexonlyscan = off`, `enable_seqscan = off`, `enable_tidscan = off`  
`-F` | `fsync = off`  
`-h _`x`_` | `listen_addresses = _`x`_`  
`-i` | `listen_addresses = '*'`  
`-k _`x`_` | `unix_socket_directories = _`x`_`  
`-l` | `ssl = on`  
`-N _`x`_` | `max_connections = _`x`_`  
`-O` | `allow_system_table_mods = on`  
`-p _`x`_` | `port = _`x`_`  
`-P` | `ignore_system_indexes = on`  
`-s` | `log_statement_stats = on`  
`-S _`x`_` | `work_mem = _`x`_`  
`-tpa`, `-tpl`, `-te` | `log_parser_stats = on`, `log_planner_stats = on`, `log_executor_stats = on`  
`-W _`x`_` | `post_auth_delay = _`x`_`  
  
  

* * *

[Prev](runtime-config-developer.html "20.17. Developer Options")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](client-authentication.html "Chapter 21. Client Authentication")  
---|---|---  
20.17. Developer Options  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 21. Client Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-short.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

