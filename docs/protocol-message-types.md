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

Supported Versions: [Current](/docs/current/protocol-message-types.html
"PostgreSQL 17 - 55.6. Message Data Types") ([17](/docs/17/protocol-message-
types.html "PostgreSQL 17 - 55.6. Message Data Types")) /
[16](/docs/16/protocol-message-types.html "PostgreSQL 16 - 55.6. Message Data
Types") / [15](/docs/15/protocol-message-types.html "PostgreSQL 15 -
55.6. Message Data Types") / [14](/docs/14/protocol-message-types.html
"PostgreSQL 14 - 55.6. Message Data Types") / [13](/docs/13/protocol-message-
types.html "PostgreSQL 13 - 55.6. Message Data Types")

Development Versions: [18](/docs/18/protocol-message-types.html "PostgreSQL 18
- 55.6. Message Data Types") / [devel](/docs/devel/protocol-message-types.html
"PostgreSQL devel - 55.6. Message Data Types")

Unsupported versions: [12](/docs/12/protocol-message-types.html "PostgreSQL 12
- 55.6. Message Data Types") / [11](/docs/11/protocol-message-types.html
"PostgreSQL 11 - 55.6. Message Data Types") / [10](/docs/10/protocol-message-
types.html "PostgreSQL 10 - 55.6. Message Data Types") /
[9.6](/docs/9.6/protocol-message-types.html "PostgreSQL 9.6 - 55.6. Message
Data Types") / [9.5](/docs/9.5/protocol-message-types.html "PostgreSQL 9.5 -
55.6. Message Data Types") / [9.4](/docs/9.4/protocol-message-types.html
"PostgreSQL 9.4 - 55.6. Message Data Types") / [9.3](/docs/9.3/protocol-
message-types.html "PostgreSQL 9.3 - 55.6. Message Data Types") /
[9.2](/docs/9.2/protocol-message-types.html "PostgreSQL 9.2 - 55.6. Message
Data Types") / [9.1](/docs/9.1/protocol-message-types.html "PostgreSQL 9.1 -
55.6. Message Data Types") / [9.0](/docs/9.0/protocol-message-types.html
"PostgreSQL 9.0 - 55.6. Message Data Types") / [8.4](/docs/8.4/protocol-
message-types.html "PostgreSQL 8.4 - 55.6. Message Data Types") /
[8.3](/docs/8.3/protocol-message-types.html "PostgreSQL 8.3 - 55.6. Message
Data Types") / [8.2](/docs/8.2/protocol-message-types.html "PostgreSQL 8.2 -
55.6. Message Data Types") / [8.1](/docs/8.1/protocol-message-types.html
"PostgreSQL 8.1 - 55.6. Message Data Types") / [8.0](/docs/8.0/protocol-
message-types.html "PostgreSQL 8.0 - 55.6. Message Data Types") /
[7.4](/docs/7.4/protocol-message-types.html "PostgreSQL 7.4 - 55.6. Message
Data Types") / [7.3](/docs/7.3/protocol-message-types.html "PostgreSQL 7.3 -
55.6. Message Data Types") / [7.2](/docs/7.2/protocol-message-types.html
"PostgreSQL 7.2 - 55.6. Message Data Types") / [7.1](/docs/7.1/protocol-
message-types.html "PostgreSQL 7.1 - 55.6. Message Data Types")

__

55.6. Message Data Types  
---  
[Prev](protocol-logical-replication.html "55.5. Logical Streaming Replication Protocol")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-message-formats.html "55.7. Message Formats")  
  
* * *

## 55.6. Message Data Types #

This section describes the base data types used in messages.

Int _`n`_(_`i`_)

    

An _`n`_ -bit integer in network byte order (most significant byte first). If
_`i`_ is specified it is the exact value that will appear, otherwise the value
is variable. Eg. Int16, Int32(42).

Int _`n`_[_`k`_]

    

An array of _`k`_ _`n`_ -bit integers, each in network byte order. The array
length _`k`_ is always determined by an earlier field in the message. Eg.
Int16[M].

String(_`s`_)

    

A null-terminated string (C-style string). There is no specific length
limitation on strings. If _`s`_ is specified it is the exact value that will
appear, otherwise the value is variable. Eg. String, String("user").

### Note

_There is no predefined limit_ on the length of a string that can be returned
by the backend. Good coding strategy for a frontend is to use an expandable
buffer so that anything that fits in memory can be accepted. If that's not
feasible, read the full string and discard trailing characters that don't fit
into your fixed-size buffer.

Byte _`n`_(_`c`_)

    

Exactly _`n`_ bytes. If the field width _`n`_ is not a constant, it is always
determinable from an earlier field in the message. If _`c`_ is specified it is
the exact value. Eg. Byte2, Byte1('\n').

* * *

[Prev](protocol-logical-replication.html "55.5. Logical Streaming Replication Protocol")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](protocol-message-formats.html "55.7. Message Formats")  
---|---|---  
55.5. Logical Streaming Replication Protocol  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.7. Message Formats  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/protocol-message-types.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

