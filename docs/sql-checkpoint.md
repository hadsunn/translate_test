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

Supported Versions: [Current](/docs/current/sql-checkpoint.html "PostgreSQL 17
- CHECKPOINT") ([17](/docs/17/sql-checkpoint.html "PostgreSQL 17 -
CHECKPOINT")) / [16](/docs/16/sql-checkpoint.html "PostgreSQL 16 -
CHECKPOINT") / [15](/docs/15/sql-checkpoint.html "PostgreSQL 15 - CHECKPOINT")
/ [14](/docs/14/sql-checkpoint.html "PostgreSQL 14 - CHECKPOINT") /
[13](/docs/13/sql-checkpoint.html "PostgreSQL 13 - CHECKPOINT")

Development Versions: [18](/docs/18/sql-checkpoint.html "PostgreSQL 18 -
CHECKPOINT") / [devel](/docs/devel/sql-checkpoint.html "PostgreSQL devel -
CHECKPOINT")

Unsupported versions: [12](/docs/12/sql-checkpoint.html "PostgreSQL 12 -
CHECKPOINT") / [11](/docs/11/sql-checkpoint.html "PostgreSQL 11 - CHECKPOINT")
/ [10](/docs/10/sql-checkpoint.html "PostgreSQL 10 - CHECKPOINT") /
[9.6](/docs/9.6/sql-checkpoint.html "PostgreSQL 9.6 - CHECKPOINT") /
[9.5](/docs/9.5/sql-checkpoint.html "PostgreSQL 9.5 - CHECKPOINT") /
[9.4](/docs/9.4/sql-checkpoint.html "PostgreSQL 9.4 - CHECKPOINT") /
[9.3](/docs/9.3/sql-checkpoint.html "PostgreSQL 9.3 - CHECKPOINT") /
[9.2](/docs/9.2/sql-checkpoint.html "PostgreSQL 9.2 - CHECKPOINT") /
[9.1](/docs/9.1/sql-checkpoint.html "PostgreSQL 9.1 - CHECKPOINT") /
[9.0](/docs/9.0/sql-checkpoint.html "PostgreSQL 9.0 - CHECKPOINT") /
[8.4](/docs/8.4/sql-checkpoint.html "PostgreSQL 8.4 - CHECKPOINT") /
[8.3](/docs/8.3/sql-checkpoint.html "PostgreSQL 8.3 - CHECKPOINT") /
[8.2](/docs/8.2/sql-checkpoint.html "PostgreSQL 8.2 - CHECKPOINT") /
[8.1](/docs/8.1/sql-checkpoint.html "PostgreSQL 8.1 - CHECKPOINT") /
[8.0](/docs/8.0/sql-checkpoint.html "PostgreSQL 8.0 - CHECKPOINT") /
[7.4](/docs/7.4/sql-checkpoint.html "PostgreSQL 7.4 - CHECKPOINT") /
[7.3](/docs/7.3/sql-checkpoint.html "PostgreSQL 7.3 - CHECKPOINT") /
[7.2](/docs/7.2/sql-checkpoint.html "PostgreSQL 7.2 - CHECKPOINT") /
[7.1](/docs/7.1/sql-checkpoint.html "PostgreSQL 7.1 - CHECKPOINT")

__

CHECKPOINT  
---  
[Prev](sql-call.html "CALL")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-close.html "CLOSE")  
  
* * *

## CHECKPOINT

CHECKPOINT — force a write-ahead log checkpoint

## Synopsis

    
    
    CHECKPOINT
    

## Description

A checkpoint is a point in the write-ahead log sequence at which all data
files have been updated to reflect the information in the log. All data files
will be flushed to disk. Refer to [Section 30.5](wal-configuration.html
"30.5. WAL Configuration") for more details about what happens during a
checkpoint.

The `CHECKPOINT` command forces an immediate checkpoint when the command is
issued, without waiting for a regular checkpoint scheduled by the system
(controlled by the settings in [Section 20.5.2](runtime-config-
wal.html#RUNTIME-CONFIG-WAL-CHECKPOINTS "20.5.2. Checkpoints")). `CHECKPOINT`
is not intended for use during normal operation.

If executed during recovery, the `CHECKPOINT` command will force a
restartpoint (see [Section 30.5](wal-configuration.html "30.5. WAL
Configuration")) rather than writing a new checkpoint.

Only superusers or users with the privileges of the
[`pg_checkpoint`](predefined-roles.html#PREDEFINED-ROLES-TABLE
"Table 22.1. Predefined Roles") role can call `CHECKPOINT`.

## Compatibility

The `CHECKPOINT` command is a PostgreSQL language extension.

* * *

[Prev](sql-call.html "CALL")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-close.html "CLOSE")  
---|---|---  
CALL  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CLOSE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-checkpoint.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

