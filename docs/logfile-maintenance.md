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

Supported Versions: [Current](/docs/current/logfile-maintenance.html
"PostgreSQL 17 - 25.3. Log File Maintenance") ([17](/docs/17/logfile-
maintenance.html "PostgreSQL 17 - 25.3. Log File Maintenance")) /
[16](/docs/16/logfile-maintenance.html "PostgreSQL 16 - 25.3. Log File
Maintenance") / [15](/docs/15/logfile-maintenance.html "PostgreSQL 15 -
25.3. Log File Maintenance") / [14](/docs/14/logfile-maintenance.html
"PostgreSQL 14 - 25.3. Log File Maintenance") / [13](/docs/13/logfile-
maintenance.html "PostgreSQL 13 - 25.3. Log File Maintenance")

Development Versions: [18](/docs/18/logfile-maintenance.html "PostgreSQL 18 -
25.3. Log File Maintenance") / [devel](/docs/devel/logfile-maintenance.html
"PostgreSQL devel - 25.3. Log File Maintenance")

Unsupported versions: [12](/docs/12/logfile-maintenance.html "PostgreSQL 12 -
25.3. Log File Maintenance") / [11](/docs/11/logfile-maintenance.html
"PostgreSQL 11 - 25.3. Log File Maintenance") / [10](/docs/10/logfile-
maintenance.html "PostgreSQL 10 - 25.3. Log File Maintenance") /
[9.6](/docs/9.6/logfile-maintenance.html "PostgreSQL 9.6 - 25.3. Log File
Maintenance") / [9.5](/docs/9.5/logfile-maintenance.html "PostgreSQL 9.5 -
25.3. Log File Maintenance") / [9.4](/docs/9.4/logfile-maintenance.html
"PostgreSQL 9.4 - 25.3. Log File Maintenance") / [9.3](/docs/9.3/logfile-
maintenance.html "PostgreSQL 9.3 - 25.3. Log File Maintenance") /
[9.2](/docs/9.2/logfile-maintenance.html "PostgreSQL 9.2 - 25.3. Log File
Maintenance") / [9.1](/docs/9.1/logfile-maintenance.html "PostgreSQL 9.1 -
25.3. Log File Maintenance") / [9.0](/docs/9.0/logfile-maintenance.html
"PostgreSQL 9.0 - 25.3. Log File Maintenance") / [8.4](/docs/8.4/logfile-
maintenance.html "PostgreSQL 8.4 - 25.3. Log File Maintenance") /
[8.3](/docs/8.3/logfile-maintenance.html "PostgreSQL 8.3 - 25.3. Log File
Maintenance") / [8.2](/docs/8.2/logfile-maintenance.html "PostgreSQL 8.2 -
25.3. Log File Maintenance") / [8.1](/docs/8.1/logfile-maintenance.html
"PostgreSQL 8.1 - 25.3. Log File Maintenance") / [8.0](/docs/8.0/logfile-
maintenance.html "PostgreSQL 8.0 - 25.3. Log File Maintenance") /
[7.4](/docs/7.4/logfile-maintenance.html "PostgreSQL 7.4 - 25.3. Log File
Maintenance") / [7.3](/docs/7.3/logfile-maintenance.html "PostgreSQL 7.3 -
25.3. Log File Maintenance") / [7.2](/docs/7.2/logfile-maintenance.html
"PostgreSQL 7.2 - 25.3. Log File Maintenance")

__

25.3. Log File Maintenance  
---  
[Prev](routine-reindex.html "25.2. Routine Reindexing")  | [Up](maintenance.html "Chapter 25. Routine Database Maintenance Tasks") | Chapter 25. Routine Database Maintenance Tasks | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](backup.html "Chapter 26. Backup and Restore")  
  
* * *

## 25.3. Log File Maintenance #

It is a good idea to save the database server's log output somewhere, rather
than just discarding it via `/dev/null`. The log output is invaluable when
diagnosing problems.

### Note

The server log can contain sensitive information and needs to be protected, no
matter how or where it is stored, or the destination to which it is routed.
For example, some DDL statements might contain plaintext passwords or other
authentication details. Logged statements at the `ERROR` level might show the
SQL source code for applications and might also contain some parts of data
rows. Recording data, events and related information is the intended function
of this facility, so this is not a leakage or a bug. Please ensure the server
logs are visible only to appropriately authorized people.

Log output tends to be voluminous (especially at higher debug levels) so you
won't want to save it indefinitely. You need to _rotate_ the log files so that
new log files are started and old ones removed after a reasonable period of
time.

If you simply direct the stderr of `postgres` into a file, you will have log
output, but the only way to truncate the log file is to stop and restart the
server. This might be acceptable if you are using PostgreSQL in a development
environment, but few production servers would find this behavior acceptable.

A better approach is to send the server's stderr output to some type of log
rotation program. There is a built-in log rotation facility, which you can use
by setting the configuration parameter `logging_collector` to `true` in
`postgresql.conf`. The control parameters for this program are described in
[Section 20.8.1](runtime-config-logging.html#RUNTIME-CONFIG-LOGGING-WHERE
"20.8.1. Where to Log"). You can also use this approach to capture the log
data in machine readable CSV (comma-separated values) format.

Alternatively, you might prefer to use an external log rotation program if you
have one that you are already using with other server software. For example,
the rotatelogs tool included in the Apache distribution can be used with
PostgreSQL. One way to do this is to pipe the server's stderr output to the
desired program. If you start the server with `pg_ctl`, then stderr is already
redirected to stdout, so you just need a pipe command, for example:

    
    
    pg_ctl start | rotatelogs /var/log/pgsql_log 86400
    

You can combine these approaches by setting up logrotate to collect log files
produced by PostgreSQL built-in logging collector. In this case, the logging
collector defines the names and location of the log files, while logrotate
periodically archives these files. When initiating log rotation, logrotate
must ensure that the application sends further output to the new file. This is
commonly done with a `postrotate` script that sends a `SIGHUP` signal to the
application, which then reopens the log file. In PostgreSQL, you can run
`pg_ctl` with the `logrotate` option instead. When the server receives this
command, the server either switches to a new log file or reopens the existing
file, depending on the logging configuration (see [Section 20.8.1](runtime-
config-logging.html#RUNTIME-CONFIG-LOGGING-WHERE "20.8.1. Where to Log")).

### Note

When using static log file names, the server might fail to reopen the log file
if the max open file limit is reached or a file table overflow occurs. In this
case, log messages are sent to the old log file until a successful log
rotation. If logrotate is configured to compress the log file and delete it,
the server may lose the messages logged in this time frame. To avoid this
issue, you can configure the logging collector to dynamically assign log file
names and use a `prerotate` script to ignore open log files.

Another production-grade approach to managing log output is to send it to
syslog and let syslog deal with file rotation. To do this, set the
configuration parameter `log_destination` to `syslog` (to log to syslog only)
in `postgresql.conf`. Then you can send a `SIGHUP` signal to the syslog daemon
whenever you want to force it to start writing a new log file. If you want to
automate log rotation, the logrotate program can be configured to work with
log files from syslog.

On many systems, however, syslog is not very reliable, particularly with large
log messages; it might truncate or drop messages just when you need them the
most. Also, on Linux, syslog will flush each message to disk, yielding poor
performance. (You can use a “`-`” at the start of the file name in the syslog
configuration file to disable syncing.)

Note that all the solutions described above take care of starting new log
files at configurable intervals, but they do not handle deletion of old, no-
longer-useful log files. You will probably want to set up a batch job to
periodically delete old log files. Another possibility is to configure the
rotation program so that old log files are overwritten cyclically.

[pgBadger](https://pgbadger.darold.net/) is an external project that does
sophisticated log file analysis.
[check_postgres](https://bucardo.org/check_postgres/) provides Nagios alerts
when important messages appear in the log files, as well as detection of many
other extraordinary conditions.

* * *

[Prev](routine-reindex.html "25.2. Routine Reindexing")  | [Up](maintenance.html "Chapter 25. Routine Database Maintenance Tasks") |  [Next](backup.html "Chapter 26. Backup and Restore")  
---|---|---  
25.2. Routine Reindexing  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 26. Backup and Restore  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logfile-maintenance.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

