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

Supported Versions: [Current](/docs/current/monitoring-locks.html "PostgreSQL
17 - 28.3. Viewing Locks") ([17](/docs/17/monitoring-locks.html "PostgreSQL 17
- 28.3. Viewing Locks")) / [16](/docs/16/monitoring-locks.html "PostgreSQL 16
- 28.3. Viewing Locks") / [15](/docs/15/monitoring-locks.html "PostgreSQL 15 -
28.3. Viewing Locks") / [14](/docs/14/monitoring-locks.html "PostgreSQL 14 -
28.3. Viewing Locks") / [13](/docs/13/monitoring-locks.html "PostgreSQL 13 -
28.3. Viewing Locks")

Development Versions: [18](/docs/18/monitoring-locks.html "PostgreSQL 18 -
28.3. Viewing Locks") / [devel](/docs/devel/monitoring-locks.html "PostgreSQL
devel - 28.3. Viewing Locks")

Unsupported versions: [12](/docs/12/monitoring-locks.html "PostgreSQL 12 -
28.3. Viewing Locks") / [11](/docs/11/monitoring-locks.html "PostgreSQL 11 -
28.3. Viewing Locks") / [10](/docs/10/monitoring-locks.html "PostgreSQL 10 -
28.3. Viewing Locks") / [9.6](/docs/9.6/monitoring-locks.html "PostgreSQL 9.6
- 28.3. Viewing Locks") / [9.5](/docs/9.5/monitoring-locks.html "PostgreSQL
9.5 - 28.3. Viewing Locks") / [9.4](/docs/9.4/monitoring-locks.html
"PostgreSQL 9.4 - 28.3. Viewing Locks") / [9.3](/docs/9.3/monitoring-
locks.html "PostgreSQL 9.3 - 28.3. Viewing Locks") /
[9.2](/docs/9.2/monitoring-locks.html "PostgreSQL 9.2 - 28.3. Viewing Locks")
/ [9.1](/docs/9.1/monitoring-locks.html "PostgreSQL 9.1 - 28.3. Viewing
Locks") / [9.0](/docs/9.0/monitoring-locks.html "PostgreSQL 9.0 -
28.3. Viewing Locks") / [8.4](/docs/8.4/monitoring-locks.html "PostgreSQL 8.4
- 28.3. Viewing Locks") / [8.3](/docs/8.3/monitoring-locks.html "PostgreSQL
8.3 - 28.3. Viewing Locks") / [8.2](/docs/8.2/monitoring-locks.html
"PostgreSQL 8.2 - 28.3. Viewing Locks") / [8.1](/docs/8.1/monitoring-
locks.html "PostgreSQL 8.1 - 28.3. Viewing Locks") /
[8.0](/docs/8.0/monitoring-locks.html "PostgreSQL 8.0 - 28.3. Viewing Locks")
/ [7.4](/docs/7.4/monitoring-locks.html "PostgreSQL 7.4 - 28.3. Viewing
Locks") / [7.3](/docs/7.3/monitoring-locks.html "PostgreSQL 7.3 -
28.3. Viewing Locks")

__

28.3. Viewing Locks  
---  
[Prev](monitoring-stats.html "28.2. The Cumulative Statistics System")  | [Up](monitoring.html "Chapter 28. Monitoring Database Activity") | Chapter 28. Monitoring Database Activity | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](progress-reporting.html "28.4. Progress Reporting")  
  
* * *

## 28.3. Viewing Locks #

Another useful tool for monitoring database activity is the `pg_locks` system
table. It allows the database administrator to view information about the
outstanding locks in the lock manager. For example, this capability can be
used to:

  * View all the locks currently outstanding, all the locks on relations in a particular database, all the locks on a particular relation, or all the locks held by a particular PostgreSQL session.

  * Determine the relation in the current database with the most ungranted locks (which might be a source of contention among database clients).

  * Determine the effect of lock contention on overall database performance, as well as the extent to which contention varies with overall database traffic.

Details of the `pg_locks` view appear in [Section 54.12](view-pg-locks.html
"54.12. pg_locks"). For more information on locking and managing concurrency
with PostgreSQL, refer to [Chapter 13](mvcc.html "Chapter 13. Concurrency
Control").

* * *

[Prev](monitoring-stats.html "28.2. The Cumulative Statistics System")  | [Up](monitoring.html "Chapter 28. Monitoring Database Activity") |  [Next](progress-reporting.html "28.4. Progress Reporting")  
---|---|---  
28.2. The Cumulative Statistics System  | [Home](index.html "PostgreSQL 16.9 Documentation") |  28.4. Progress Reporting  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/monitoring-locks.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

