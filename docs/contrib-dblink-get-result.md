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

Supported Versions: [Current](/docs/current/contrib-dblink-get-result.html
"PostgreSQL 17 - dblink_get_result") ([17](/docs/17/contrib-dblink-get-
result.html "PostgreSQL 17 - dblink_get_result")) / [16](/docs/16/contrib-
dblink-get-result.html "PostgreSQL 16 - dblink_get_result") /
[15](/docs/15/contrib-dblink-get-result.html "PostgreSQL 15 -
dblink_get_result") / [14](/docs/14/contrib-dblink-get-result.html "PostgreSQL
14 - dblink_get_result") / [13](/docs/13/contrib-dblink-get-result.html
"PostgreSQL 13 - dblink_get_result")

Development Versions: [18](/docs/18/contrib-dblink-get-result.html "PostgreSQL
18 - dblink_get_result") / [devel](/docs/devel/contrib-dblink-get-result.html
"PostgreSQL devel - dblink_get_result")

Unsupported versions: [12](/docs/12/contrib-dblink-get-result.html "PostgreSQL
12 - dblink_get_result") / [11](/docs/11/contrib-dblink-get-result.html
"PostgreSQL 11 - dblink_get_result") / [10](/docs/10/contrib-dblink-get-
result.html "PostgreSQL 10 - dblink_get_result") / [9.6](/docs/9.6/contrib-
dblink-get-result.html "PostgreSQL 9.6 - dblink_get_result") /
[9.5](/docs/9.5/contrib-dblink-get-result.html "PostgreSQL 9.5 -
dblink_get_result") / [9.4](/docs/9.4/contrib-dblink-get-result.html
"PostgreSQL 9.4 - dblink_get_result") / [9.3](/docs/9.3/contrib-dblink-get-
result.html "PostgreSQL 9.3 - dblink_get_result") / [9.2](/docs/9.2/contrib-
dblink-get-result.html "PostgreSQL 9.2 - dblink_get_result") /
[9.1](/docs/9.1/contrib-dblink-get-result.html "PostgreSQL 9.1 -
dblink_get_result") / [9.0](/docs/9.0/contrib-dblink-get-result.html
"PostgreSQL 9.0 - dblink_get_result") / [8.4](/docs/8.4/contrib-dblink-get-
result.html "PostgreSQL 8.4 - dblink_get_result") / [8.3](/docs/8.3/contrib-
dblink-get-result.html "PostgreSQL 8.3 - dblink_get_result")

__

dblink_get_result  
---  
[Prev](contrib-dblink-get-notify.html "dblink_get_notify")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-cancel-query.html "dblink_cancel_query")  
  
* * *

## dblink_get_result

dblink_get_result — gets an async query result

## Synopsis

    
    
    dblink_get_result(text connname [, bool fail_on_error]) returns setof record
    

## Description

`dblink_get_result` collects the results of an asynchronous query previously
sent with `dblink_send_query`. If the query is not already completed,
`dblink_get_result` will wait until it is.

## Arguments

_`connname`_

    

Name of the connection to use.

_`fail_on_error`_

    

If true (the default when omitted) then an error thrown on the remote side of
the connection causes an error to also be thrown locally. If false, the remote
error is locally reported as a NOTICE, and the function returns no rows.

## Return Value

For an async query (that is, an SQL statement returning rows), the function
returns the row(s) produced by the query. To use this function, you will need
to specify the expected set of columns, as previously discussed for `dblink`.

For an async command (that is, an SQL statement not returning rows), the
function returns a single row with a single text column containing the
command's status string. It is still necessary to specify that the result will
have a single text column in the calling `FROM` clause.

## Notes

This function _must_ be called if `dblink_send_query` returned 1. It must be
called once for each query sent, and one additional time to obtain an empty
set result, before the connection can be used again.

When using `dblink_send_query` and `dblink_get_result`, dblink fetches the
entire remote query result before returning any of it to the local query
processor. If the query returns a large number of rows, this can result in
transient memory bloat in the local session. It may be better to open such a
query as a cursor with `dblink_open` and then fetch a manageable number of
rows at a time. Alternatively, use plain `dblink()`, which avoids memory bloat
by spooling large result sets to disk.

## Examples

    
    
    contrib_regression=# SELECT dblink_connect('dtest1', 'dbname=contrib_regression');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    contrib_regression=# SELECT * FROM
    contrib_regression-# dblink_send_query('dtest1', 'select * from foo where f1 < 3') AS t1;
     t1
    ----
      1
    (1 row)
    
    contrib_regression=# SELECT * FROM dblink_get_result('dtest1') AS t1(f1 int, f2 text, f3 text[]);
     f1 | f2 |     f3
    ----+----+------------
      0 | a  | {a0,b0,c0}
      1 | b  | {a1,b1,c1}
      2 | c  | {a2,b2,c2}
    (3 rows)
    
    contrib_regression=# SELECT * FROM dblink_get_result('dtest1') AS t1(f1 int, f2 text, f3 text[]);
     f1 | f2 | f3
    ----+----+----
    (0 rows)
    
    contrib_regression=# SELECT * FROM
    contrib_regression-# dblink_send_query('dtest1', 'select * from foo where f1 < 3; select * from foo where f1 > 6') AS t1;
     t1
    ----
      1
    (1 row)
    
    contrib_regression=# SELECT * FROM dblink_get_result('dtest1') AS t1(f1 int, f2 text, f3 text[]);
     f1 | f2 |     f3
    ----+----+------------
      0 | a  | {a0,b0,c0}
      1 | b  | {a1,b1,c1}
      2 | c  | {a2,b2,c2}
    (3 rows)
    
    contrib_regression=# SELECT * FROM dblink_get_result('dtest1') AS t1(f1 int, f2 text, f3 text[]);
     f1 | f2 |      f3
    ----+----+---------------
      7 | h  | {a7,b7,c7}
      8 | i  | {a8,b8,c8}
      9 | j  | {a9,b9,c9}
     10 | k  | {a10,b10,c10}
    (4 rows)
    
    contrib_regression=# SELECT * FROM dblink_get_result('dtest1') AS t1(f1 int, f2 text, f3 text[]);
     f1 | f2 | f3
    ----+----+----
    (0 rows)
    

* * *

[Prev](contrib-dblink-get-notify.html "dblink_get_notify")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-cancel-query.html "dblink_cancel_query")  
---|---|---  
dblink_get_notify  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_cancel_query  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-get-
result.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

