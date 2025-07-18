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

Supported Versions: [Current](/docs/current/libpq-exec.html "PostgreSQL 17 -
34.3. Command Execution Functions") ([17](/docs/17/libpq-exec.html "PostgreSQL
17 - 34.3. Command Execution Functions")) / [16](/docs/16/libpq-exec.html
"PostgreSQL 16 - 34.3. Command Execution Functions") / [15](/docs/15/libpq-
exec.html "PostgreSQL 15 - 34.3. Command Execution Functions") /
[14](/docs/14/libpq-exec.html "PostgreSQL 14 - 34.3. Command Execution
Functions") / [13](/docs/13/libpq-exec.html "PostgreSQL 13 - 34.3. Command
Execution Functions")

Development Versions: [18](/docs/18/libpq-exec.html "PostgreSQL 18 -
34.3. Command Execution Functions") / [devel](/docs/devel/libpq-exec.html
"PostgreSQL devel - 34.3. Command Execution Functions")

Unsupported versions: [12](/docs/12/libpq-exec.html "PostgreSQL 12 -
34.3. Command Execution Functions") / [11](/docs/11/libpq-exec.html
"PostgreSQL 11 - 34.3. Command Execution Functions") / [10](/docs/10/libpq-
exec.html "PostgreSQL 10 - 34.3. Command Execution Functions") /
[9.6](/docs/9.6/libpq-exec.html "PostgreSQL 9.6 - 34.3. Command Execution
Functions") / [9.5](/docs/9.5/libpq-exec.html "PostgreSQL 9.5 - 34.3. Command
Execution Functions") / [9.4](/docs/9.4/libpq-exec.html "PostgreSQL 9.4 -
34.3. Command Execution Functions") / [9.3](/docs/9.3/libpq-exec.html
"PostgreSQL 9.3 - 34.3. Command Execution Functions") / [9.2](/docs/9.2/libpq-
exec.html "PostgreSQL 9.2 - 34.3. Command Execution Functions") /
[9.1](/docs/9.1/libpq-exec.html "PostgreSQL 9.1 - 34.3. Command Execution
Functions") / [9.0](/docs/9.0/libpq-exec.html "PostgreSQL 9.0 - 34.3. Command
Execution Functions") / [8.4](/docs/8.4/libpq-exec.html "PostgreSQL 8.4 -
34.3. Command Execution Functions") / [8.3](/docs/8.3/libpq-exec.html
"PostgreSQL 8.3 - 34.3. Command Execution Functions") / [8.2](/docs/8.2/libpq-
exec.html "PostgreSQL 8.2 - 34.3. Command Execution Functions") /
[8.1](/docs/8.1/libpq-exec.html "PostgreSQL 8.1 - 34.3. Command Execution
Functions") / [8.0](/docs/8.0/libpq-exec.html "PostgreSQL 8.0 - 34.3. Command
Execution Functions") / [7.4](/docs/7.4/libpq-exec.html "PostgreSQL 7.4 -
34.3. Command Execution Functions") / [7.3](/docs/7.3/libpq-exec.html
"PostgreSQL 7.3 - 34.3. Command Execution Functions") / [7.2](/docs/7.2/libpq-
exec.html "PostgreSQL 7.2 - 34.3. Command Execution Functions") /
[7.1](/docs/7.1/libpq-exec.html "PostgreSQL 7.1 - 34.3. Command Execution
Functions")

__

34.3. Command Execution Functions  
---  
[Prev](libpq-status.html "34.2. Connection Status Functions")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-async.html "34.4. Asynchronous Command Processing")  
  
* * *

## 34.3. Command Execution Functions #

[34.3.1. Main Functions](libpq-exec.html#LIBPQ-EXEC-MAIN)

[34.3.2. Retrieving Query Result Information](libpq-exec.html#LIBPQ-EXEC-
SELECT-INFO)

[34.3.3. Retrieving Other Result Information](libpq-exec.html#LIBPQ-EXEC-
NONSELECT)

[34.3.4. Escaping Strings for Inclusion in SQL Commands](libpq-
exec.html#LIBPQ-EXEC-ESCAPE-STRING)

Once a connection to a database server has been successfully established, the
functions described here are used to perform SQL queries and commands.

### 34.3.1. Main Functions #

`PQexec` #

    

Submits a command to the server and waits for the result.

    
    
    PGresult *PQexec(PGconn *conn, const char *command);
    

Returns a `PGresult` pointer or possibly a null pointer. A non-null pointer
will generally be returned except in out-of-memory conditions or serious
errors such as inability to send the command to the server. The
[`PQresultStatus`](libpq-exec.html#LIBPQ-PQRESULTSTATUS) function should be
called to check the return value for any errors (including the value of a null
pointer, in which case it will return `PGRES_FATAL_ERROR`). Use
[`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE) to get more
information about such errors.

The command string can include multiple SQL commands (separated by
semicolons). Multiple queries sent in a single [`PQexec`](libpq-
exec.html#LIBPQ-PQEXEC) call are processed in a single transaction, unless
there are explicit `BEGIN`/`COMMIT` commands included in the query string to
divide it into multiple transactions. (See [Section 55.2.2.1](protocol-
flow.html#PROTOCOL-FLOW-MULTI-STATEMENT "55.2.2.1. Multiple Statements in a
Simple Query") for more details about how the server handles multi-query
strings.) Note however that the returned `PGresult` structure describes only
the result of the last command executed from the string. Should one of the
commands fail, processing of the string stops with it and the returned
`PGresult` describes the error condition.

`PQexecParams` #

    

Submits a command to the server and waits for the result, with the ability to
pass parameters separately from the SQL command text.

    
    
    PGresult *PQexecParams(PGconn *conn,
                           const char *command,
                           int nParams,
                           const Oid *paramTypes,
                           const char * const *paramValues,
                           const int *paramLengths,
                           const int *paramFormats,
                           int resultFormat);
    

[`PQexecParams`](libpq-exec.html#LIBPQ-PQEXECPARAMS) is like [`PQexec`](libpq-
exec.html#LIBPQ-PQEXEC), but offers additional functionality: parameter values
can be specified separately from the command string proper, and query results
can be requested in either text or binary format.

The function arguments are:

_`conn`_

    

The connection object to send the command through.

_`command`_

    

The SQL command string to be executed. If parameters are used, they are
referred to in the command string as `$1`, `$2`, etc.

_`nParams`_

    

The number of parameters supplied; it is the length of the arrays
_`paramTypes[]`_ , _`paramValues[]`_ , _`paramLengths[]`_ , and
_`paramFormats[]`_. (The array pointers can be `NULL` when _`nParams`_ is
zero.)

_`paramTypes[]`_

    

Specifies, by OID, the data types to be assigned to the parameter symbols. If
_`paramTypes`_ is `NULL`, or any particular element in the array is zero, the
server infers a data type for the parameter symbol in the same way it would do
for an untyped literal string.

_`paramValues[]`_

    

Specifies the actual values of the parameters. A null pointer in this array
means the corresponding parameter is null; otherwise the pointer points to a
zero-terminated text string (for text format) or binary data in the format
expected by the server (for binary format).

_`paramLengths[]`_

    

Specifies the actual data lengths of binary-format parameters. It is ignored
for null parameters and text-format parameters. The array pointer can be null
when there are no binary parameters.

_`paramFormats[]`_

    

Specifies whether parameters are text (put a zero in the array entry for the
corresponding parameter) or binary (put a one in the array entry for the
corresponding parameter). If the array pointer is null then all parameters are
presumed to be text strings.

Values passed in binary format require knowledge of the internal
representation expected by the backend. For example, integers must be passed
in network byte order. Passing `numeric` values requires knowledge of the
server storage format, as implemented in
`src/backend/utils/adt/numeric.c::numeric_send()` and
`src/backend/utils/adt/numeric.c::numeric_recv()`.

_`resultFormat`_

    

Specify zero to obtain results in text format, or one to obtain results in
binary format. (There is not currently a provision to obtain different result
columns in different formats, although that is possible in the underlying
protocol.)

The primary advantage of [`PQexecParams`](libpq-exec.html#LIBPQ-PQEXECPARAMS)
over [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) is that parameter values can be
separated from the command string, thus avoiding the need for tedious and
error-prone quoting and escaping.

Unlike [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC), [`PQexecParams`](libpq-
exec.html#LIBPQ-PQEXECPARAMS) allows at most one SQL command in the given
string. (There can be semicolons in it, but not more than one nonempty
command.) This is a limitation of the underlying protocol, but has some
usefulness as an extra defense against SQL-injection attacks.

### Tip

Specifying parameter types via OIDs is tedious, particularly if you prefer not
to hard-wire particular OID values into your program. However, you can avoid
doing so even in cases where the server by itself cannot determine the type of
the parameter, or chooses a different type than you want. In the SQL command
text, attach an explicit cast to the parameter symbol to show what data type
you will send. For example:

    
    
    SELECT * FROM mytable WHERE x = $1::bigint;
    

This forces parameter `$1` to be treated as `bigint`, whereas by default it
would be assigned the same type as `x`. Forcing the parameter type decision,
either this way or by specifying a numeric type OID, is strongly recommended
when sending parameter values in binary format, because binary format has less
redundancy than text format and so there is less chance that the server will
detect a type mismatch mistake for you.

`PQprepare` #

    

Submits a request to create a prepared statement with the given parameters,
and waits for completion.

    
    
    PGresult *PQprepare(PGconn *conn,
                        const char *stmtName,
                        const char *query,
                        int nParams,
                        const Oid *paramTypes);
    

[`PQprepare`](libpq-exec.html#LIBPQ-PQPREPARE) creates a prepared statement
for later execution with [`PQexecPrepared`](libpq-exec.html#LIBPQ-
PQEXECPREPARED). This feature allows commands to be executed repeatedly
without being parsed and planned each time; see [PREPARE](sql-prepare.html
"PREPARE") for details.

The function creates a prepared statement named _`stmtName`_ from the
_`query`_ string, which must contain a single SQL command. _`stmtName`_ can be
`""` to create an unnamed statement, in which case any pre-existing unnamed
statement is automatically replaced; otherwise it is an error if the statement
name is already defined in the current session. If any parameters are used,
they are referred to in the query as `$1`, `$2`, etc. _`nParams`_ is the
number of parameters for which types are pre-specified in the array
_`paramTypes[]`_. (The array pointer can be `NULL` when _`nParams`_ is zero.)
_`paramTypes[]`_ specifies, by OID, the data types to be assigned to the
parameter symbols. If _`paramTypes`_ is `NULL`, or any particular element in
the array is zero, the server assigns a data type to the parameter symbol in
the same way it would do for an untyped literal string. Also, the query can
use parameter symbols with numbers higher than _`nParams`_ ; data types will
be inferred for these symbols as well. (See [`PQdescribePrepared`](libpq-
exec.html#LIBPQ-PQDESCRIBEPREPARED) for a means to find out what data types
were inferred.)

As with [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC), the result is normally a
`PGresult` object whose contents indicate server-side success or failure. A
null result indicates out-of-memory or inability to send the command at all.
Use [`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE) to get more
information about such errors.

Prepared statements for use with [`PQexecPrepared`](libpq-exec.html#LIBPQ-
PQEXECPREPARED) can also be created by executing SQL [PREPARE](sql-
prepare.html "PREPARE") statements. Also, although there is no libpq function
for deleting a prepared statement, the SQL [DEALLOCATE](sql-deallocate.html
"DEALLOCATE") statement can be used for that purpose.

`PQexecPrepared` #

    

Sends a request to execute a prepared statement with given parameters, and
waits for the result.

    
    
    PGresult *PQexecPrepared(PGconn *conn,
                             const char *stmtName,
                             int nParams,
                             const char * const *paramValues,
                             const int *paramLengths,
                             const int *paramFormats,
                             int resultFormat);
    

[`PQexecPrepared`](libpq-exec.html#LIBPQ-PQEXECPREPARED) is like
[`PQexecParams`](libpq-exec.html#LIBPQ-PQEXECPARAMS), but the command to be
executed is specified by naming a previously-prepared statement, instead of
giving a query string. This feature allows commands that will be used
repeatedly to be parsed and planned just once, rather than each time they are
executed. The statement must have been prepared previously in the current
session.

The parameters are identical to [`PQexecParams`](libpq-exec.html#LIBPQ-
PQEXECPARAMS), except that the name of a prepared statement is given instead
of a query string, and the _`paramTypes[]`_ parameter is not present (it is
not needed since the prepared statement's parameter types were determined when
it was created).

`PQdescribePrepared` #

    

Submits a request to obtain information about the specified prepared
statement, and waits for completion.

    
    
    PGresult *PQdescribePrepared(PGconn *conn, const char *stmtName);
    

[`PQdescribePrepared`](libpq-exec.html#LIBPQ-PQDESCRIBEPREPARED) allows an
application to obtain information about a previously prepared statement.

_`stmtName`_ can be `""` or `NULL` to reference the unnamed statement,
otherwise it must be the name of an existing prepared statement. On success, a
`PGresult` with status `PGRES_COMMAND_OK` is returned. The functions
[`PQnparams`](libpq-exec.html#LIBPQ-PQNPARAMS) and [`PQparamtype`](libpq-
exec.html#LIBPQ-PQPARAMTYPE) can be applied to this `PGresult` to obtain
information about the parameters of the prepared statement, and the functions
[`PQnfields`](libpq-exec.html#LIBPQ-PQNFIELDS), [`PQfname`](libpq-
exec.html#LIBPQ-PQFNAME), [`PQftype`](libpq-exec.html#LIBPQ-PQFTYPE), etc.
provide information about the result columns (if any) of the statement.

`PQdescribePortal` #

    

Submits a request to obtain information about the specified portal, and waits
for completion.

    
    
    PGresult *PQdescribePortal(PGconn *conn, const char *portalName);
    

[`PQdescribePortal`](libpq-exec.html#LIBPQ-PQDESCRIBEPORTAL) allows an
application to obtain information about a previously created portal. (libpq
does not provide any direct access to portals, but you can use this function
to inspect the properties of a cursor created with a `DECLARE CURSOR` SQL
command.)

_`portalName`_ can be `""` or `NULL` to reference the unnamed portal,
otherwise it must be the name of an existing portal. On success, a `PGresult`
with status `PGRES_COMMAND_OK` is returned. The functions [`PQnfields`](libpq-
exec.html#LIBPQ-PQNFIELDS), [`PQfname`](libpq-exec.html#LIBPQ-PQFNAME),
[`PQftype`](libpq-exec.html#LIBPQ-PQFTYPE), etc. can be applied to the
`PGresult` to obtain information about the result columns (if any) of the
portal.

The `PGresult` structure encapsulates the result returned by the server. libpq
application programmers should be careful to maintain the `PGresult`
abstraction. Use the accessor functions below to get at the contents of
`PGresult`. Avoid directly referencing the fields of the `PGresult` structure
because they are subject to change in the future.

`PQresultStatus` #

    

Returns the result status of the command.

    
    
    ExecStatusType PQresultStatus(const PGresult *res);
    

[`PQresultStatus`](libpq-exec.html#LIBPQ-PQRESULTSTATUS) can return one of the
following values:

`PGRES_EMPTY_QUERY` #

    

The string sent to the server was empty.

`PGRES_COMMAND_OK` #

    

Successful completion of a command returning no data.

`PGRES_TUPLES_OK` #

    

Successful completion of a command returning data (such as a `SELECT` or
`SHOW`).

`PGRES_COPY_OUT` #

    

Copy Out (from server) data transfer started.

`PGRES_COPY_IN` #

    

Copy In (to server) data transfer started.

`PGRES_BAD_RESPONSE` #

    

The server's response was not understood.

`PGRES_NONFATAL_ERROR` #

    

A nonfatal error (a notice or warning) occurred.

`PGRES_FATAL_ERROR` #

    

A fatal error occurred.

`PGRES_COPY_BOTH` #

    

Copy In/Out (to and from server) data transfer started. This feature is
currently used only for streaming replication, so this status should not occur
in ordinary applications.

`PGRES_SINGLE_TUPLE` #

    

The `PGresult` contains a single result tuple from the current command. This
status occurs only when single-row mode has been selected for the query (see
[Section 34.6](libpq-single-row-mode.html "34.6. Retrieving Query Results Row-
by-Row")).

`PGRES_PIPELINE_SYNC` #

    

The `PGresult` represents a synchronization point in pipeline mode, requested
by [`PQpipelineSync`](libpq-pipeline-mode.html#LIBPQ-PQPIPELINESYNC). This
status occurs only when pipeline mode has been selected.

`PGRES_PIPELINE_ABORTED` #

    

The `PGresult` represents a pipeline that has received an error from the
server. `PQgetResult` must be called repeatedly, and each time it will return
this status code until the end of the current pipeline, at which point it will
return `PGRES_PIPELINE_SYNC` and normal processing can resume.

If the result status is `PGRES_TUPLES_OK` or `PGRES_SINGLE_TUPLE`, then the
functions described below can be used to retrieve the rows returned by the
query. Note that a `SELECT` command that happens to retrieve zero rows still
shows `PGRES_TUPLES_OK`. `PGRES_COMMAND_OK` is for commands that can never
return rows (`INSERT` or `UPDATE` without a `RETURNING` clause, etc.). A
response of `PGRES_EMPTY_QUERY` might indicate a bug in the client software.

A result of status `PGRES_NONFATAL_ERROR` will never be returned directly by
[`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) or other query execution functions;
results of this kind are instead passed to the notice processor (see [Section
34.13](libpq-notice-processing.html "34.13. Notice Processing")).

`PQresStatus` #

    

Converts the enumerated type returned by [`PQresultStatus`](libpq-
exec.html#LIBPQ-PQRESULTSTATUS) into a string constant describing the status
code. The caller should not free the result.

    
    
    char *PQresStatus(ExecStatusType status);
    

`PQresultErrorMessage` #

    

Returns the error message associated with the command, or an empty string if
there was no error.

    
    
    char *PQresultErrorMessage(const PGresult *res);
    

If there was an error, the returned string will include a trailing newline.
The caller should not free the result directly. It will be freed when the
associated `PGresult` handle is passed to [`PQclear`](libpq-exec.html#LIBPQ-
PQCLEAR).

Immediately following a [`PQexec`](libpq-exec.html#LIBPQ-PQEXEC) or
[`PQgetResult`](libpq-async.html#LIBPQ-PQGETRESULT) call,
[`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE) (on the connection)
will return the same string as [`PQresultErrorMessage`](libpq-exec.html#LIBPQ-
PQRESULTERRORMESSAGE) (on the result). However, a `PGresult` will retain its
error message until destroyed, whereas the connection's error message will
change when subsequent operations are done. Use
[`PQresultErrorMessage`](libpq-exec.html#LIBPQ-PQRESULTERRORMESSAGE) when you
want to know the status associated with a particular `PGresult`; use
[`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE) when you want to
know the status from the latest operation on the connection.

`PQresultVerboseErrorMessage` #

    

Returns a reformatted version of the error message associated with a
`PGresult` object.

    
    
    char *PQresultVerboseErrorMessage(const PGresult *res,
                                      PGVerbosity verbosity,
                                      PGContextVisibility show_context);
    

In some situations a client might wish to obtain a more detailed version of a
previously-reported error. [`PQresultVerboseErrorMessage`](libpq-
exec.html#LIBPQ-PQRESULTVERBOSEERRORMESSAGE) addresses this need by computing
the message that would have been produced by [`PQresultErrorMessage`](libpq-
exec.html#LIBPQ-PQRESULTERRORMESSAGE) if the specified verbosity settings had
been in effect for the connection when the given `PGresult` was generated. If
the `PGresult` is not an error result, “PGresult is not an error result” is
reported instead. The returned string includes a trailing newline.

Unlike most other functions for extracting data from a `PGresult`, the result
of this function is a freshly allocated string. The caller must free it using
`PQfreemem()` when the string is no longer needed.

A NULL return is possible if there is insufficient memory.

`PQresultErrorField` #

    

Returns an individual field of an error report.

    
    
    char *PQresultErrorField(const PGresult *res, int fieldcode);
    

_`fieldcode`_ is an error field identifier; see the symbols listed below.
`NULL` is returned if the `PGresult` is not an error or warning result, or
does not include the specified field. Field values will normally not include a
trailing newline. The caller should not free the result directly. It will be
freed when the associated `PGresult` handle is passed to [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR).

The following field codes are available:

`PG_DIAG_SEVERITY` #

    

The severity; the field contents are `ERROR`, `FATAL`, or `PANIC` (in an error
message), or `WARNING`, `NOTICE`, `DEBUG`, `INFO`, or `LOG` (in a notice
message), or a localized translation of one of these. Always present.

`PG_DIAG_SEVERITY_NONLOCALIZED` #

    

The severity; the field contents are `ERROR`, `FATAL`, or `PANIC` (in an error
message), or `WARNING`, `NOTICE`, `DEBUG`, `INFO`, or `LOG` (in a notice
message). This is identical to the `PG_DIAG_SEVERITY` field except that the
contents are never localized. This is present only in reports generated by
PostgreSQL versions 9.6 and later.

`PG_DIAG_SQLSTATE` #

    

The SQLSTATE code for the error. The SQLSTATE code identifies the type of
error that has occurred; it can be used by front-end applications to perform
specific operations (such as error handling) in response to a particular
database error. For a list of the possible SQLSTATE codes, see [Appendix
A](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes"). This field is
not localizable, and is always present.

`PG_DIAG_MESSAGE_PRIMARY` #

    

The primary human-readable error message (typically one line). Always present.

`PG_DIAG_MESSAGE_DETAIL` #

    

Detail: an optional secondary error message carrying more detail about the
problem. Might run to multiple lines.

`PG_DIAG_MESSAGE_HINT` #

    

Hint: an optional suggestion what to do about the problem. This is intended to
differ from detail in that it offers advice (potentially inappropriate) rather
than hard facts. Might run to multiple lines.

`PG_DIAG_STATEMENT_POSITION` #

    

A string containing a decimal integer indicating an error cursor position as
an index into the original statement string. The first character has index 1,
and positions are measured in characters not bytes.

`PG_DIAG_INTERNAL_POSITION` #

    

This is defined the same as the `PG_DIAG_STATEMENT_POSITION` field, but it is
used when the cursor position refers to an internally generated command rather
than the one submitted by the client. The `PG_DIAG_INTERNAL_QUERY` field will
always appear when this field appears.

`PG_DIAG_INTERNAL_QUERY` #

    

The text of a failed internally-generated command. This could be, for example,
an SQL query issued by a PL/pgSQL function.

`PG_DIAG_CONTEXT` #

    

An indication of the context in which the error occurred. Presently this
includes a call stack traceback of active procedural language functions and
internally-generated queries. The trace is one entry per line, most recent
first.

`PG_DIAG_SCHEMA_NAME` #

    

If the error was associated with a specific database object, the name of the
schema containing that object, if any.

`PG_DIAG_TABLE_NAME` #

    

If the error was associated with a specific table, the name of the table.
(Refer to the schema name field for the name of the table's schema.)

`PG_DIAG_COLUMN_NAME` #

    

If the error was associated with a specific table column, the name of the
column. (Refer to the schema and table name fields to identify the table.)

`PG_DIAG_DATATYPE_NAME` #

    

If the error was associated with a specific data type, the name of the data
type. (Refer to the schema name field for the name of the data type's schema.)

`PG_DIAG_CONSTRAINT_NAME` #

    

If the error was associated with a specific constraint, the name of the
constraint. Refer to fields listed above for the associated table or domain.
(For this purpose, indexes are treated as constraints, even if they weren't
created with constraint syntax.)

`PG_DIAG_SOURCE_FILE` #

    

The file name of the source-code location where the error was reported.

`PG_DIAG_SOURCE_LINE` #

    

The line number of the source-code location where the error was reported.

`PG_DIAG_SOURCE_FUNCTION` #

    

The name of the source-code function reporting the error.

### Note

The fields for schema name, table name, column name, data type name, and
constraint name are supplied only for a limited number of error types; see
[Appendix A](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes"). Do
not assume that the presence of any of these fields guarantees the presence of
another field. Core error sources observe the interrelationships noted above,
but user-defined functions may use these fields in other ways. In the same
vein, do not assume that these fields denote contemporary objects in the
current database.

The client is responsible for formatting displayed information to meet its
needs; in particular it should break long lines as needed. Newline characters
appearing in the error message fields should be treated as paragraph breaks,
not line breaks.

Errors generated internally by libpq will have severity and primary message,
but typically no other fields.

Note that error fields are only available from `PGresult` objects, not
`PGconn` objects; there is no `PQerrorField` function.

`PQclear` #

    

Frees the storage associated with a `PGresult`. Every command result should be
freed via [`PQclear`](libpq-exec.html#LIBPQ-PQCLEAR) when it is no longer
needed.

    
    
    void PQclear(PGresult *res);
    

If the argument is a `NULL` pointer, no operation is performed.

You can keep a `PGresult` object around for as long as you need it; it does
not go away when you issue a new command, nor even if you close the
connection. To get rid of it, you must call [`PQclear`](libpq-exec.html#LIBPQ-
PQCLEAR). Failure to do this will result in memory leaks in your application.

### 34.3.2. Retrieving Query Result Information #

These functions are used to extract information from a `PGresult` object that
represents a successful query result (that is, one that has status
`PGRES_TUPLES_OK` or `PGRES_SINGLE_TUPLE`). They can also be used to extract
information from a successful Describe operation: a Describe's result has all
the same column information that actual execution of the query would provide,
but it has zero rows. For objects with other status values, these functions
will act as though the result has zero rows and zero columns.

`PQntuples` #

    

Returns the number of rows (tuples) in the query result. (Note that `PGresult`
objects are limited to no more than `INT_MAX` rows, so an `int` result is
sufficient.)

    
    
    int PQntuples(const PGresult *res);
    

`PQnfields` #

    

Returns the number of columns (fields) in each row of the query result.

    
    
    int PQnfields(const PGresult *res);
    

`PQfname` #

    

Returns the column name associated with the given column number. Column
numbers start at 0. The caller should not free the result directly. It will be
freed when the associated `PGresult` handle is passed to [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR).

    
    
    char *PQfname(const PGresult *res,
                  int column_number);
    

`NULL` is returned if the column number is out of range.

`PQfnumber` #

    

Returns the column number associated with the given column name.

    
    
    int PQfnumber(const PGresult *res,
                  const char *column_name);
    

-1 is returned if the given name does not match any column.

The given name is treated like an identifier in an SQL command, that is, it is
downcased unless double-quoted. For example, given a query result generated
from the SQL command:

    
    
    SELECT 1 AS FOO, 2 AS "BAR";
    

we would have the results:

    
    
    PQfname(res, 0)              _foo_
    PQfname(res, 1)              _BAR_
    PQfnumber(res, "FOO")        _0_
    PQfnumber(res, "foo")        _0_
    PQfnumber(res, "BAR")        _-1_
    PQfnumber(res, "\"BAR\"")    _1_
    

`PQftable` #

    

Returns the OID of the table from which the given column was fetched. Column
numbers start at 0.

    
    
    Oid PQftable(const PGresult *res,
                 int column_number);
    

`InvalidOid` is returned if the column number is out of range, or if the
specified column is not a simple reference to a table column. You can query
the system table `pg_class` to determine exactly which table is referenced.

The type `Oid` and the constant `InvalidOid` will be defined when you include
the libpq header file. They will both be some integer type.

`PQftablecol` #

    

Returns the column number (within its table) of the column making up the
specified query result column. Query-result column numbers start at 0, but
table columns have nonzero numbers.

    
    
    int PQftablecol(const PGresult *res,
                    int column_number);
    

Zero is returned if the column number is out of range, or if the specified
column is not a simple reference to a table column.

`PQfformat` #

    

Returns the format code indicating the format of the given column. Column
numbers start at 0.

    
    
    int PQfformat(const PGresult *res,
                  int column_number);
    

Format code zero indicates textual data representation, while format code one
indicates binary representation. (Other codes are reserved for future
definition.)

`PQftype` #

    

Returns the data type associated with the given column number. The integer
returned is the internal OID number of the type. Column numbers start at 0.

    
    
    Oid PQftype(const PGresult *res,
                int column_number);
    

You can query the system table `pg_type` to obtain the names and properties of
the various data types. The OIDs of the built-in data types are defined in the
file `catalog/pg_type_d.h` in the PostgreSQL installation's `include`
directory.

`PQfmod` #

    

Returns the type modifier of the column associated with the given column
number. Column numbers start at 0.

    
    
    int PQfmod(const PGresult *res,
               int column_number);
    

The interpretation of modifier values is type-specific; they typically
indicate precision or size limits. The value -1 is used to indicate “no
information available”. Most data types do not use modifiers, in which case
the value is always -1.

`PQfsize` #

    

Returns the size in bytes of the column associated with the given column
number. Column numbers start at 0.

    
    
    int PQfsize(const PGresult *res,
                int column_number);
    

[`PQfsize`](libpq-exec.html#LIBPQ-PQFSIZE) returns the space allocated for
this column in a database row, in other words the size of the server's
internal representation of the data type. (Accordingly, it is not really very
useful to clients.) A negative value indicates the data type is variable-
length.

`PQbinaryTuples` #

    

Returns 1 if the `PGresult` contains binary data and 0 if it contains text
data.

    
    
    int PQbinaryTuples(const PGresult *res);
    

This function is deprecated (except for its use in connection with `COPY`),
because it is possible for a single `PGresult` to contain text data in some
columns and binary data in others. [`PQfformat`](libpq-exec.html#LIBPQ-
PQFFORMAT) is preferred. [`PQbinaryTuples`](libpq-exec.html#LIBPQ-
PQBINARYTUPLES) returns 1 only if all columns of the result are binary (format
1).

`PQgetvalue` #

    

Returns a single field value of one row of a `PGresult`. Row and column
numbers start at 0. The caller should not free the result directly. It will be
freed when the associated `PGresult` handle is passed to [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR).

    
    
    char *PQgetvalue(const PGresult *res,
                     int row_number,
                     int column_number);
    

For data in text format, the value returned by [`PQgetvalue`](libpq-
exec.html#LIBPQ-PQGETVALUE) is a null-terminated character string
representation of the field value. For data in binary format, the value is in
the binary representation determined by the data type's `typsend` and
`typreceive` functions. (The value is actually followed by a zero byte in this
case too, but that is not ordinarily useful, since the value is likely to
contain embedded nulls.)

An empty string is returned if the field value is null. See
[`PQgetisnull`](libpq-exec.html#LIBPQ-PQGETISNULL) to distinguish null values
from empty-string values.

The pointer returned by [`PQgetvalue`](libpq-exec.html#LIBPQ-PQGETVALUE)
points to storage that is part of the `PGresult` structure. One should not
modify the data it points to, and one must explicitly copy the data into other
storage if it is to be used past the lifetime of the `PGresult` structure
itself.

`PQgetisnull` #

    

Tests a field for a null value. Row and column numbers start at 0.

    
    
    int PQgetisnull(const PGresult *res,
                    int row_number,
                    int column_number);
    

This function returns 1 if the field is null and 0 if it contains a non-null
value. (Note that [`PQgetvalue`](libpq-exec.html#LIBPQ-PQGETVALUE) will return
an empty string, not a null pointer, for a null field.)

`PQgetlength` #

    

Returns the actual length of a field value in bytes. Row and column numbers
start at 0.

    
    
    int PQgetlength(const PGresult *res,
                    int row_number,
                    int column_number);
    

This is the actual data length for the particular data value, that is, the
size of the object pointed to by [`PQgetvalue`](libpq-exec.html#LIBPQ-
PQGETVALUE). For text data format this is the same as `strlen()`. For binary
format this is essential information. Note that one should _not_ rely on
[`PQfsize`](libpq-exec.html#LIBPQ-PQFSIZE) to obtain the actual data length.

`PQnparams` #

    

Returns the number of parameters of a prepared statement.

    
    
    int PQnparams(const PGresult *res);
    

This function is only useful when inspecting the result of
[`PQdescribePrepared`](libpq-exec.html#LIBPQ-PQDESCRIBEPREPARED). For other
types of results it will return zero.

`PQparamtype` #

    

Returns the data type of the indicated statement parameter. Parameter numbers
start at 0.

    
    
    Oid PQparamtype(const PGresult *res, int param_number);
    

This function is only useful when inspecting the result of
[`PQdescribePrepared`](libpq-exec.html#LIBPQ-PQDESCRIBEPREPARED). For other
types of results it will return zero.

`PQprint` #

    

Prints out all the rows and, optionally, the column names to the specified
output stream.

    
    
    void PQprint(FILE *fout,      /* output stream */
                 const PGresult *res,
                 const PQprintOpt *po);
    typedef struct
    {
        pqbool  header;      /* print output field headings and row count */
        pqbool  align;       /* fill align the fields */
        pqbool  standard;    /* old brain dead format */
        pqbool  html3;       /* output HTML tables */
        pqbool  expanded;    /* expand tables */
        pqbool  pager;       /* use pager for output if needed */
        char    *fieldSep;   /* field separator */
        char    *tableOpt;   /* attributes for HTML table element */
        char    *caption;    /* HTML table caption */
        char    **fieldName; /* null-terminated array of replacement field names */
    } PQprintOpt;
    

This function was formerly used by psql to print query results, but this is no
longer the case. Note that it assumes all the data is in text format.

### 34.3.3. Retrieving Other Result Information #

These functions are used to extract other information from `PGresult` objects.

`PQcmdStatus` #

    

Returns the command status tag from the SQL command that generated the
`PGresult`.

    
    
    char *PQcmdStatus(PGresult *res);
    

Commonly this is just the name of the command, but it might include additional
data such as the number of rows processed. The caller should not free the
result directly. It will be freed when the associated `PGresult` handle is
passed to [`PQclear`](libpq-exec.html#LIBPQ-PQCLEAR).

`PQcmdTuples` #

    

Returns the number of rows affected by the SQL command.

    
    
    char *PQcmdTuples(PGresult *res);
    

This function returns a string containing the number of rows affected by the
SQL statement that generated the `PGresult`. This function can only be used
following the execution of a `SELECT`, `CREATE TABLE AS`, `INSERT`, `UPDATE`,
`DELETE`, `MERGE`, `MOVE`, `FETCH`, or `COPY` statement, or an `EXECUTE` of a
prepared query that contains an `INSERT`, `UPDATE`, `DELETE`, or `MERGE`
statement. If the command that generated the `PGresult` was anything else,
[`PQcmdTuples`](libpq-exec.html#LIBPQ-PQCMDTUPLES) returns an empty string.
The caller should not free the return value directly. It will be freed when
the associated `PGresult` handle is passed to [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR).

`PQoidValue` #

    

Returns the OID of the inserted row, if the SQL command was an `INSERT` that
inserted exactly one row into a table that has OIDs, or a `EXECUTE` of a
prepared query containing a suitable `INSERT` statement. Otherwise, this
function returns `InvalidOid`. This function will also return `InvalidOid` if
the table affected by the `INSERT` statement does not contain OIDs.

    
    
    Oid PQoidValue(const PGresult *res);
    

`PQoidStatus` #

    

This function is deprecated in favor of [`PQoidValue`](libpq-exec.html#LIBPQ-
PQOIDVALUE) and is not thread-safe. It returns a string with the OID of the
inserted row, while [`PQoidValue`](libpq-exec.html#LIBPQ-PQOIDVALUE) returns
the OID value.

    
    
    char *PQoidStatus(const PGresult *res);
    

### 34.3.4. Escaping Strings for Inclusion in SQL Commands #

`PQescapeLiteral` #

    
    
    
    char *PQescapeLiteral(PGconn *conn, const char *str, size_t length);
    

[`PQescapeLiteral`](libpq-exec.html#LIBPQ-PQESCAPELITERAL) escapes a string
for use within an SQL command. This is useful when inserting data values as
literal constants in SQL commands. Certain characters (such as quotes and
backslashes) must be escaped to prevent them from being interpreted specially
by the SQL parser. [`PQescapeLiteral`](libpq-exec.html#LIBPQ-PQESCAPELITERAL)
performs this operation.

[`PQescapeLiteral`](libpq-exec.html#LIBPQ-PQESCAPELITERAL) returns an escaped
version of the _`str`_ parameter in memory allocated with `malloc()`. This
memory should be freed using `PQfreemem()` when the result is no longer
needed. A terminating zero byte is not required, and should not be counted in
_`length`_. (If a terminating zero byte is found before _`length`_ bytes are
processed, [`PQescapeLiteral`](libpq-exec.html#LIBPQ-PQESCAPELITERAL) stops at
the zero; the behavior is thus rather like `strncpy`.) The return string has
all special characters replaced so that they can be properly processed by the
PostgreSQL string literal parser. A terminating zero byte is also added. The
single quotes that must surround PostgreSQL string literals are included in
the result string.

On error, [`PQescapeLiteral`](libpq-exec.html#LIBPQ-PQESCAPELITERAL) returns
`NULL` and a suitable message is stored in the _`conn`_ object.

### Tip

It is especially important to do proper escaping when handling strings that
were received from an untrustworthy source. Otherwise there is a security
risk: you are vulnerable to “SQL injection” attacks wherein unwanted SQL
commands are fed to your database.

Note that it is neither necessary nor correct to do escaping when a data value
is passed as a separate parameter in [`PQexecParams`](libpq-exec.html#LIBPQ-
PQEXECPARAMS) or its sibling routines.

`PQescapeIdentifier` #

    
    
    
    char *PQescapeIdentifier(PGconn *conn, const char *str, size_t length);
    

[`PQescapeIdentifier`](libpq-exec.html#LIBPQ-PQESCAPEIDENTIFIER) escapes a
string for use as an SQL identifier, such as a table, column, or function
name. This is useful when a user-supplied identifier might contain special
characters that would otherwise not be interpreted as part of the identifier
by the SQL parser, or when the identifier might contain upper case characters
whose case should be preserved.

[`PQescapeIdentifier`](libpq-exec.html#LIBPQ-PQESCAPEIDENTIFIER) returns a
version of the _`str`_ parameter escaped as an SQL identifier in memory
allocated with `malloc()`. This memory must be freed using `PQfreemem()` when
the result is no longer needed. A terminating zero byte is not required, and
should not be counted in _`length`_. (If a terminating zero byte is found
before _`length`_ bytes are processed, [`PQescapeIdentifier`](libpq-
exec.html#LIBPQ-PQESCAPEIDENTIFIER) stops at the zero; the behavior is thus
rather like `strncpy`.) The return string has all special characters replaced
so that it will be properly processed as an SQL identifier. A terminating zero
byte is also added. The return string will also be surrounded by double
quotes.

On error, [`PQescapeIdentifier`](libpq-exec.html#LIBPQ-PQESCAPEIDENTIFIER)
returns `NULL` and a suitable message is stored in the _`conn`_ object.

### Tip

As with string literals, to prevent SQL injection attacks, SQL identifiers
must be escaped when they are received from an untrustworthy source.

`PQescapeStringConn` #

    
    
    
    size_t PQescapeStringConn(PGconn *conn,
                              char *to, const char *from, size_t length,
                              int *error);
    

[`PQescapeStringConn`](libpq-exec.html#LIBPQ-PQESCAPESTRINGCONN) escapes
string literals, much like [`PQescapeLiteral`](libpq-exec.html#LIBPQ-
PQESCAPELITERAL). Unlike [`PQescapeLiteral`](libpq-exec.html#LIBPQ-
PQESCAPELITERAL), the caller is responsible for providing an appropriately
sized buffer. Furthermore, [`PQescapeStringConn`](libpq-exec.html#LIBPQ-
PQESCAPESTRINGCONN) does not generate the single quotes that must surround
PostgreSQL string literals; they should be provided in the SQL command that
the result is inserted into. The parameter _`from`_ points to the first
character of the string that is to be escaped, and the _`length`_ parameter
gives the number of bytes in this string. A terminating zero byte is not
required, and should not be counted in _`length`_. (If a terminating zero byte
is found before _`length`_ bytes are processed, [`PQescapeStringConn`](libpq-
exec.html#LIBPQ-PQESCAPESTRINGCONN) stops at the zero; the behavior is thus
rather like `strncpy`.) _`to`_ shall point to a buffer that is able to hold at
least one more byte than twice the value of _`length`_ , otherwise the
behavior is undefined. Behavior is likewise undefined if the _`to`_ and
_`from`_ strings overlap.

If the _`error`_ parameter is not `NULL`, then `*error` is set to zero on
success, nonzero on error. Presently the only possible error conditions
involve invalid multibyte encoding in the source string. The output string is
still generated on error, but it can be expected that the server will reject
it as malformed. On error, a suitable message is stored in the _`conn`_
object, whether or not _`error`_ is `NULL`.

[`PQescapeStringConn`](libpq-exec.html#LIBPQ-PQESCAPESTRINGCONN) returns the
number of bytes written to _`to`_ , not including the terminating zero byte.

`PQescapeString` #

    

[`PQescapeString`](libpq-exec.html#LIBPQ-PQESCAPESTRING) is an older,
deprecated version of [`PQescapeStringConn`](libpq-exec.html#LIBPQ-
PQESCAPESTRINGCONN).

    
    
    size_t PQescapeString (char *to, const char *from, size_t length);
    

The only difference from [`PQescapeStringConn`](libpq-exec.html#LIBPQ-
PQESCAPESTRINGCONN) is that [`PQescapeString`](libpq-exec.html#LIBPQ-
PQESCAPESTRING) does not take `PGconn` or _`error`_ parameters. Because of
this, it cannot adjust its behavior depending on the connection properties
(such as character encoding) and therefore _it might give the wrong results_.
Also, it has no way to report error conditions.

[`PQescapeString`](libpq-exec.html#LIBPQ-PQESCAPESTRING) can be used safely in
client programs that work with only one PostgreSQL connection at a time (in
this case it can find out what it needs to know “behind the scenes”). In other
contexts it is a security hazard and should be avoided in favor of
[`PQescapeStringConn`](libpq-exec.html#LIBPQ-PQESCAPESTRINGCONN).

`PQescapeByteaConn` #

    

Escapes binary data for use within an SQL command with the type `bytea`. As
with [`PQescapeStringConn`](libpq-exec.html#LIBPQ-PQESCAPESTRINGCONN), this is
only used when inserting data directly into an SQL command string.

    
    
    unsigned char *PQescapeByteaConn(PGconn *conn,
                                     const unsigned char *from,
                                     size_t from_length,
                                     size_t *to_length);
    

Certain byte values must be escaped when used as part of a `bytea` literal in
an SQL statement. [`PQescapeByteaConn`](libpq-exec.html#LIBPQ-
PQESCAPEBYTEACONN) escapes bytes using either hex encoding or backslash
escaping. See [Section 8.4](datatype-binary.html "8.4. Binary Data Types") for
more information.

The _`from`_ parameter points to the first byte of the string that is to be
escaped, and the _`from_length`_ parameter gives the number of bytes in this
binary string. (A terminating zero byte is neither necessary nor counted.) The
_`to_length`_ parameter points to a variable that will hold the resultant
escaped string length. This result string length includes the terminating zero
byte of the result.

[`PQescapeByteaConn`](libpq-exec.html#LIBPQ-PQESCAPEBYTEACONN) returns an
escaped version of the _`from`_ parameter binary string in memory allocated
with `malloc()`. This memory should be freed using `PQfreemem()` when the
result is no longer needed. The return string has all special characters
replaced so that they can be properly processed by the PostgreSQL string
literal parser, and the `bytea` input function. A terminating zero byte is
also added. The single quotes that must surround PostgreSQL string literals
are not part of the result string.

On error, a null pointer is returned, and a suitable error message is stored
in the _`conn`_ object. Currently, the only possible error is insufficient
memory for the result string.

`PQescapeBytea` #

    

[`PQescapeBytea`](libpq-exec.html#LIBPQ-PQESCAPEBYTEA) is an older, deprecated
version of [`PQescapeByteaConn`](libpq-exec.html#LIBPQ-PQESCAPEBYTEACONN).

    
    
    unsigned char *PQescapeBytea(const unsigned char *from,
                                 size_t from_length,
                                 size_t *to_length);
    

The only difference from [`PQescapeByteaConn`](libpq-exec.html#LIBPQ-
PQESCAPEBYTEACONN) is that [`PQescapeBytea`](libpq-exec.html#LIBPQ-
PQESCAPEBYTEA) does not take a `PGconn` parameter. Because of this,
[`PQescapeBytea`](libpq-exec.html#LIBPQ-PQESCAPEBYTEA) can only be used safely
in client programs that use a single PostgreSQL connection at a time (in this
case it can find out what it needs to know “behind the scenes”). It _might
give the wrong results_ if used in programs that use multiple database
connections (use [`PQescapeByteaConn`](libpq-exec.html#LIBPQ-
PQESCAPEBYTEACONN) in such cases).

`PQunescapeBytea` #

    

Converts a string representation of binary data into binary data — the reverse
of [`PQescapeBytea`](libpq-exec.html#LIBPQ-PQESCAPEBYTEA). This is needed when
retrieving `bytea` data in text format, but not when retrieving it in binary
format.

    
    
    unsigned char *PQunescapeBytea(const unsigned char *from, size_t *to_length);
    

The _`from`_ parameter points to a string such as might be returned by
[`PQgetvalue`](libpq-exec.html#LIBPQ-PQGETVALUE) when applied to a `bytea`
column. [`PQunescapeBytea`](libpq-exec.html#LIBPQ-PQUNESCAPEBYTEA) converts
this string representation into its binary representation. It returns a
pointer to a buffer allocated with `malloc()`, or `NULL` on error, and puts
the size of the buffer in _`to_length`_. The result must be freed using
[`PQfreemem`](libpq-misc.html#LIBPQ-PQFREEMEM) when it is no longer needed.

This conversion is not exactly the inverse of [`PQescapeBytea`](libpq-
exec.html#LIBPQ-PQESCAPEBYTEA), because the string is not expected to be
“escaped” when received from [`PQgetvalue`](libpq-exec.html#LIBPQ-PQGETVALUE).
In particular this means there is no need for string quoting considerations,
and so no need for a `PGconn` parameter.

* * *

[Prev](libpq-status.html "34.2. Connection Status Functions")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-async.html "34.4. Asynchronous Command Processing")  
---|---|---  
34.2. Connection Status Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.4. Asynchronous Command Processing  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-exec.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

