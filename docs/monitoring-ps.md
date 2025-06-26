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

Supported Versions: [Current](/docs/current/monitoring-ps.html "PostgreSQL 17
- 28.1. Standard Unix Tools") ([17](/docs/17/monitoring-ps.html "PostgreSQL 17
- 28.1. Standard Unix Tools")) / [16](/docs/16/monitoring-ps.html "PostgreSQL
16 - 28.1. Standard Unix Tools") / [15](/docs/15/monitoring-ps.html
"PostgreSQL 15 - 28.1. Standard Unix Tools") / [14](/docs/14/monitoring-
ps.html "PostgreSQL 14 - 28.1. Standard Unix Tools") /
[13](/docs/13/monitoring-ps.html "PostgreSQL 13 - 28.1. Standard Unix Tools")

Development Versions: [18](/docs/18/monitoring-ps.html "PostgreSQL 18 -
28.1. Standard Unix Tools") / [devel](/docs/devel/monitoring-ps.html
"PostgreSQL devel - 28.1. Standard Unix Tools")

Unsupported versions: [12](/docs/12/monitoring-ps.html "PostgreSQL 12 -
28.1. Standard Unix Tools") / [11](/docs/11/monitoring-ps.html "PostgreSQL 11
- 28.1. Standard Unix Tools") / [10](/docs/10/monitoring-ps.html "PostgreSQL
10 - 28.1. Standard Unix Tools") / [9.6](/docs/9.6/monitoring-ps.html
"PostgreSQL 9.6 - 28.1. Standard Unix Tools") / [9.5](/docs/9.5/monitoring-
ps.html "PostgreSQL 9.5 - 28.1. Standard Unix Tools") /
[9.4](/docs/9.4/monitoring-ps.html "PostgreSQL 9.4 - 28.1. Standard Unix
Tools") / [9.3](/docs/9.3/monitoring-ps.html "PostgreSQL 9.3 - 28.1. Standard
Unix Tools") / [9.2](/docs/9.2/monitoring-ps.html "PostgreSQL 9.2 -
28.1. Standard Unix Tools") / [9.1](/docs/9.1/monitoring-ps.html "PostgreSQL
9.1 - 28.1. Standard Unix Tools") / [9.0](/docs/9.0/monitoring-ps.html
"PostgreSQL 9.0 - 28.1. Standard Unix Tools") / [8.4](/docs/8.4/monitoring-
ps.html "PostgreSQL 8.4 - 28.1. Standard Unix Tools") /
[8.3](/docs/8.3/monitoring-ps.html "PostgreSQL 8.3 - 28.1. Standard Unix
Tools") / [8.2](/docs/8.2/monitoring-ps.html "PostgreSQL 8.2 - 28.1. Standard
Unix Tools")

__

28.1. Standard Unix Tools  
---  
[Prev](monitoring.html "Chapter 28. Monitoring Database Activity")  | [Up](monitoring.html "Chapter 28. Monitoring Database Activity") | Chapter 28. Monitoring Database Activity | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](monitoring-stats.html "28.2. The Cumulative Statistics System")  
  
* * *

## 28.1. Standard Unix Tools #

On most Unix platforms, PostgreSQL modifies its command title as reported by
`ps`, so that individual server processes can readily be identified. A sample
display is

    
    
    $ ps auxww | grep ^postgres
    postgres  15551  0.0  0.1  57536  7132 pts/0    S    18:02   0:00 postgres -i
    postgres  15554  0.0  0.0  57536  1184 ?        Ss   18:02   0:00 postgres: background writer
    postgres  15555  0.0  0.0  57536   916 ?        Ss   18:02   0:00 postgres: checkpointer
    postgres  15556  0.0  0.0  57536   916 ?        Ss   18:02   0:00 postgres: walwriter
    postgres  15557  0.0  0.0  58504  2244 ?        Ss   18:02   0:00 postgres: autovacuum launcher
    postgres  15582  0.0  0.0  58772  3080 ?        Ss   18:04   0:00 postgres: joe runbug 127.0.0.1 idle
    postgres  15606  0.0  0.0  58772  3052 ?        Ss   18:07   0:00 postgres: tgl regression [local] SELECT waiting
    postgres  15610  0.0  0.0  58772  3056 ?        Ss   18:07   0:00 postgres: tgl regression [local] idle in transaction
    

(The appropriate invocation of `ps` varies across different platforms, as do
the details of what is shown. This example is from a recent Linux system.) The
first process listed here is the primary server process. The command arguments
shown for it are the same ones used when it was launched. The next four
processes are background worker processes automatically launched by the
primary process. (The “autovacuum launcher” process will not be present if you
have set the system not to run autovacuum.) Each of the remaining processes is
a server process handling one client connection. Each such process sets its
command line display in the form

    
    
    postgres: _user_ _database_ _host_ _activity_
    

The user, database, and (client) host items remain the same for the life of
the client connection, but the activity indicator changes. The activity can be
`idle` (i.e., waiting for a client command), `idle in transaction` (waiting
for client inside a `BEGIN` block), or a command type name such as `SELECT`.
Also, `waiting` is appended if the server process is presently waiting on a
lock held by another session. In the above example we can infer that process
15606 is waiting for process 15610 to complete its transaction and thereby
release some lock. (Process 15610 must be the blocker, because there is no
other active session. In more complicated cases it would be necessary to look
into the [`pg_locks`](view-pg-locks.html "54.12. pg_locks") system view to
determine who is blocking whom.)

If [cluster_name](runtime-config-logging.html#GUC-CLUSTER-NAME) has been
configured the cluster name will also be shown in `ps` output:

    
    
    $ psql -c 'SHOW cluster_name'
     cluster_name
    --------------
     server1
    (1 row)
    
    $ ps aux|grep server1
    postgres   27093  0.0  0.0  30096  2752 ?        Ss   11:34   0:00 postgres: server1: background writer
    ...
    

If you have turned off [update_process_title](runtime-config-logging.html#GUC-
UPDATE-PROCESS-TITLE) then the activity indicator is not updated; the process
title is set only once when a new process is launched. On some platforms this
saves a measurable amount of per-command overhead; on others it's
insignificant.

### Tip

Solaris requires special handling. You must use `/usr/ucb/ps`, rather than
`/bin/ps`. You also must use two `w` flags, not just one. In addition, your
original invocation of the `postgres` command must have a shorter `ps` status
display than that provided by each server process. If you fail to do all three
things, the `ps` output for each server process will be the original
`postgres` command line.

* * *

[Prev](monitoring.html "Chapter 28. Monitoring Database Activity")  | [Up](monitoring.html "Chapter 28. Monitoring Database Activity") |  [Next](monitoring-stats.html "28.2. The Cumulative Statistics System")  
---|---|---  
Chapter 28. Monitoring Database Activity  | [Home](index.html "PostgreSQL 16.9 Documentation") |  28.2. The Cumulative Statistics System  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/monitoring-ps.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

