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

Supported Versions: [Current](/docs/current/contrib-dblink-is-busy.html
"PostgreSQL 17 - dblink_is_busy") ([17](/docs/17/contrib-dblink-is-busy.html
"PostgreSQL 17 - dblink_is_busy")) / [16](/docs/16/contrib-dblink-is-busy.html
"PostgreSQL 16 - dblink_is_busy") / [15](/docs/15/contrib-dblink-is-busy.html
"PostgreSQL 15 - dblink_is_busy") / [14](/docs/14/contrib-dblink-is-busy.html
"PostgreSQL 14 - dblink_is_busy") / [13](/docs/13/contrib-dblink-is-busy.html
"PostgreSQL 13 - dblink_is_busy")

Development Versions: [18](/docs/18/contrib-dblink-is-busy.html "PostgreSQL 18
- dblink_is_busy") / [devel](/docs/devel/contrib-dblink-is-busy.html
"PostgreSQL devel - dblink_is_busy")

Unsupported versions: [12](/docs/12/contrib-dblink-is-busy.html "PostgreSQL 12
- dblink_is_busy") / [11](/docs/11/contrib-dblink-is-busy.html "PostgreSQL 11
- dblink_is_busy") / [10](/docs/10/contrib-dblink-is-busy.html "PostgreSQL 10
- dblink_is_busy") / [9.6](/docs/9.6/contrib-dblink-is-busy.html "PostgreSQL
9.6 - dblink_is_busy") / [9.5](/docs/9.5/contrib-dblink-is-busy.html
"PostgreSQL 9.5 - dblink_is_busy") / [9.4](/docs/9.4/contrib-dblink-is-
busy.html "PostgreSQL 9.4 - dblink_is_busy") / [9.3](/docs/9.3/contrib-dblink-
is-busy.html "PostgreSQL 9.3 - dblink_is_busy") / [9.2](/docs/9.2/contrib-
dblink-is-busy.html "PostgreSQL 9.2 - dblink_is_busy") /
[9.1](/docs/9.1/contrib-dblink-is-busy.html "PostgreSQL 9.1 - dblink_is_busy")
/ [9.0](/docs/9.0/contrib-dblink-is-busy.html "PostgreSQL 9.0 -
dblink_is_busy") / [8.4](/docs/8.4/contrib-dblink-is-busy.html "PostgreSQL 8.4
- dblink_is_busy") / [8.3](/docs/8.3/contrib-dblink-is-busy.html "PostgreSQL
8.3 - dblink_is_busy")

__

dblink_is_busy  
---  
[Prev](contrib-dblink-send-query.html "dblink_send_query")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-get-notify.html "dblink_get_notify")  
  
* * *

## dblink_is_busy

dblink_is_busy — checks if connection is busy with an async query

## Synopsis

    
    
    dblink_is_busy(text connname) returns int
    

## Description

`dblink_is_busy` tests whether an async query is in progress.

## Arguments

_`connname`_

    

Name of the connection to check.

## Return Value

Returns 1 if connection is busy, 0 if it is not busy. If this function returns
0, it is guaranteed that `dblink_get_result` will not block.

## Examples

    
    
    SELECT dblink_is_busy('dtest1');
    

* * *

[Prev](contrib-dblink-send-query.html "dblink_send_query")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-get-notify.html "dblink_get_notify")  
---|---|---  
dblink_send_query  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_get_notify  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-is-busy.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

