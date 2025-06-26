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

Supported Versions: [Current](/docs/current/protocol-logical-replication.html
"PostgreSQL 17 - 55.5. Logical Streaming Replication Protocol")
([17](/docs/17/protocol-logical-replication.html "PostgreSQL 17 -
55.5. Logical Streaming Replication Protocol")) / [16](/docs/16/protocol-
logical-replication.html "PostgreSQL 16 - 55.5. Logical Streaming Replication
Protocol") / [15](/docs/15/protocol-logical-replication.html "PostgreSQL 15 -
55.5. Logical Streaming Replication Protocol") / [14](/docs/14/protocol-
logical-replication.html "PostgreSQL 14 - 55.5. Logical Streaming Replication
Protocol") / [13](/docs/13/protocol-logical-replication.html "PostgreSQL 13 -
55.5. Logical Streaming Replication Protocol")

Development Versions: [18](/docs/18/protocol-logical-replication.html
"PostgreSQL 18 - 55.5. Logical Streaming Replication Protocol") /
[devel](/docs/devel/protocol-logical-replication.html "PostgreSQL devel -
55.5. Logical Streaming Replication Protocol")

Unsupported versions: [12](/docs/12/protocol-logical-replication.html
"PostgreSQL 12 - 55.5. Logical Streaming Replication Protocol") /
[11](/docs/11/protocol-logical-replication.html "PostgreSQL 11 - 55.5. Logical
Streaming Replication Protocol") / [10](/docs/10/protocol-logical-
replication.html "PostgreSQL 10 - 55.5. Logical Streaming Replication
Protocol")

__

55.5. Logical Streaming Replication Protocol  
---  
[Prev](protocol-replication.html "55.4. Streaming Replication Protocol")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-message-types.html "55.6. Message Data Types")  
  
* * *

## 55.5. Logical Streaming Replication Protocol #

[55.5.1. Logical Streaming Replication Parameters](protocol-logical-
replication.html#PROTOCOL-LOGICAL-REPLICATION-PARAMS)

[55.5.2. Logical Replication Protocol Messages](protocol-logical-
replication.html#PROTOCOL-LOGICAL-MESSAGES)

[55.5.3. Logical Replication Protocol Message Flow](protocol-logical-
replication.html#PROTOCOL-LOGICAL-MESSAGES-FLOW)

This section describes the logical replication protocol, which is the message
flow started by the `START_REPLICATION` `SLOT` _`slot_name`_ `LOGICAL`
replication command.

The logical streaming replication protocol builds on the primitives of the
physical streaming replication protocol.

PostgreSQL logical decoding supports output plugins. `pgoutput` is the
standard one used for the built-in logical replication.

### 55.5.1. Logical Streaming Replication Parameters #

Using the `START_REPLICATION` command, `pgoutput` accepts the following
options:

proto_version

    

Protocol version. Currently versions `1`, `2`, `3`, and `4` are supported. A
valid version is required.

Version `2` is supported only for server version 14 and above, and it allows
streaming of large in-progress transactions.

Version `3` is supported only for server version 15 and above, and it allows
streaming of two-phase commits.

Version `4` is supported only for server version 16 and above, and it allows
streams of large in-progress transactions to be applied in parallel.

publication_names

    

Comma separated list of publication names for which to subscribe (receive
changes). The individual publication names are treated as standard objects
names and can be quoted the same as needed. At least one publication name is
required.

binary

    

Boolean option to use binary transfer mode. Binary mode is faster than the
text mode but slightly less robust.

messages

    

Boolean option to enable sending the messages that are written by
`pg_logical_emit_message`.

streaming

    

Boolean option to enable streaming of in-progress transactions. It accepts an
additional value "parallel" to enable sending extra information with some
messages to be used for parallelisation. Minimum protocol version 2 is
required to turn it on. Minimum protocol version 4 is required for the
"parallel" option.

two_phase

    

Boolean option to enable two-phase transactions. Minimum protocol version 3 is
required to turn it on.

origin

    

Option to send changes by their origin. Possible values are "none" to only
send the changes that have no origin associated, or "any" to send the changes
regardless of their origin. This can be used to avoid loops (infinite
replication of the same data) among replication nodes.

### 55.5.2. Logical Replication Protocol Messages #

The individual protocol messages are discussed in the following subsections.
Individual messages are described in [Section 55.9](protocol-logicalrep-
message-formats.html "55.9. Logical Replication Message Formats").

All top-level protocol messages begin with a message type byte. While
represented in code as a character, this is a signed byte with no associated
encoding.

Since the streaming replication protocol supplies a message length there is no
need for top-level protocol messages to embed a length in their header.

### 55.5.3. Logical Replication Protocol Message Flow #

With the exception of the `START_REPLICATION` command and the replay progress
messages, all information flows only from the backend to the frontend.

The logical replication protocol sends individual transactions one by one.
This means that all messages between a pair of Begin and Commit messages
belong to the same transaction. Similarly, all messages between a pair of
Begin Prepare and Prepare messages belong to the same transaction. It also
sends changes of large in-progress transactions between a pair of Stream Start
and Stream Stop messages. The last stream of such a transaction contains a
Stream Commit or Stream Abort message.

Every sent transaction contains zero or more DML messages (Insert, Update,
Delete). In case of a cascaded setup it can also contain Origin messages. The
origin message indicates that the transaction originated on different
replication node. Since a replication node in the scope of logical replication
protocol can be pretty much anything, the only identifier is the origin name.
It's downstream's responsibility to handle this as needed (if needed). The
Origin message is always sent before any DML messages in the transaction.

Every DML message contains a relation OID, identifying the publisher's
relation that was acted on. Before the first DML message for a given relation
OID, a Relation message will be sent, describing the schema of that relation.
Subsequently, a new Relation message will be sent if the relation's definition
has changed since the last Relation message was sent for it. (The protocol
assumes that the client is capable of remembering this metadata for as many
relations as needed.)

Relation messages identify column types by their OIDs. In the case of a built-
in type, it is assumed that the client can look up that type OID locally, so
no additional data is needed. For a non-built-in type OID, a Type message will
be sent before the Relation message, to provide the type name associated with
that OID. Thus, a client that needs to specifically identify the types of
relation columns should cache the contents of Type messages, and first consult
that cache to see if the type OID is defined there. If not, look up the type
OID locally.

* * *

[Prev](protocol-replication.html "55.4. Streaming Replication Protocol")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](protocol-message-types.html "55.6. Message Data Types")  
---|---|---  
55.4. Streaming Replication Protocol  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.6. Message Data Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol-logical-
replication.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

