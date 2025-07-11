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

Supported Versions: [Current](/docs/current/protocol-message-formats.html
"PostgreSQL 17 - 55.7. Message Formats") ([17](/docs/17/protocol-message-
formats.html "PostgreSQL 17 - 55.7. Message Formats")) /
[16](/docs/16/protocol-message-formats.html "PostgreSQL 16 - 55.7. Message
Formats") / [15](/docs/15/protocol-message-formats.html "PostgreSQL 15 -
55.7. Message Formats") / [14](/docs/14/protocol-message-formats.html
"PostgreSQL 14 - 55.7. Message Formats") / [13](/docs/13/protocol-message-
formats.html "PostgreSQL 13 - 55.7. Message Formats")

Development Versions: [18](/docs/18/protocol-message-formats.html "PostgreSQL
18 - 55.7. Message Formats") / [devel](/docs/devel/protocol-message-
formats.html "PostgreSQL devel - 55.7. Message Formats")

Unsupported versions: [12](/docs/12/protocol-message-formats.html "PostgreSQL
12 - 55.7. Message Formats") / [11](/docs/11/protocol-message-formats.html
"PostgreSQL 11 - 55.7. Message Formats") / [10](/docs/10/protocol-message-
formats.html "PostgreSQL 10 - 55.7. Message Formats") /
[9.6](/docs/9.6/protocol-message-formats.html "PostgreSQL 9.6 - 55.7. Message
Formats") / [9.5](/docs/9.5/protocol-message-formats.html "PostgreSQL 9.5 -
55.7. Message Formats") / [9.4](/docs/9.4/protocol-message-formats.html
"PostgreSQL 9.4 - 55.7. Message Formats") / [9.3](/docs/9.3/protocol-message-
formats.html "PostgreSQL 9.3 - 55.7. Message Formats") /
[9.2](/docs/9.2/protocol-message-formats.html "PostgreSQL 9.2 - 55.7. Message
Formats") / [9.1](/docs/9.1/protocol-message-formats.html "PostgreSQL 9.1 -
55.7. Message Formats") / [9.0](/docs/9.0/protocol-message-formats.html
"PostgreSQL 9.0 - 55.7. Message Formats") / [8.4](/docs/8.4/protocol-message-
formats.html "PostgreSQL 8.4 - 55.7. Message Formats") /
[8.3](/docs/8.3/protocol-message-formats.html "PostgreSQL 8.3 - 55.7. Message
Formats") / [8.2](/docs/8.2/protocol-message-formats.html "PostgreSQL 8.2 -
55.7. Message Formats") / [8.1](/docs/8.1/protocol-message-formats.html
"PostgreSQL 8.1 - 55.7. Message Formats") / [8.0](/docs/8.0/protocol-message-
formats.html "PostgreSQL 8.0 - 55.7. Message Formats") /
[7.4](/docs/7.4/protocol-message-formats.html "PostgreSQL 7.4 - 55.7. Message
Formats") / [7.3](/docs/7.3/protocol-message-formats.html "PostgreSQL 7.3 -
55.7. Message Formats") / [7.2](/docs/7.2/protocol-message-formats.html
"PostgreSQL 7.2 - 55.7. Message Formats") / [7.1](/docs/7.1/protocol-message-
formats.html "PostgreSQL 7.1 - 55.7. Message Formats")

__

55.7. Message Formats  
---  
[Prev](protocol-message-types.html "55.6. Message Data Types")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-error-fields.html "55.8. Error and Notice Message Fields")  
  
* * *

## 55.7. Message Formats #

This section describes the detailed format of each message. Each is marked to
indicate that it can be sent by a frontend (F), a backend (B), or both (F &
B). Notice that although each message includes a byte count at the beginning,
the message format is defined so that the message end can be found without
reference to the byte count. This aids validity checking. (The CopyData
message is an exception, because it forms part of a data stream; the contents
of any individual CopyData message cannot be interpretable on their own.)

AuthenticationOk (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32(8)

    

Length of message contents in bytes, including self.

Int32(0)

    

Specifies that the authentication was successful.

AuthenticationKerberosV5 (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32(8)

    

Length of message contents in bytes, including self.

Int32(2)

    

Specifies that Kerberos V5 authentication is required.

AuthenticationCleartextPassword (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32(8)

    

Length of message contents in bytes, including self.

Int32(3)

    

Specifies that a clear-text password is required.

AuthenticationMD5Password (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32(12)

    

Length of message contents in bytes, including self.

Int32(5)

    

Specifies that an MD5-encrypted password is required.

Byte4

    

The salt to use when encrypting the password.

AuthenticationGSS (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32(8)

    

Length of message contents in bytes, including self.

Int32(7)

    

Specifies that GSSAPI authentication is required.

AuthenticationGSSContinue (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32

    

Length of message contents in bytes, including self.

Int32(8)

    

Specifies that this message contains GSSAPI or SSPI data.

Byte _`n`_

    

GSSAPI or SSPI authentication data.

AuthenticationSSPI (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32(8)

    

Length of message contents in bytes, including self.

Int32(9)

    

Specifies that SSPI authentication is required.

AuthenticationSASL (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32

    

Length of message contents in bytes, including self.

Int32(10)

    

Specifies that SASL authentication is required.

The message body is a list of SASL authentication mechanisms, in the server's
order of preference. A zero byte is required as terminator after the last
authentication mechanism name. For each mechanism, there is the following:

String

    

Name of a SASL authentication mechanism.

AuthenticationSASLContinue (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32

    

Length of message contents in bytes, including self.

Int32(11)

    

Specifies that this message contains a SASL challenge.

Byte _`n`_

    

SASL data, specific to the SASL mechanism being used.

AuthenticationSASLFinal (B) #

    

Byte1('R')

    

Identifies the message as an authentication request.

Int32

    

Length of message contents in bytes, including self.

Int32(12)

    

Specifies that SASL authentication has completed.

Byte _`n`_

    

SASL outcome "additional data", specific to the SASL mechanism being used.

BackendKeyData (B) #

    

Byte1('K')

    

Identifies the message as cancellation key data. The frontend must save these
values if it wishes to be able to issue CancelRequest messages later.

Int32(12)

    

Length of message contents in bytes, including self.

Int32

    

The process ID of this backend.

Int32

    

The secret key of this backend.

Bind (F) #

    

Byte1('B')

    

Identifies the message as a Bind command.

Int32

    

Length of message contents in bytes, including self.

String

    

The name of the destination portal (an empty string selects the unnamed
portal).

String

    

The name of the source prepared statement (an empty string selects the unnamed
prepared statement).

Int16

    

The number of parameter format codes that follow (denoted _`C`_ below). This
can be zero to indicate that there are no parameters or that the parameters
all use the default format (text); or one, in which case the specified format
code is applied to all parameters; or it can equal the actual number of
parameters.

Int16[_`C`_]

    

The parameter format codes. Each must presently be zero (text) or one
(binary).

Int16

    

The number of parameter values that follow (possibly zero). This must match
the number of parameters needed by the query.

Next, the following pair of fields appear for each parameter:

Int32

    

The length of the parameter value, in bytes (this count does not include
itself). Can be zero. As a special case, -1 indicates a NULL parameter value.
No value bytes follow in the NULL case.

Byte _`n`_

    

The value of the parameter, in the format indicated by the associated format
code. _`n`_ is the above length.

After the last parameter, the following fields appear:

Int16

    

The number of result-column format codes that follow (denoted _`R`_ below).
This can be zero to indicate that there are no result columns or that the
result columns should all use the default format (text); or one, in which case
the specified format code is applied to all result columns (if any); or it can
equal the actual number of result columns of the query.

Int16[_`R`_]

    

The result-column format codes. Each must presently be zero (text) or one
(binary).

BindComplete (B) #

    

Byte1('2')

    

Identifies the message as a Bind-complete indicator.

Int32(4)

    

Length of message contents in bytes, including self.

CancelRequest (F) #

    

Int32(16)

    

Length of message contents in bytes, including self.

Int32(80877102)

    

The cancel request code. The value is chosen to contain `1234` in the most
significant 16 bits, and `5678` in the least significant 16 bits. (To avoid
confusion, this code must not be the same as any protocol version number.)

Int32

    

The process ID of the target backend.

Int32

    

The secret key for the target backend.

Close (F) #

    

Byte1('C')

    

Identifies the message as a Close command.

Int32

    

Length of message contents in bytes, including self.

Byte1

    

'`S`' to close a prepared statement; or '`P`' to close a portal.

String

    

The name of the prepared statement or portal to close (an empty string selects
the unnamed prepared statement or portal).

CloseComplete (B) #

    

Byte1('3')

    

Identifies the message as a Close-complete indicator.

Int32(4)

    

Length of message contents in bytes, including self.

CommandComplete (B) #

    

Byte1('C')

    

Identifies the message as a command-completed response.

Int32

    

Length of message contents in bytes, including self.

String

    

The command tag. This is usually a single word that identifies which SQL
command was completed.

For an `INSERT` command, the tag is `INSERT _`oid`_ _`rows`_`, where _`rows`_
is the number of rows inserted. _`oid`_ used to be the object ID of the
inserted row if _`rows`_ was 1 and the target table had OIDs, but OIDs system
columns are not supported anymore; therefore _`oid`_ is always 0.

For a `DELETE` command, the tag is `DELETE _`rows`_` where _`rows`_ is the
number of rows deleted.

For an `UPDATE` command, the tag is `UPDATE _`rows`_` where _`rows`_ is the
number of rows updated.

For a `MERGE` command, the tag is `MERGE _`rows`_` where _`rows`_ is the
number of rows inserted, updated, or deleted.

For a `SELECT` or `CREATE TABLE AS` command, the tag is `SELECT _`rows`_`
where _`rows`_ is the number of rows retrieved.

For a `MOVE` command, the tag is `MOVE _`rows`_` where _`rows`_ is the number
of rows the cursor's position has been changed by.

For a `FETCH` command, the tag is `FETCH _`rows`_` where _`rows`_ is the
number of rows that have been retrieved from the cursor.

For a `COPY` command, the tag is `COPY _`rows`_` where _`rows`_ is the number
of rows copied. (Note: the row count appears only in PostgreSQL 8.2 and
later.)

CopyData (F & B) #

    

Byte1('d')

    

Identifies the message as `COPY` data.

Int32

    

Length of message contents in bytes, including self.

Byte _`n`_

    

Data that forms part of a `COPY` data stream. Messages sent from the backend
will always correspond to single data rows, but messages sent by frontends
might divide the data stream arbitrarily.

CopyDone (F & B) #

    

Byte1('c')

    

Identifies the message as a `COPY`-complete indicator.

Int32(4)

    

Length of message contents in bytes, including self.

CopyFail (F) #

    

Byte1('f')

    

Identifies the message as a `COPY`-failure indicator.

Int32

    

Length of message contents in bytes, including self.

String

    

An error message to report as the cause of failure.

CopyInResponse (B) #

    

Byte1('G')

    

Identifies the message as a Start Copy In response. The frontend must now send
copy-in data (if not prepared to do so, send a CopyFail message).

Int32

    

Length of message contents in bytes, including self.

Int8

    

0 indicates the overall `COPY` format is textual (rows separated by newlines,
columns separated by separator characters, etc.). 1 indicates the overall copy
format is binary (similar to DataRow format). See [COPY](sql-copy.html "COPY")
for more information.

Int16

    

The number of columns in the data to be copied (denoted _`N`_ below).

Int16[_`N`_]

    

The format codes to be used for each column. Each must presently be zero
(text) or one (binary). All must be zero if the overall copy format is
textual.

CopyOutResponse (B) #

    

Byte1('H')

    

Identifies the message as a Start Copy Out response. This message will be
followed by copy-out data.

Int32

    

Length of message contents in bytes, including self.

Int8

    

0 indicates the overall `COPY` format is textual (rows separated by newlines,
columns separated by separator characters, etc.). 1 indicates the overall copy
format is binary (similar to DataRow format). See [COPY](sql-copy.html "COPY")
for more information.

Int16

    

The number of columns in the data to be copied (denoted _`N`_ below).

Int16[_`N`_]

    

The format codes to be used for each column. Each must presently be zero
(text) or one (binary). All must be zero if the overall copy format is
textual.

CopyBothResponse (B) #

    

Byte1('W')

    

Identifies the message as a Start Copy Both response. This message is used
only for Streaming Replication.

Int32

    

Length of message contents in bytes, including self.

Int8

    

0 indicates the overall `COPY` format is textual (rows separated by newlines,
columns separated by separator characters, etc.). 1 indicates the overall copy
format is binary (similar to DataRow format). See [COPY](sql-copy.html "COPY")
for more information.

Int16

    

The number of columns in the data to be copied (denoted _`N`_ below).

Int16[_`N`_]

    

The format codes to be used for each column. Each must presently be zero
(text) or one (binary). All must be zero if the overall copy format is
textual.

DataRow (B) #

    

Byte1('D')

    

Identifies the message as a data row.

Int32

    

Length of message contents in bytes, including self.

Int16

    

The number of column values that follow (possibly zero).

Next, the following pair of fields appear for each column:

Int32

    

The length of the column value, in bytes (this count does not include itself).
Can be zero. As a special case, -1 indicates a NULL column value. No value
bytes follow in the NULL case.

Byte _`n`_

    

The value of the column, in the format indicated by the associated format
code. _`n`_ is the above length.

Describe (F) #

    

Byte1('D')

    

Identifies the message as a Describe command.

Int32

    

Length of message contents in bytes, including self.

Byte1

    

'`S`' to describe a prepared statement; or '`P`' to describe a portal.

String

    

The name of the prepared statement or portal to describe (an empty string
selects the unnamed prepared statement or portal).

EmptyQueryResponse (B) #

    

Byte1('I')

    

Identifies the message as a response to an empty query string. (This
substitutes for CommandComplete.)

Int32(4)

    

Length of message contents in bytes, including self.

ErrorResponse (B) #

    

Byte1('E')

    

Identifies the message as an error.

Int32

    

Length of message contents in bytes, including self.

The message body consists of one or more identified fields, followed by a zero
byte as a terminator. Fields can appear in any order. For each field there is
the following:

Byte1

    

A code identifying the field type; if zero, this is the message terminator and
no string follows. The presently defined field types are listed in [Section
55.8](protocol-error-fields.html "55.8. Error and Notice Message Fields").
Since more field types might be added in future, frontends should silently
ignore fields of unrecognized type.

String

    

The field value.

Execute (F) #

    

Byte1('E')

    

Identifies the message as an Execute command.

Int32

    

Length of message contents in bytes, including self.

String

    

The name of the portal to execute (an empty string selects the unnamed
portal).

Int32

    

Maximum number of rows to return, if portal contains a query that returns rows
(ignored otherwise). Zero denotes “no limit”.

Flush (F) #

    

Byte1('H')

    

Identifies the message as a Flush command.

Int32(4)

    

Length of message contents in bytes, including self.

FunctionCall (F) #

    

Byte1('F')

    

Identifies the message as a function call.

Int32

    

Length of message contents in bytes, including self.

Int32

    

Specifies the object ID of the function to call.

Int16

    

The number of argument format codes that follow (denoted _`C`_ below). This
can be zero to indicate that there are no arguments or that the arguments all
use the default format (text); or one, in which case the specified format code
is applied to all arguments; or it can equal the actual number of arguments.

Int16[_`C`_]

    

The argument format codes. Each must presently be zero (text) or one (binary).

Int16

    

Specifies the number of arguments being supplied to the function.

Next, the following pair of fields appear for each argument:

Int32

    

The length of the argument value, in bytes (this count does not include
itself). Can be zero. As a special case, -1 indicates a NULL argument value.
No value bytes follow in the NULL case.

Byte _`n`_

    

The value of the argument, in the format indicated by the associated format
code. _`n`_ is the above length.

After the last argument, the following field appears:

Int16

    

The format code for the function result. Must presently be zero (text) or one
(binary).

FunctionCallResponse (B) #

    

Byte1('V')

    

Identifies the message as a function call result.

Int32

    

Length of message contents in bytes, including self.

Int32

    

The length of the function result value, in bytes (this count does not include
itself). Can be zero. As a special case, -1 indicates a NULL function result.
No value bytes follow in the NULL case.

Byte _`n`_

    

The value of the function result, in the format indicated by the associated
format code. _`n`_ is the above length.

GSSENCRequest (F) #

    

Int32(8)

    

Length of message contents in bytes, including self.

Int32(80877104)

    

The GSSAPI Encryption request code. The value is chosen to contain `1234` in
the most significant 16 bits, and `5680` in the least significant 16 bits. (To
avoid confusion, this code must not be the same as any protocol version
number.)

GSSResponse (F) #

    

Byte1('p')

    

Identifies the message as a GSSAPI or SSPI response. Note that this is also
used for SASL and password response messages. The exact message type can be
deduced from the context.

Int32

    

Length of message contents in bytes, including self.

Byte _`n`_

    

GSSAPI/SSPI specific message data.

NegotiateProtocolVersion (B) #

    

Byte1('v')

    

Identifies the message as a protocol version negotiation message.

Int32

    

Length of message contents in bytes, including self.

Int32

    

Newest minor protocol version supported by the server for the major protocol
version requested by the client.

Int32

    

Number of protocol options not recognized by the server.

Then, for protocol option not recognized by the server, there is the
following:

String

    

The option name.

NoData (B) #

    

Byte1('n')

    

Identifies the message as a no-data indicator.

Int32(4)

    

Length of message contents in bytes, including self.

NoticeResponse (B) #

    

Byte1('N')

    

Identifies the message as a notice.

Int32

    

Length of message contents in bytes, including self.

The message body consists of one or more identified fields, followed by a zero
byte as a terminator. Fields can appear in any order. For each field there is
the following:

Byte1

    

A code identifying the field type; if zero, this is the message terminator and
no string follows. The presently defined field types are listed in [Section
55.8](protocol-error-fields.html "55.8. Error and Notice Message Fields").
Since more field types might be added in future, frontends should silently
ignore fields of unrecognized type.

String

    

The field value.

NotificationResponse (B) #

    

Byte1('A')

    

Identifies the message as a notification response.

Int32

    

Length of message contents in bytes, including self.

Int32

    

The process ID of the notifying backend process.

String

    

The name of the channel that the notify has been raised on.

String

    

The “payload” string passed from the notifying process.

ParameterDescription (B) #

    

Byte1('t')

    

Identifies the message as a parameter description.

Int32

    

Length of message contents in bytes, including self.

Int16

    

The number of parameters used by the statement (can be zero).

Then, for each parameter, there is the following:

Int32

    

Specifies the object ID of the parameter data type.

ParameterStatus (B) #

    

Byte1('S')

    

Identifies the message as a run-time parameter status report.

Int32

    

Length of message contents in bytes, including self.

String

    

The name of the run-time parameter being reported.

String

    

The current value of the parameter.

Parse (F) #

    

Byte1('P')

    

Identifies the message as a Parse command.

Int32

    

Length of message contents in bytes, including self.

String

    

The name of the destination prepared statement (an empty string selects the
unnamed prepared statement).

String

    

The query string to be parsed.

Int16

    

The number of parameter data types specified (can be zero). Note that this is
not an indication of the number of parameters that might appear in the query
string, only the number that the frontend wants to prespecify types for.

Then, for each parameter, there is the following:

Int32

    

Specifies the object ID of the parameter data type. Placing a zero here is
equivalent to leaving the type unspecified.

ParseComplete (B) #

    

Byte1('1')

    

Identifies the message as a Parse-complete indicator.

Int32(4)

    

Length of message contents in bytes, including self.

PasswordMessage (F) #

    

Byte1('p')

    

Identifies the message as a password response. Note that this is also used for
GSSAPI, SSPI and SASL response messages. The exact message type can be deduced
from the context.

Int32

    

Length of message contents in bytes, including self.

String

    

The password (encrypted, if requested).

PortalSuspended (B) #

    

Byte1('s')

    

Identifies the message as a portal-suspended indicator. Note this only appears
if an Execute message's row-count limit was reached.

Int32(4)

    

Length of message contents in bytes, including self.

Query (F) #

    

Byte1('Q')

    

Identifies the message as a simple query.

Int32

    

Length of message contents in bytes, including self.

String

    

The query string itself.

ReadyForQuery (B) #

    

Byte1('Z')

    

Identifies the message type. ReadyForQuery is sent whenever the backend is
ready for a new query cycle.

Int32(5)

    

Length of message contents in bytes, including self.

Byte1

    

Current backend transaction status indicator. Possible values are '`I`' if
idle (not in a transaction block); '`T`' if in a transaction block; or '`E`'
if in a failed transaction block (queries will be rejected until block is
ended).

RowDescription (B) #

    

Byte1('T')

    

Identifies the message as a row description.

Int32

    

Length of message contents in bytes, including self.

Int16

    

Specifies the number of fields in a row (can be zero).

Then, for each field, there is the following:

String

    

The field name.

Int32

    

If the field can be identified as a column of a specific table, the object ID
of the table; otherwise zero.

Int16

    

If the field can be identified as a column of a specific table, the attribute
number of the column; otherwise zero.

Int32

    

The object ID of the field's data type.

Int16

    

The data type size (see `pg_type.typlen`). Note that negative values denote
variable-width types.

Int32

    

The type modifier (see `pg_attribute.atttypmod`). The meaning of the modifier
is type-specific.

Int16

    

The format code being used for the field. Currently will be zero (text) or one
(binary). In a RowDescription returned from the statement variant of Describe,
the format code is not yet known and will always be zero.

SASLInitialResponse (F) #

    

Byte1('p')

    

Identifies the message as an initial SASL response. Note that this is also
used for GSSAPI, SSPI and password response messages. The exact message type
is deduced from the context.

Int32

    

Length of message contents in bytes, including self.

String

    

Name of the SASL authentication mechanism that the client selected.

Int32

    

Length of SASL mechanism specific "Initial Client Response" that follows, or
-1 if there is no Initial Response.

Byte _`n`_

    

SASL mechanism specific "Initial Response".

SASLResponse (F) #

    

Byte1('p')

    

Identifies the message as a SASL response. Note that this is also used for
GSSAPI, SSPI and password response messages. The exact message type can be
deduced from the context.

Int32

    

Length of message contents in bytes, including self.

Byte _`n`_

    

SASL mechanism specific message data.

SSLRequest (F) #

    

Int32(8)

    

Length of message contents in bytes, including self.

Int32(80877103)

    

The SSL request code. The value is chosen to contain `1234` in the most
significant 16 bits, and `5679` in the least significant 16 bits. (To avoid
confusion, this code must not be the same as any protocol version number.)

StartupMessage (F) #

    

Int32

    

Length of message contents in bytes, including self.

Int32(196608)

    

The protocol version number. The most significant 16 bits are the major
version number (3 for the protocol described here). The least significant 16
bits are the minor version number (0 for the protocol described here).

The protocol version number is followed by one or more pairs of parameter name
and value strings. A zero byte is required as a terminator after the last
name/value pair. Parameters can appear in any order. `user` is required,
others are optional. Each parameter is specified as:

String

    

The parameter name. Currently recognized names are:

`user`

    

The database user name to connect as. Required; there is no default.

`database`

    

The database to connect to. Defaults to the user name.

`options`

    

Command-line arguments for the backend. (This is deprecated in favor of
setting individual run-time parameters.) Spaces within this string are
considered to separate arguments, unless escaped with a backslash (`\`); write
`\\` to represent a literal backslash.

`replication`

    

Used to connect in streaming replication mode, where a small set of
replication commands can be issued instead of SQL statements. Value can be
`true`, `false`, or `database`, and the default is `false`. See [Section
55.4](protocol-replication.html "55.4. Streaming Replication Protocol") for
details.

In addition to the above, other parameters may be listed. Parameter names
beginning with `_pq_.` are reserved for use as protocol extensions, while
others are treated as run-time parameters to be set at backend start time.
Such settings will be applied during backend start (after parsing the command-
line arguments if any) and will act as session defaults.

String

    

The parameter value.

Sync (F) #

    

Byte1('S')

    

Identifies the message as a Sync command.

Int32(4)

    

Length of message contents in bytes, including self.

Terminate (F) #

    

Byte1('X')

    

Identifies the message as a termination.

Int32(4)

    

Length of message contents in bytes, including self.

* * *

[Prev](protocol-message-types.html "55.6. Message Data Types")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](protocol-error-fields.html "55.8. Error and Notice Message Fields")  
---|---|---  
55.6. Message Data Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.8. Error and Notice Message Fields  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol-message-
formats.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

