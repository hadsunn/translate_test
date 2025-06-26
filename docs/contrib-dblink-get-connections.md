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

Supported Versions: [Current](/docs/current/contrib-dblink-get-
connections.html "PostgreSQL 17 - dblink_get_connections")
([17](/docs/17/contrib-dblink-get-connections.html "PostgreSQL 17 -
dblink_get_connections")) / [16](/docs/16/contrib-dblink-get-connections.html
"PostgreSQL 16 - dblink_get_connections") / [15](/docs/15/contrib-dblink-get-
connections.html "PostgreSQL 15 - dblink_get_connections") /
[14](/docs/14/contrib-dblink-get-connections.html "PostgreSQL 14 -
dblink_get_connections") / [13](/docs/13/contrib-dblink-get-connections.html
"PostgreSQL 13 - dblink_get_connections")

Development Versions: [18](/docs/18/contrib-dblink-get-connections.html
"PostgreSQL 18 - dblink_get_connections") / [devel](/docs/devel/contrib-
dblink-get-connections.html "PostgreSQL devel - dblink_get_connections")

Unsupported versions: [12](/docs/12/contrib-dblink-get-connections.html
"PostgreSQL 12 - dblink_get_connections") / [11](/docs/11/contrib-dblink-get-
connections.html "PostgreSQL 11 - dblink_get_connections") /
[10](/docs/10/contrib-dblink-get-connections.html "PostgreSQL 10 -
dblink_get_connections") / [9.6](/docs/9.6/contrib-dblink-get-connections.html
"PostgreSQL 9.6 - dblink_get_connections") / [9.5](/docs/9.5/contrib-dblink-
get-connections.html "PostgreSQL 9.5 - dblink_get_connections") /
[9.4](/docs/9.4/contrib-dblink-get-connections.html "PostgreSQL 9.4 -
dblink_get_connections") / [9.3](/docs/9.3/contrib-dblink-get-connections.html
"PostgreSQL 9.3 - dblink_get_connections") / [9.2](/docs/9.2/contrib-dblink-
get-connections.html "PostgreSQL 9.2 - dblink_get_connections") /
[9.1](/docs/9.1/contrib-dblink-get-connections.html "PostgreSQL 9.1 -
dblink_get_connections") / [9.0](/docs/9.0/contrib-dblink-get-connections.html
"PostgreSQL 9.0 - dblink_get_connections") / [8.4](/docs/8.4/contrib-dblink-
get-connections.html "PostgreSQL 8.4 - dblink_get_connections") /
[8.3](/docs/8.3/contrib-dblink-get-connections.html "PostgreSQL 8.3 -
dblink_get_connections")

__

dblink_get_connections  
---  
[Prev](contrib-dblink-close.html "dblink_close")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-error-message.html "dblink_error_message")  
  
* * *

## dblink_get_connections

dblink_get_connections — returns the names of all open named dblink
connections

## Synopsis

    
    
    dblink_get_connections() returns text[]
    

## Description

`dblink_get_connections` returns an array of the names of all open named
`dblink` connections.

## Return Value

Returns a text array of connection names, or NULL if none.

## Examples

    
    
    SELECT dblink_get_connections();
    

* * *

[Prev](contrib-dblink-close.html "dblink_close")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-error-message.html "dblink_error_message")  
---|---|---  
dblink_close  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_error_message  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-get-
connections.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

