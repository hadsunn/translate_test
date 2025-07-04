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

Supported Versions: [Current](/docs/current/contrib-dblink-error-message.html
"PostgreSQL 17 - dblink_error_message") ([17](/docs/17/contrib-dblink-error-
message.html "PostgreSQL 17 - dblink_error_message")) / [16](/docs/16/contrib-
dblink-error-message.html "PostgreSQL 16 - dblink_error_message") /
[15](/docs/15/contrib-dblink-error-message.html "PostgreSQL 15 -
dblink_error_message") / [14](/docs/14/contrib-dblink-error-message.html
"PostgreSQL 14 - dblink_error_message") / [13](/docs/13/contrib-dblink-error-
message.html "PostgreSQL 13 - dblink_error_message")

Development Versions: [18](/docs/18/contrib-dblink-error-message.html
"PostgreSQL 18 - dblink_error_message") / [devel](/docs/devel/contrib-dblink-
error-message.html "PostgreSQL devel - dblink_error_message")

Unsupported versions: [12](/docs/12/contrib-dblink-error-message.html
"PostgreSQL 12 - dblink_error_message") / [11](/docs/11/contrib-dblink-error-
message.html "PostgreSQL 11 - dblink_error_message") / [10](/docs/10/contrib-
dblink-error-message.html "PostgreSQL 10 - dblink_error_message") /
[9.6](/docs/9.6/contrib-dblink-error-message.html "PostgreSQL 9.6 -
dblink_error_message") / [9.5](/docs/9.5/contrib-dblink-error-message.html
"PostgreSQL 9.5 - dblink_error_message") / [9.4](/docs/9.4/contrib-dblink-
error-message.html "PostgreSQL 9.4 - dblink_error_message") /
[9.3](/docs/9.3/contrib-dblink-error-message.html "PostgreSQL 9.3 -
dblink_error_message") / [9.2](/docs/9.2/contrib-dblink-error-message.html
"PostgreSQL 9.2 - dblink_error_message") / [9.1](/docs/9.1/contrib-dblink-
error-message.html "PostgreSQL 9.1 - dblink_error_message") /
[9.0](/docs/9.0/contrib-dblink-error-message.html "PostgreSQL 9.0 -
dblink_error_message") / [8.4](/docs/8.4/contrib-dblink-error-message.html
"PostgreSQL 8.4 - dblink_error_message") / [8.3](/docs/8.3/contrib-dblink-
error-message.html "PostgreSQL 8.3 - dblink_error_message")

__

dblink_error_message  
---  
[Prev](contrib-dblink-get-connections.html "dblink_get_connections")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-send-query.html "dblink_send_query")  
  
* * *

## dblink_error_message

dblink_error_message — gets last error message on the named connection

## Synopsis

    
    
    dblink_error_message(text connname) returns text
    

## Description

`dblink_error_message` fetches the most recent remote error message for a
given connection.

## Arguments

_`connname`_

    

Name of the connection to use.

## Return Value

Returns last error message, or `OK` if there has been no error in this
connection.

## Notes

When asynchronous queries are initiated by `dblink_send_query`, the error
message associated with the connection might not get updated until the
server's response message is consumed. This typically means that
`dblink_is_busy` or `dblink_get_result` should be called prior to
`dblink_error_message`, so that any error generated by the asynchronous query
will be visible.

## Examples

    
    
    SELECT dblink_error_message('dtest1');
    

* * *

[Prev](contrib-dblink-get-connections.html "dblink_get_connections")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-send-query.html "dblink_send_query")  
---|---|---  
dblink_get_connections  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_send_query  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-error-
message.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

