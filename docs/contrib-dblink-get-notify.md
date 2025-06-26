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

Supported Versions: [Current](/docs/current/contrib-dblink-get-notify.html
"PostgreSQL 17 - dblink_get_notify") ([17](/docs/17/contrib-dblink-get-
notify.html "PostgreSQL 17 - dblink_get_notify")) / [16](/docs/16/contrib-
dblink-get-notify.html "PostgreSQL 16 - dblink_get_notify") /
[15](/docs/15/contrib-dblink-get-notify.html "PostgreSQL 15 -
dblink_get_notify") / [14](/docs/14/contrib-dblink-get-notify.html "PostgreSQL
14 - dblink_get_notify") / [13](/docs/13/contrib-dblink-get-notify.html
"PostgreSQL 13 - dblink_get_notify")

Development Versions: [18](/docs/18/contrib-dblink-get-notify.html "PostgreSQL
18 - dblink_get_notify") / [devel](/docs/devel/contrib-dblink-get-notify.html
"PostgreSQL devel - dblink_get_notify")

Unsupported versions: [12](/docs/12/contrib-dblink-get-notify.html "PostgreSQL
12 - dblink_get_notify") / [11](/docs/11/contrib-dblink-get-notify.html
"PostgreSQL 11 - dblink_get_notify") / [10](/docs/10/contrib-dblink-get-
notify.html "PostgreSQL 10 - dblink_get_notify") / [9.6](/docs/9.6/contrib-
dblink-get-notify.html "PostgreSQL 9.6 - dblink_get_notify") /
[9.5](/docs/9.5/contrib-dblink-get-notify.html "PostgreSQL 9.5 -
dblink_get_notify") / [9.4](/docs/9.4/contrib-dblink-get-notify.html
"PostgreSQL 9.4 - dblink_get_notify") / [9.3](/docs/9.3/contrib-dblink-get-
notify.html "PostgreSQL 9.3 - dblink_get_notify") / [9.2](/docs/9.2/contrib-
dblink-get-notify.html "PostgreSQL 9.2 - dblink_get_notify") /
[9.1](/docs/9.1/contrib-dblink-get-notify.html "PostgreSQL 9.1 -
dblink_get_notify") / [9.0](/docs/9.0/contrib-dblink-get-notify.html
"PostgreSQL 9.0 - dblink_get_notify")

__

dblink_get_notify  
---  
[Prev](contrib-dblink-is-busy.html "dblink_is_busy")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-get-result.html "dblink_get_result")  
  
* * *

## dblink_get_notify

dblink_get_notify — retrieve async notifications on a connection

## Synopsis

    
    
    dblink_get_notify() returns setof (notify_name text, be_pid int, extra text)
    dblink_get_notify(text connname) returns setof (notify_name text, be_pid int, extra text)
    

## Description

`dblink_get_notify` retrieves notifications on either the unnamed connection,
or on a named connection if specified. To receive notifications via dblink,
`LISTEN` must first be issued, using `dblink_exec`. For details see
[LISTEN](sql-listen.html "LISTEN") and [NOTIFY](sql-notify.html "NOTIFY").

## Arguments

_`connname`_

    

The name of a named connection to get notifications on.

## Return Value

Returns `setof (notify_name text, be_pid int, extra text)`, or an empty set if
none.

## Examples

    
    
    SELECT dblink_exec('LISTEN virtual');
     dblink_exec
    -------------
     LISTEN
    (1 row)
    
    SELECT * FROM dblink_get_notify();
     notify_name | be_pid | extra
    -------------+--------+-------
    (0 rows)
    
    NOTIFY virtual;
    NOTIFY
    
    SELECT * FROM dblink_get_notify();
     notify_name | be_pid | extra
    -------------+--------+-------
     virtual     |   1229 |
    (1 row)
    

* * *

[Prev](contrib-dblink-is-busy.html "dblink_is_busy")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-get-result.html "dblink_get_result")  
---|---|---  
dblink_is_busy  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_get_result  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-get-
notify.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

