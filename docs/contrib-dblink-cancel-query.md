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

Supported Versions: [Current](/docs/current/contrib-dblink-cancel-query.html
"PostgreSQL 17 - dblink_cancel_query") ([17](/docs/17/contrib-dblink-cancel-
query.html "PostgreSQL 17 - dblink_cancel_query")) / [16](/docs/16/contrib-
dblink-cancel-query.html "PostgreSQL 16 - dblink_cancel_query") /
[15](/docs/15/contrib-dblink-cancel-query.html "PostgreSQL 15 -
dblink_cancel_query") / [14](/docs/14/contrib-dblink-cancel-query.html
"PostgreSQL 14 - dblink_cancel_query") / [13](/docs/13/contrib-dblink-cancel-
query.html "PostgreSQL 13 - dblink_cancel_query")

Development Versions: [18](/docs/18/contrib-dblink-cancel-query.html
"PostgreSQL 18 - dblink_cancel_query") / [devel](/docs/devel/contrib-dblink-
cancel-query.html "PostgreSQL devel - dblink_cancel_query")

Unsupported versions: [12](/docs/12/contrib-dblink-cancel-query.html
"PostgreSQL 12 - dblink_cancel_query") / [11](/docs/11/contrib-dblink-cancel-
query.html "PostgreSQL 11 - dblink_cancel_query") / [10](/docs/10/contrib-
dblink-cancel-query.html "PostgreSQL 10 - dblink_cancel_query") /
[9.6](/docs/9.6/contrib-dblink-cancel-query.html "PostgreSQL 9.6 -
dblink_cancel_query") / [9.5](/docs/9.5/contrib-dblink-cancel-query.html
"PostgreSQL 9.5 - dblink_cancel_query") / [9.4](/docs/9.4/contrib-dblink-
cancel-query.html "PostgreSQL 9.4 - dblink_cancel_query") /
[9.3](/docs/9.3/contrib-dblink-cancel-query.html "PostgreSQL 9.3 -
dblink_cancel_query") / [9.2](/docs/9.2/contrib-dblink-cancel-query.html
"PostgreSQL 9.2 - dblink_cancel_query") / [9.1](/docs/9.1/contrib-dblink-
cancel-query.html "PostgreSQL 9.1 - dblink_cancel_query") /
[9.0](/docs/9.0/contrib-dblink-cancel-query.html "PostgreSQL 9.0 -
dblink_cancel_query") / [8.4](/docs/8.4/contrib-dblink-cancel-query.html
"PostgreSQL 8.4 - dblink_cancel_query") / [8.3](/docs/8.3/contrib-dblink-
cancel-query.html "PostgreSQL 8.3 - dblink_cancel_query")

__

dblink_cancel_query  
---  
[Prev](contrib-dblink-get-result.html "dblink_get_result")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-get-pkey.html "dblink_get_pkey")  
  
* * *

## dblink_cancel_query

dblink_cancel_query — cancels any active query on the named connection

## Synopsis

    
    
    dblink_cancel_query(text connname) returns text
    

## Description

`dblink_cancel_query` attempts to cancel any query that is in progress on the
named connection. Note that this is not certain to succeed (since, for
example, the remote query might already have finished). A cancel request
simply improves the odds that the query will fail soon. You must still
complete the normal query protocol, for example by calling
`dblink_get_result`.

## Arguments

_`connname`_

    

Name of the connection to use.

## Return Value

Returns `OK` if the cancel request has been sent, or the text of an error
message on failure.

## Examples

    
    
    SELECT dblink_cancel_query('dtest1');
    

* * *

[Prev](contrib-dblink-get-result.html "dblink_get_result")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-get-pkey.html "dblink_get_pkey")  
---|---|---  
dblink_get_result  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_get_pkey  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-cancel-
query.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

