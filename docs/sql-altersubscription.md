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

Supported Versions: [Current](/docs/current/sql-altersubscription.html
"PostgreSQL 17 - ALTER SUBSCRIPTION") ([17](/docs/17/sql-
altersubscription.html "PostgreSQL 17 - ALTER SUBSCRIPTION")) /
[16](/docs/16/sql-altersubscription.html "PostgreSQL 16 - ALTER SUBSCRIPTION")
/ [15](/docs/15/sql-altersubscription.html "PostgreSQL 15 - ALTER
SUBSCRIPTION") / [14](/docs/14/sql-altersubscription.html "PostgreSQL 14 -
ALTER SUBSCRIPTION") / [13](/docs/13/sql-altersubscription.html "PostgreSQL 13
- ALTER SUBSCRIPTION")

Development Versions: [18](/docs/18/sql-altersubscription.html "PostgreSQL 18
- ALTER SUBSCRIPTION") / [devel](/docs/devel/sql-altersubscription.html
"PostgreSQL devel - ALTER SUBSCRIPTION")

Unsupported versions: [12](/docs/12/sql-altersubscription.html "PostgreSQL 12
- ALTER SUBSCRIPTION") / [11](/docs/11/sql-altersubscription.html "PostgreSQL
11 - ALTER SUBSCRIPTION") / [10](/docs/10/sql-altersubscription.html
"PostgreSQL 10 - ALTER SUBSCRIPTION")

__

ALTER SUBSCRIPTION  
---  
[Prev](sql-alterstatistics.html "ALTER STATISTICS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altersystem.html "ALTER SYSTEM")  
  
* * *

## ALTER SUBSCRIPTION

ALTER SUBSCRIPTION — change the definition of a subscription

## Synopsis

    
    
    ALTER SUBSCRIPTION _name_ CONNECTION '_conninfo_ '
    ALTER SUBSCRIPTION _name_ SET PUBLICATION _publication_name_ [, ...] [ WITH ( _publication_option_ [= _value_] [, ... ] ) ]
    ALTER SUBSCRIPTION _name_ ADD PUBLICATION _publication_name_ [, ...] [ WITH ( _publication_option_ [= _value_] [, ... ] ) ]
    ALTER SUBSCRIPTION _name_ DROP PUBLICATION _publication_name_ [, ...] [ WITH ( _publication_option_ [= _value_] [, ... ] ) ]
    ALTER SUBSCRIPTION _name_ REFRESH PUBLICATION [ WITH ( _refresh_option_ [= _value_] [, ... ] ) ]
    ALTER SUBSCRIPTION _name_ ENABLE
    ALTER SUBSCRIPTION _name_ DISABLE
    ALTER SUBSCRIPTION _name_ SET ( _subscription_parameter_ [= _value_] [, ... ] )
    ALTER SUBSCRIPTION _name_ SKIP ( _skip_option_ = _value_ )
    ALTER SUBSCRIPTION _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER SUBSCRIPTION _name_ RENAME TO _new_name_
    

## Description

`ALTER SUBSCRIPTION` can change most of the subscription properties that can
be specified in [CREATE SUBSCRIPTION](sql-createsubscription.html "CREATE
SUBSCRIPTION").

You must own the subscription to use `ALTER SUBSCRIPTION`. To rename a
subscription or alter the owner, you must have `CREATE` permission on the
database. In addition, to alter the owner, you must be able to `SET ROLE` to
the new owning role. If the subscription has `password_required=false`, only
superusers can modify it.

When refreshing a publication we remove the relations that are no longer part
of the publication and we also remove the table synchronization slots if there
are any. It is necessary to remove these slots so that the resources allocated
for the subscription on the remote host are released. If due to network
breakdown or some other error, PostgreSQL is unable to remove the slots, an
error will be reported. To proceed in this situation, the user either needs to
retry the operation or disassociate the slot from the subscription and drop
the subscription as explained in [DROP SUBSCRIPTION](sql-dropsubscription.html
"DROP SUBSCRIPTION").

Commands `ALTER SUBSCRIPTION ... REFRESH PUBLICATION` and `ALTER SUBSCRIPTION
... {SET|ADD|DROP} PUBLICATION ...` with `refresh` option as `true` cannot be
executed inside a transaction block. These commands also cannot be executed
when the subscription has [`two_phase`](sql-createsubscription.html#SQL-
CREATESUBSCRIPTION-WITH-TWO-PHASE) commit enabled, unless [`copy_data`](sql-
createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-COPY-DATA) is `false`. See
column `subtwophasestate` of [`pg_subscription`](catalog-pg-subscription.html
"53.54. pg_subscription") to know the actual two-phase state.

## Parameters

_`name`_

    

The name of a subscription whose properties are to be altered.

`CONNECTION '_`conninfo`_ '`

    

This clause replaces the connection string originally set by [CREATE
SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION"). See there
for more information.

`SET PUBLICATION _`publication_name`_`  
`ADD PUBLICATION _`publication_name`_`  
`DROP PUBLICATION _`publication_name`_`

    

These forms change the list of subscribed publications. `SET` replaces the
entire list of publications with a new list, `ADD` adds additional
publications to the list of publications, and `DROP` removes the publications
from the list of publications. We allow non-existent publications to be
specified in `ADD` and `SET` variants so that users can add those later. See
[CREATE SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION") for
more information. By default, this command will also act like `REFRESH
PUBLICATION`.

_`publication_option`_ specifies additional options for this operation. The
supported options are:

`refresh` (`boolean`)

    

When false, the command will not try to refresh table information. `REFRESH
PUBLICATION` should then be executed separately. The default is `true`.

Additionally, the options described under `REFRESH PUBLICATION` may be
specified, to control the implicit refresh operation.

`REFRESH PUBLICATION`

    

Fetch missing table information from publisher. This will start replication of
tables that were added to the subscribed-to publications since `CREATE
SUBSCRIPTION` or the last invocation of `REFRESH PUBLICATION`.

_`refresh_option`_ specifies additional options for the refresh operation. The
supported options are:

`copy_data` (`boolean`)

    

Specifies whether to copy pre-existing data in the publications that are being
subscribed to when the replication starts. The default is `true`.

Previously subscribed tables are not copied, even if a table's row filter
`WHERE` clause has since been modified.

See [Notes](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-NOTES "Notes")
for details of how `copy_data = true` can interact with the [`origin`](sql-
createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-ORIGIN) parameter.

See the [`binary`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-
BINARY) parameter of `CREATE SUBSCRIPTION` for details about copying pre-
existing data in binary format.

`ENABLE`

    

Enables a previously disabled subscription, starting the logical replication
worker at the end of the transaction.

`DISABLE`

    

Disables a running subscription, stopping the logical replication worker at
the end of the transaction.

`SET ( _`subscription_parameter`_ [= _`value`_] [, ... ] )`

    

This clause alters parameters originally set by [CREATE SUBSCRIPTION](sql-
createsubscription.html "CREATE SUBSCRIPTION"). See there for more
information. The parameters that can be altered are [`slot_name`](sql-
createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-SLOT-NAME),
[`synchronous_commit`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-
WITH-SYNCHRONOUS-COMMIT), [`binary`](sql-createsubscription.html#SQL-
CREATESUBSCRIPTION-WITH-BINARY), [`streaming`](sql-
createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-STREAMING),
[`disable_on_error`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-
DISABLE-ON-ERROR), [`password_required`](sql-createsubscription.html#SQL-
CREATESUBSCRIPTION-WITH-PASSWORD-REQUIRED), [`run_as_owner`](sql-
createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-RUN-AS-OWNER), and
[`origin`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-ORIGIN).
Only a superuser can set `password_required = false`.

`SKIP ( _`skip_option`_ = _`value`_ )`

    

Skips applying all changes of the remote transaction. If incoming data
violates any constraints, logical replication will stop until it is resolved.
By using the `ALTER SUBSCRIPTION ... SKIP` command, the logical replication
worker skips all data modification changes within the transaction. This option
has no effect on the transactions that are already prepared by enabling
[`two_phase`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-TWO-
PHASE) on the subscriber. After the logical replication worker successfully
skips the transaction or finishes a transaction, the LSN (stored in
`pg_subscription`.`subskiplsn`) is cleared. See [Section 31.5](logical-
replication-conflicts.html "31.5. Conflicts") for the details of logical
replication conflicts.

_`skip_option`_ specifies options for this operation. The supported option is:

`lsn` (`pg_lsn`)

    

Specifies the finish LSN of the remote transaction whose changes are to be
skipped by the logical replication worker. The finish LSN is the LSN at which
the transaction is either committed or prepared. Skipping individual
subtransactions is not supported. Setting `NONE` resets the LSN.

_`new_owner`_

    

The user name of the new owner of the subscription.

_`new_name`_

    

The new name for the subscription.

When specifying a parameter of type `boolean`, the `=` _`value`_ part can be
omitted, which is equivalent to specifying `TRUE`.

## Examples

Change the publication subscribed by a subscription to `insert_only`:

    
    
    ALTER SUBSCRIPTION mysub SET PUBLICATION insert_only;
    

Disable (stop) the subscription:

    
    
    ALTER SUBSCRIPTION mysub DISABLE;
    

## Compatibility

`ALTER SUBSCRIPTION` is a PostgreSQL extension.

## See Also

[CREATE SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION"),
[DROP SUBSCRIPTION](sql-dropsubscription.html "DROP SUBSCRIPTION"), [CREATE
PUBLICATION](sql-createpublication.html "CREATE PUBLICATION"), [ALTER
PUBLICATION](sql-alterpublication.html "ALTER PUBLICATION")

* * *

[Prev](sql-alterstatistics.html "ALTER STATISTICS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altersystem.html "ALTER SYSTEM")  
---|---|---  
ALTER STATISTICS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER SYSTEM  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altersubscription.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

