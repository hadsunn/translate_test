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

Supported Versions: [Current](/docs/current/protocol-logicalrep-message-
formats.html "PostgreSQL 17 - 55.9. Logical Replication Message Formats")
([17](/docs/17/protocol-logicalrep-message-formats.html "PostgreSQL 17 -
55.9. Logical Replication Message Formats")) / [16](/docs/16/protocol-
logicalrep-message-formats.html "PostgreSQL 16 - 55.9. Logical Replication
Message Formats") / [15](/docs/15/protocol-logicalrep-message-formats.html
"PostgreSQL 15 - 55.9. Logical Replication Message Formats") /
[14](/docs/14/protocol-logicalrep-message-formats.html "PostgreSQL 14 -
55.9. Logical Replication Message Formats") / [13](/docs/13/protocol-
logicalrep-message-formats.html "PostgreSQL 13 - 55.9. Logical Replication
Message Formats")

Development Versions: [18](/docs/18/protocol-logicalrep-message-formats.html
"PostgreSQL 18 - 55.9. Logical Replication Message Formats") /
[devel](/docs/devel/protocol-logicalrep-message-formats.html "PostgreSQL devel
- 55.9. Logical Replication Message Formats")

Unsupported versions: [12](/docs/12/protocol-logicalrep-message-formats.html
"PostgreSQL 12 - 55.9. Logical Replication Message Formats") /
[11](/docs/11/protocol-logicalrep-message-formats.html "PostgreSQL 11 -
55.9. Logical Replication Message Formats") / [10](/docs/10/protocol-
logicalrep-message-formats.html "PostgreSQL 10 - 55.9. Logical Replication
Message Formats")

__

55.9. Logical Replication Message Formats  
---  
[Prev](protocol-error-fields.html "55.8. Error and Notice Message Fields")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-changes.html "55.10. Summary of Changes since Protocol 2.0")  
  
* * *

## 55.9. Logical Replication Message Formats #

This section describes the detailed format of each logical replication
message. These messages are either returned by the replication slot SQL
interface or are sent by a walsender. In the case of a walsender, they are
encapsulated inside replication protocol WAL messages as described in [Section
55.4](protocol-replication.html "55.4. Streaming Replication Protocol"), and
generally obey the same message flow as physical replication.

Begin #

    

Byte1('B')

    

Identifies the message as a begin message.

Int64 (XLogRecPtr)

    

The final LSN of the transaction.

Int64 (TimestampTz)

    

Commit timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int32 (TransactionId)

    

Xid of the transaction.

Message #

    

Byte1('M')

    

Identifies the message as a logical decoding message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int8

    

Flags; Either 0 for no flags or 1 if the logical decoding message is
transactional.

Int64 (XLogRecPtr)

    

The LSN of the logical decoding message.

String

    

The prefix of the logical decoding message.

Int32

    

Length of the content.

Byte _`n`_

    

The content of the logical decoding message.

Commit #

    

Byte1('C')

    

Identifies the message as a commit message.

Int8(0)

    

Flags; currently unused.

Int64 (XLogRecPtr)

    

The LSN of the commit.

Int64 (XLogRecPtr)

    

The end LSN of the transaction.

Int64 (TimestampTz)

    

Commit timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Origin #

    

Byte1('O')

    

Identifies the message as an origin message.

Int64 (XLogRecPtr)

    

The LSN of the commit on the origin server.

String

    

Name of the origin.

Note that there can be multiple Origin messages inside a single transaction.

Relation #

    

Byte1('R')

    

Identifies the message as a relation message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int32 (Oid)

    

OID of the relation.

String

    

Namespace (empty string for `pg_catalog`).

String

    

Relation name.

Int8

    

Replica identity setting for the relation (same as `relreplident` in
`pg_class`).

Int16

    

Number of columns.

Next, the following message part appears for each column included in the
publication (except generated columns):

Int8

    

Flags for the column. Currently can be either 0 for no flags or 1 which marks
the column as part of the key.

String

    

Name of the column.

Int32 (Oid)

    

OID of the column's data type.

Int32

    

Type modifier of the column (`atttypmod`).

Type #

    

Byte1('Y')

    

Identifies the message as a type message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int32 (Oid)

    

OID of the data type.

String

    

Namespace (empty string for `pg_catalog`).

String

    

Name of the data type.

Insert #

    

Byte1('I')

    

Identifies the message as an insert message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int32 (Oid)

    

OID of the relation corresponding to the ID in the relation message.

Byte1('N')

    

Identifies the following TupleData message as a new tuple.

TupleData

    

TupleData message part representing the contents of new tuple.

Update #

    

Byte1('U')

    

Identifies the message as an update message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int32 (Oid)

    

OID of the relation corresponding to the ID in the relation message.

Byte1('K')

    

Identifies the following TupleData submessage as a key. This field is optional
and is only present if the update changed data in any of the column(s) that
are part of the REPLICA IDENTITY index.

Byte1('O')

    

Identifies the following TupleData submessage as an old tuple. This field is
optional and is only present if table in which the update happened has REPLICA
IDENTITY set to FULL.

TupleData

    

TupleData message part representing the contents of the old tuple or primary
key. Only present if the previous 'O' or 'K' part is present.

Byte1('N')

    

Identifies the following TupleData message as a new tuple.

TupleData

    

TupleData message part representing the contents of a new tuple.

The Update message may contain either a 'K' message part or an 'O' message
part or neither of them, but never both of them.

Delete #

    

Byte1('D')

    

Identifies the message as a delete message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int32 (Oid)

    

OID of the relation corresponding to the ID in the relation message.

Byte1('K')

    

Identifies the following TupleData submessage as a key. This field is present
if the table in which the delete has happened uses an index as REPLICA
IDENTITY.

Byte1('O')

    

Identifies the following TupleData message as an old tuple. This field is
present if the table in which the delete happened has REPLICA IDENTITY set to
FULL.

TupleData

    

TupleData message part representing the contents of the old tuple or primary
key, depending on the previous field.

The Delete message may contain either a 'K' message part or an 'O' message
part, but never both of them.

Truncate #

    

Byte1('T')

    

Identifies the message as a truncate message.

Int32 (TransactionId)

    

Xid of the transaction (only present for streamed transactions). This field is
available since protocol version 2.

Int32

    

Number of relations

Int8

    

Option bits for `TRUNCATE`: 1 for `CASCADE`, 2 for `RESTART IDENTITY`

Int32 (Oid)

    

OID of the relation corresponding to the ID in the relation message. This
field is repeated for each relation.

The following messages (Stream Start, Stream Stop, Stream Commit, and Stream
Abort) are available since protocol version 2.

Stream Start #

    

Byte1('S')

    

Identifies the message as a stream start message.

Int32 (TransactionId)

    

Xid of the transaction.

Int8

    

A value of 1 indicates this is the first stream segment for this XID, 0 for
any other stream segment.

Stream Stop #

    

Byte1('E')

    

Identifies the message as a stream stop message.

Stream Commit #

    

Byte1('c')

    

Identifies the message as a stream commit message.

Int32 (TransactionId)

    

Xid of the transaction.

Int8(0)

    

Flags; currently unused.

Int64 (XLogRecPtr)

    

The LSN of the commit.

Int64 (XLogRecPtr)

    

The end LSN of the transaction.

Int64 (TimestampTz)

    

Commit timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Stream Abort #

    

Byte1('A')

    

Identifies the message as a stream abort message.

Int32 (TransactionId)

    

Xid of the transaction.

Int32 (TransactionId)

    

Xid of the subtransaction (will be same as xid of the transaction for top-
level transactions).

Int64 (XLogRecPtr)

    

The LSN of the abort. This field is available since protocol version 4.

Int64 (TimestampTz)

    

Abort timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01). This field is available since protocol
version 4.

The following messages (Begin Prepare, Prepare, Commit Prepared, Rollback
Prepared, Stream Prepare) are available since protocol version 3.

Begin Prepare #

    

Byte1('b')

    

Identifies the message as the beginning of a prepared transaction message.

Int64 (XLogRecPtr)

    

The LSN of the prepare.

Int64 (XLogRecPtr)

    

The end LSN of the prepared transaction.

Int64 (TimestampTz)

    

Prepare timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int32 (TransactionId)

    

Xid of the transaction.

String

    

The user defined GID of the prepared transaction.

Prepare #

    

Byte1('P')

    

Identifies the message as a prepared transaction message.

Int8(0)

    

Flags; currently unused.

Int64 (XLogRecPtr)

    

The LSN of the prepare.

Int64 (XLogRecPtr)

    

The end LSN of the prepared transaction.

Int64 (TimestampTz)

    

Prepare timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int32 (TransactionId)

    

Xid of the transaction.

String

    

The user defined GID of the prepared transaction.

Commit Prepared #

    

Byte1('K')

    

Identifies the message as the commit of a prepared transaction message.

Int8(0)

    

Flags; currently unused.

Int64 (XLogRecPtr)

    

The LSN of the commit of the prepared transaction.

Int64 (XLogRecPtr)

    

The end LSN of the commit of the prepared transaction.

Int64 (TimestampTz)

    

Commit timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int32 (TransactionId)

    

Xid of the transaction.

String

    

The user defined GID of the prepared transaction.

Rollback Prepared #

    

Byte1('r')

    

Identifies the message as the rollback of a prepared transaction message.

Int8(0)

    

Flags; currently unused.

Int64 (XLogRecPtr)

    

The end LSN of the prepared transaction.

Int64 (XLogRecPtr)

    

The end LSN of the rollback of the prepared transaction.

Int64 (TimestampTz)

    

Prepare timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int64 (TimestampTz)

    

Rollback timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int32 (TransactionId)

    

Xid of the transaction.

String

    

The user defined GID of the prepared transaction.

Stream Prepare #

    

Byte1('p')

    

Identifies the message as a stream prepared transaction message.

Int8(0)

    

Flags; currently unused.

Int64 (XLogRecPtr)

    

The LSN of the prepare.

Int64 (XLogRecPtr)

    

The end LSN of the prepared transaction.

Int64 (TimestampTz)

    

Prepare timestamp of the transaction. The value is in number of microseconds
since PostgreSQL epoch (2000-01-01).

Int32 (TransactionId)

    

Xid of the transaction.

String

    

The user defined GID of the prepared transaction.

The following message parts are shared by the above messages.

TupleData #

    

Int16

    

Number of columns.

Next, one of the following submessages appears for each column (except
generated columns):

Byte1('n')

    

Identifies the data as NULL value.

Or

Byte1('u')

    

Identifies unchanged TOASTed value (the actual value is not sent).

Or

Byte1('t')

    

Identifies the data as text formatted value.

Or

Byte1('b')

    

Identifies the data as binary formatted value.

Int32

    

Length of the column value.

Byte _`n`_

    

The value of the column, either in binary or in text format. (As specified in
the preceding format byte). _`n`_ is the above length.

* * *

[Prev](protocol-error-fields.html "55.8. Error and Notice Message Fields")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](protocol-changes.html "55.10. Summary of Changes since Protocol 2.0")  
---|---|---  
55.8. Error and Notice Message Fields  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.10. Summary of Changes since Protocol 2.0  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol-logicalrep-message-
formats.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

