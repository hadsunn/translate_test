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

Supported Versions: [Current](/docs/current/runtime-config-locks.html
"PostgreSQL 17 - 20.12. Lock Management") ([17](/docs/17/runtime-config-
locks.html "PostgreSQL 17 - 20.12. Lock Management")) / [16](/docs/16/runtime-
config-locks.html "PostgreSQL 16 - 20.12. Lock Management") /
[15](/docs/15/runtime-config-locks.html "PostgreSQL 15 - 20.12. Lock
Management") / [14](/docs/14/runtime-config-locks.html "PostgreSQL 14 -
20.12. Lock Management") / [13](/docs/13/runtime-config-locks.html "PostgreSQL
13 - 20.12. Lock Management")

Development Versions: [18](/docs/18/runtime-config-locks.html "PostgreSQL 18 -
20.12. Lock Management") / [devel](/docs/devel/runtime-config-locks.html
"PostgreSQL devel - 20.12. Lock Management")

Unsupported versions: [12](/docs/12/runtime-config-locks.html "PostgreSQL 12 -
20.12. Lock Management") / [11](/docs/11/runtime-config-locks.html "PostgreSQL
11 - 20.12. Lock Management") / [10](/docs/10/runtime-config-locks.html
"PostgreSQL 10 - 20.12. Lock Management") / [9.6](/docs/9.6/runtime-config-
locks.html "PostgreSQL 9.6 - 20.12. Lock Management") /
[9.5](/docs/9.5/runtime-config-locks.html "PostgreSQL 9.5 - 20.12. Lock
Management") / [9.4](/docs/9.4/runtime-config-locks.html "PostgreSQL 9.4 -
20.12. Lock Management") / [9.3](/docs/9.3/runtime-config-locks.html
"PostgreSQL 9.3 - 20.12. Lock Management") / [9.2](/docs/9.2/runtime-config-
locks.html "PostgreSQL 9.2 - 20.12. Lock Management") /
[9.1](/docs/9.1/runtime-config-locks.html "PostgreSQL 9.1 - 20.12. Lock
Management") / [9.0](/docs/9.0/runtime-config-locks.html "PostgreSQL 9.0 -
20.12. Lock Management") / [8.4](/docs/8.4/runtime-config-locks.html
"PostgreSQL 8.4 - 20.12. Lock Management") / [8.3](/docs/8.3/runtime-config-
locks.html "PostgreSQL 8.3 - 20.12. Lock Management") /
[8.2](/docs/8.2/runtime-config-locks.html "PostgreSQL 8.2 - 20.12. Lock
Management") / [8.1](/docs/8.1/runtime-config-locks.html "PostgreSQL 8.1 -
20.12. Lock Management")

__

20.12. Lock Management  
---  
[Prev](runtime-config-client.html "20.11. Client Connection Defaults")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-compatible.html "20.13. Version and Platform Compatibility")  
  
* * *

## 20.12. Lock Management #

`deadlock_timeout` (`integer`)  #

    

This is the amount of time to wait on a lock before checking to see if there
is a deadlock condition. The check for deadlock is relatively expensive, so
the server doesn't run it every time it waits for a lock. We optimistically
assume that deadlocks are not common in production applications and just wait
on the lock for a while before checking for a deadlock. Increasing this value
reduces the amount of time wasted in needless deadlock checks, but slows down
reporting of real deadlock errors. If this value is specified without units,
it is taken as milliseconds. The default is one second (`1s`), which is
probably about the smallest value you would want in practice. On a heavily
loaded server you might want to raise it. Ideally the setting should exceed
your typical transaction time, so as to improve the odds that a lock will be
released before the waiter decides to check for deadlock. Only superusers and
users with the appropriate `SET` privilege can change this setting.

When [log_lock_waits](runtime-config-logging.html#GUC-LOG-LOCK-WAITS) is set,
this parameter also determines the amount of time to wait before a log message
is issued about the lock wait. If you are trying to investigate locking delays
you might want to set a shorter than normal `deadlock_timeout`.

`max_locks_per_transaction` (`integer`)  #

    

The shared lock table has space for `max_locks_per_transaction` objects (e.g.,
tables) per server process or prepared transaction; hence, no more than this
many distinct objects can be locked at any one time. This parameter limits the
average number of object locks used by each transaction; individual
transactions can lock more objects as long as the locks of all transactions
fit in the lock table. This is _not_ the number of rows that can be locked;
that value is unlimited. The default, 64, has historically proven sufficient,
but you might need to raise this value if you have queries that touch many
different tables in a single transaction, e.g., query of a parent table with
many children. This parameter can only be set at server start.

When running a standby server, you must set this parameter to have the same or
higher value as on the primary server. Otherwise, queries will not be allowed
in the standby server.

`max_pred_locks_per_transaction` (`integer`)  #

    

The shared predicate lock table has space for `max_pred_locks_per_transaction`
objects (e.g., tables) per server process or prepared transaction; hence, no
more than this many distinct objects can be locked at any one time. This
parameter limits the average number of object locks used by each transaction;
individual transactions can lock more objects as long as the locks of all
transactions fit in the lock table. This is _not_ the number of rows that can
be locked; that value is unlimited. The default, 64, has historically proven
sufficient, but you might need to raise this value if you have clients that
touch many different tables in a single serializable transaction. This
parameter can only be set at server start.

`max_pred_locks_per_relation` (`integer`)  #

    

This controls how many pages or tuples of a single relation can be predicate-
locked before the lock is promoted to covering the whole relation. Values
greater than or equal to zero mean an absolute limit, while negative values
mean [max_pred_locks_per_transaction](runtime-config-locks.html#GUC-MAX-PRED-
LOCKS-PER-TRANSACTION) divided by the absolute value of this setting. The
default is -2, which keeps the behavior from previous versions of PostgreSQL.
This parameter can only be set in the `postgresql.conf` file or on the server
command line.

`max_pred_locks_per_page` (`integer`)  #

    

This controls how many rows on a single page can be predicate-locked before
the lock is promoted to covering the whole page. The default is 2. This
parameter can only be set in the `postgresql.conf` file or on the server
command line.

* * *

[Prev](runtime-config-client.html "20.11. Client Connection Defaults")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-compatible.html "20.13. Version and Platform Compatibility")  
---|---|---  
20.11. Client Connection Defaults  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.13. Version and Platform Compatibility  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-locks.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

