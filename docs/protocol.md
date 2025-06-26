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

Supported Versions: [Current](/docs/current/protocol.html "PostgreSQL 17 -
Chapter 55. Frontend/Backend Protocol") ([17](/docs/17/protocol.html
"PostgreSQL 17 - Chapter 55. Frontend/Backend Protocol")) /
[16](/docs/16/protocol.html "PostgreSQL 16 - Chapter 55. Frontend/Backend
Protocol") / [15](/docs/15/protocol.html "PostgreSQL 15 -
Chapter 55. Frontend/Backend Protocol") / [14](/docs/14/protocol.html
"PostgreSQL 14 - Chapter 55. Frontend/Backend Protocol") /
[13](/docs/13/protocol.html "PostgreSQL 13 - Chapter 55. Frontend/Backend
Protocol")

Development Versions: [18](/docs/18/protocol.html "PostgreSQL 18 -
Chapter 55. Frontend/Backend Protocol") / [devel](/docs/devel/protocol.html
"PostgreSQL devel - Chapter 55. Frontend/Backend Protocol")

Unsupported versions: [12](/docs/12/protocol.html "PostgreSQL 12 -
Chapter 55. Frontend/Backend Protocol") / [11](/docs/11/protocol.html
"PostgreSQL 11 - Chapter 55. Frontend/Backend Protocol") /
[10](/docs/10/protocol.html "PostgreSQL 10 - Chapter 55. Frontend/Backend
Protocol") / [9.6](/docs/9.6/protocol.html "PostgreSQL 9.6 -
Chapter 55. Frontend/Backend Protocol") / [9.5](/docs/9.5/protocol.html
"PostgreSQL 9.5 - Chapter 55. Frontend/Backend Protocol") /
[9.4](/docs/9.4/protocol.html "PostgreSQL 9.4 - Chapter 55. Frontend/Backend
Protocol") / [9.3](/docs/9.3/protocol.html "PostgreSQL 9.3 -
Chapter 55. Frontend/Backend Protocol") / [9.2](/docs/9.2/protocol.html
"PostgreSQL 9.2 - Chapter 55. Frontend/Backend Protocol") /
[9.1](/docs/9.1/protocol.html "PostgreSQL 9.1 - Chapter 55. Frontend/Backend
Protocol") / [9.0](/docs/9.0/protocol.html "PostgreSQL 9.0 -
Chapter 55. Frontend/Backend Protocol") / [8.4](/docs/8.4/protocol.html
"PostgreSQL 8.4 - Chapter 55. Frontend/Backend Protocol") /
[8.3](/docs/8.3/protocol.html "PostgreSQL 8.3 - Chapter 55. Frontend/Backend
Protocol") / [8.2](/docs/8.2/protocol.html "PostgreSQL 8.2 -
Chapter 55. Frontend/Backend Protocol") / [8.1](/docs/8.1/protocol.html
"PostgreSQL 8.1 - Chapter 55. Frontend/Backend Protocol") /
[8.0](/docs/8.0/protocol.html "PostgreSQL 8.0 - Chapter 55. Frontend/Backend
Protocol") / [7.4](/docs/7.4/protocol.html "PostgreSQL 7.4 -
Chapter 55. Frontend/Backend Protocol") / [7.3](/docs/7.3/protocol.html
"PostgreSQL 7.3 - Chapter 55. Frontend/Backend Protocol") /
[7.2](/docs/7.2/protocol.html "PostgreSQL 7.2 - Chapter 55. Frontend/Backend
Protocol") / [7.1](/docs/7.1/protocol.html "PostgreSQL 7.1 -
Chapter 55. Frontend/Backend Protocol")

__

Chapter 55. Frontend/Backend Protocol  
---  
[Prev](view-pg-views.html "54.35. pg_views")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-overview.html "55.1. Overview")  
  
* * *

## Chapter 55. Frontend/Backend Protocol

**Table of Contents**

[55.1. Overview](protocol-overview.html)

    

[55.1.1. Messaging Overview](protocol-overview.html#PROTOCOL-MESSAGE-CONCEPTS)

[55.1.2. Extended Query Overview](protocol-overview.html#PROTOCOL-QUERY-
CONCEPTS)

[55.1.3. Formats and Format Codes](protocol-overview.html#PROTOCOL-FORMAT-
CODES)

[55.2. Message Flow](protocol-flow.html)

    

[55.2.1. Start-up](protocol-flow.html#PROTOCOL-FLOW-START-UP)

[55.2.2. Simple Query](protocol-flow.html#PROTOCOL-FLOW-SIMPLE-QUERY)

[55.2.3. Extended Query](protocol-flow.html#PROTOCOL-FLOW-EXT-QUERY)

[55.2.4. Pipelining](protocol-flow.html#PROTOCOL-FLOW-PIPELINING)

[55.2.5. Function Call](protocol-flow.html#PROTOCOL-FLOW-FUNCTION-CALL)

[55.2.6. COPY Operations](protocol-flow.html#PROTOCOL-COPY)

[55.2.7. Asynchronous Operations](protocol-flow.html#PROTOCOL-ASYNC)

[55.2.8. Canceling Requests in Progress](protocol-flow.html#PROTOCOL-FLOW-
CANCELING-REQUESTS)

[55.2.9. Termination](protocol-flow.html#PROTOCOL-FLOW-TERMINATION)

[55.2.10. SSL Session Encryption](protocol-flow.html#PROTOCOL-FLOW-SSL)

[55.2.11. GSSAPI Session Encryption](protocol-flow.html#PROTOCOL-FLOW-GSSAPI)

[55.3. SASL Authentication](sasl-authentication.html)

    

[55.3.1. SCRAM-SHA-256 Authentication](sasl-authentication.html#SASL-SCRAM-
SHA-256)

[55.4. Streaming Replication Protocol](protocol-replication.html)

[55.5. Logical Streaming Replication Protocol](protocol-logical-
replication.html)

    

[55.5.1. Logical Streaming Replication Parameters](protocol-logical-
replication.html#PROTOCOL-LOGICAL-REPLICATION-PARAMS)

[55.5.2. Logical Replication Protocol Messages](protocol-logical-
replication.html#PROTOCOL-LOGICAL-MESSAGES)

[55.5.3. Logical Replication Protocol Message Flow](protocol-logical-
replication.html#PROTOCOL-LOGICAL-MESSAGES-FLOW)

[55.6. Message Data Types](protocol-message-types.html)

[55.7. Message Formats](protocol-message-formats.html)

[55.8. Error and Notice Message Fields](protocol-error-fields.html)

[55.9. Logical Replication Message Formats](protocol-logicalrep-message-
formats.html)

[55.10. Summary of Changes since Protocol 2.0](protocol-changes.html)

PostgreSQL uses a message-based protocol for communication between frontends
and backends (clients and servers). The protocol is supported over TCP/IP and
also over Unix-domain sockets. Port number 5432 has been registered with IANA
as the customary TCP port number for servers supporting this protocol, but in
practice any non-privileged port number can be used.

This document describes version 3.0 of the protocol, implemented in PostgreSQL
7.4 and later. For descriptions of the earlier protocol versions, see previous
releases of the PostgreSQL documentation. A single server can support multiple
protocol versions. The initial startup-request message tells the server which
protocol version the client is attempting to use. If the major version
requested by the client is not supported by the server, the connection will be
rejected (for example, this would occur if the client requested protocol
version 4.0, which does not exist as of this writing). If the minor version
requested by the client is not supported by the server (e.g., the client
requests version 3.1, but the server supports only 3.0), the server may either
reject the connection or may respond with a NegotiateProtocolVersion message
containing the highest minor protocol version which it supports. The client
may then choose either to continue with the connection using the specified
protocol version or to abort the connection.

In order to serve multiple clients efficiently, the server launches a new
“backend” process for each client. In the current implementation, a new child
process is created immediately after an incoming connection is detected. This
is transparent to the protocol, however. For purposes of the protocol, the
terms “backend” and “server” are interchangeable; likewise “frontend” and
“client” are interchangeable.

* * *

[Prev](view-pg-views.html "54.35. pg_views")  | [Up](internals.html "Part VII. Internals") |  [Next](protocol-overview.html "55.1. Overview")  
---|---|---  
54.35. `pg_views`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.1. Overview  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

