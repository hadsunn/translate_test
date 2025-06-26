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

Supported Versions: [Current](/docs/current/maintenance.html "PostgreSQL 17 -
Chapter 25. Routine Database Maintenance Tasks")
([17](/docs/17/maintenance.html "PostgreSQL 17 - Chapter 25. Routine Database
Maintenance Tasks")) / [16](/docs/16/maintenance.html "PostgreSQL 16 -
Chapter 25. Routine Database Maintenance Tasks") /
[15](/docs/15/maintenance.html "PostgreSQL 15 - Chapter 25. Routine Database
Maintenance Tasks") / [14](/docs/14/maintenance.html "PostgreSQL 14 -
Chapter 25. Routine Database Maintenance Tasks") /
[13](/docs/13/maintenance.html "PostgreSQL 13 - Chapter 25. Routine Database
Maintenance Tasks")

Development Versions: [18](/docs/18/maintenance.html "PostgreSQL 18 -
Chapter 25. Routine Database Maintenance Tasks") /
[devel](/docs/devel/maintenance.html "PostgreSQL devel - Chapter 25. Routine
Database Maintenance Tasks")

Unsupported versions: [12](/docs/12/maintenance.html "PostgreSQL 12 -
Chapter 25. Routine Database Maintenance Tasks") /
[11](/docs/11/maintenance.html "PostgreSQL 11 - Chapter 25. Routine Database
Maintenance Tasks") / [10](/docs/10/maintenance.html "PostgreSQL 10 -
Chapter 25. Routine Database Maintenance Tasks") /
[9.6](/docs/9.6/maintenance.html "PostgreSQL 9.6 - Chapter 25. Routine
Database Maintenance Tasks") / [9.5](/docs/9.5/maintenance.html "PostgreSQL
9.5 - Chapter 25. Routine Database Maintenance Tasks") /
[9.4](/docs/9.4/maintenance.html "PostgreSQL 9.4 - Chapter 25. Routine
Database Maintenance Tasks") / [9.3](/docs/9.3/maintenance.html "PostgreSQL
9.3 - Chapter 25. Routine Database Maintenance Tasks") /
[9.2](/docs/9.2/maintenance.html "PostgreSQL 9.2 - Chapter 25. Routine
Database Maintenance Tasks") / [9.1](/docs/9.1/maintenance.html "PostgreSQL
9.1 - Chapter 25. Routine Database Maintenance Tasks") /
[9.0](/docs/9.0/maintenance.html "PostgreSQL 9.0 - Chapter 25. Routine
Database Maintenance Tasks") / [8.4](/docs/8.4/maintenance.html "PostgreSQL
8.4 - Chapter 25. Routine Database Maintenance Tasks") /
[8.3](/docs/8.3/maintenance.html "PostgreSQL 8.3 - Chapter 25. Routine
Database Maintenance Tasks") / [8.2](/docs/8.2/maintenance.html "PostgreSQL
8.2 - Chapter 25. Routine Database Maintenance Tasks") /
[8.1](/docs/8.1/maintenance.html "PostgreSQL 8.1 - Chapter 25. Routine
Database Maintenance Tasks") / [8.0](/docs/8.0/maintenance.html "PostgreSQL
8.0 - Chapter 25. Routine Database Maintenance Tasks") /
[7.4](/docs/7.4/maintenance.html "PostgreSQL 7.4 - Chapter 25. Routine
Database Maintenance Tasks") / [7.3](/docs/7.3/maintenance.html "PostgreSQL
7.3 - Chapter 25. Routine Database Maintenance Tasks") /
[7.2](/docs/7.2/maintenance.html "PostgreSQL 7.2 - Chapter 25. Routine
Database Maintenance Tasks")

__

Chapter 25. Routine Database Maintenance Tasks  
---  
[Prev](multibyte.html "24.3. Character Set Support")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](routine-vacuuming.html "25.1. Routine Vacuuming")  
  
* * *

## Chapter 25. Routine Database Maintenance Tasks

**Table of Contents**

[25.1. Routine Vacuuming](routine-vacuuming.html)

    

[25.1.1. Vacuuming Basics](routine-vacuuming.html#VACUUM-BASICS)

[25.1.2. Recovering Disk Space](routine-vacuuming.html#VACUUM-FOR-SPACE-
RECOVERY)

[25.1.3. Updating Planner Statistics](routine-vacuuming.html#VACUUM-FOR-
STATISTICS)

[25.1.4. Updating the Visibility Map](routine-vacuuming.html#VACUUM-FOR-
VISIBILITY-MAP)

[25.1.5. Preventing Transaction ID Wraparound Failures](routine-
vacuuming.html#VACUUM-FOR-WRAPAROUND)

[25.1.6. The Autovacuum Daemon](routine-vacuuming.html#AUTOVACUUM)

[25.2. Routine Reindexing](routine-reindex.html)

[25.3. Log File Maintenance](logfile-maintenance.html)

PostgreSQL, like any database software, requires that certain tasks be
performed regularly to achieve optimum performance. The tasks discussed here
are _required_ , but they are repetitive in nature and can easily be automated
using standard tools such as cron scripts or Windows' Task Scheduler. It is
the database administrator's responsibility to set up appropriate scripts, and
to check that they execute successfully.

One obvious maintenance task is the creation of backup copies of the data on a
regular schedule. Without a recent backup, you have no chance of recovery
after a catastrophe (disk failure, fire, mistakenly dropping a critical table,
etc.). The backup and recovery mechanisms available in PostgreSQL are
discussed at length in [Chapter 26](backup.html "Chapter 26. Backup and
Restore").

The other main category of maintenance task is periodic “vacuuming” of the
database. This activity is discussed in [Section 25.1](routine-vacuuming.html
"25.1. Routine Vacuuming"). Closely related to this is updating the statistics
that will be used by the query planner, as discussed in [Section
25.1.3](routine-vacuuming.html#VACUUM-FOR-STATISTICS "25.1.3. Updating Planner
Statistics").

Another task that might need periodic attention is log file management. This
is discussed in [Section 25.3](logfile-maintenance.html "25.3. Log File
Maintenance").

[check_postgres](https://bucardo.org/check_postgres/) is available for
monitoring database health and reporting unusual conditions. check_postgres
integrates with Nagios and MRTG, but can be run standalone too.

PostgreSQL is low-maintenance compared to some other database management
systems. Nonetheless, appropriate attention to these tasks will go far towards
ensuring a pleasant and productive experience with the system.

* * *

[Prev](multibyte.html "24.3. Character Set Support")  | [Up](admin.html "Part III. Server Administration") |  [Next](routine-vacuuming.html "25.1. Routine Vacuuming")  
---|---|---  
24.3. Character Set Support  | [Home](index.html "PostgreSQL 16.9 Documentation") |  25.1. Routine Vacuuming  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/maintenance.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

