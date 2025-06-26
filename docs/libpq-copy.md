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

Supported Versions: [Current](/docs/current/libpq-copy.html "PostgreSQL 17 -
34.10. Functions Associated with the COPY Command") ([17](/docs/17/libpq-
copy.html "PostgreSQL 17 - 34.10. Functions Associated with the COPY
Command")) / [16](/docs/16/libpq-copy.html "PostgreSQL 16 - 34.10. Functions
Associated with the COPY Command") / [15](/docs/15/libpq-copy.html "PostgreSQL
15 - 34.10. Functions Associated with the COPY Command") /
[14](/docs/14/libpq-copy.html "PostgreSQL 14 - 34.10. Functions Associated
with the COPY Command") / [13](/docs/13/libpq-copy.html "PostgreSQL 13 -
34.10. Functions Associated with the COPY Command")

Development Versions: [18](/docs/18/libpq-copy.html "PostgreSQL 18 -
34.10. Functions Associated with the COPY Command") /
[devel](/docs/devel/libpq-copy.html "PostgreSQL devel - 34.10. Functions
Associated with the COPY Command")

Unsupported versions: [12](/docs/12/libpq-copy.html "PostgreSQL 12 -
34.10. Functions Associated with the COPY Command") / [11](/docs/11/libpq-
copy.html "PostgreSQL 11 - 34.10. Functions Associated with the COPY Command")
/ [10](/docs/10/libpq-copy.html "PostgreSQL 10 - 34.10. Functions Associated
with the COPY Command") / [9.6](/docs/9.6/libpq-copy.html "PostgreSQL 9.6 -
34.10. Functions Associated with the COPY Command") / [9.5](/docs/9.5/libpq-
copy.html "PostgreSQL 9.5 - 34.10. Functions Associated with the COPY
Command") / [9.4](/docs/9.4/libpq-copy.html "PostgreSQL 9.4 - 34.10. Functions
Associated with the COPY Command") / [9.3](/docs/9.3/libpq-copy.html
"PostgreSQL 9.3 - 34.10. Functions Associated with the COPY Command") /
[9.2](/docs/9.2/libpq-copy.html "PostgreSQL 9.2 - 34.10. Functions Associated
with the COPY Command") / [9.1](/docs/9.1/libpq-copy.html "PostgreSQL 9.1 -
34.10. Functions Associated with the COPY Command") / [9.0](/docs/9.0/libpq-
copy.html "PostgreSQL 9.0 - 34.10. Functions Associated with the COPY
Command") / [8.4](/docs/8.4/libpq-copy.html "PostgreSQL 8.4 - 34.10. Functions
Associated with the COPY Command") / [8.3](/docs/8.3/libpq-copy.html
"PostgreSQL 8.3 - 34.10. Functions Associated with the COPY Command") /
[8.2](/docs/8.2/libpq-copy.html "PostgreSQL 8.2 - 34.10. Functions Associated
with the COPY Command") / [8.1](/docs/8.1/libpq-copy.html "PostgreSQL 8.1 -
34.10. Functions Associated with the COPY Command") / [8.0](/docs/8.0/libpq-
copy.html "PostgreSQL 8.0 - 34.10. Functions Associated with the COPY
Command") / [7.4](/docs/7.4/libpq-copy.html "PostgreSQL 7.4 - 34.10. Functions
Associated with the COPY Command") / [7.3](/docs/7.3/libpq-copy.html
"PostgreSQL 7.3 - 34.10. Functions Associated with the COPY Command") /
[7.2](/docs/7.2/libpq-copy.html "PostgreSQL 7.2 - 34.10. Functions Associated
with the COPY Command") / [7.1](/docs/7.1/libpq-copy.html "PostgreSQL 7.1 -
34.10. Functions Associated with the COPY Command")

__

34.10. Functions Associated with the `COPY` Command  
---  
[Prev](libpq-notify.html "34.9. Asynchronous Notification")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-control.html "34.11. Control Functions")  
  
* * *

## 34.10. Functions Associated with the `COPY` Command #

[34.10.1. Functions for Sending `COPY` Data](libpq-copy.html#LIBPQ-COPY-SEND)

[34.10.2. Functions for Receiving `COPY` Data](libpq-copy.html#LIBPQ-COPY-
RECEIVE)

[34.10.3. Obsolete Functions for `COPY`](libpq-copy.html#LIBPQ-COPY-
DEPRECATED)

The `COPY` command in PostgreSQL has options to read from or write to the
network connection used by libpq. The functions described in this section
allow applications to take advantage of this capability by supplying or
consuming copied data.

The overall process is that the application first issues the SQL `COPY`
command via [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) or one of the equivalent
functions. The response to this (if there is no error in the command) will be
a `PGresult` object bearing a status code of `PGRES_COPY_OUT` or
`PGRES_COPY_IN` (depending on the specified copy direction). The application
should then use the functions of this section to receive or transmit data
rows. When the data transfer is complete, another `PGresult` object is
returned to indicate success or failure of the transfer. Its status will be
`PGRES_COMMAND_OK` for success or `PGRES_FATAL_ERROR` if some problem was
encountered. At this point further SQL commands can be issued via
[`PQexec`](libpq-exec.html#LIBPQ-PQEXEC). (It is not possible to execute other
SQL commands using the same connection while the `COPY` operation is in
progress.)

If a `COPY` command is issued via [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) in
a string that could contain additional commands, the application must continue
fetching results via [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) after
completing the `COPY` sequence. Only when [`PQgetResult`](libpq-
async.html#LIBPQ-PQGETRESULT) returns `NULL` is it certain that the
[`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) command string is done and it is safe
to issue more commands.

The functions of this section should be executed only after obtaining a result
status of `PGRES_COPY_OUT` or `PGRES_COPY_IN` from [`PQexec`](libpq-
exec.html#LIBPQ-PQEXEC) or [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT).

A `PGresult` object bearing one of these status values carries some additional
data about the `COPY` operation that is starting. This additional data is
available using functions that are also used in connection with query results:

`PQnfields` #

    

Returns the number of columns (fields) to be copied.

`PQbinaryTuples` #

    

0 indicates the overall copy format is textual (rows separated by newlines,
columns separated by separator characters, etc.). 1 indicates the overall copy
format is binary. See [COPY](sql-copy.html "COPY") for more information.

`PQfformat` #

    

Returns the format code (0 for text, 1 for binary) associated with each column
of the copy operation. The per-column format codes will always be zero when
the overall copy format is textual, but the binary format can support both
text and binary columns. (However, as of the current implementation of `COPY`,
only binary columns appear in a binary copy; so the per-column formats always
match the overall format at present.)

### 34.10.1. Functions for Sending `COPY` Data #

These functions are used to send data during `COPY FROM STDIN`. They will fail
if called when the connection is not in `COPY_IN` state.

`PQputCopyData` #

    

Sends data to the server during `COPY_IN` state.

    
    
    int PQputCopyData(PGconn *conn,
                      const char *buffer,
                      int nbytes);
    

Transmits the `COPY` data in the specified _`buffer`_ , of length _`nbytes`_ ,
to the server. The result is 1 if the data was queued, zero if it was not
queued because of full buffers (this will only happen in nonblocking mode), or
-1 if an error occurred. (Use [`PQerrorMessage`](libpq-status.html#LIBPQ-
PQERRORMESSAGE) to retrieve details if the return value is -1. If the value is
zero, wait for write-ready and try again.)

The application can divide the `COPY` data stream into buffer loads of any
convenient size. Buffer-load boundaries have no semantic significance when
sending. The contents of the data stream must match the data format expected
by the `COPY` command; see [COPY](sql-copy.html "COPY") for details.

`PQputCopyEnd` #

    

Sends end-of-data indication to the server during `COPY_IN` state.

    
    
    int PQputCopyEnd(PGconn *conn,
                     const char *errormsg);
    

Ends the `COPY_IN` operation successfully if _`errormsg`_ is `NULL`. If
_`errormsg`_ is not `NULL` then the `COPY` is forced to fail, with the string
pointed to by _`errormsg`_ used as the error message. (One should not assume
that this exact error message will come back from the server, however, as the
server might have already failed the `COPY` for its own reasons.)

The result is 1 if the termination message was sent; or in nonblocking mode,
this may only indicate that the termination message was successfully queued.
(In nonblocking mode, to be certain that the data has been sent, you should
next wait for write-ready and call [`PQflush`](libpq-async.html#LIBPQ-
PQFLUSH), repeating until it returns zero.) Zero indicates that the function
could not queue the termination message because of full buffers; this will
only happen in nonblocking mode. (In this case, wait for write-ready and try
the [`PQputCopyEnd`](libpq-copy.html#LIBPQ-PQPUTCOPYEND) call again.) If a
hard error occurs, -1 is returned; you can use [`PQerrorMessage`](libpq-
status.html#LIBPQ-PQERRORMESSAGE) to retrieve details.

After successfully calling [`PQputCopyEnd`](libpq-copy.html#LIBPQ-
PQPUTCOPYEND), call [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) to
obtain the final result status of the `COPY` command. One can wait for this
result to be available in the usual way. Then return to normal operation.

### 34.10.2. Functions for Receiving `COPY` Data #

These functions are used to receive data during `COPY TO STDOUT`. They will
fail if called when the connection is not in `COPY_OUT` state.

`PQgetCopyData` #

    

Receives data from the server during `COPY_OUT` state.

    
    
    int PQgetCopyData(PGconn *conn,
                      char **buffer,
                      int async);
    

Attempts to obtain another row of data from the server during a `COPY`. Data
is always returned one data row at a time; if only a partial row is available,
it is not returned. Successful return of a data row involves allocating a
chunk of memory to hold the data. The _`buffer`_ parameter must be non-`NULL`.
_`*buffer`_ is set to point to the allocated memory, or to `NULL` in cases
where no buffer is returned. A non-`NULL` result buffer should be freed using
[`PQfreemem`](libpq-misc.html#LIBPQ-PQFREEMEM) when no longer needed.

When a row is successfully returned, the return value is the number of data
bytes in the row (this will always be greater than zero). The returned string
is always null-terminated, though this is probably only useful for textual
`COPY`. A result of zero indicates that the `COPY` is still in progress, but
no row is yet available (this is only possible when _`async`_ is true). A
result of -1 indicates that the `COPY` is done. A result of -2 indicates that
an error occurred (consult [`PQerrorMessage`](libpq-status.html#LIBPQ-
PQERRORMESSAGE) for the reason).

When _`async`_ is true (not zero), [`PQgetCopyData`](libpq-copy.html#LIBPQ-
PQGETCOPYDATA) will not block waiting for input; it will return zero if the
`COPY` is still in progress but no complete row is available. (In this case
wait for read-ready and then call [`PQconsumeInput`](libpq-async.html#LIBPQ-
PQCONSUMEINPUT) before calling [`PQgetCopyData`](libpq-copy.html#LIBPQ-
PQGETCOPYDATA) again.) When _`async`_ is false (zero),
[`PQgetCopyData`](libpq-copy.html#LIBPQ-PQGETCOPYDATA) will block until data
is available or the operation completes.

After [`PQgetCopyData`](libpq-copy.html#LIBPQ-PQGETCOPYDATA) returns -1, call
[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) to obtain the final result
status of the `COPY` command. One can wait for this result to be available in
the usual way. Then return to normal operation.

### 34.10.3. Obsolete Functions for `COPY` #

These functions represent older methods of handling `COPY`. Although they
still work, they are deprecated due to poor error handling, inconvenient
methods of detecting end-of-data, and lack of support for binary or
nonblocking transfers.

`PQgetline` #

    

Reads a newline-terminated line of characters (transmitted by the server) into
a buffer string of size _`length`_.

    
    
    int PQgetline(PGconn *conn,
                  char *buffer,
                  int length);
    

This function copies up to _`length`_ -1 characters into the buffer and
converts the terminating newline into a zero byte. [`PQgetline`](libpq-
copy.html#LIBPQ-PQGETLINE) returns `EOF` at the end of input, 0 if the entire
line has been read, and 1 if the buffer is full but the terminating newline
has not yet been read.

Note that the application must check to see if a new line consists of the two
characters `\.`, which indicates that the server has finished sending the
results of the `COPY` command. If the application might receive lines that are
more than _`length`_ -1 characters long, care is needed to be sure it
recognizes the `\.` line correctly (and does not, for example, mistake the end
of a long data line for a terminator line).

`PQgetlineAsync` #

    

Reads a row of `COPY` data (transmitted by the server) into a buffer without
blocking.

    
    
    int PQgetlineAsync(PGconn *conn,
                       char *buffer,
                       int bufsize);
    

This function is similar to [`PQgetline`](libpq-copy.html#LIBPQ-PQGETLINE),
but it can be used by applications that must read `COPY` data asynchronously,
that is, without blocking. Having issued the `COPY` command and gotten a
`PGRES_COPY_OUT` response, the application should call
[`PQconsumeInput`](libpq-async.html#LIBPQ-PQCONSUMEINPUT) and
[`PQgetlineAsync`](libpq-copy.html#LIBPQ-PQGETLINEASYNC) until the end-of-data
signal is detected.

Unlike [`PQgetline`](libpq-copy.html#LIBPQ-PQGETLINE), this function takes
responsibility for detecting end-of-data.

On each call, [`PQgetlineAsync`](libpq-copy.html#LIBPQ-PQGETLINEASYNC) will
return data if a complete data row is available in libpq's input buffer.
Otherwise, no data is returned until the rest of the row arrives. The function
returns -1 if the end-of-copy-data marker has been recognized, or 0 if no data
is available, or a positive number giving the number of bytes of data
returned. If -1 is returned, the caller must next call [`PQendcopy`](libpq-
copy.html#LIBPQ-PQENDCOPY), and then return to normal processing.

The data returned will not extend beyond a data-row boundary. If possible a
whole row will be returned at one time. But if the buffer offered by the
caller is too small to hold a row sent by the server, then a partial data row
will be returned. With textual data this can be detected by testing whether
the last returned byte is `\n` or not. (In a binary `COPY`, actual parsing of
the `COPY` data format will be needed to make the equivalent determination.)
The returned string is not null-terminated. (If you want to add a terminating
null, be sure to pass a _`bufsize`_ one smaller than the room actually
available.)

`PQputline` #

    

Sends a null-terminated string to the server. Returns 0 if OK and `EOF` if
unable to send the string.

    
    
    int PQputline(PGconn *conn,
                  const char *string);
    

The `COPY` data stream sent by a series of calls to [`PQputline`](libpq-
copy.html#LIBPQ-PQPUTLINE) has the same format as that returned by
[`PQgetlineAsync`](libpq-copy.html#LIBPQ-PQGETLINEASYNC), except that
applications are not obliged to send exactly one data row per
[`PQputline`](libpq-copy.html#LIBPQ-PQPUTLINE) call; it is okay to send a
partial line or multiple lines per call.

### Note

Before PostgreSQL protocol 3.0, it was necessary for the application to
explicitly send the two characters `\.` as a final line to indicate to the
server that it had finished sending `COPY` data. While this still works, it is
deprecated and the special meaning of `\.` can be expected to be removed in a
future release. It is sufficient to call [`PQendcopy`](libpq-copy.html#LIBPQ-
PQENDCOPY) after having sent the actual data.

`PQputnbytes` #

    

Sends a non-null-terminated string to the server. Returns 0 if OK and `EOF` if
unable to send the string.

    
    
    int PQputnbytes(PGconn *conn,
                    const char *buffer,
                    int nbytes);
    

This is exactly like [`PQputline`](libpq-copy.html#LIBPQ-PQPUTLINE), except
that the data buffer need not be null-terminated since the number of bytes to
send is specified directly. Use this procedure when sending binary data.

`PQendcopy` #

    

Synchronizes with the server.

    
    
    int PQendcopy(PGconn *conn);
    

This function waits until the server has finished the copying. It should
either be issued when the last string has been sent to the server using
[`PQputline`](libpq-copy.html#LIBPQ-PQPUTLINE) or when the last string has
been received from the server using `PQgetline`. It must be issued or the
server will get “out of sync” with the client. Upon return from this function,
the server is ready to receive the next SQL command. The return value is 0 on
successful completion, nonzero otherwise. (Use [`PQerrorMessage`](libpq-
status.html#LIBPQ-PQERRORMESSAGE) to retrieve details if the return value is
nonzero.)

When using [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT), the
application should respond to a `PGRES_COPY_OUT` result by executing
[`PQgetline`](libpq-copy.html#LIBPQ-PQGETLINE) repeatedly, followed by
[`PQendcopy`](libpq-copy.html#LIBPQ-PQENDCOPY) after the terminator line is
seen. It should then return to the [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT) loop until [`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT)
returns a null pointer. Similarly a `PGRES_COPY_IN` result is processed by a
series of [`PQputline`](libpq-copy.html#LIBPQ-PQPUTLINE) calls followed by
[`PQendcopy`](libpq-copy.html#LIBPQ-PQENDCOPY), then return to the
[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) loop. This arrangement
will ensure that a `COPY` command embedded in a series of SQL commands will be
executed correctly.

Older applications are likely to submit a `COPY` via [`PQexec`](libpq-
exec.html#LIBPQ-PQEXEC) and assume that the transaction is done after
[`PQendcopy`](libpq-copy.html#LIBPQ-PQENDCOPY). This will work correctly only
if the `COPY` is the only SQL command in the command string.

* * *

[Prev](libpq-notify.html "34.9. Asynchronous Notification")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-control.html "34.11. Control Functions")  
---|---|---  
34.9. Asynchronous Notification  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.11. Control Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-copy.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

