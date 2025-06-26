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

Supported Versions: [Current](/docs/current/logical-replication-security.html
"PostgreSQL 17 - 31.9. Security") ([17](/docs/17/logical-replication-
security.html "PostgreSQL 17 - 31.9. Security")) / [16](/docs/16/logical-
replication-security.html "PostgreSQL 16 - 31.9. Security") /
[15](/docs/15/logical-replication-security.html "PostgreSQL 15 -
31.9. Security") / [14](/docs/14/logical-replication-security.html "PostgreSQL
14 - 31.9. Security") / [13](/docs/13/logical-replication-security.html
"PostgreSQL 13 - 31.9. Security")

Development Versions: [18](/docs/18/logical-replication-security.html
"PostgreSQL 18 - 31.9. Security") / [devel](/docs/devel/logical-replication-
security.html "PostgreSQL devel - 31.9. Security")

Unsupported versions: [12](/docs/12/logical-replication-security.html
"PostgreSQL 12 - 31.9. Security") / [11](/docs/11/logical-replication-
security.html "PostgreSQL 11 - 31.9. Security") / [10](/docs/10/logical-
replication-security.html "PostgreSQL 10 - 31.9. Security")

__

31.9. Security  
---  
[Prev](logical-replication-monitoring.html "31.8. Monitoring")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-config.html "31.10. Configuration Settings")  
  
* * *

## 31.9. Security #

The role used for the replication connection must have the `REPLICATION`
attribute (or be a superuser). If the role lacks `SUPERUSER` and `BYPASSRLS`,
publisher row security policies can execute. If the role does not trust all
table owners, include `options=-crow_security=off` in the connection string;
if a table owner then adds a row security policy, that setting will cause
replication to halt rather than execute the policy. Access for the role must
be configured in `pg_hba.conf` and it must have the `LOGIN` attribute.

In order to be able to copy the initial table data, the role used for the
replication connection must have the `SELECT` privilege on a published table
(or be a superuser).

To create a publication, the user must have the `CREATE` privilege in the
database.

To add tables to a publication, the user must have ownership rights on the
table. To add all tables in schema to a publication, the user must be a
superuser. To create a publication that publishes all tables or all tables in
schema automatically, the user must be a superuser.

There are currently no privileges on publications. Any subscription (that is
able to connect) can access any publication. Thus, if you intend to hide some
information from particular subscribers, such as by using row filters or
column lists, or by not adding the whole table to the publication, be aware
that other publications in the same database could expose the same
information. Publication privileges might be added to PostgreSQL in the future
to allow for finer-grained access control.

To create a subscription, the user must have the privileges of the the
`pg_create_subscription` role, as well as `CREATE` privileges on the database.

The subscription apply process will, at a session level, run with the
privileges of the subscription owner. However, when performing an insert,
update, delete, or truncate operation on a particular table, it will switch
roles to the table owner and perform the operation with the table owner's
privileges. This means that the subscription owner needs to be able to `SET
ROLE` to each role that owns a replicated table.

If the subscription has been configured with `run_as_owner = true`, then no
user switching will occur. Instead, all operations will be performed with the
permissions of the subscription owner. In this case, the subscription owner
only needs privileges to `SELECT`, `INSERT`, `UPDATE`, and `DELETE` from the
target table, and does not need privileges to `SET ROLE` to the table owner.
However, this also means that any user who owns a table into which replication
is happening can execute arbitrary code with the privileges of the
subscription owner. For example, they could do this by simply attaching a
trigger to one of the tables which they own. Because it is usually undesirable
to allow one role to freely assume the privileges of another, this option
should be avoided unless user security within the database is of no concern.

On the publisher, privileges are only checked once at the start of a
replication connection and are not re-checked as each change record is read.

On the subscriber, the subscription owner's privileges are re-checked for each
transaction when applied. If a worker is in the process of applying a
transaction when the ownership of the subscription is changed by a concurrent
transaction, the application of the current transaction will continue under
the old owner's privileges.

* * *

[Prev](logical-replication-monitoring.html "31.8. Monitoring")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-config.html "31.10. Configuration Settings")  
---|---|---  
31.8. Monitoring  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.10. Configuration Settings  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
security.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

