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

Supported Versions: [Current](/docs/current/recovery-config.html "PostgreSQL
17 - O.1. recovery.conf file merged into postgresql.conf")
([17](/docs/17/recovery-config.html "PostgreSQL 17 - O.1. recovery.conf file
merged into postgresql.conf")) / [16](/docs/16/recovery-config.html
"PostgreSQL 16 - O.1. recovery.conf file merged into postgresql.conf") /
[15](/docs/15/recovery-config.html "PostgreSQL 15 - O.1. recovery.conf file
merged into postgresql.conf") / [14](/docs/14/recovery-config.html "PostgreSQL
14 - O.1. recovery.conf file merged into postgresql.conf") /
[13](/docs/13/recovery-config.html "PostgreSQL 13 - O.1. recovery.conf file
merged into postgresql.conf")

Development Versions: [18](/docs/18/recovery-config.html "PostgreSQL 18 -
O.1. recovery.conf file merged into postgresql.conf") /
[devel](/docs/devel/recovery-config.html "PostgreSQL devel -
O.1. recovery.conf file merged into postgresql.conf")

Unsupported versions: [12](/docs/12/recovery-config.html "PostgreSQL 12 -
O.1. recovery.conf file merged into postgresql.conf") /
[11](/docs/11/recovery-config.html "PostgreSQL 11 - O.1. recovery.conf file
merged into postgresql.conf") / [10](/docs/10/recovery-config.html "PostgreSQL
10 - O.1. recovery.conf file merged into postgresql.conf") /
[9.6](/docs/9.6/recovery-config.html "PostgreSQL 9.6 - O.1. recovery.conf file
merged into postgresql.conf") / [9.5](/docs/9.5/recovery-config.html
"PostgreSQL 9.5 - O.1. recovery.conf file merged into postgresql.conf") /
[9.4](/docs/9.4/recovery-config.html "PostgreSQL 9.4 - O.1. recovery.conf file
merged into postgresql.conf") / [9.3](/docs/9.3/recovery-config.html
"PostgreSQL 9.3 - O.1. recovery.conf file merged into postgresql.conf") /
[9.2](/docs/9.2/recovery-config.html "PostgreSQL 9.2 - O.1. recovery.conf file
merged into postgresql.conf") / [9.1](/docs/9.1/recovery-config.html
"PostgreSQL 9.1 - O.1. recovery.conf file merged into postgresql.conf") /
[9.0](/docs/9.0/recovery-config.html "PostgreSQL 9.0 - O.1. recovery.conf file
merged into postgresql.conf")

__

O.1. `recovery.conf` file merged into `postgresql.conf`  
---  
[Prev](appendix-obsolete.html "Appendix O. Obsolete or Renamed Features")  | [Up](appendix-obsolete.html "Appendix O. Obsolete or Renamed Features") | Appendix O. Obsolete or Renamed Features | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](default-roles.html "O.2. Default Roles Renamed to Predefined Roles")  
  
* * *

## O.1. `recovery.conf` file merged into `postgresql.conf` #

PostgreSQL 11 and below used a configuration file named `recovery.conf` to
manage replicas and standbys. Support for this file was removed in PostgreSQL
12. See [the release notes for PostgreSQL 12](release-prior.html "E.11. Prior
Releases") for details on this change.

On PostgreSQL 12 and above, [archive recovery, streaming replication, and
PITR](continuous-archiving.html "26.3. Continuous Archiving and Point-in-Time
Recovery \(PITR\)") are configured using [normal server configuration
parameters](runtime-config-replication.html#RUNTIME-CONFIG-REPLICATION-STANDBY
"20.6.3. Standby Servers"). These are set in `postgresql.conf` or via [ALTER
SYSTEM](sql-altersystem.html "ALTER SYSTEM") like any other parameter.

The server will not start if a `recovery.conf` exists.

PostgreSQL 15 and below had a setting `promote_trigger_file`, or
`trigger_file` before 12. Use `pg_ctl promote` or call `pg_promote()` to
promote a standby instead.

The `standby_mode` setting has been removed. A `standby.signal` file in the
data directory is used instead. See [Standby Server Operation](warm-
standby.html#STANDBY-SERVER-OPERATION "27.2.2. Standby Server Operation") for
details.

* * *

[Prev](appendix-obsolete.html "Appendix O. Obsolete or Renamed Features")  | [Up](appendix-obsolete.html "Appendix O. Obsolete or Renamed Features") |  [Next](default-roles.html "O.2. Default Roles Renamed to Predefined Roles")  
---|---|---  
Appendix O. Obsolete or Renamed Features  | [Home](index.html "PostgreSQL 16.9 Documentation") |  O.2. Default Roles Renamed to Predefined Roles  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/recovery-config.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

