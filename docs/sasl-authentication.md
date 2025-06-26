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

Supported Versions: [Current](/docs/current/sasl-authentication.html
"PostgreSQL 17 - 55.3. SASL Authentication") ([17](/docs/17/sasl-
authentication.html "PostgreSQL 17 - 55.3. SASL Authentication")) /
[16](/docs/16/sasl-authentication.html "PostgreSQL 16 - 55.3. SASL
Authentication") / [15](/docs/15/sasl-authentication.html "PostgreSQL 15 -
55.3. SASL Authentication") / [14](/docs/14/sasl-authentication.html
"PostgreSQL 14 - 55.3. SASL Authentication") / [13](/docs/13/sasl-
authentication.html "PostgreSQL 13 - 55.3. SASL Authentication")

Development Versions: [18](/docs/18/sasl-authentication.html "PostgreSQL 18 -
55.3. SASL Authentication") / [devel](/docs/devel/sasl-authentication.html
"PostgreSQL devel - 55.3. SASL Authentication")

Unsupported versions: [12](/docs/12/sasl-authentication.html "PostgreSQL 12 -
55.3. SASL Authentication") / [11](/docs/11/sasl-authentication.html
"PostgreSQL 11 - 55.3. SASL Authentication") / [10](/docs/10/sasl-
authentication.html "PostgreSQL 10 - 55.3. SASL Authentication")

__

55.3. SASL Authentication  
---  
[Prev](protocol-flow.html "55.2. Message Flow")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") | Chapter 55. Frontend/Backend Protocol | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol-replication.html "55.4. Streaming Replication Protocol")  
  
* * *

## 55.3. SASL Authentication #

[55.3.1. SCRAM-SHA-256 Authentication](sasl-authentication.html#SASL-SCRAM-
SHA-256)

_SASL_ is a framework for authentication in connection-oriented protocols. At
the moment, PostgreSQL implements two SASL authentication mechanisms, SCRAM-
SHA-256 and SCRAM-SHA-256-PLUS. More might be added in the future. The below
steps illustrate how SASL authentication is performed in general, while the
next subsection gives more details on SCRAM-SHA-256 and SCRAM-SHA-256-PLUS.

**SASL Authentication Message Flow**

  1. To begin a SASL authentication exchange, the server sends an AuthenticationSASL message. It includes a list of SASL authentication mechanisms that the server can accept, in the server's preferred order.

  2. The client selects one of the supported mechanisms from the list, and sends a SASLInitialResponse message to the server. The message includes the name of the selected mechanism, and an optional Initial Client Response, if the selected mechanism uses that.

  3. One or more server-challenge and client-response message will follow. Each server-challenge is sent in an AuthenticationSASLContinue message, followed by a response from client in a SASLResponse message. The particulars of the messages are mechanism specific.

  4. Finally, when the authentication exchange is completed successfully, the server sends an AuthenticationSASLFinal message, followed immediately by an AuthenticationOk message. The AuthenticationSASLFinal contains additional server-to-client data, whose content is particular to the selected authentication mechanism. If the authentication mechanism doesn't use additional data that's sent at completion, the AuthenticationSASLFinal message is not sent.

On error, the server can abort the authentication at any stage, and send an
ErrorMessage.

### 55.3.1. SCRAM-SHA-256 Authentication #

The implemented SASL mechanisms at the moment are `SCRAM-SHA-256` and its
variant with channel binding `SCRAM-SHA-256-PLUS`. They are described in
detail in [RFC 7677](https://datatracker.ietf.org/doc/html/rfc7677) and [RFC
5802](https://datatracker.ietf.org/doc/html/rfc5802).

When SCRAM-SHA-256 is used in PostgreSQL, the server will ignore the user name
that the client sends in the `client-first-message`. The user name that was
already sent in the startup message is used instead. PostgreSQL supports
multiple character encodings, while SCRAM dictates UTF-8 to be used for the
user name, so it might be impossible to represent the PostgreSQL user name in
UTF-8.

The SCRAM specification dictates that the password is also in UTF-8, and is
processed with the _SASLprep_ algorithm. PostgreSQL, however, does not require
UTF-8 to be used for the password. When a user's password is set, it is
processed with SASLprep as if it was in UTF-8, regardless of the actual
encoding used. However, if it is not a legal UTF-8 byte sequence, or it
contains UTF-8 byte sequences that are prohibited by the SASLprep algorithm,
the raw password will be used without SASLprep processing, instead of throwing
an error. This allows the password to be normalized when it is in UTF-8, but
still allows a non-UTF-8 password to be used, and doesn't require the system
to know which encoding the password is in.

_Channel binding_ is supported in PostgreSQL builds with SSL support. The SASL
mechanism name for SCRAM with channel binding is `SCRAM-SHA-256-PLUS`. The
channel binding type used by PostgreSQL is `tls-server-end-point`.

In SCRAM without channel binding, the server chooses a random number that is
transmitted to the client to be mixed with the user-supplied password in the
transmitted password hash. While this prevents the password hash from being
successfully retransmitted in a later session, it does not prevent a fake
server between the real server and client from passing through the server's
random value and successfully authenticating.

SCRAM with channel binding prevents such man-in-the-middle attacks by mixing
the signature of the server's certificate into the transmitted password hash.
While a fake server can retransmit the real server's certificate, it doesn't
have access to the private key matching that certificate, and therefore cannot
prove it is the owner, causing SSL connection failure.

**Example**

  1. The server sends an AuthenticationSASL message. It includes a list of SASL authentication mechanisms that the server can accept. This will be `SCRAM-SHA-256-PLUS` and `SCRAM-SHA-256` if the server is built with SSL support, or else just the latter.

  2. The client responds by sending a SASLInitialResponse message, which indicates the chosen mechanism, `SCRAM-SHA-256` or `SCRAM-SHA-256-PLUS`. (A client is free to choose either mechanism, but for better security it should choose the channel-binding variant if it can support it.) In the Initial Client response field, the message contains the SCRAM `client-first-message`. The `client-first-message` also contains the channel binding type chosen by the client.

  3. Server sends an AuthenticationSASLContinue message, with a SCRAM `server-first-message` as the content.

  4. Client sends a SASLResponse message, with SCRAM `client-final-message` as the content.

  5. Server sends an AuthenticationSASLFinal message, with the SCRAM `server-final-message`, followed immediately by an AuthenticationOk message.

* * *

[Prev](protocol-flow.html "55.2. Message Flow")  | [Up](protocol.html "Chapter 55. Frontend/Backend Protocol") |  [Next](protocol-replication.html "55.4. Streaming Replication Protocol")  
---|---|---  
55.2. Message Flow  | [Home](index.html "PostgreSQL 16.9 Documentation") |  55.4. Streaming Replication Protocol  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sasl-authentication.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

