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

Supported Versions: [Current](/docs/current/runtime-config-autovacuum.html
"PostgreSQL 17 - 20.10. Automatic Vacuuming") ([17](/docs/17/runtime-config-
autovacuum.html "PostgreSQL 17 - 20.10. Automatic Vacuuming")) /
[16](/docs/16/runtime-config-autovacuum.html "PostgreSQL 16 - 20.10. Automatic
Vacuuming") / [15](/docs/15/runtime-config-autovacuum.html "PostgreSQL 15 -
20.10. Automatic Vacuuming") / [14](/docs/14/runtime-config-autovacuum.html
"PostgreSQL 14 - 20.10. Automatic Vacuuming") / [13](/docs/13/runtime-config-
autovacuum.html "PostgreSQL 13 - 20.10. Automatic Vacuuming")

Unsupported versions: [12](/docs/12/runtime-config-autovacuum.html "PostgreSQL
12 - 20.10. Automatic Vacuuming") / [11](/docs/11/runtime-config-
autovacuum.html "PostgreSQL 11 - 20.10. Automatic Vacuuming") /
[10](/docs/10/runtime-config-autovacuum.html "PostgreSQL 10 - 20.10. Automatic
Vacuuming") / [9.6](/docs/9.6/runtime-config-autovacuum.html "PostgreSQL 9.6 -
20.10. Automatic Vacuuming") / [9.5](/docs/9.5/runtime-config-autovacuum.html
"PostgreSQL 9.5 - 20.10. Automatic Vacuuming") / [9.4](/docs/9.4/runtime-
config-autovacuum.html "PostgreSQL 9.4 - 20.10. Automatic Vacuuming") /
[9.3](/docs/9.3/runtime-config-autovacuum.html "PostgreSQL 9.3 -
20.10. Automatic Vacuuming") / [9.2](/docs/9.2/runtime-config-autovacuum.html
"PostgreSQL 9.2 - 20.10. Automatic Vacuuming") / [9.1](/docs/9.1/runtime-
config-autovacuum.html "PostgreSQL 9.1 - 20.10. Automatic Vacuuming") /
[9.0](/docs/9.0/runtime-config-autovacuum.html "PostgreSQL 9.0 -
20.10. Automatic Vacuuming") / [8.4](/docs/8.4/runtime-config-autovacuum.html
"PostgreSQL 8.4 - 20.10. Automatic Vacuuming") / [8.3](/docs/8.3/runtime-
config-autovacuum.html "PostgreSQL 8.3 - 20.10. Automatic Vacuuming") /
[8.2](/docs/8.2/runtime-config-autovacuum.html "PostgreSQL 8.2 -
20.10. Automatic Vacuuming") / [8.1](/docs/8.1/runtime-config-autovacuum.html
"PostgreSQL 8.1 - 20.10. Automatic Vacuuming")

__

20.10. Automatic Vacuuming  
---  
[Prev](runtime-config-statistics.html "20.9. Run-time Statistics")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-client.html "20.11. Client Connection Defaults")  
  
* * *

## 20.10. Automatic Vacuuming #

These settings control the behavior of the _autovacuum_ feature. Refer to
[Section 25.1.6](routine-vacuuming.html#AUTOVACUUM "25.1.6. The Autovacuum
Daemon") for more information. Note that many of these settings can be
overridden on a per-table basis; see [Storage Parameters](sql-
createtable.html#SQL-CREATETABLE-STORAGE-PARAMETERS "Storage Parameters").

`autovacuum` (`boolean`)  #

    

Controls whether the server should run the autovacuum launcher daemon. This is
on by default; however, [track_counts](runtime-config-statistics.html#GUC-
TRACK-COUNTS) must also be enabled for autovacuum to work. This parameter can
only be set in the `postgresql.conf` file or on the server command line;
however, autovacuuming can be disabled for individual tables by changing table
storage parameters.

Note that even when this parameter is disabled, the system will launch
autovacuum processes if necessary to prevent transaction ID wraparound. See
[Section 25.1.5](routine-vacuuming.html#VACUUM-FOR-WRAPAROUND
"25.1.5. Preventing Transaction ID Wraparound Failures") for more information.

`autovacuum_max_workers` (`integer`)  #

    

Specifies the maximum number of autovacuum processes (other than the
autovacuum launcher) that may be running at any one time. The default is
three. This parameter can only be set at server start.

`autovacuum_naptime` (`integer`)  #

    

Specifies the minimum delay between autovacuum runs on any given database. In
each round the daemon examines the database and issues `VACUUM` and `ANALYZE`
commands as needed for tables in that database. If this value is specified
without units, it is taken as seconds. The default is one minute (`1min`).
This parameter can only be set in the `postgresql.conf` file or on the server
command line.

`autovacuum_vacuum_threshold` (`integer`)  #

    

Specifies the minimum number of updated or deleted tuples needed to trigger a
`VACUUM` in any one table. The default is 50 tuples. This parameter can only
be set in the `postgresql.conf` file or on the server command line; but the
setting can be overridden for individual tables by changing table storage
parameters.

`autovacuum_vacuum_insert_threshold` (`integer`)  #

    

Specifies the number of inserted tuples needed to trigger a `VACUUM` in any
one table. The default is 1000 tuples. If -1 is specified, autovacuum will not
trigger a `VACUUM` operation on any tables based on the number of inserts.
This parameter can only be set in the `postgresql.conf` file or on the server
command line; but the setting can be overridden for individual tables by
changing table storage parameters.

`autovacuum_analyze_threshold` (`integer`)  #

    

Specifies the minimum number of inserted, updated or deleted tuples needed to
trigger an `ANALYZE` in any one table. The default is 50 tuples. This
parameter can only be set in the `postgresql.conf` file or on the server
command line; but the setting can be overridden for individual tables by
changing table storage parameters.

`autovacuum_vacuum_scale_factor` (`floating point`)  #

    

Specifies a fraction of the table size to add to `autovacuum_vacuum_threshold`
when deciding whether to trigger a `VACUUM`. The default is 0.2 (20% of table
size). This parameter can only be set in the `postgresql.conf` file or on the
server command line; but the setting can be overridden for individual tables
by changing table storage parameters.

`autovacuum_vacuum_insert_scale_factor` (`floating point`)  #

    

Specifies a fraction of the table size to add to
`autovacuum_vacuum_insert_threshold` when deciding whether to trigger a
`VACUUM`. The default is 0.2 (20% of table size). This parameter can only be
set in the `postgresql.conf` file or on the server command line; but the
setting can be overridden for individual tables by changing table storage
parameters.

`autovacuum_analyze_scale_factor` (`floating point`)  #

    

Specifies a fraction of the table size to add to
`autovacuum_analyze_threshold` when deciding whether to trigger an `ANALYZE`.
The default is 0.1 (10% of table size). This parameter can only be set in the
`postgresql.conf` file or on the server command line; but the setting can be
overridden for individual tables by changing table storage parameters.

`autovacuum_freeze_max_age` (`integer`)  #

    

Specifies the maximum age (in transactions) that a table's
`pg_class`.`relfrozenxid` field can attain before a `VACUUM` operation is
forced to prevent transaction ID wraparound within the table. Note that the
system will launch autovacuum processes to prevent wraparound even when
autovacuum is otherwise disabled.

Vacuum also allows removal of old files from the `pg_xact` subdirectory, which
is why the default is a relatively low 200 million transactions. This
parameter can only be set at server start, but the setting can be reduced for
individual tables by changing table storage parameters. For more information
see [Section 25.1.5](routine-vacuuming.html#VACUUM-FOR-WRAPAROUND
"25.1.5. Preventing Transaction ID Wraparound Failures").

`autovacuum_multixact_freeze_max_age` (`integer`)  #

    

Specifies the maximum age (in multixacts) that a table's
`pg_class`.`relminmxid` field can attain before a `VACUUM` operation is forced
to prevent multixact ID wraparound within the table. Note that the system will
launch autovacuum processes to prevent wraparound even when autovacuum is
otherwise disabled.

Vacuuming multixacts also allows removal of old files from the
`pg_multixact/members` and `pg_multixact/offsets` subdirectories, which is why
the default is a relatively low 400 million multixacts. This parameter can
only be set at server start, but the setting can be reduced for individual
tables by changing table storage parameters. For more information see [Section
25.1.5.1](routine-vacuuming.html#VACUUM-FOR-MULTIXACT-WRAPAROUND
"25.1.5.1. Multixacts and Wraparound").

`autovacuum_vacuum_cost_delay` (`floating point`)  #

    

Specifies the cost delay value that will be used in automatic `VACUUM`
operations. If -1 is specified, the regular [vacuum_cost_delay](runtime-
config-resource.html#GUC-VACUUM-COST-DELAY) value will be used. If this value
is specified without units, it is taken as milliseconds. The default value is
2 milliseconds. This parameter can only be set in the `postgresql.conf` file
or on the server command line; but the setting can be overridden for
individual tables by changing table storage parameters.

`autovacuum_vacuum_cost_limit` (`integer`)  #

    

Specifies the cost limit value that will be used in automatic `VACUUM`
operations. If -1 is specified (which is the default), the regular
[vacuum_cost_limit](runtime-config-resource.html#GUC-VACUUM-COST-LIMIT) value
will be used. Note that the value is distributed proportionally among the
running autovacuum workers, if there is more than one, so that the sum of the
limits for each worker does not exceed the value of this variable. This
parameter can only be set in the `postgresql.conf` file or on the server
command line; but the setting can be overridden for individual tables by
changing table storage parameters.

* * *

[Prev](runtime-config-statistics.html "20.9. Run-time Statistics")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-client.html "20.11. Client Connection Defaults")  
---|---|---  
20.9. Run-time Statistics  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.11. Client Connection Defaults  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-
autovacuum.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

