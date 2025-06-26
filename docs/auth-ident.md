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

Supported Versions: [Current](/docs/current/auth-ident.html "PostgreSQL 17 -
21.8. Ident Authentication") ([17](/docs/17/auth-ident.html "PostgreSQL 17 -
21.8. Ident Authentication")) / [16](/docs/16/auth-ident.html "PostgreSQL 16 -
21.8. Ident Authentication") / [15](/docs/15/auth-ident.html "PostgreSQL 15 -
21.8. Ident Authentication") / [14](/docs/14/auth-ident.html "PostgreSQL 14 -
21.8. Ident Authentication") / [13](/docs/13/auth-ident.html "PostgreSQL 13 -
21.8. Ident Authentication")

Development Versions: [18](/docs/18/auth-ident.html "PostgreSQL 18 -
21.8. Ident Authentication") / [devel](/docs/devel/auth-ident.html "PostgreSQL
devel - 21.8. Ident Authentication")

Unsupported versions: [12](/docs/12/auth-ident.html "PostgreSQL 12 -
21.8. Ident Authentication") / [11](/docs/11/auth-ident.html "PostgreSQL 11 -
21.8. Ident Authentication")

__

21.8. Ident Authentication  
---  
[Prev](sspi-auth.html "21.7. SSPI Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-peer.html "21.9. Peer Authentication")  
  
* * *

## 21.8. Ident Authentication #

The ident authentication method works by obtaining the client's operating
system user name from an ident server and using it as the allowed database
user name (with an optional user name mapping). This is only supported on
TCP/IP connections.

### Note

When ident is specified for a local (non-TCP/IP) connection, peer
authentication (see [Section 21.9](auth-peer.html "21.9. Peer
Authentication")) will be used instead.

The following configuration options are supported for `ident`:

`map`

    

Allows for mapping between system and database user names. See [Section
21.2](auth-username-maps.html "21.2. User Name Maps") for details.

The “Identification Protocol” is described in [RFC
1413](https://datatracker.ietf.org/doc/html/rfc1413). Virtually every Unix-
like operating system ships with an ident server that listens on TCP port 113
by default. The basic functionality of an ident server is to answer questions
like “What user initiated the connection that goes out of your port _`X`_ and
connects to my port _`Y`_?”. Since PostgreSQL knows both _`X`_ and _`Y`_ when
a physical connection is established, it can interrogate the ident server on
the host of the connecting client and can theoretically determine the
operating system user for any given connection.

The drawback of this procedure is that it depends on the integrity of the
client: if the client machine is untrusted or compromised, an attacker could
run just about any program on port 113 and return any user name they choose.
This authentication method is therefore only appropriate for closed networks
where each client machine is under tight control and where the database and
system administrators operate in close contact. In other words, you must trust
the machine running the ident server. Heed the warning:

  |  The Identification Protocol is not intended as an authorization or access control protocol. |    
---|---|---  
  | \--RFC 1413  
  
Some ident servers have a nonstandard option that causes the returned user
name to be encrypted, using a key that only the originating machine's
administrator knows. This option _must not_ be used when using the ident
server with PostgreSQL, since PostgreSQL does not have any way to decrypt the
returned string to determine the actual user name.

* * *

[Prev](sspi-auth.html "21.7. SSPI Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-peer.html "21.9. Peer Authentication")  
---|---|---  
21.7. SSPI Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.9. Peer Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-ident.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

