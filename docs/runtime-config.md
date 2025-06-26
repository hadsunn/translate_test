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

Supported Versions: [Current](/docs/current/runtime-config.html "PostgreSQL 17
- Chapter 20. Server Configuration") ([17](/docs/17/runtime-config.html
"PostgreSQL 17 - Chapter 20. Server Configuration")) / [16](/docs/16/runtime-
config.html "PostgreSQL 16 - Chapter 20. Server Configuration") /
[15](/docs/15/runtime-config.html "PostgreSQL 15 - Chapter 20. Server
Configuration") / [14](/docs/14/runtime-config.html "PostgreSQL 14 -
Chapter 20. Server Configuration") / [13](/docs/13/runtime-config.html
"PostgreSQL 13 - Chapter 20. Server Configuration")

Development Versions: [18](/docs/18/runtime-config.html "PostgreSQL 18 -
Chapter 20. Server Configuration") / [devel](/docs/devel/runtime-config.html
"PostgreSQL devel - Chapter 20. Server Configuration")

Unsupported versions: [12](/docs/12/runtime-config.html "PostgreSQL 12 -
Chapter 20. Server Configuration") / [11](/docs/11/runtime-config.html
"PostgreSQL 11 - Chapter 20. Server Configuration") / [10](/docs/10/runtime-
config.html "PostgreSQL 10 - Chapter 20. Server Configuration") /
[9.6](/docs/9.6/runtime-config.html "PostgreSQL 9.6 - Chapter 20. Server
Configuration") / [9.5](/docs/9.5/runtime-config.html "PostgreSQL 9.5 -
Chapter 20. Server Configuration") / [9.4](/docs/9.4/runtime-config.html
"PostgreSQL 9.4 - Chapter 20. Server Configuration") /
[9.3](/docs/9.3/runtime-config.html "PostgreSQL 9.3 - Chapter 20. Server
Configuration") / [9.2](/docs/9.2/runtime-config.html "PostgreSQL 9.2 -
Chapter 20. Server Configuration") / [9.1](/docs/9.1/runtime-config.html
"PostgreSQL 9.1 - Chapter 20. Server Configuration") /
[9.0](/docs/9.0/runtime-config.html "PostgreSQL 9.0 - Chapter 20. Server
Configuration") / [8.4](/docs/8.4/runtime-config.html "PostgreSQL 8.4 -
Chapter 20. Server Configuration") / [8.3](/docs/8.3/runtime-config.html
"PostgreSQL 8.3 - Chapter 20. Server Configuration") /
[8.2](/docs/8.2/runtime-config.html "PostgreSQL 8.2 - Chapter 20. Server
Configuration") / [8.1](/docs/8.1/runtime-config.html "PostgreSQL 8.1 -
Chapter 20. Server Configuration") / [8.0](/docs/8.0/runtime-config.html
"PostgreSQL 8.0 - Chapter 20. Server Configuration") /
[7.4](/docs/7.4/runtime-config.html "PostgreSQL 7.4 - Chapter 20. Server
Configuration") / [7.3](/docs/7.3/runtime-config.html "PostgreSQL 7.3 -
Chapter 20. Server Configuration") / [7.2](/docs/7.2/runtime-config.html
"PostgreSQL 7.2 - Chapter 20. Server Configuration") /
[7.1](/docs/7.1/runtime-config.html "PostgreSQL 7.1 - Chapter 20. Server
Configuration")

__

Chapter 20. Server Configuration  
---  
[Prev](event-log-registration.html "19.12. Registering Event Log on Windows")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](config-setting.html "20.1. Setting Parameters")  
  
* * *

## Chapter 20. Server Configuration

**Table of Contents**

[20.1. Setting Parameters](config-setting.html)

    

[20.1.1. Parameter Names and Values](config-setting.html#CONFIG-SETTING-NAMES-
VALUES)

[20.1.2. Parameter Interaction via the Configuration File](config-
setting.html#CONFIG-SETTING-CONFIGURATION-FILE)

[20.1.3. Parameter Interaction via SQL](config-setting.html#CONFIG-SETTING-
SQL)

[20.1.4. Parameter Interaction via the Shell](config-setting.html#CONFIG-
SETTING-SHELL)

[20.1.5. Managing Configuration File Contents](config-setting.html#CONFIG-
INCLUDES)

[20.2. File Locations](runtime-config-file-locations.html)

[20.3. Connections and Authentication](runtime-config-connection.html)

    

[20.3.1. Connection Settings](runtime-config-connection.html#RUNTIME-CONFIG-
CONNECTION-SETTINGS)

[20.3.2. TCP Settings](runtime-config-connection.html#RUNTIME-CONFIG-TCP-
SETTINGS)

[20.3.3. Authentication](runtime-config-connection.html#RUNTIME-CONFIG-
CONNECTION-AUTHENTICATION)

[20.3.4. SSL](runtime-config-connection.html#RUNTIME-CONFIG-CONNECTION-SSL)

[20.4. Resource Consumption](runtime-config-resource.html)

    

[20.4.1. Memory](runtime-config-resource.html#RUNTIME-CONFIG-RESOURCE-MEMORY)

[20.4.2. Disk](runtime-config-resource.html#RUNTIME-CONFIG-RESOURCE-DISK)

[20.4.3. Kernel Resource Usage](runtime-config-resource.html#RUNTIME-CONFIG-
RESOURCE-KERNEL)

[20.4.4. Cost-based Vacuum Delay](runtime-config-resource.html#RUNTIME-CONFIG-
RESOURCE-VACUUM-COST)

[20.4.5. Background Writer](runtime-config-resource.html#RUNTIME-CONFIG-
RESOURCE-BACKGROUND-WRITER)

[20.4.6. Asynchronous Behavior](runtime-config-resource.html#RUNTIME-CONFIG-
RESOURCE-ASYNC-BEHAVIOR)

[20.5. Write Ahead Log](runtime-config-wal.html)

    

[20.5.1. Settings](runtime-config-wal.html#RUNTIME-CONFIG-WAL-SETTINGS)

[20.5.2. Checkpoints](runtime-config-wal.html#RUNTIME-CONFIG-WAL-CHECKPOINTS)

[20.5.3. Archiving](runtime-config-wal.html#RUNTIME-CONFIG-WAL-ARCHIVING)

[20.5.4. Recovery](runtime-config-wal.html#RUNTIME-CONFIG-WAL-RECOVERY)

[20.5.5. Archive Recovery](runtime-config-wal.html#RUNTIME-CONFIG-WAL-ARCHIVE-
RECOVERY)

[20.5.6. Recovery Target](runtime-config-wal.html#RUNTIME-CONFIG-WAL-RECOVERY-
TARGET)

[20.6. Replication](runtime-config-replication.html)

    

[20.6.1. Sending Servers](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-SENDER)

[20.6.2. Primary Server](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-PRIMARY)

[20.6.3. Standby Servers](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-STANDBY)

[20.6.4. Subscribers](runtime-config-replication.html#RUNTIME-CONFIG-
REPLICATION-SUBSCRIBER)

[20.7. Query Planning](runtime-config-query.html)

    

[20.7.1. Planner Method Configuration](runtime-config-query.html#RUNTIME-
CONFIG-QUERY-ENABLE)

[20.7.2. Planner Cost Constants](runtime-config-query.html#RUNTIME-CONFIG-
QUERY-CONSTANTS)

[20.7.3. Genetic Query Optimizer](runtime-config-query.html#RUNTIME-CONFIG-
QUERY-GEQO)

[20.7.4. Other Planner Options](runtime-config-query.html#RUNTIME-CONFIG-
QUERY-OTHER)

[20.8. Error Reporting and Logging](runtime-config-logging.html)

    

[20.8.1. Where to Log](runtime-config-logging.html#RUNTIME-CONFIG-LOGGING-
WHERE)

[20.8.2. When to Log](runtime-config-logging.html#RUNTIME-CONFIG-LOGGING-WHEN)

[20.8.3. What to Log](runtime-config-logging.html#RUNTIME-CONFIG-LOGGING-WHAT)

[20.8.4. Using CSV-Format Log Output](runtime-config-logging.html#RUNTIME-
CONFIG-LOGGING-CSVLOG)

[20.8.5. Using JSON-Format Log Output](runtime-config-logging.html#RUNTIME-
CONFIG-LOGGING-JSONLOG)

[20.8.6. Process Title](runtime-config-logging.html#RUNTIME-CONFIG-LOGGING-
PROC-TITLE)

[20.9. Run-time Statistics](runtime-config-statistics.html)

    

[20.9.1. Cumulative Query and Index Statistics](runtime-config-
statistics.html#RUNTIME-CONFIG-CUMULATIVE-STATISTICS)

[20.9.2. Statistics Monitoring](runtime-config-statistics.html#RUNTIME-CONFIG-
STATISTICS-MONITOR)

[20.10. Automatic Vacuuming](runtime-config-autovacuum.html)

[20.11. Client Connection Defaults](runtime-config-client.html)

    

[20.11.1. Statement Behavior](runtime-config-client.html#RUNTIME-CONFIG-
CLIENT-STATEMENT)

[20.11.2. Locale and Formatting](runtime-config-client.html#RUNTIME-CONFIG-
CLIENT-FORMAT)

[20.11.3. Shared Library Preloading](runtime-config-client.html#RUNTIME-
CONFIG-CLIENT-PRELOAD)

[20.11.4. Other Defaults](runtime-config-client.html#RUNTIME-CONFIG-CLIENT-
OTHER)

[20.12. Lock Management](runtime-config-locks.html)

[20.13. Version and Platform Compatibility](runtime-config-compatible.html)

    

[20.13.1. Previous PostgreSQL Versions](runtime-config-
compatible.html#RUNTIME-CONFIG-COMPATIBLE-VERSION)

[20.13.2. Platform and Client Compatibility](runtime-config-
compatible.html#RUNTIME-CONFIG-COMPATIBLE-CLIENTS)

[20.14. Error Handling](runtime-config-error-handling.html)

[20.15. Preset Options](runtime-config-preset.html)

[20.16. Customized Options](runtime-config-custom.html)

[20.17. Developer Options](runtime-config-developer.html)

[20.18. Short Options](runtime-config-short.html)

There are many configuration parameters that affect the behavior of the
database system. In the first section of this chapter we describe how to
interact with configuration parameters. The subsequent sections discuss each
parameter in detail.

* * *

[Prev](event-log-registration.html "19.12. Registering Event Log on Windows")  | [Up](admin.html "Part III. Server Administration") |  [Next](config-setting.html "20.1. Setting Parameters")  
---|---|---  
19.12. Registering Event Log on Windows  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.1. Setting Parameters  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

