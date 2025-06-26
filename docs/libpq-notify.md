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

Supported Versions: [Current](/docs/current/libpq-notify.html "PostgreSQL 17 -
34.9. Asynchronous Notification") ([17](/docs/17/libpq-notify.html "PostgreSQL
17 - 34.9. Asynchronous Notification")) / [16](/docs/16/libpq-notify.html
"PostgreSQL 16 - 34.9. Asynchronous Notification") / [15](/docs/15/libpq-
notify.html "PostgreSQL 15 - 34.9. Asynchronous Notification") /
[14](/docs/14/libpq-notify.html "PostgreSQL 14 - 34.9. Asynchronous
Notification") / [13](/docs/13/libpq-notify.html "PostgreSQL 13 -
34.9. Asynchronous Notification")

Development Versions: [18](/docs/18/libpq-notify.html "PostgreSQL 18 -
34.9. Asynchronous Notification") / [devel](/docs/devel/libpq-notify.html
"PostgreSQL devel - 34.9. Asynchronous Notification")

Unsupported versions: [12](/docs/12/libpq-notify.html "PostgreSQL 12 -
34.9. Asynchronous Notification") / [11](/docs/11/libpq-notify.html
"PostgreSQL 11 - 34.9. Asynchronous Notification") / [10](/docs/10/libpq-
notify.html "PostgreSQL 10 - 34.9. Asynchronous Notification") /
[9.6](/docs/9.6/libpq-notify.html "PostgreSQL 9.6 - 34.9. Asynchronous
Notification") / [9.5](/docs/9.5/libpq-notify.html "PostgreSQL 9.5 -
34.9. Asynchronous Notification") / [9.4](/docs/9.4/libpq-notify.html
"PostgreSQL 9.4 - 34.9. Asynchronous Notification") / [9.3](/docs/9.3/libpq-
notify.html "PostgreSQL 9.3 - 34.9. Asynchronous Notification") /
[9.2](/docs/9.2/libpq-notify.html "PostgreSQL 9.2 - 34.9. Asynchronous
Notification") / [9.1](/docs/9.1/libpq-notify.html "PostgreSQL 9.1 -
34.9. Asynchronous Notification") / [9.0](/docs/9.0/libpq-notify.html
"PostgreSQL 9.0 - 34.9. Asynchronous Notification") / [8.4](/docs/8.4/libpq-
notify.html "PostgreSQL 8.4 - 34.9. Asynchronous Notification") /
[8.3](/docs/8.3/libpq-notify.html "PostgreSQL 8.3 - 34.9. Asynchronous
Notification") / [8.2](/docs/8.2/libpq-notify.html "PostgreSQL 8.2 -
34.9. Asynchronous Notification") / [8.1](/docs/8.1/libpq-notify.html
"PostgreSQL 8.1 - 34.9. Asynchronous Notification") / [8.0](/docs/8.0/libpq-
notify.html "PostgreSQL 8.0 - 34.9. Asynchronous Notification") /
[7.4](/docs/7.4/libpq-notify.html "PostgreSQL 7.4 - 34.9. Asynchronous
Notification") / [7.3](/docs/7.3/libpq-notify.html "PostgreSQL 7.3 -
34.9. Asynchronous Notification") / [7.2](/docs/7.2/libpq-notify.html
"PostgreSQL 7.2 - 34.9. Asynchronous Notification") / [7.1](/docs/7.1/libpq-
notify.html "PostgreSQL 7.1 - 34.9. Asynchronous Notification")

__

34.9. Asynchronous Notification  
---  
[Prev](libpq-fastpath.html "34.8. The Fast-Path Interface")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-copy.html "34.10. Functions Associated with the COPY Command")  
  
* * *

## 34.9. Asynchronous Notification #

PostgreSQL offers asynchronous notification via the `LISTEN` and `NOTIFY`
commands. A client session registers its interest in a particular notification
channel with the `LISTEN` command (and can stop listening with the `UNLISTEN`
command). All sessions listening on a particular channel will be notified
asynchronously when a `NOTIFY` command with that channel name is executed by
any session. A “payload” string can be passed to communicate additional data
to the listeners.

libpq applications submit `LISTEN`, `UNLISTEN`, and `NOTIFY` commands as
ordinary SQL commands. The arrival of `NOTIFY` messages can subsequently be
detected by calling `PQnotifies`.

The function `PQnotifies` returns the next notification from a list of
unhandled notification messages received from the server. It returns a null
pointer if there are no pending notifications. Once a notification is returned
from `PQnotifies`, it is considered handled and will be removed from the list
of notifications.

    
    
    PGnotify *PQnotifies(PGconn *conn);
    
    typedef struct pgNotify
    {
        char *relname;              /* notification channel name */
        int  be_pid;                /* process ID of notifying server process */
        char *extra;                /* notification payload string */
    } PGnotify;
    

After processing a `PGnotify` object returned by `PQnotifies`, be sure to free
it with [`PQfreemem`](libpq-misc.html#LIBPQ-PQFREEMEM). It is sufficient to
free the `PGnotify` pointer; the `relname` and `extra` fields do not represent
separate allocations. (The names of these fields are historical; in
particular, channel names need not have anything to do with relation names.)

[Example 34.2](libpq-example.html#LIBPQ-EXAMPLE-2 "Example 34.2. libpq Example
Program 2") gives a sample program that illustrates the use of asynchronous
notification.

`PQnotifies` does not actually read data from the server; it just returns
messages previously absorbed by another libpq function. In ancient releases of
libpq, the only way to ensure timely receipt of `NOTIFY` messages was to
constantly submit commands, even empty ones, and then check `PQnotifies` after
each [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC). While this still works, it is
deprecated as a waste of processing power.

A better way to check for `NOTIFY` messages when you have no useful commands
to execute is to call [`PQconsumeInput`](libpq-async.html#LIBPQ-
PQCONSUMEINPUT) , then check `PQnotifies`. You can use `select()` to wait for
data to arrive from the server, thereby using no CPU power unless there is
something to do. (See [`PQsocket`](libpq-status.html#LIBPQ-PQSOCKET) to obtain
the file descriptor number to use with `select()`.) Note that this will work
OK whether you submit commands with [`PQsendQuery`](libpq-async.html#LIBPQ-
PQSENDQUERY)/[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) or simply use
[`PQexec`](libpq-exec.html#LIBPQ-PQEXEC). You should, however, remember to
check `PQnotifies` after each [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) or [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC), to see if any
notifications came in during the processing of the command.

* * *

[Prev](libpq-fastpath.html "34.8. The Fast-Path Interface")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-copy.html "34.10. Functions Associated with the COPY Command")  
---|---|---  
34.8. The Fast-Path Interface  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.10. Functions Associated with the `COPY` Command  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-notify.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

