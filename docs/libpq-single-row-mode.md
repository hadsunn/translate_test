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

Supported Versions: [Current](/docs/current/libpq-single-row-mode.html
"PostgreSQL 17 - 34.6. Retrieving Query Results Row-by-Row")
([17](/docs/17/libpq-single-row-mode.html "PostgreSQL 17 - 34.6. Retrieving
Query Results Row-by-Row")) / [16](/docs/16/libpq-single-row-mode.html
"PostgreSQL 16 - 34.6. Retrieving Query Results Row-by-Row") /
[15](/docs/15/libpq-single-row-mode.html "PostgreSQL 15 - 34.6. Retrieving
Query Results Row-by-Row") / [14](/docs/14/libpq-single-row-mode.html
"PostgreSQL 14 - 34.6. Retrieving Query Results Row-by-Row") /
[13](/docs/13/libpq-single-row-mode.html "PostgreSQL 13 - 34.6. Retrieving
Query Results Row-by-Row")

Development Versions: [18](/docs/18/libpq-single-row-mode.html "PostgreSQL 18
- 34.6. Retrieving Query Results Row-by-Row") / [devel](/docs/devel/libpq-
single-row-mode.html "PostgreSQL devel - 34.6. Retrieving Query Results Row-
by-Row")

Unsupported versions: [12](/docs/12/libpq-single-row-mode.html "PostgreSQL 12
- 34.6. Retrieving Query Results Row-by-Row") / [11](/docs/11/libpq-single-
row-mode.html "PostgreSQL 11 - 34.6. Retrieving Query Results Row-by-Row") /
[10](/docs/10/libpq-single-row-mode.html "PostgreSQL 10 - 34.6. Retrieving
Query Results Row-by-Row") / [9.6](/docs/9.6/libpq-single-row-mode.html
"PostgreSQL 9.6 - 34.6. Retrieving Query Results Row-by-Row") /
[9.5](/docs/9.5/libpq-single-row-mode.html "PostgreSQL 9.5 - 34.6. Retrieving
Query Results Row-by-Row") / [9.4](/docs/9.4/libpq-single-row-mode.html
"PostgreSQL 9.4 - 34.6. Retrieving Query Results Row-by-Row") /
[9.3](/docs/9.3/libpq-single-row-mode.html "PostgreSQL 9.3 - 34.6. Retrieving
Query Results Row-by-Row") / [9.2](/docs/9.2/libpq-single-row-mode.html
"PostgreSQL 9.2 - 34.6. Retrieving Query Results Row-by-Row")

__

34.6. Retrieving Query Results Row-by-Row  
---  
[Prev](libpq-pipeline-mode.html "34.5. Pipeline Mode")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-cancel.html "34.7. Canceling Queries in Progress")  
  
* * *

## 34.6. Retrieving Query Results Row-by-Row #

Ordinarily, libpq collects an SQL command's entire result and returns it to
the application as a single `PGresult`. This can be unworkable for commands
that return a large number of rows. For such cases, applications can use
[`PQsendQuery`](libpq-async.html#LIBPQ-PQSENDQUERY) and [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT) in _single-row mode_. In this mode, the result
row(s) are returned to the application one at a time, as they are received
from the server.

To enter single-row mode, call [`PQsetSingleRowMode`](libpq-single-row-
mode.html#LIBPQ-PQSETSINGLEROWMODE) immediately after a successful call of
[`PQsendQuery`](libpq-async.html#LIBPQ-PQSENDQUERY) (or a sibling function).
This mode selection is effective only for the currently executing query. Then
call [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) repeatedly, until it
returns null, as documented in [Section 34.4](libpq-async.html
"34.4. Asynchronous Command Processing"). If the query returns any rows, they
are returned as individual `PGresult` objects, which look like normal query
results except for having status code `PGRES_SINGLE_TUPLE` instead of
`PGRES_TUPLES_OK`. After the last row, or immediately if the query returns
zero rows, a zero-row object with status `PGRES_TUPLES_OK` is returned; this
is the signal that no more rows will arrive. (But note that it is still
necessary to continue calling [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) until it returns null.) All of these `PGresult` objects will
contain the same row description data (column names, types, etc.) that an
ordinary `PGresult` object for the query would have. Each object should be
freed with [`PQclear`](libpq-exec.html#LIBPQ-PQCLEAR) as usual.

When using pipeline mode, single-row mode needs to be activated for each query
in the pipeline before retrieving results for that query with `PQgetResult`.
See [Section 34.5](libpq-pipeline-mode.html "34.5. Pipeline Mode") for more
information.

`PQsetSingleRowMode` #

    

Select single-row mode for the currently-executing query.

    
    
    int PQsetSingleRowMode(PGconn *conn);
    

This function can only be called immediately after [`PQsendQuery`](libpq-
async.html#LIBPQ-PQSENDQUERY) or one of its sibling functions, before any
other operation on the connection such as [`PQconsumeInput`](libpq-
async.html#LIBPQ-PQCONSUMEINPUT) or [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT). If called at the correct time, the function activates single-row
mode for the current query and returns 1. Otherwise the mode stays unchanged
and the function returns 0. In any case, the mode reverts to normal after
completion of the current query.

### Caution

While processing a query, the server may return some rows and then encounter
an error, causing the query to be aborted. Ordinarily, libpq discards any such
rows and reports only the error. But in single-row mode, those rows will have
already been returned to the application. Hence, the application will see some
`PGRES_SINGLE_TUPLE` `PGresult` objects followed by a `PGRES_FATAL_ERROR`
object. For proper transactional behavior, the application must be designed to
discard or undo whatever has been done with the previously-processed rows, if
the query ultimately fails.

* * *

[Prev](libpq-pipeline-mode.html "34.5. Pipeline Mode")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-cancel.html "34.7. Canceling Queries in Progress")  
---|---|---  
34.5. Pipeline Mode  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.7. Canceling Queries in Progress  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-single-row-mode.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

