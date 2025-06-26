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

Supported Versions: [Current](/docs/current/logical-replication-conflicts.html
"PostgreSQL 17 - 31.5. Conflicts") ([17](/docs/17/logical-replication-
conflicts.html "PostgreSQL 17 - 31.5. Conflicts")) / [16](/docs/16/logical-
replication-conflicts.html "PostgreSQL 16 - 31.5. Conflicts") /
[15](/docs/15/logical-replication-conflicts.html "PostgreSQL 15 -
31.5. Conflicts") / [14](/docs/14/logical-replication-conflicts.html
"PostgreSQL 14 - 31.5. Conflicts") / [13](/docs/13/logical-replication-
conflicts.html "PostgreSQL 13 - 31.5. Conflicts")

Development Versions: [18](/docs/18/logical-replication-conflicts.html
"PostgreSQL 18 - 31.5. Conflicts") / [devel](/docs/devel/logical-replication-
conflicts.html "PostgreSQL devel - 31.5. Conflicts")

Unsupported versions: [12](/docs/12/logical-replication-conflicts.html
"PostgreSQL 12 - 31.5. Conflicts") / [11](/docs/11/logical-replication-
conflicts.html "PostgreSQL 11 - 31.5. Conflicts") / [10](/docs/10/logical-
replication-conflicts.html "PostgreSQL 10 - 31.5. Conflicts")

__

31.5. Conflicts  
---  
[Prev](logical-replication-col-lists.html "31.4. Column Lists")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-restrictions.html "31.6. Restrictions")  
  
* * *

## 31.5. Conflicts #

Logical replication behaves similarly to normal DML operations in that the
data will be updated even if it was changed locally on the subscriber node. If
incoming data violates any constraints the replication will stop. This is
referred to as a _conflict_. When replicating `UPDATE` or `DELETE` operations,
missing data will not produce a conflict and such operations will simply be
skipped.

Logical replication operations are performed with the privileges of the role
which owns the subscription. Permissions failures on target tables will cause
replication conflicts, as will enabled [row-level security](ddl-
rowsecurity.html "5.8. Row Security Policies") on target tables that the
subscription owner is subject to, without regard to whether any policy would
ordinarily reject the `INSERT`, `UPDATE`, `DELETE` or `TRUNCATE` which is
being replicated. This restriction on row-level security may be lifted in a
future version of PostgreSQL.

A conflict will produce an error and will stop the replication; it must be
resolved manually by the user. Details about the conflict can be found in the
subscriber's server log.

The resolution can be done either by changing data or permissions on the
subscriber so that it does not conflict with the incoming change or by
skipping the transaction that conflicts with the existing data. When a
conflict produces an error, the replication won't proceed, and the logical
replication worker will emit the following kind of message to the subscriber's
server log:

    
    
    ERROR:  duplicate key value violates unique constraint "test_pkey"
    DETAIL:  Key (c)=(1) already exists.
    CONTEXT:  processing remote data for replication origin "pg_16395" during "INSERT" for replication target relation "public.test" in transaction 725 finished at 0/14C0378
    

The LSN of the transaction that contains the change violating the constraint
and the replication origin name can be found from the server log (LSN
0/14C0378 and replication origin `pg_16395` in the above case). The
transaction that produced the conflict can be skipped by using `ALTER
SUBSCRIPTION ... SKIP` with the finish LSN (i.e., LSN 0/14C0378). The finish
LSN could be an LSN at which the transaction is committed or prepared on the
publisher. Alternatively, the transaction can also be skipped by calling the
[`pg_replication_origin_advance()`](functions-admin.html#PG-REPLICATION-
ORIGIN-ADVANCE) function. Before using this function, the subscription needs
to be disabled temporarily either by `ALTER SUBSCRIPTION ... DISABLE` or, the
subscription can be used with the [`disable_on_error`](sql-
createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-DISABLE-ON-ERROR) option.
Then, you can use `pg_replication_origin_advance()` function with the
_`node_name`_ (i.e., `pg_16395`) and the next LSN of the finish LSN (i.e.,
0/14C0379). The current position of origins can be seen in the
[`pg_replication_origin_status`](view-pg-replication-origin-status.html
"54.18. pg_replication_origin_status") system view. Please note that skipping
the whole transaction includes skipping changes that might not violate any
constraint. This can easily make the subscriber inconsistent.

When the [`streaming`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-
WITH-STREAMING) mode is `parallel`, the finish LSN of failed transactions may
not be logged. In that case, it may be necessary to change the streaming mode
to `on` or `off` and cause the same conflicts again so the finish LSN of the
failed transaction will be written to the server log. For the usage of finish
LSN, please refer to [`ALTER SUBSCRIPTION ... SKIP`](sql-
altersubscription.html "ALTER SUBSCRIPTION").

* * *

[Prev](logical-replication-col-lists.html "31.4. Column Lists")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-restrictions.html "31.6. Restrictions")  
---|---|---  
31.4. Column Lists  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.6. Restrictions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
conflicts.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

