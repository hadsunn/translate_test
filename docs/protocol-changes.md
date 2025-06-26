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

Supported Versions: [Current](/docs/current/protocol-changes.html "PostgreSQL
17 - 55.10. Summary of Changes since Protocol 2.0") ([17](/docs/17/protocol-
changes.html "PostgreSQL 17 - 55.10. Summary of Changes since Protocol 2.0"))
/ [16](/docs/16/protocol-changes.html "PostgreSQL 16 - 55.10. Summary of
Changes since Protocol 2.0") / [15](/docs/15/protocol-changes.html "PostgreSQL
15 - 55.10. Summary of Changes since Protocol 2.0") / [14](/docs/14/protocol-
changes.html "PostgreSQL 14 - 55.10. Summary of Changes since Protocol 2.0") /
[13](/docs/13/protocol-changes.html "PostgreSQL 13 - 55.10. Summary of Changes
since Protocol 2.0")

Development Versions: [18](/docs/18/protocol-changes.html "PostgreSQL 18 -
55.10. Summary of Changes since Protocol 2.0") / [devel](/docs/devel/protocol-
changes.html "PostgreSQL devel - 55.10. Summary of Changes since Protocol
2.0")

Unsupported versions: [12](/docs/12/protocol-changes.html "PostgreSQL 12 -
55.10. Summary of Changes since Protocol 2.0") / [11](/docs/11/protocol-
changes.html "PostgreSQL 11 - 55.10. Summary of Changes since Protocol 2.0") /
[10](/docs/10/protocol-changes.html "PostgreSQL 10 - 55.10. Summary of Changes
since Protocol 2.0") / [9.6](/docs/9.6/protocol-changes.html "PostgreSQL 9.6 -
55.10. Summary of Changes since Protocol 2.0") / [9.5](/docs/9.5/protocol-
changes.html "PostgreSQL 9.5 - 55.10. Summary of Changes since Protocol 2.0")
/ [9.4](/docs/9.4/protocol-changes.html "PostgreSQL 9.4 - 55.10. Summary of
Changes since Protocol 2.0") / [9.3](/docs/9.3/protocol-changes.html
"PostgreSQL 9.3 - 55.10. Summary of Changes since Protocol 2.0") /
[9.2](/docs/9.2/protocol-changes.html "PostgreSQL 9.2 - 55.10. Summary of
Changes since Protocol 2.0") / [9.1](/docs/9.1/protocol-changes.html
"PostgreSQL 9.1 - 55.10. Summary of Changes since Protocol 2.0") /
[9.0](/docs/9.0/protocol-changes.html "PostgreSQL 9.0 - 55.10. Summary of
Changes since Protocol 2.0") / [8.4](/docs/8.4/protocol-changes.html
"PostgreSQL 8.4 - 55.10. Summary of Changes since Protocol 2.0") /
[8.3](/docs/8.3/protocol-changes.html "PostgreSQL 8.3 - 55.10. Summary of
Changes since Protocol 2.0") / [8.2](/docs/8.2/protocol-changes.html
"PostgreSQL 8.2 - 55.10. Summary of Changes since Protocol 2.0") /
[8.1](/docs/8.1/protocol-changes.html "PostgreSQL 8.1 - 55.10. Summary of
Changes since Protocol 2.0") / [8.0](/docs/8.0/protocol-changes.html
"PostgreSQL 8.0 - 55.10. Summary of Changes since Protocol 2.0") /
[7.4](/docs/7.4/protocol-changes.html "PostgreSQL 7.4 - 55.10. Summary of
Changes since Protocol 2.0")

__

55.10. Summary of Changes since Protocol 2.0  
---  
[Prev](protocol-logicalrep-message-formats.html "55.9. Logical Replication Message Formats")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](source.html "Chapter 56. PostgreSQL Coding Conventions")  
  
* * *

## 55.10. Summary of Changes since Protocol 2.0 #

This section provides a quick checklist of changes, for the benefit of
developers trying to update existing client libraries to protocol 3.0.

The initial startup packet uses a flexible list-of-strings format instead of a
fixed format. Notice that session default values for run-time parameters can
now be specified directly in the startup packet. (Actually, you could do that
before using the `options` field, but given the limited width of `options` and
the lack of any way to quote whitespace in the values, it wasn't a very safe
technique.)

All messages now have a length count immediately following the message type
byte (except for startup packets, which have no type byte). Also note that
PasswordMessage now has a type byte.

ErrorResponse and NoticeResponse ('`E`' and '`N`') messages now contain
multiple fields, from which the client code can assemble an error message of
the desired level of verbosity. Note that individual fields will typically not
end with a newline, whereas the single string sent in the older protocol
always did.

The ReadyForQuery ('`Z`') message includes a transaction status indicator.

The distinction between BinaryRow and DataRow message types is gone; the
single DataRow message type serves for returning data in all formats. Note
that the layout of DataRow has changed to make it easier to parse. Also, the
representation of binary values has changed: it is no longer directly tied to
the server's internal representation.

There is a new “extended query” sub-protocol, which adds the frontend message
types Parse, Bind, Execute, Describe, Close, Flush, and Sync, and the backend
message types ParseComplete, BindComplete, PortalSuspended,
ParameterDescription, NoData, and CloseComplete. Existing clients do not have
to concern themselves with this sub-protocol, but making use of it might allow
improvements in performance or functionality.

`COPY` data is now encapsulated into CopyData and CopyDone messages. There is
a well-defined way to recover from errors during `COPY`. The special “`\.`”
last line is not needed anymore, and is not sent during `COPY OUT`. (It is
still recognized as a terminator during `COPY IN`, but its use is deprecated
and will eventually be removed.) Binary `COPY` is supported. The
CopyInResponse and CopyOutResponse messages include fields indicating the
number of columns and the format of each column.

The layout of FunctionCall and FunctionCallResponse messages has changed.
FunctionCall can now support passing NULL arguments to functions. It also can
handle passing parameters and retrieving results in either text or binary
format. There is no longer any reason to consider FunctionCall a potential
security hole, since it does not offer direct access to internal server data
representations.

The backend sends ParameterStatus ('`S`') messages during connection startup
for all parameters it considers interesting to the client library.
Subsequently, a ParameterStatus message is sent whenever the active value
changes for any of these parameters.

The RowDescription ('`T`') message carries new table OID and column number
fields for each column of the described row. It also shows the format code for
each column.

The CursorResponse ('`P`') message is no longer generated by the backend.

The NotificationResponse ('`A`') message has an additional string field, which
can carry a “payload” string passed from the `NOTIFY` event sender.

The EmptyQueryResponse ('`I`') message used to include an empty string
parameter; this has been removed.

* * *

[Prev](protocol-logicalrep-message-formats.html "55.9. Logical Replication Message Formats")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](source.html "Chapter 56. PostgreSQL Coding Conventions")  
---|---|---  
55.9. Logical Replication Message Formats  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 56. PostgreSQL Coding Conventions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol-changes.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

