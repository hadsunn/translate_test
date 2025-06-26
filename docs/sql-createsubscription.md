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

Supported Versions: [Current](/docs/current/sql-createsubscription.html
"PostgreSQL 17 - CREATE SUBSCRIPTION") ([17](/docs/17/sql-
createsubscription.html "PostgreSQL 17 - CREATE SUBSCRIPTION")) /
[16](/docs/16/sql-createsubscription.html "PostgreSQL 16 - CREATE
SUBSCRIPTION") / [15](/docs/15/sql-createsubscription.html "PostgreSQL 15 -
CREATE SUBSCRIPTION") / [14](/docs/14/sql-createsubscription.html "PostgreSQL
14 - CREATE SUBSCRIPTION") / [13](/docs/13/sql-createsubscription.html
"PostgreSQL 13 - CREATE SUBSCRIPTION")

Development Versions: [18](/docs/18/sql-createsubscription.html "PostgreSQL 18
- CREATE SUBSCRIPTION") / [devel](/docs/devel/sql-createsubscription.html
"PostgreSQL devel - CREATE SUBSCRIPTION")

Unsupported versions: [12](/docs/12/sql-createsubscription.html "PostgreSQL 12
- CREATE SUBSCRIPTION") / [11](/docs/11/sql-createsubscription.html
"PostgreSQL 11 - CREATE SUBSCRIPTION") / [10](/docs/10/sql-
createsubscription.html "PostgreSQL 10 - CREATE SUBSCRIPTION")

__

CREATE SUBSCRIPTION  
---  
[Prev](sql-createstatistics.html "CREATE STATISTICS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtable.html "CREATE TABLE")  
  
* * *

## CREATE SUBSCRIPTION

CREATE SUBSCRIPTION — define a new subscription

## Synopsis

    
    
    CREATE SUBSCRIPTION _subscription_name_
        CONNECTION '_conninfo_ '
        PUBLICATION _publication_name_ [, ...]
        [ WITH ( _subscription_parameter_ [= _value_] [, ... ] ) ]
    

## Description

`CREATE SUBSCRIPTION` adds a new logical-replication subscription. The user
that creates a subscription becomes the owner of the subscription. The
subscription name must be distinct from the name of any existing subscription
in the current database.

A subscription represents a replication connection to the publisher. Hence, in
addition to adding definitions in the local catalogs, this command normally
creates a replication slot on the publisher.

A logical replication worker will be started to replicate data for the new
subscription at the commit of the transaction where this command is run,
unless the subscription is initially disabled.

To be able to create a subscription, you must have the privileges of the the
`pg_create_subscription` role, as well as `CREATE` privileges on the current
database.

Additional information about subscriptions and logical replication as a whole
is available at [Section 31.2](logical-replication-subscription.html
"31.2. Subscription") and [Chapter 31](logical-replication.html
"Chapter 31. Logical Replication").

## Parameters

_`subscription_name`_ #

    

The name of the new subscription.

`CONNECTION '_`conninfo`_ '` #

    

The libpq connection string defining how to connect to the publisher database.
For details see [Section 34.1.1](libpq-connect.html#LIBPQ-CONNSTRING
"34.1.1. Connection Strings").

`PUBLICATION _`publication_name`_ [, ...]` #

    

Names of the publications on the publisher to subscribe to.

`WITH ( _`subscription_parameter`_ [= _`value`_] [, ... ] )` #

    

This clause specifies optional parameters for a subscription.

The following parameters control what happens during subscription creation:

`connect` (`boolean`) #

    

Specifies whether the `CREATE SUBSCRIPTION` command should connect to the
publisher at all. The default is `true`. Setting this to `false` will force
the values of `create_slot`, `enabled` and `copy_data` to `false`. (You cannot
combine setting `connect` to `false` with setting `create_slot`, `enabled`, or
`copy_data` to `true`.)

Since no connection is made when this option is `false`, no tables are
subscribed. To initiate replication, you must manually create the replication
slot, enable the subscription, and refresh the subscription. See [Section
31.2.3](logical-replication-subscription.html#LOGICAL-REPLICATION-
SUBSCRIPTION-EXAMPLES-DEFERRED-SLOT "31.2.3. Examples: Deferred Replication
Slot Creation") for examples.

`create_slot` (`boolean`) #

    

Specifies whether the command should create the replication slot on the
publisher. The default is `true`.

If set to `false`, you are responsible for creating the publisher's slot in
some other way. See [Section 31.2.3](logical-replication-
subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-EXAMPLES-DEFERRED-SLOT
"31.2.3. Examples: Deferred Replication Slot Creation") for examples.

`enabled` (`boolean`) #

    

Specifies whether the subscription should be actively replicating or whether
it should just be set up but not started yet. The default is `true`.

`slot_name` (`string`) #

    

Name of the publisher's replication slot to use. The default is to use the
name of the subscription for the slot name.

Setting `slot_name` to `NONE` means there will be no replication slot
associated with the subscription. Such subscriptions must also have both
`enabled` and `create_slot` set to `false`. Use this when you will be creating
the replication slot later manually. See [Section 31.2.3](logical-replication-
subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-EXAMPLES-DEFERRED-SLOT
"31.2.3. Examples: Deferred Replication Slot Creation") for examples.

The following parameters control the subscription's replication behavior after
it has been created:

`binary` (`boolean`) #

    

Specifies whether the subscription will request the publisher to send the data
in binary format (as opposed to text). The default is `false`. Any initial
table synchronization copy (see `copy_data`) also uses the same format. Binary
format can be faster than the text format, but it is less portable across
machine architectures and PostgreSQL versions. Binary format is very data type
specific; for example, it will not allow copying from a `smallint` column to
an `integer` column, even though that would work fine in text format. Even
when this option is enabled, only data types having binary send and receive
functions will be transferred in binary. Note that the initial synchronization
requires all data types to have binary send and receive functions, otherwise
the synchronization will fail (see [CREATE TYPE](sql-createtype.html "CREATE
TYPE") for more about send/receive functions).

When doing cross-version replication, it could be that the publisher has a
binary send function for some data type, but the subscriber lacks a binary
receive function for that type. In such a case, data transfer will fail, and
the `binary` option cannot be used.

If the publisher is a PostgreSQL version before 16, then any initial table
synchronization will use text format even if `binary = true`.

`copy_data` (`boolean`) #

    

Specifies whether to copy pre-existing data in the publications that are being
subscribed to when the replication starts. The default is `true`.

If the publications contain `WHERE` clauses, it will affect what data is
copied. Refer to the [Notes](sql-createsubscription.html#SQL-
CREATESUBSCRIPTION-NOTES "Notes") for details.

See [Notes](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-NOTES "Notes")
for details of how `copy_data = true` can interact with the `origin`
parameter.

`streaming` (`enum`) #

    

Specifies whether to enable streaming of in-progress transactions for this
subscription. The default value is `off`, meaning all transactions are fully
decoded on the publisher and only then sent to the subscriber as a whole.

If set to `on`, the incoming changes are written to temporary files and then
applied only after the transaction is committed on the publisher and received
by the subscriber.

If set to `parallel`, incoming changes are directly applied via one of the
parallel apply workers, if available. If no parallel apply worker is free to
handle streaming transactions then the changes are written to temporary files
and applied after the transaction is committed. Note that if an error happens
in a parallel apply worker, the finish LSN of the remote transaction might not
be reported in the server log.

`synchronous_commit` (`enum`) #

    

The value of this parameter overrides the [synchronous_commit](runtime-config-
wal.html#GUC-SYNCHRONOUS-COMMIT) setting within this subscription's apply
worker processes. The default value is `off`.

It is safe to use `off` for logical replication: If the subscriber loses
transactions because of missing synchronization, the data will be sent again
from the publisher.

A different setting might be appropriate when doing synchronous logical
replication. The logical replication workers report the positions of writes
and flushes to the publisher, and when using synchronous replication, the
publisher will wait for the actual flush. This means that setting
`synchronous_commit` for the subscriber to `off` when the subscription is used
for synchronous replication might increase the latency for `COMMIT` on the
publisher. In this scenario, it can be advantageous to set
`synchronous_commit` to `local` or higher.

`two_phase` (`boolean`) #

    

Specifies whether two-phase commit is enabled for this subscription. The
default is `false`.

When two-phase commit is enabled, prepared transactions are sent to the
subscriber at the time of `PREPARE TRANSACTION`, and are processed as two-
phase transactions on the subscriber too. Otherwise, prepared transactions are
sent to the subscriber only when committed, and are then processed immediately
by the subscriber.

The implementation of two-phase commit requires that replication has
successfully finished the initial table synchronization phase. So even when
`two_phase` is enabled for a subscription, the internal two-phase state
remains temporarily “pending” until the initialization phase completes. See
column `subtwophasestate` of [`pg_subscription`](catalog-pg-subscription.html
"53.54. pg_subscription") to know the actual two-phase state.

`disable_on_error` (`boolean`) #

    

Specifies whether the subscription should be automatically disabled if any
errors are detected by subscription workers during data replication from the
publisher. The default is `false`.

`password_required` (`boolean`) #

    

If set to `true`, connections to the publisher made as a result of this
subscription must use password authentication and the password must be
specified as a part of the connection string. This setting is ignored when the
subscription is owned by a superuser. The default is `true`. Only superusers
can set this value to `false`.

`run_as_owner` (`boolean`) #

    

If true, all replication actions are performed as the subscription owner. If
false, replication workers will perform actions on each table as the owner of
that table. The latter configuration is generally much more secure; for
details, see [Section 31.9](logical-replication-security.html
"31.9. Security"). The default is `false`.

`origin` (`string`) #

    

Specifies whether the subscription will request the publisher to only send
changes that don't have an origin or send changes regardless of origin.
Setting `origin` to `none` means that the subscription will request the
publisher to only send changes that don't have an origin. Setting `origin` to
`any` means that the publisher sends changes regardless of their origin. The
default is `any`.

See [Notes](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-NOTES "Notes")
for details of how `copy_data = true` can interact with the `origin`
parameter.

When specifying a parameter of type `boolean`, the `=` _`value`_ part can be
omitted, which is equivalent to specifying `TRUE`.

## Notes

See [Section 31.9](logical-replication-security.html "31.9. Security") for
details on how to configure access control between the subscription and the
publication instance.

When creating a replication slot (the default behavior), `CREATE SUBSCRIPTION`
cannot be executed inside a transaction block.

Creating a subscription that connects to the same database cluster (for
example, to replicate between databases in the same cluster or to replicate
within the same database) will only succeed if the replication slot is not
created as part of the same command. Otherwise, the `CREATE SUBSCRIPTION` call
will hang. To make this work, create the replication slot separately (using
the function `pg_create_logical_replication_slot` with the plugin name
`pgoutput`) and create the subscription using the parameter `create_slot =
false`. See [Section 31.2.3](logical-replication-subscription.html#LOGICAL-
REPLICATION-SUBSCRIPTION-EXAMPLES-DEFERRED-SLOT "31.2.3. Examples: Deferred
Replication Slot Creation") for examples. This is an implementation
restriction that might be lifted in a future release.

If any table in the publication has a `WHERE` clause, rows for which the
_`expression`_ evaluates to false or null will not be published. If the
subscription has several publications in which the same table has been
published with different `WHERE` clauses, a row will be published if any of
the expressions (referring to that publish operation) are satisfied. In the
case of different `WHERE` clauses, if one of the publications has no `WHERE`
clause (referring to that publish operation) or the publication is declared as
[`FOR ALL TABLES`](sql-createpublication.html#SQL-CREATEPUBLICATION-FOR-ALL-
TABLES) or [`FOR TABLES IN SCHEMA`](sql-createpublication.html#SQL-
CREATEPUBLICATION-FOR-TABLES-IN-SCHEMA), rows are always published regardless
of the definition of the other expressions. If the subscriber is a PostgreSQL
version before 15, then any row filtering is ignored during the initial data
synchronization phase. For this case, the user might want to consider deleting
any initially copied data that would be incompatible with subsequent
filtering. Because initial data synchronization does not take into account the
publication [`publish`](sql-createpublication.html#SQL-CREATEPUBLICATION-WITH-
PUBLISH) parameter when copying existing table data, some rows may be copied
that would not be replicated using DML. See [Section 31.2.2](logical-
replication-subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-EXAMPLES
"31.2.2. Examples: Set Up Logical Replication") for examples.

Subscriptions having several publications in which the same table has been
published with different column lists are not supported.

We allow non-existent publications to be specified so that users can add those
later. This means [`pg_subscription`](catalog-pg-subscription.html
"53.54. pg_subscription") can have non-existent publications.

When using a subscription parameter combination of `copy_data = true` and
`origin = NONE`, the initial sync table data is copied directly from the
publisher, meaning that knowledge of the true origin of that data is not
possible. If the publisher also has subscriptions then the copied table data
might have originated from further upstream. This scenario is detected and a
WARNING is logged to the user, but the warning is only an indication of a
potential problem; it is the user's responsibility to make the necessary
checks to ensure the copied data origins are really as wanted or not.

To find which tables might potentially include non-local origins (due to other
subscriptions created on the publisher) try this SQL query:

    
    
    # substitute <pub-names> below with your publication name(s) to be queried
    SELECT DISTINCT PT.schemaname, PT.tablename
    FROM pg_publication_tables PT
         JOIN pg_class C ON (C.relname = PT.tablename)
         JOIN pg_namespace N ON (N.nspname = PT.schemaname),
         pg_subscription_rel PS
    WHERE C.relnamespace = N.oid AND
          (PS.srrelid = C.oid OR
          C.oid IN (SELECT relid FROM pg_partition_ancestors(PS.srrelid) UNION
                    SELECT relid FROM pg_partition_tree(PS.srrelid))) AND
          PT.pubname IN (<pub-names>);
    

## Examples

Create a subscription to a remote server that replicates tables in the
publications `mypublication` and `insert_only` and starts replicating
immediately on commit:

    
    
    CREATE SUBSCRIPTION mysub
             CONNECTION 'host=192.168.1.50 port=5432 user=foo dbname=foodb'
            PUBLICATION mypublication, insert_only;
    

Create a subscription to a remote server that replicates tables in the
`insert_only` publication and does not start replicating until enabled at a
later time.

    
    
    CREATE SUBSCRIPTION mysub
             CONNECTION 'host=192.168.1.50 port=5432 user=foo dbname=foodb'
            PUBLICATION insert_only
                   WITH (enabled = false);
    

## Compatibility

`CREATE SUBSCRIPTION` is a PostgreSQL extension.

## See Also

[ALTER SUBSCRIPTION](sql-altersubscription.html "ALTER SUBSCRIPTION"), [DROP
SUBSCRIPTION](sql-dropsubscription.html "DROP SUBSCRIPTION"), [CREATE
PUBLICATION](sql-createpublication.html "CREATE PUBLICATION"), [ALTER
PUBLICATION](sql-alterpublication.html "ALTER PUBLICATION")

* * *

[Prev](sql-createstatistics.html "CREATE STATISTICS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtable.html "CREATE TABLE")  
---|---|---  
CREATE STATISTICS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TABLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createsubscription.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

