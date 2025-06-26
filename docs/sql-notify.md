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

Supported Versions: [Current](/docs/current/sql-notify.html "PostgreSQL 17 -
NOTIFY") ([17](/docs/17/sql-notify.html "PostgreSQL 17 - NOTIFY")) /
[16](/docs/16/sql-notify.html "PostgreSQL 16 - NOTIFY") / [15](/docs/15/sql-
notify.html "PostgreSQL 15 - NOTIFY") / [14](/docs/14/sql-notify.html
"PostgreSQL 14 - NOTIFY") / [13](/docs/13/sql-notify.html "PostgreSQL 13 -
NOTIFY")

Development Versions: [18](/docs/18/sql-notify.html "PostgreSQL 18 - NOTIFY")
/ [devel](/docs/devel/sql-notify.html "PostgreSQL devel - NOTIFY")

Unsupported versions: [12](/docs/12/sql-notify.html "PostgreSQL 12 - NOTIFY")
/ [11](/docs/11/sql-notify.html "PostgreSQL 11 - NOTIFY") / [10](/docs/10/sql-
notify.html "PostgreSQL 10 - NOTIFY") / [9.6](/docs/9.6/sql-notify.html
"PostgreSQL 9.6 - NOTIFY") / [9.5](/docs/9.5/sql-notify.html "PostgreSQL 9.5 -
NOTIFY") / [9.4](/docs/9.4/sql-notify.html "PostgreSQL 9.4 - NOTIFY") /
[9.3](/docs/9.3/sql-notify.html "PostgreSQL 9.3 - NOTIFY") /
[9.2](/docs/9.2/sql-notify.html "PostgreSQL 9.2 - NOTIFY") /
[9.1](/docs/9.1/sql-notify.html "PostgreSQL 9.1 - NOTIFY") /
[9.0](/docs/9.0/sql-notify.html "PostgreSQL 9.0 - NOTIFY") /
[8.4](/docs/8.4/sql-notify.html "PostgreSQL 8.4 - NOTIFY") /
[8.3](/docs/8.3/sql-notify.html "PostgreSQL 8.3 - NOTIFY") /
[8.2](/docs/8.2/sql-notify.html "PostgreSQL 8.2 - NOTIFY") /
[8.1](/docs/8.1/sql-notify.html "PostgreSQL 8.1 - NOTIFY") /
[8.0](/docs/8.0/sql-notify.html "PostgreSQL 8.0 - NOTIFY") /
[7.4](/docs/7.4/sql-notify.html "PostgreSQL 7.4 - NOTIFY") /
[7.3](/docs/7.3/sql-notify.html "PostgreSQL 7.3 - NOTIFY") /
[7.2](/docs/7.2/sql-notify.html "PostgreSQL 7.2 - NOTIFY") /
[7.1](/docs/7.1/sql-notify.html "PostgreSQL 7.1 - NOTIFY")

__

NOTIFY  
---  
[Prev](sql-move.html "MOVE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-prepare.html "PREPARE")  
  
* * *

## NOTIFY

NOTIFY — generate a notification

## Synopsis

    
    
    NOTIFY _channel_ [ , _payload_ ]
    

## Description

The `NOTIFY` command sends a notification event together with an optional
“payload” string to each client application that has previously executed
`LISTEN _`channel`_` for the specified channel name in the current database.
Notifications are visible to all users.

`NOTIFY` provides a simple interprocess communication mechanism for a
collection of processes accessing the same PostgreSQL database. A payload
string can be sent along with the notification, and higher-level mechanisms
for passing structured data can be built by using tables in the database to
pass additional data from notifier to listener(s).

The information passed to the client for a notification event includes the
notification channel name, the notifying session's server process PID, and the
payload string, which is an empty string if it has not been specified.

It is up to the database designer to define the channel names that will be
used in a given database and what each one means. Commonly, the channel name
is the same as the name of some table in the database, and the notify event
essentially means, “I changed this table, take a look at it to see what's
new”. But no such association is enforced by the `NOTIFY` and `LISTEN`
commands. For example, a database designer could use several different channel
names to signal different sorts of changes to a single table. Alternatively,
the payload string could be used to differentiate various cases.

When `NOTIFY` is used to signal the occurrence of changes to a particular
table, a useful programming technique is to put the `NOTIFY` in a statement
trigger that is triggered by table updates. In this way, notification happens
automatically when the table is changed, and the application programmer cannot
accidentally forget to do it.

`NOTIFY` interacts with SQL transactions in some important ways. Firstly, if a
`NOTIFY` is executed inside a transaction, the notify events are not delivered
until and unless the transaction is committed. This is appropriate, since if
the transaction is aborted, all the commands within it have had no effect,
including `NOTIFY`. But it can be disconcerting if one is expecting the
notification events to be delivered immediately. Secondly, if a listening
session receives a notification signal while it is within a transaction, the
notification event will not be delivered to its connected client until just
after the transaction is completed (either committed or aborted). Again, the
reasoning is that if a notification were delivered within a transaction that
was later aborted, one would want the notification to be undone somehow — but
the server cannot “take back” a notification once it has sent it to the
client. So notification events are only delivered between transactions. The
upshot of this is that applications using `NOTIFY` for real-time signaling
should try to keep their transactions short.

If the same channel name is signaled multiple times with identical payload
strings within the same transaction, only one instance of the notification
event is delivered to listeners. On the other hand, notifications with
distinct payload strings will always be delivered as distinct notifications.
Similarly, notifications from different transactions will never get folded
into one notification. Except for dropping later instances of duplicate
notifications, `NOTIFY` guarantees that notifications from the same
transaction get delivered in the order they were sent. It is also guaranteed
that messages from different transactions are delivered in the order in which
the transactions committed.

It is common for a client that executes `NOTIFY` to be listening on the same
notification channel itself. In that case it will get back a notification
event, just like all the other listening sessions. Depending on the
application logic, this could result in useless work, for example, reading a
database table to find the same updates that that session just wrote out. It
is possible to avoid such extra work by noticing whether the notifying
session's server process PID (supplied in the notification event message) is
the same as one's own session's PID (available from libpq). When they are the
same, the notification event is one's own work bouncing back, and can be
ignored.

## Parameters

_`channel`_

    

Name of the notification channel to be signaled (any identifier).

_`payload`_

    

The “payload” string to be communicated along with the notification. This must
be specified as a simple string literal. In the default configuration it must
be shorter than 8000 bytes. (If binary data or large amounts of information
need to be communicated, it's best to put it in a database table and send the
key of the record.)

## Notes

There is a queue that holds notifications that have been sent but not yet
processed by all listening sessions. If this queue becomes full, transactions
calling `NOTIFY` will fail at commit. The queue is quite large (8GB in a
standard installation) and should be sufficiently sized for almost every use
case. However, no cleanup can take place if a session executes `LISTEN` and
then enters a transaction for a very long time. Once the queue is half full
you will see warnings in the log file pointing you to the session that is
preventing cleanup. In this case you should make sure that this session ends
its current transaction so that cleanup can proceed.

The function `pg_notification_queue_usage` returns the fraction of the queue
that is currently occupied by pending notifications. See [Section
9.26](functions-info.html "9.26. System Information Functions and Operators")
for more information.

A transaction that has executed `NOTIFY` cannot be prepared for two-phase
commit.

### pg_notify

To send a notification you can also use the function ``pg_notify`(`text`,
`text`)`. The function takes the channel name as the first argument and the
payload as the second. The function is much easier to use than the `NOTIFY`
command if you need to work with non-constant channel names and payloads.

## Examples

Configure and execute a listen/notify sequence from psql:

    
    
    LISTEN virtual;
    NOTIFY virtual;
    Asynchronous notification "virtual" received from server process with PID 8448.
    NOTIFY virtual, 'This is the payload';
    Asynchronous notification "virtual" with payload "This is the payload" received from server process with PID 8448.
    
    LISTEN foo;
    SELECT pg_notify('fo' || 'o', 'pay' || 'load');
    Asynchronous notification "foo" with payload "payload" received from server process with PID 14728.
    

## Compatibility

There is no `NOTIFY` statement in the SQL standard.

## See Also

[LISTEN](sql-listen.html "LISTEN"), [UNLISTEN](sql-unlisten.html "UNLISTEN")

* * *

[Prev](sql-move.html "MOVE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-prepare.html "PREPARE")  
---|---|---  
MOVE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  PREPARE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-notify.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

