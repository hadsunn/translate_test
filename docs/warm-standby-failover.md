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

Supported Versions: [Current](/docs/current/warm-standby-failover.html
"PostgreSQL 17 - 27.3. Failover") ([17](/docs/17/warm-standby-failover.html
"PostgreSQL 17 - 27.3. Failover")) / [16](/docs/16/warm-standby-failover.html
"PostgreSQL 16 - 27.3. Failover") / [15](/docs/15/warm-standby-failover.html
"PostgreSQL 15 - 27.3. Failover") / [14](/docs/14/warm-standby-failover.html
"PostgreSQL 14 - 27.3. Failover") / [13](/docs/13/warm-standby-failover.html
"PostgreSQL 13 - 27.3. Failover")

Development Versions: [18](/docs/18/warm-standby-failover.html "PostgreSQL 18
- 27.3. Failover") / [devel](/docs/devel/warm-standby-failover.html
"PostgreSQL devel - 27.3. Failover")

Unsupported versions: [12](/docs/12/warm-standby-failover.html "PostgreSQL 12
- 27.3. Failover") / [11](/docs/11/warm-standby-failover.html "PostgreSQL 11 -
27.3. Failover") / [10](/docs/10/warm-standby-failover.html "PostgreSQL 10 -
27.3. Failover") / [9.6](/docs/9.6/warm-standby-failover.html "PostgreSQL 9.6
- 27.3. Failover") / [9.5](/docs/9.5/warm-standby-failover.html "PostgreSQL
9.5 - 27.3. Failover") / [9.4](/docs/9.4/warm-standby-failover.html
"PostgreSQL 9.4 - 27.3. Failover") / [9.3](/docs/9.3/warm-standby-
failover.html "PostgreSQL 9.3 - 27.3. Failover") / [9.2](/docs/9.2/warm-
standby-failover.html "PostgreSQL 9.2 - 27.3. Failover") /
[9.1](/docs/9.1/warm-standby-failover.html "PostgreSQL 9.1 - 27.3. Failover")
/ [9.0](/docs/9.0/warm-standby-failover.html "PostgreSQL 9.0 -
27.3. Failover")

__

27.3. Failover  
---  
[Prev](warm-standby.html "27.2. Log-Shipping Standby Servers")  | [Up](high-availability.html "Chapter 27. High Availability, Load Balancing, and Replication") | Chapter 27. High Availability, Load Balancing, and Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](hot-standby.html "27.4. Hot Standby")  
  
* * *

## 27.3. Failover #

If the primary server fails then the standby server should begin failover
procedures.

If the standby server fails then no failover need take place. If the standby
server can be restarted, even some time later, then the recovery process can
also be restarted immediately, taking advantage of restartable recovery. If
the standby server cannot be restarted, then a full new standby server
instance should be created.

If the primary server fails and the standby server becomes the new primary,
and then the old primary restarts, you must have a mechanism for informing the
old primary that it is no longer the primary. This is sometimes known as
STONITH (Shoot The Other Node In The Head), which is necessary to avoid
situations where both systems think they are the primary, which will lead to
confusion and ultimately data loss.

Many failover systems use just two systems, the primary and the standby,
connected by some kind of heartbeat mechanism to continually verify the
connectivity between the two and the viability of the primary. It is also
possible to use a third system (called a witness server) to prevent some cases
of inappropriate failover, but the additional complexity might not be
worthwhile unless it is set up with sufficient care and rigorous testing.

PostgreSQL does not provide the system software required to identify a failure
on the primary and notify the standby database server. Many such tools exist
and are well integrated with the operating system facilities required for
successful failover, such as IP address migration.

Once failover to the standby occurs, there is only a single server in
operation. This is known as a degenerate state. The former standby is now the
primary, but the former primary is down and might stay down. To return to
normal operation, a standby server must be recreated, either on the former
primary system when it comes up, or on a third, possibly new, system. The
[pg_rewind](app-pgrewind.html "pg_rewind") utility can be used to speed up
this process on large clusters. Once complete, the primary and standby can be
considered to have switched roles. Some people choose to use a third server to
provide backup for the new primary until the new standby server is recreated,
though clearly this complicates the system configuration and operational
processes.

So, switching from primary to standby server can be fast but requires some
time to re-prepare the failover cluster. Regular switching from primary to
standby is useful, since it allows regular downtime on each system for
maintenance. This also serves as a test of the failover mechanism to ensure
that it will really work when you need it. Written administration procedures
are advised.

To trigger failover of a log-shipping standby server, run `pg_ctl promote` or
call `pg_promote()`. If you're setting up reporting servers that are only used
to offload read-only queries from the primary, not for high availability
purposes, you don't need to promote.

* * *

[Prev](warm-standby.html "27.2. Log-Shipping Standby Servers")  | [Up](high-availability.html "Chapter 27. High Availability, Load Balancing, and Replication") |  [Next](hot-standby.html "27.4. Hot Standby")  
---|---|---  
27.2. Log-Shipping Standby Servers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  27.4. Hot Standby  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/warm-standby-failover.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

