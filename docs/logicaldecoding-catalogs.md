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

Supported Versions: [Current](/docs/current/logicaldecoding-catalogs.html
"PostgreSQL 17 - 49.5. System Catalogs Related to Logical Decoding")
([17](/docs/17/logicaldecoding-catalogs.html "PostgreSQL 17 - 49.5. System
Catalogs Related to Logical Decoding")) / [16](/docs/16/logicaldecoding-
catalogs.html "PostgreSQL 16 - 49.5. System Catalogs Related to Logical
Decoding") / [15](/docs/15/logicaldecoding-catalogs.html "PostgreSQL 15 -
49.5. System Catalogs Related to Logical Decoding") /
[14](/docs/14/logicaldecoding-catalogs.html "PostgreSQL 14 - 49.5. System
Catalogs Related to Logical Decoding") / [13](/docs/13/logicaldecoding-
catalogs.html "PostgreSQL 13 - 49.5. System Catalogs Related to Logical
Decoding")

Development Versions: [18](/docs/18/logicaldecoding-catalogs.html "PostgreSQL
18 - 49.5. System Catalogs Related to Logical Decoding") /
[devel](/docs/devel/logicaldecoding-catalogs.html "PostgreSQL devel -
49.5. System Catalogs Related to Logical Decoding")

Unsupported versions: [12](/docs/12/logicaldecoding-catalogs.html "PostgreSQL
12 - 49.5. System Catalogs Related to Logical Decoding") /
[11](/docs/11/logicaldecoding-catalogs.html "PostgreSQL 11 - 49.5. System
Catalogs Related to Logical Decoding") / [10](/docs/10/logicaldecoding-
catalogs.html "PostgreSQL 10 - 49.5. System Catalogs Related to Logical
Decoding") / [9.6](/docs/9.6/logicaldecoding-catalogs.html "PostgreSQL 9.6 -
49.5. System Catalogs Related to Logical Decoding") /
[9.5](/docs/9.5/logicaldecoding-catalogs.html "PostgreSQL 9.5 - 49.5. System
Catalogs Related to Logical Decoding") / [9.4](/docs/9.4/logicaldecoding-
catalogs.html "PostgreSQL 9.4 - 49.5. System Catalogs Related to Logical
Decoding")

__

49.5. System Catalogs Related to Logical Decoding  
---  
[Prev](logicaldecoding-sql.html "49.4. Logical Decoding SQL Interface")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-output-plugin.html "49.6. Logical Decoding Output Plugins")  
  
* * *

## 49.5. System Catalogs Related to Logical Decoding #

The [`pg_replication_slots`](view-pg-replication-slots.html
"54.19. pg_replication_slots") view and the
[`pg_stat_replication`](monitoring-stats.html#MONITORING-PG-STAT-REPLICATION-
VIEW "28.2.4. pg_stat_replication") view provide information about the current
state of replication slots and streaming replication connections respectively.
These views apply to both physical and logical replication. The
[`pg_stat_replication_slots`](monitoring-stats.html#MONITORING-PG-STAT-
REPLICATION-SLOTS-VIEW "28.2.5. pg_stat_replication_slots") view provides
statistics information about the logical replication slots.

* * *

[Prev](logicaldecoding-sql.html "49.4. Logical Decoding SQL Interface")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-output-plugin.html "49.6. Logical Decoding Output Plugins")  
---|---|---  
49.4. Logical Decoding SQL Interface  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.6. Logical Decoding Output Plugins  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-
catalogs.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

