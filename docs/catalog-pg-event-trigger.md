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

Supported Versions: [Current](/docs/current/catalog-pg-event-trigger.html
"PostgreSQL 17 - 53.21. pg_event_trigger") ([17](/docs/17/catalog-pg-event-
trigger.html "PostgreSQL 17 - 53.21. pg_event_trigger")) /
[16](/docs/16/catalog-pg-event-trigger.html "PostgreSQL 16 -
53.21. pg_event_trigger") / [15](/docs/15/catalog-pg-event-trigger.html
"PostgreSQL 15 - 53.21. pg_event_trigger") / [14](/docs/14/catalog-pg-event-
trigger.html "PostgreSQL 14 - 53.21. pg_event_trigger") /
[13](/docs/13/catalog-pg-event-trigger.html "PostgreSQL 13 -
53.21. pg_event_trigger")

Development Versions: [18](/docs/18/catalog-pg-event-trigger.html "PostgreSQL
18 - 53.21. pg_event_trigger") / [devel](/docs/devel/catalog-pg-event-
trigger.html "PostgreSQL devel - 53.21. pg_event_trigger")

Unsupported versions: [12](/docs/12/catalog-pg-event-trigger.html "PostgreSQL
12 - 53.21. pg_event_trigger") / [11](/docs/11/catalog-pg-event-trigger.html
"PostgreSQL 11 - 53.21. pg_event_trigger") / [10](/docs/10/catalog-pg-event-
trigger.html "PostgreSQL 10 - 53.21. pg_event_trigger") /
[9.6](/docs/9.6/catalog-pg-event-trigger.html "PostgreSQL 9.6 -
53.21. pg_event_trigger") / [9.5](/docs/9.5/catalog-pg-event-trigger.html
"PostgreSQL 9.5 - 53.21. pg_event_trigger") / [9.4](/docs/9.4/catalog-pg-
event-trigger.html "PostgreSQL 9.4 - 53.21. pg_event_trigger") /
[9.3](/docs/9.3/catalog-pg-event-trigger.html "PostgreSQL 9.3 -
53.21. pg_event_trigger")

__

53.21. `pg_event_trigger`  
---  
[Prev](catalog-pg-enum.html "53.20. pg_enum")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-extension.html "53.22. pg_extension")  
  
* * *

## 53.21. `pg_event_trigger` #

The catalog `pg_event_trigger` stores event triggers. See [Chapter 40](event-
triggers.html "Chapter 40. Event Triggers") for more information.

**Table  53.21. `pg_event_trigger` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`evtname` `name` Trigger name (must be unique)  
`evtevent` `name` Identifies the event for which this trigger fires  
`evtowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the event trigger  
`evtfoid` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) The function to be called  
`evtenabled` `char` Controls in which [session_replication_role](runtime-
config-client.html#GUC-SESSION-REPLICATION-ROLE) modes the event trigger
fires. `O` = trigger fires in “origin” and “local” modes, `D` = trigger is
disabled, `R` = trigger fires in “replica” mode, `A` = trigger fires always.  
`evttags` `text[]` Command tags for which this trigger will fire. If NULL, the
firing of this trigger is not restricted on the basis of the command tag.  
  
  

* * *

[Prev](catalog-pg-enum.html "53.20. pg_enum")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-extension.html "53.22. pg_extension")  
---|---|---  
53.20. `pg_enum`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.22. `pg_extension`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-event-
trigger.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

