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

Supported Versions: [Current](/docs/current/contrib-dblink-disconnect.html
"PostgreSQL 17 - dblink_disconnect") ([17](/docs/17/contrib-dblink-
disconnect.html "PostgreSQL 17 - dblink_disconnect")) / [16](/docs/16/contrib-
dblink-disconnect.html "PostgreSQL 16 - dblink_disconnect") /
[15](/docs/15/contrib-dblink-disconnect.html "PostgreSQL 15 -
dblink_disconnect") / [14](/docs/14/contrib-dblink-disconnect.html "PostgreSQL
14 - dblink_disconnect") / [13](/docs/13/contrib-dblink-disconnect.html
"PostgreSQL 13 - dblink_disconnect")

Development Versions: [18](/docs/18/contrib-dblink-disconnect.html "PostgreSQL
18 - dblink_disconnect") / [devel](/docs/devel/contrib-dblink-disconnect.html
"PostgreSQL devel - dblink_disconnect")

Unsupported versions: [12](/docs/12/contrib-dblink-disconnect.html "PostgreSQL
12 - dblink_disconnect") / [11](/docs/11/contrib-dblink-disconnect.html
"PostgreSQL 11 - dblink_disconnect") / [10](/docs/10/contrib-dblink-
disconnect.html "PostgreSQL 10 - dblink_disconnect") /
[9.6](/docs/9.6/contrib-dblink-disconnect.html "PostgreSQL 9.6 -
dblink_disconnect") / [9.5](/docs/9.5/contrib-dblink-disconnect.html
"PostgreSQL 9.5 - dblink_disconnect") / [9.4](/docs/9.4/contrib-dblink-
disconnect.html "PostgreSQL 9.4 - dblink_disconnect") /
[9.3](/docs/9.3/contrib-dblink-disconnect.html "PostgreSQL 9.3 -
dblink_disconnect") / [9.2](/docs/9.2/contrib-dblink-disconnect.html
"PostgreSQL 9.2 - dblink_disconnect") / [9.1](/docs/9.1/contrib-dblink-
disconnect.html "PostgreSQL 9.1 - dblink_disconnect") /
[9.0](/docs/9.0/contrib-dblink-disconnect.html "PostgreSQL 9.0 -
dblink_disconnect") / [8.4](/docs/8.4/contrib-dblink-disconnect.html
"PostgreSQL 8.4 - dblink_disconnect") / [8.3](/docs/8.3/contrib-dblink-
disconnect.html "PostgreSQL 8.3 - dblink_disconnect")

__

dblink_disconnect  
---  
[Prev](contrib-dblink-connect-u.html "dblink_connect_u")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-function.html "dblink")  
  
* * *

## dblink_disconnect

dblink_disconnect — closes a persistent connection to a remote database

## Synopsis

    
    
    dblink_disconnect() returns text
    dblink_disconnect(text connname) returns text
    

## Description

`dblink_disconnect()` closes a connection previously opened by
`dblink_connect()`. The form with no arguments closes an unnamed connection.

## Arguments

_`connname`_

    

The name of a named connection to be closed.

## Return Value

Returns status, which is always `OK` (since any error causes the function to
throw an error instead of returning).

## Examples

    
    
    SELECT dblink_disconnect();
     dblink_disconnect
    -------------------
     OK
    (1 row)
    
    SELECT dblink_disconnect('myconn');
     dblink_disconnect
    -------------------
     OK
    (1 row)
    

* * *

[Prev](contrib-dblink-connect-u.html "dblink_connect_u")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-function.html "dblink")  
---|---|---  
dblink_connect_u  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-
disconnect.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

