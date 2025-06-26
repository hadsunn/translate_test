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

Supported Versions: [Current](/docs/current/libpq-async.html "PostgreSQL 17 -
34.4. Asynchronous Command Processing") ([17](/docs/17/libpq-async.html
"PostgreSQL 17 - 34.4. Asynchronous Command Processing")) /
[16](/docs/16/libpq-async.html "PostgreSQL 16 - 34.4. Asynchronous Command
Processing") / [15](/docs/15/libpq-async.html "PostgreSQL 15 -
34.4. Asynchronous Command Processing") / [14](/docs/14/libpq-async.html
"PostgreSQL 14 - 34.4. Asynchronous Command Processing") /
[13](/docs/13/libpq-async.html "PostgreSQL 13 - 34.4. Asynchronous Command
Processing")

Development Versions: [18](/docs/18/libpq-async.html "PostgreSQL 18 -
34.4. Asynchronous Command Processing") / [devel](/docs/devel/libpq-async.html
"PostgreSQL devel - 34.4. Asynchronous Command Processing")

Unsupported versions: [12](/docs/12/libpq-async.html "PostgreSQL 12 -
34.4. Asynchronous Command Processing") / [11](/docs/11/libpq-async.html
"PostgreSQL 11 - 34.4. Asynchronous Command Processing") /
[10](/docs/10/libpq-async.html "PostgreSQL 10 - 34.4. Asynchronous Command
Processing") / [9.6](/docs/9.6/libpq-async.html "PostgreSQL 9.6 -
34.4. Asynchronous Command Processing") / [9.5](/docs/9.5/libpq-async.html
"PostgreSQL 9.5 - 34.4. Asynchronous Command Processing") /
[9.4](/docs/9.4/libpq-async.html "PostgreSQL 9.4 - 34.4. Asynchronous Command
Processing") / [9.3](/docs/9.3/libpq-async.html "PostgreSQL 9.3 -
34.4. Asynchronous Command Processing") / [9.2](/docs/9.2/libpq-async.html
"PostgreSQL 9.2 - 34.4. Asynchronous Command Processing") /
[9.1](/docs/9.1/libpq-async.html "PostgreSQL 9.1 - 34.4. Asynchronous Command
Processing") / [9.0](/docs/9.0/libpq-async.html "PostgreSQL 9.0 -
34.4. Asynchronous Command Processing") / [8.4](/docs/8.4/libpq-async.html
"PostgreSQL 8.4 - 34.4. Asynchronous Command Processing") /
[8.3](/docs/8.3/libpq-async.html "PostgreSQL 8.3 - 34.4. Asynchronous Command
Processing") / [8.2](/docs/8.2/libpq-async.html "PostgreSQL 8.2 -
34.4. Asynchronous Command Processing") / [8.1](/docs/8.1/libpq-async.html
"PostgreSQL 8.1 - 34.4. Asynchronous Command Processing") /
[8.0](/docs/8.0/libpq-async.html "PostgreSQL 8.0 - 34.4. Asynchronous Command
Processing") / [7.4](/docs/7.4/libpq-async.html "PostgreSQL 7.4 -
34.4. Asynchronous Command Processing") / [7.3](/docs/7.3/libpq-async.html
"PostgreSQL 7.3 - 34.4. Asynchronous Command Processing") /
[7.2](/docs/7.2/libpq-async.html "PostgreSQL 7.2 - 34.4. Asynchronous Command
Processing") / [7.1](/docs/7.1/libpq-async.html "PostgreSQL 7.1 -
34.4. Asynchronous Command Processing")

__

34.4. Asynchronous Command Processing  
---  
[Prev](libpq-exec.html "34.3. Command Execution Functions")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-pipeline-mode.html "34.5. Pipeline Mode")  
  
* * *

## 34.4. Asynchronous Command Processing #

The [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) function is adequate for
submitting commands in normal, synchronous applications. It has a few
deficiencies, however, that can be of importance to some users:

  * [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) waits for the command to be completed. The application might have other work to do (such as maintaining a user interface), in which case it won't want to block waiting for the response.

  * Since the execution of the client application is suspended while it waits for the result, it is hard for the application to decide that it would like to try to cancel the ongoing command. (It can be done from a signal handler, but not otherwise.)

  * [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) can return only one `PGresult` structure. If the submitted command string contains multiple SQL commands, all but the last `PGresult` are discarded by [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC).

  * [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) always collects the command's entire result, buffering it in a single `PGresult`. While this simplifies error-handling logic for the application, it can be impractical for results containing many rows.

Applications that do not like these limitations can instead use the underlying
functions that [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) is built from:
[`PQsendQuery`](libpq-async.html#LIBPQ-PQSENDQUERY) and [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT). There are also [`PQsendQueryParams`](libpq-
async.html#LIBPQ-PQSENDQUERYPARAMS), [`PQsendPrepare`](libpq-async.html#LIBPQ-
PQSENDPREPARE), [`PQsendQueryPrepared`](libpq-async.html#LIBPQ-
PQSENDQUERYPREPARED), [`PQsendDescribePrepared`](libpq-async.html#LIBPQ-
PQSENDDESCRIBEPREPARED), and [`PQsendDescribePortal`](libpq-async.html#LIBPQ-
PQSENDDESCRIBEPORTAL), which can be used with [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT) to duplicate the functionality of
[`PQexecParams`](libpq-exec.html#LIBPQ-PQEXECPARAMS), [`PQprepare`](libpq-
exec.html#LIBPQ-PQPREPARE), [`PQexecPrepared`](libpq-exec.html#LIBPQ-
PQEXECPREPARED), [`PQdescribePrepared`](libpq-exec.html#LIBPQ-
PQDESCRIBEPREPARED), and [`PQdescribePortal`](libpq-exec.html#LIBPQ-
PQDESCRIBEPORTAL) respectively.

`PQsendQuery` #

    

Submits a command to the server without waiting for the result(s). 1 is
returned if the command was successfully dispatched and 0 if not (in which
case, use [`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE) to get
more information about the failure).

    
    
    int PQsendQuery(PGconn *conn, const char *command);
    

After successfully calling [`PQsendQuery`](libpq-async.html#LIBPQ-
PQSENDQUERY), call [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) one or
more times to obtain the results. [`PQsendQuery`](libpq-async.html#LIBPQ-
PQSENDQUERY) cannot be called again (on the same connection) until
[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) has returned a null
pointer, indicating that the command is done.

In pipeline mode, this function is disallowed.

`PQsendQueryParams` #

    

Submits a command and separate parameters to the server without waiting for
the result(s).

    
    
    int PQsendQueryParams(PGconn *conn,
                          const char *command,
                          int nParams,
                          const Oid *paramTypes,
                          const char * const *paramValues,
                          const int *paramLengths,
                          const int *paramFormats,
                          int resultFormat);
    

This is equivalent to [`PQsendQuery`](libpq-async.html#LIBPQ-PQSENDQUERY)
except that query parameters can be specified separately from the query
string. The function's parameters are handled identically to
[`PQexecParams`](libpq-exec.html#LIBPQ-PQEXECPARAMS). Like
[`PQexecParams`](libpq-exec.html#LIBPQ-PQEXECPARAMS), it allows only one
command in the query string.

`PQsendPrepare` #

    

Sends a request to create a prepared statement with the given parameters,
without waiting for completion.

    
    
    int PQsendPrepare(PGconn *conn,
                      const char *stmtName,
                      const char *query,
                      int nParams,
                      const Oid *paramTypes);
    

This is an asynchronous version of [`PQprepare`](libpq-exec.html#LIBPQ-
PQPREPARE): it returns 1 if it was able to dispatch the request, and 0 if not.
After a successful call, call [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) to determine whether the server successfully created the prepared
statement. The function's parameters are handled identically to
[`PQprepare`](libpq-exec.html#LIBPQ-PQPREPARE).

`PQsendQueryPrepared` #

    

Sends a request to execute a prepared statement with given parameters, without
waiting for the result(s).

    
    
    int PQsendQueryPrepared(PGconn *conn,
                            const char *stmtName,
                            int nParams,
                            const char * const *paramValues,
                            const int *paramLengths,
                            const int *paramFormats,
                            int resultFormat);
    

This is similar to [`PQsendQueryParams`](libpq-async.html#LIBPQ-
PQSENDQUERYPARAMS), but the command to be executed is specified by naming a
previously-prepared statement, instead of giving a query string. The
function's parameters are handled identically to [`PQexecPrepared`](libpq-
exec.html#LIBPQ-PQEXECPREPARED).

`PQsendDescribePrepared` #

    

Submits a request to obtain information about the specified prepared
statement, without waiting for completion.

    
    
    int PQsendDescribePrepared(PGconn *conn, const char *stmtName);
    

This is an asynchronous version of [`PQdescribePrepared`](libpq-
exec.html#LIBPQ-PQDESCRIBEPREPARED): it returns 1 if it was able to dispatch
the request, and 0 if not. After a successful call, call
[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) to obtain the results. The
function's parameters are handled identically to [`PQdescribePrepared`](libpq-
exec.html#LIBPQ-PQDESCRIBEPREPARED).

`PQsendDescribePortal` #

    

Submits a request to obtain information about the specified portal, without
waiting for completion.

    
    
    int PQsendDescribePortal(PGconn *conn, const char *portalName);
    

This is an asynchronous version of [`PQdescribePortal`](libpq-exec.html#LIBPQ-
PQDESCRIBEPORTAL): it returns 1 if it was able to dispatch the request, and 0
if not. After a successful call, call [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) to obtain the results. The function's parameters are handled
identically to [`PQdescribePortal`](libpq-exec.html#LIBPQ-PQDESCRIBEPORTAL).

`PQgetResult` #

    

Waits for the next result from a prior [`PQsendQuery`](libpq-async.html#LIBPQ-
PQSENDQUERY), [`PQsendQueryParams`](libpq-async.html#LIBPQ-PQSENDQUERYPARAMS),
[`PQsendPrepare`](libpq-async.html#LIBPQ-PQSENDPREPARE),
[`PQsendQueryPrepared`](libpq-async.html#LIBPQ-PQSENDQUERYPREPARED),
[`PQsendDescribePrepared`](libpq-async.html#LIBPQ-PQSENDDESCRIBEPREPARED),
[`PQsendDescribePortal`](libpq-async.html#LIBPQ-PQSENDDESCRIBEPORTAL), or
[`PQpipelineSync`](libpq-pipeline-mode.html#LIBPQ-PQPIPELINESYNC) call, and
returns it. A null pointer is returned when the command is complete and there
will be no more results.

    
    
    PGresult *PQgetResult(PGconn *conn);
    

[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) must be called repeatedly
until it returns a null pointer, indicating that the command is done. (If
called when no command is active, [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) will just return a null pointer at once.) Each non-null result
from [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) should be processed
using the same `PGresult` accessor functions previously described. Don't
forget to free each result object with [`PQclear`](libpq-exec.html#LIBPQ-
PQCLEAR) when done with it. Note that [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) will block only if a command is active and the necessary response
data has not yet been read by [`PQconsumeInput`](libpq-async.html#LIBPQ-
PQCONSUMEINPUT) .

In pipeline mode, `PQgetResult` will return normally unless an error occurs;
for any subsequent query sent after the one that caused the error until (and
excluding) the next synchronization point, a special result of type
`PGRES_PIPELINE_ABORTED` will be returned, and a null pointer will be returned
after it. When the pipeline synchronization point is reached, a result of type
`PGRES_PIPELINE_SYNC` will be returned. The result of the next query after the
synchronization point follows immediately (that is, no null pointer is
returned after the synchronization point).

### Note

Even when [`PQresultStatus`](libpq-exec.html#LIBPQ-PQRESULTSTATUS) indicates a
fatal error, [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) should be
called until it returns a null pointer, to allow libpq to process the error
information completely.

Using [`PQsendQuery`](libpq-async.html#LIBPQ-PQSENDQUERY) and
[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) solves one of
[`PQexec`](libpq-exec.html#LIBPQ-PQEXEC)'s problems: If a command string
contains multiple SQL commands, the results of those commands can be obtained
individually. (This allows a simple form of overlapped processing, by the way:
the client can be handling the results of one command while the server is
still working on later queries in the same command string.)

Another frequently-desired feature that can be obtained with
[`PQsendQuery`](libpq-async.html#LIBPQ-PQSENDQUERY) and [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT) is retrieving large query results a row at a
time. This is discussed in [Section 34.6](libpq-single-row-mode.html
"34.6. Retrieving Query Results Row-by-Row").

By itself, calling [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) will
still cause the client to block until the server completes the next SQL
command. This can be avoided by proper use of two more functions:

`PQconsumeInput` #

    

If input is available from the server, consume it.

    
    
    int PQconsumeInput(PGconn *conn);
    

[`PQconsumeInput`](libpq-async.html#LIBPQ-PQCONSUMEINPUT) normally returns 1
indicating “no error”, but returns 0 if there was some kind of trouble (in
which case [`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE) can be
consulted). Note that the result does not say whether any input data was
actually collected. After calling [`PQconsumeInput`](libpq-async.html#LIBPQ-
PQCONSUMEINPUT) , the application can check [`PQisBusy`](libpq-
async.html#LIBPQ-PQISBUSY) and/or `PQnotifies` to see if their state has
changed.

[`PQconsumeInput`](libpq-async.html#LIBPQ-PQCONSUMEINPUT) can be called even
if the application is not prepared to deal with a result or notification just
yet. The function will read available data and save it in a buffer, thereby
causing a `select()` read-ready indication to go away. The application can
thus use [`PQconsumeInput`](libpq-async.html#LIBPQ-PQCONSUMEINPUT) to clear
the `select()` condition immediately, and then examine the results at leisure.

`PQisBusy` #

    

Returns 1 if a command is busy, that is, [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT) would block waiting for input. A 0 return
indicates that [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) can be
called with assurance of not blocking.

    
    
    int PQisBusy(PGconn *conn);
    

[`PQisBusy`](libpq-async.html#LIBPQ-PQISBUSY) will not itself attempt to read
data from the server; therefore [`PQconsumeInput`](libpq-async.html#LIBPQ-
PQCONSUMEINPUT) must be invoked first, or the busy state will never end.

A typical application using these functions will have a main loop that uses
`select()` or `poll()` to wait for all the conditions that it must respond to.
One of the conditions will be input available from the server, which in terms
of `select()` means readable data on the file descriptor identified by
[`PQsocket`](libpq-status.html#LIBPQ-PQSOCKET). When the main loop detects
input ready, it should call [`PQconsumeInput`](libpq-async.html#LIBPQ-
PQCONSUMEINPUT) to read the input. It can then call [`PQisBusy`](libpq-
async.html#LIBPQ-PQISBUSY), followed by [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT) if [`PQisBusy`](libpq-async.html#LIBPQ-PQISBUSY)
returns false (0). It can also call `PQnotifies` to detect `NOTIFY` messages
(see [Section 34.9](libpq-notify.html "34.9. Asynchronous Notification")).

A client that uses [`PQsendQuery`](libpq-async.html#LIBPQ-
PQSENDQUERY)/[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) can also
attempt to cancel a command that is still being processed by the server; see
[Section 34.7](libpq-cancel.html "34.7. Canceling Queries in Progress"). But
regardless of the return value of [`PQcancel`](libpq-cancel.html#LIBPQ-
PQCANCEL), the application must continue with the normal result-reading
sequence using [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT). A
successful cancellation will simply cause the command to terminate sooner than
it would have otherwise.

By using the functions described above, it is possible to avoid blocking while
waiting for input from the database server. However, it is still possible that
the application will block waiting to send output to the server. This is
relatively uncommon but can happen if very long SQL commands or data values
are sent. (It is much more probable if the application sends data via `COPY
IN`, however.) To prevent this possibility and achieve completely nonblocking
database operation, the following additional functions can be used.

`PQsetnonblocking` #

    

Sets the nonblocking status of the connection.

    
    
    int PQsetnonblocking(PGconn *conn, int arg);
    

Sets the state of the connection to nonblocking if _`arg`_ is 1, or blocking
if _`arg`_ is 0. Returns 0 if OK, -1 if error.

In the nonblocking state, successful calls to [`PQsendQuery`](libpq-
async.html#LIBPQ-PQSENDQUERY), [`PQputline`](libpq-copy.html#LIBPQ-PQPUTLINE),
[`PQputnbytes`](libpq-copy.html#LIBPQ-PQPUTNBYTES), [`PQputCopyData`](libpq-
copy.html#LIBPQ-PQPUTCOPYDATA), and [`PQendcopy`](libpq-copy.html#LIBPQ-
PQENDCOPY) will not block; their changes are stored in the local output buffer
until they are flushed. Unsuccessful calls will return an error and must be
retried.

Note that [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) does not honor nonblocking
mode; if it is called, it will act in blocking fashion anyway.

`PQisnonblocking` #

    

Returns the blocking status of the database connection.

    
    
    int PQisnonblocking(const PGconn *conn);
    

Returns 1 if the connection is set to nonblocking mode and 0 if blocking.

`PQflush` #

    

Attempts to flush any queued output data to the server. Returns 0 if
successful (or if the send queue is empty), -1 if it failed for some reason,
or 1 if it was unable to send all the data in the send queue yet (this case
can only occur if the connection is nonblocking).

    
    
    int PQflush(PGconn *conn);
    

After sending any command or data on a nonblocking connection, call
[`PQflush`](libpq-async.html#LIBPQ-PQFLUSH). If it returns 1, wait for the
socket to become read- or write-ready. If it becomes write-ready, call
[`PQflush`](libpq-async.html#LIBPQ-PQFLUSH) again. If it becomes read-ready,
call [`PQconsumeInput`](libpq-async.html#LIBPQ-PQCONSUMEINPUT) , then call
[`PQflush`](libpq-async.html#LIBPQ-PQFLUSH) again. Repeat until
[`PQflush`](libpq-async.html#LIBPQ-PQFLUSH) returns 0. (It is necessary to
check for read-ready and drain the input with [`PQconsumeInput`](libpq-
async.html#LIBPQ-PQCONSUMEINPUT) , because the server can block trying to send
us data, e.g., NOTICE messages, and won't read our data until we read its.)
Once [`PQflush`](libpq-async.html#LIBPQ-PQFLUSH) returns 0, wait for the
socket to be read-ready and then read the response as described above.

* * *

[Prev](libpq-exec.html "34.3. Command Execution Functions")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-pipeline-mode.html "34.5. Pipeline Mode")  
---|---|---  
34.3. Command Execution Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.5. Pipeline Mode  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-async.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

