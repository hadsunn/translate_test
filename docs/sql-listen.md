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

Supported Versions: [Current](/docs/current/sql-listen.html "PostgreSQL 17 -
LISTEN") ([17](/docs/17/sql-listen.html "PostgreSQL 17 - LISTEN")) /
[16](/docs/16/sql-listen.html "PostgreSQL 16 - LISTEN") / [15](/docs/15/sql-
listen.html "PostgreSQL 15 - LISTEN") / [14](/docs/14/sql-listen.html
"PostgreSQL 14 - LISTEN") / [13](/docs/13/sql-listen.html "PostgreSQL 13 -
LISTEN")

Development Versions: [18](/docs/18/sql-listen.html "PostgreSQL 18 - LISTEN")
/ [devel](/docs/devel/sql-listen.html "PostgreSQL devel - LISTEN")

Unsupported versions: [12](/docs/12/sql-listen.html "PostgreSQL 12 - LISTEN")
/ [11](/docs/11/sql-listen.html "PostgreSQL 11 - LISTEN") / [10](/docs/10/sql-
listen.html "PostgreSQL 10 - LISTEN") / [9.6](/docs/9.6/sql-listen.html
"PostgreSQL 9.6 - LISTEN") / [9.5](/docs/9.5/sql-listen.html "PostgreSQL 9.5 -
LISTEN") / [9.4](/docs/9.4/sql-listen.html "PostgreSQL 9.4 - LISTEN") /
[9.3](/docs/9.3/sql-listen.html "PostgreSQL 9.3 - LISTEN") /
[9.2](/docs/9.2/sql-listen.html "PostgreSQL 9.2 - LISTEN") /
[9.1](/docs/9.1/sql-listen.html "PostgreSQL 9.1 - LISTEN") /
[9.0](/docs/9.0/sql-listen.html "PostgreSQL 9.0 - LISTEN") /
[8.4](/docs/8.4/sql-listen.html "PostgreSQL 8.4 - LISTEN") /
[8.3](/docs/8.3/sql-listen.html "PostgreSQL 8.3 - LISTEN") /
[8.2](/docs/8.2/sql-listen.html "PostgreSQL 8.2 - LISTEN") /
[8.1](/docs/8.1/sql-listen.html "PostgreSQL 8.1 - LISTEN") /
[8.0](/docs/8.0/sql-listen.html "PostgreSQL 8.0 - LISTEN") /
[7.4](/docs/7.4/sql-listen.html "PostgreSQL 7.4 - LISTEN") /
[7.3](/docs/7.3/sql-listen.html "PostgreSQL 7.3 - LISTEN") /
[7.2](/docs/7.2/sql-listen.html "PostgreSQL 7.2 - LISTEN") /
[7.1](/docs/7.1/sql-listen.html "PostgreSQL 7.1 - LISTEN")

__

LISTEN  
---  
[Prev](sql-insert.html "INSERT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-load.html "LOAD")  
  
* * *

## LISTEN

LISTEN — listen for a notification

## Synopsis

    
    
    LISTEN _channel_
    

## Description

`LISTEN` registers the current session as a listener on the notification
channel named _`channel`_. If the current session is already registered as a
listener for this notification channel, nothing is done.

Whenever the command `NOTIFY _`channel`_` is invoked, either by this session
or another one connected to the same database, all the sessions currently
listening on that notification channel are notified, and each will in turn
notify its connected client application.

A session can be unregistered for a given notification channel with the
`UNLISTEN` command. A session's listen registrations are automatically cleared
when the session ends.

The method a client application must use to detect notification events depends
on which PostgreSQL application programming interface it uses. With the libpq
library, the application issues `LISTEN` as an ordinary SQL command, and then
must periodically call the function `PQnotifies` to find out whether any
notification events have been received. Other interfaces such as libpgtcl
provide higher-level methods for handling notify events; indeed, with libpgtcl
the application programmer should not even issue `LISTEN` or `UNLISTEN`
directly. See the documentation for the interface you are using for more
details.

## Parameters

_`channel`_

    

Name of a notification channel (any identifier).

## Notes

`LISTEN` takes effect at transaction commit. If `LISTEN` or `UNLISTEN` is
executed within a transaction that later rolls back, the set of notification
channels being listened to is unchanged.

A transaction that has executed `LISTEN` cannot be prepared for two-phase
commit.

There is a race condition when first setting up a listening session: if
concurrently-committing transactions are sending notify events, exactly which
of those will the newly listening session receive? The answer is that the
session will receive all events committed after an instant during the
transaction's commit step. But that is slightly later than any database state
that the transaction could have observed in queries. This leads to the
following rule for using `LISTEN`: first execute (and commit!) that command,
then in a new transaction inspect the database state as needed by the
application logic, then rely on notifications to find out about subsequent
changes to the database state. The first few received notifications might
refer to updates already observed in the initial database inspection, but this
is usually harmless.

[NOTIFY](sql-notify.html "NOTIFY") contains a more extensive discussion of the
use of `LISTEN` and `NOTIFY`.

## Examples

Configure and execute a listen/notify sequence from psql:

    
    
    LISTEN virtual;
    NOTIFY virtual;
    Asynchronous notification "virtual" received from server process with PID 8448.
    

## Compatibility

There is no `LISTEN` statement in the SQL standard.

## See Also

[NOTIFY](sql-notify.html "NOTIFY"), [UNLISTEN](sql-unlisten.html "UNLISTEN")

* * *

[Prev](sql-insert.html "INSERT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-load.html "LOAD")  
---|---|---  
INSERT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  LOAD  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-listen.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

