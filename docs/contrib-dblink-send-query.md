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

Supported Versions: [Current](/docs/current/contrib-dblink-send-query.html
"PostgreSQL 17 - dblink_send_query") ([17](/docs/17/contrib-dblink-send-
query.html "PostgreSQL 17 - dblink_send_query")) / [16](/docs/16/contrib-
dblink-send-query.html "PostgreSQL 16 - dblink_send_query") /
[15](/docs/15/contrib-dblink-send-query.html "PostgreSQL 15 -
dblink_send_query") / [14](/docs/14/contrib-dblink-send-query.html "PostgreSQL
14 - dblink_send_query") / [13](/docs/13/contrib-dblink-send-query.html
"PostgreSQL 13 - dblink_send_query")

Development Versions: [18](/docs/18/contrib-dblink-send-query.html "PostgreSQL
18 - dblink_send_query") / [devel](/docs/devel/contrib-dblink-send-query.html
"PostgreSQL devel - dblink_send_query")

Unsupported versions: [12](/docs/12/contrib-dblink-send-query.html "PostgreSQL
12 - dblink_send_query") / [11](/docs/11/contrib-dblink-send-query.html
"PostgreSQL 11 - dblink_send_query") / [10](/docs/10/contrib-dblink-send-
query.html "PostgreSQL 10 - dblink_send_query") / [9.6](/docs/9.6/contrib-
dblink-send-query.html "PostgreSQL 9.6 - dblink_send_query") /
[9.5](/docs/9.5/contrib-dblink-send-query.html "PostgreSQL 9.5 -
dblink_send_query") / [9.4](/docs/9.4/contrib-dblink-send-query.html
"PostgreSQL 9.4 - dblink_send_query") / [9.3](/docs/9.3/contrib-dblink-send-
query.html "PostgreSQL 9.3 - dblink_send_query") / [9.2](/docs/9.2/contrib-
dblink-send-query.html "PostgreSQL 9.2 - dblink_send_query") /
[9.1](/docs/9.1/contrib-dblink-send-query.html "PostgreSQL 9.1 -
dblink_send_query") / [9.0](/docs/9.0/contrib-dblink-send-query.html
"PostgreSQL 9.0 - dblink_send_query") / [8.4](/docs/8.4/contrib-dblink-send-
query.html "PostgreSQL 8.4 - dblink_send_query") / [8.3](/docs/8.3/contrib-
dblink-send-query.html "PostgreSQL 8.3 - dblink_send_query")

__

dblink_send_query  
---  
[Prev](contrib-dblink-error-message.html "dblink_error_message")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-is-busy.html "dblink_is_busy")  
  
* * *

## dblink_send_query

dblink_send_query — sends an async query to a remote database

## Synopsis

    
    
    dblink_send_query(text connname, text sql) returns int
    

## Description

`dblink_send_query` sends a query to be executed asynchronously, that is,
without immediately waiting for the result. There must not be an async query
already in progress on the connection.

After successfully dispatching an async query, completion status can be
checked with `dblink_is_busy`, and the results are ultimately collected with
`dblink_get_result`. It is also possible to attempt to cancel an active async
query using `dblink_cancel_query`.

## Arguments

_`connname`_

    

Name of the connection to use.

_`sql`_

    

The SQL statement that you wish to execute in the remote database, for example
`select * from pg_class`.

## Return Value

Returns 1 if the query was successfully dispatched, 0 otherwise.

## Examples

    
    
    SELECT dblink_send_query('dtest1', 'SELECT * FROM foo WHERE f1 < 3');
    

* * *

[Prev](contrib-dblink-error-message.html "dblink_error_message")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-is-busy.html "dblink_is_busy")  
---|---|---  
dblink_error_message  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_is_busy  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-send-
query.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

