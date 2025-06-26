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

Supported Versions: [Current](/docs/current/protocol-overview.html "PostgreSQL
17 - 55.1. Overview") ([17](/docs/17/protocol-overview.html "PostgreSQL 17 -
55.1. Overview")) / [16](/docs/16/protocol-overview.html "PostgreSQL 16 -
55.1. Overview") / [15](/docs/15/protocol-overview.html "PostgreSQL 15 -
55.1. Overview") / [14](/docs/14/protocol-overview.html "PostgreSQL 14 -
55.1. Overview") / [13](/docs/13/protocol-overview.html "PostgreSQL 13 -
55.1. Overview")

Development Versions: [18](/docs/18/protocol-overview.html "PostgreSQL 18 -
55.1. Overview") / [devel](/docs/devel/protocol-overview.html "PostgreSQL
devel - 55.1. Overview")

Unsupported versions: [12](/docs/12/protocol-overview.html "PostgreSQL 12 -
55.1. Overview") / [11](/docs/11/protocol-overview.html "PostgreSQL 11 -
55.1. Overview") / [10](/docs/10/protocol-overview.html "PostgreSQL 10 -
55.1. Overview") / [9.6](/docs/9.6/protocol-overview.html "PostgreSQL 9.6 -
55.1. Overview") / [9.5](/docs/9.5/protocol-overview.html "PostgreSQL 9.5 -
55.1. Overview") / [9.4](/docs/9.4/protocol-overview.html "PostgreSQL 9.4 -
55.1. Overview") / [9.3](/docs/9.3/protocol-overview.html "PostgreSQL 9.3 -
55.1. Overview") / [9.2](/docs/9.2/protocol-overview.html "PostgreSQL 9.2 -
55.1. Overview") / [9.1](/docs/9.1/protocol-overview.html "PostgreSQL 9.1 -
55.1. Overview") / [9.0](/docs/9.0/protocol-overview.html "PostgreSQL 9.0 -
55.1. Overview") / [8.4](/docs/8.4/protocol-overview.html "PostgreSQL 8.4 -
55.1. Overview") / [8.3](/docs/8.3/protocol-overview.html "PostgreSQL 8.3 -
55.1. Overview") / [8.2](/docs/8.2/protocol-overview.html "PostgreSQL 8.2 -
55.1. Overview")

__

55.1. Overview  
---  
[Prev](protocol.html "Chapter 55. Frontend/Backend Protocol")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-flow.html "55.2. Message Flow")  
  
* * *

## 55.1. Overview #

[55.1.1. Messaging Overview](protocol-overview.html#PROTOCOL-MESSAGE-CONCEPTS)

[55.1.2. Extended Query Overview](protocol-overview.html#PROTOCOL-QUERY-
CONCEPTS)

[55.1.3. Formats and Format Codes](protocol-overview.html#PROTOCOL-FORMAT-
CODES)

The protocol has separate phases for startup and normal operation. In the
startup phase, the frontend opens a connection to the server and authenticates
itself to the satisfaction of the server. (This might involve a single
message, or multiple messages depending on the authentication method being
used.) If all goes well, the server then sends status information to the
frontend, and finally enters normal operation. Except for the initial startup-
request message, this part of the protocol is driven by the server.

During normal operation, the frontend sends queries and other commands to the
backend, and the backend sends back query results and other responses. There
are a few cases (such as `NOTIFY`) wherein the backend will send unsolicited
messages, but for the most part this portion of a session is driven by
frontend requests.

Termination of the session is normally by frontend choice, but can be forced
by the backend in certain cases. In any case, when the backend closes the
connection, it will roll back any open (incomplete) transaction before
exiting.

Within normal operation, SQL commands can be executed through either of two
sub-protocols. In the “simple query” protocol, the frontend just sends a
textual query string, which is parsed and immediately executed by the backend.
In the “extended query” protocol, processing of queries is separated into
multiple steps: parsing, binding of parameter values, and execution. This
offers flexibility and performance benefits, at the cost of extra complexity.

Normal operation has additional sub-protocols for special operations such as
`COPY`.

### 55.1.1. Messaging Overview #

All communication is through a stream of messages. The first byte of a message
identifies the message type, and the next four bytes specify the length of the
rest of the message (this length count includes itself, but not the message-
type byte). The remaining contents of the message are determined by the
message type. For historical reasons, the very first message sent by the
client (the startup message) has no initial message-type byte.

To avoid losing synchronization with the message stream, both servers and
clients typically read an entire message into a buffer (using the byte count)
before attempting to process its contents. This allows easy recovery if an
error is detected while processing the contents. In extreme situations (such
as not having enough memory to buffer the message), the receiver can use the
byte count to determine how much input to skip before it resumes reading
messages.

Conversely, both servers and clients must take care never to send an
incomplete message. This is commonly done by marshaling the entire message in
a buffer before beginning to send it. If a communications failure occurs
partway through sending or receiving a message, the only sensible response is
to abandon the connection, since there is little hope of recovering message-
boundary synchronization.

### 55.1.2. Extended Query Overview #

In the extended-query protocol, execution of SQL commands is divided into
multiple steps. The state retained between steps is represented by two types
of objects: _prepared statements_ and _portals_. A prepared statement
represents the result of parsing and semantic analysis of a textual query
string. A prepared statement is not in itself ready to execute, because it
might lack specific values for _parameters_. A portal represents a ready-to-
execute or already-partially-executed statement, with any missing parameter
values filled in. (For `SELECT` statements, a portal is equivalent to an open
cursor, but we choose to use a different term since cursors don't handle
non-`SELECT` statements.)

The overall execution cycle consists of a _parse_ step, which creates a
prepared statement from a textual query string; a _bind_ step, which creates a
portal given a prepared statement and values for any needed parameters; and an
_execute_ step that runs a portal's query. In the case of a query that returns
rows (`SELECT`, `SHOW`, etc.), the execute step can be told to fetch only a
limited number of rows, so that multiple execute steps might be needed to
complete the operation.

The backend can keep track of multiple prepared statements and portals (but
note that these exist only within a session, and are never shared across
sessions). Existing prepared statements and portals are referenced by names
assigned when they were created. In addition, an “unnamed” prepared statement
and portal exist. Although these behave largely the same as named objects,
operations on them are optimized for the case of executing a query only once
and then discarding it, whereas operations on named objects are optimized on
the expectation of multiple uses.

### 55.1.3. Formats and Format Codes #

Data of a particular data type might be transmitted in any of several
different _formats_. As of PostgreSQL 7.4 the only supported formats are
“text” and “binary”, but the protocol makes provision for future extensions.
The desired format for any value is specified by a _format code_. Clients can
specify a format code for each transmitted parameter value and for each column
of a query result. Text has format code zero, binary has format code one, and
all other format codes are reserved for future definition.

The text representation of values is whatever strings are produced and
accepted by the input/output conversion functions for the particular data
type. In the transmitted representation, there is no trailing null character;
the frontend must add one to received values if it wants to process them as C
strings. (The text format does not allow embedded nulls, by the way.)

Binary representations for integers use network byte order (most significant
byte first). For other data types consult the documentation or source code to
learn about the binary representation. Keep in mind that binary
representations for complex data types might change across server versions;
the text format is usually the more portable choice.

* * *

[Prev](protocol.html "Chapter 55. Frontend/Backend Protocol")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](protocol-flow.html "55.2. Message Flow")  
---|---|---  
Chapter 55. Frontend/Backend Protocol  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.2. Message Flow  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol-overview.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

