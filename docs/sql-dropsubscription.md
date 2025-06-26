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

Supported Versions: [Current](/docs/current/sql-dropsubscription.html
"PostgreSQL 17 - DROP SUBSCRIPTION") ([17](/docs/17/sql-dropsubscription.html
"PostgreSQL 17 - DROP SUBSCRIPTION")) / [16](/docs/16/sql-
dropsubscription.html "PostgreSQL 16 - DROP SUBSCRIPTION") /
[15](/docs/15/sql-dropsubscription.html "PostgreSQL 15 - DROP SUBSCRIPTION") /
[14](/docs/14/sql-dropsubscription.html "PostgreSQL 14 - DROP SUBSCRIPTION") /
[13](/docs/13/sql-dropsubscription.html "PostgreSQL 13 - DROP SUBSCRIPTION")

Development Versions: [18](/docs/18/sql-dropsubscription.html "PostgreSQL 18 -
DROP SUBSCRIPTION") / [devel](/docs/devel/sql-dropsubscription.html
"PostgreSQL devel - DROP SUBSCRIPTION")

Unsupported versions: [12](/docs/12/sql-dropsubscription.html "PostgreSQL 12 -
DROP SUBSCRIPTION") / [11](/docs/11/sql-dropsubscription.html "PostgreSQL 11 -
DROP SUBSCRIPTION") / [10](/docs/10/sql-dropsubscription.html "PostgreSQL 10 -
DROP SUBSCRIPTION")

__

DROP SUBSCRIPTION  
---  
[Prev](sql-dropstatistics.html "DROP STATISTICS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droptable.html "DROP TABLE")  
  
* * *

## DROP SUBSCRIPTION

DROP SUBSCRIPTION — remove a subscription

## Synopsis

    
    
    DROP SUBSCRIPTION [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP SUBSCRIPTION` removes a subscription from the database cluster.

To execute this command the user must be the owner of the subscription.

`DROP SUBSCRIPTION` cannot be executed inside a transaction block if the
subscription is associated with a replication slot. (You can use `ALTER
SUBSCRIPTION` to unset the slot.)

## Parameters

_`name`_

    

The name of a subscription to be dropped.

`CASCADE`  
`RESTRICT`

    

These key words do not have any effect, since there are no dependencies on
subscriptions.

## Notes

When dropping a subscription that is associated with a replication slot on the
remote host (the normal state), `DROP SUBSCRIPTION` will connect to the remote
host and try to drop the replication slot (and any remaining table
synchronization slots) as part of its operation. This is necessary so that the
resources allocated for the subscription on the remote host are released. If
this fails, either because the remote host is not reachable or because the
remote replication slot cannot be dropped or does not exist or never existed,
the `DROP SUBSCRIPTION` command will fail. To proceed in this situation, first
disable the subscription by executing `ALTER SUBSCRIPTION ... DISABLE`, and
then disassociate it from the replication slot by executing `ALTER
SUBSCRIPTION ... SET (slot_name = NONE)`. After that, `DROP SUBSCRIPTION` will
no longer attempt any actions on a remote host. Note that if the remote
replication slot still exists, it (and any related table synchronization
slots) should then be dropped manually; otherwise it/they will continue to
reserve WAL and might eventually cause the disk to fill up. See also [Section
31.2.1](logical-replication-subscription.html#LOGICAL-REPLICATION-
SUBSCRIPTION-SLOT "31.2.1. Replication Slot Management").

If a subscription is associated with a replication slot, then `DROP
SUBSCRIPTION` cannot be executed inside a transaction block.

## Examples

Drop a subscription:

    
    
    DROP SUBSCRIPTION mysub;
    

## Compatibility

`DROP SUBSCRIPTION` is a PostgreSQL extension.

## See Also

[CREATE SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION"),
[ALTER SUBSCRIPTION](sql-altersubscription.html "ALTER SUBSCRIPTION")

* * *

[Prev](sql-dropstatistics.html "DROP STATISTICS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droptable.html "DROP TABLE")  
---|---|---  
DROP STATISTICS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP TABLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropsubscription.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

