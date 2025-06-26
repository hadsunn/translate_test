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

Supported Versions: [Current](/docs/current/sql-unlisten.html "PostgreSQL 17 -
UNLISTEN") ([17](/docs/17/sql-unlisten.html "PostgreSQL 17 - UNLISTEN")) /
[16](/docs/16/sql-unlisten.html "PostgreSQL 16 - UNLISTEN") /
[15](/docs/15/sql-unlisten.html "PostgreSQL 15 - UNLISTEN") /
[14](/docs/14/sql-unlisten.html "PostgreSQL 14 - UNLISTEN") /
[13](/docs/13/sql-unlisten.html "PostgreSQL 13 - UNLISTEN")

Development Versions: [18](/docs/18/sql-unlisten.html "PostgreSQL 18 -
UNLISTEN") / [devel](/docs/devel/sql-unlisten.html "PostgreSQL devel -
UNLISTEN")

Unsupported versions: [12](/docs/12/sql-unlisten.html "PostgreSQL 12 -
UNLISTEN") / [11](/docs/11/sql-unlisten.html "PostgreSQL 11 - UNLISTEN") /
[10](/docs/10/sql-unlisten.html "PostgreSQL 10 - UNLISTEN") /
[9.6](/docs/9.6/sql-unlisten.html "PostgreSQL 9.6 - UNLISTEN") /
[9.5](/docs/9.5/sql-unlisten.html "PostgreSQL 9.5 - UNLISTEN") /
[9.4](/docs/9.4/sql-unlisten.html "PostgreSQL 9.4 - UNLISTEN") /
[9.3](/docs/9.3/sql-unlisten.html "PostgreSQL 9.3 - UNLISTEN") /
[9.2](/docs/9.2/sql-unlisten.html "PostgreSQL 9.2 - UNLISTEN") /
[9.1](/docs/9.1/sql-unlisten.html "PostgreSQL 9.1 - UNLISTEN") /
[9.0](/docs/9.0/sql-unlisten.html "PostgreSQL 9.0 - UNLISTEN") /
[8.4](/docs/8.4/sql-unlisten.html "PostgreSQL 8.4 - UNLISTEN") /
[8.3](/docs/8.3/sql-unlisten.html "PostgreSQL 8.3 - UNLISTEN") /
[8.2](/docs/8.2/sql-unlisten.html "PostgreSQL 8.2 - UNLISTEN") /
[8.1](/docs/8.1/sql-unlisten.html "PostgreSQL 8.1 - UNLISTEN") /
[8.0](/docs/8.0/sql-unlisten.html "PostgreSQL 8.0 - UNLISTEN") /
[7.4](/docs/7.4/sql-unlisten.html "PostgreSQL 7.4 - UNLISTEN") /
[7.3](/docs/7.3/sql-unlisten.html "PostgreSQL 7.3 - UNLISTEN") /
[7.2](/docs/7.2/sql-unlisten.html "PostgreSQL 7.2 - UNLISTEN") /
[7.1](/docs/7.1/sql-unlisten.html "PostgreSQL 7.1 - UNLISTEN")

__

UNLISTEN  
---  
[Prev](sql-truncate.html "TRUNCATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-update.html "UPDATE")  
  
* * *

## UNLISTEN

UNLISTEN — stop listening for a notification

## Synopsis

    
    
    UNLISTEN { _channel_ | * }
    

## Description

`UNLISTEN` is used to remove an existing registration for `NOTIFY` events.
`UNLISTEN` cancels any existing registration of the current PostgreSQL session
as a listener on the notification channel named _`channel`_. The special
wildcard `*` cancels all listener registrations for the current session.

[NOTIFY](sql-notify.html "NOTIFY") contains a more extensive discussion of the
use of `LISTEN` and `NOTIFY`.

## Parameters

_`channel`_

    

Name of a notification channel (any identifier).

`*`

    

All current listen registrations for this session are cleared.

## Notes

You can unlisten something you were not listening for; no warning or error
will appear.

At the end of each session, `UNLISTEN *` is automatically executed.

A transaction that has executed `UNLISTEN` cannot be prepared for two-phase
commit.

## Examples

To make a registration:

    
    
    LISTEN virtual;
    NOTIFY virtual;
    Asynchronous notification "virtual" received from server process with PID 8448.
    

Once `UNLISTEN` has been executed, further `NOTIFY` messages will be ignored:

    
    
    UNLISTEN virtual;
    NOTIFY virtual;
    -- no NOTIFY event is received
    

## Compatibility

There is no `UNLISTEN` command in the SQL standard.

## See Also

[LISTEN](sql-listen.html "LISTEN"), [NOTIFY](sql-notify.html "NOTIFY")

* * *

[Prev](sql-truncate.html "TRUNCATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-update.html "UPDATE")  
---|---|---  
TRUNCATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  UPDATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-unlisten.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

