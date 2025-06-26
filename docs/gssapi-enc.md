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

Supported Versions: [Current](/docs/current/gssapi-enc.html "PostgreSQL 17 -
19.10. Secure TCP/IP Connections with GSSAPI Encryption")
([17](/docs/17/gssapi-enc.html "PostgreSQL 17 - 19.10. Secure TCP/IP
Connections with GSSAPI Encryption")) / [16](/docs/16/gssapi-enc.html
"PostgreSQL 16 - 19.10. Secure TCP/IP Connections with GSSAPI Encryption") /
[15](/docs/15/gssapi-enc.html "PostgreSQL 15 - 19.10. Secure TCP/IP
Connections with GSSAPI Encryption") / [14](/docs/14/gssapi-enc.html
"PostgreSQL 14 - 19.10. Secure TCP/IP Connections with GSSAPI Encryption") /
[13](/docs/13/gssapi-enc.html "PostgreSQL 13 - 19.10. Secure TCP/IP
Connections with GSSAPI Encryption")

Development Versions: [18](/docs/18/gssapi-enc.html "PostgreSQL 18 -
19.10. Secure TCP/IP Connections with GSSAPI Encryption") /
[devel](/docs/devel/gssapi-enc.html "PostgreSQL devel - 19.10. Secure TCP/IP
Connections with GSSAPI Encryption")

Unsupported versions: [12](/docs/12/gssapi-enc.html "PostgreSQL 12 -
19.10. Secure TCP/IP Connections with GSSAPI Encryption")

__

19.10. Secure TCP/IP Connections with GSSAPI Encryption  
---  
[Prev](ssl-tcp.html "19.9. Secure TCP/IP Connections with SSL")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ssh-tunnels.html "19.11. Secure TCP/IP Connections with SSH Tunnels")  
  
* * *

## 19.10. Secure TCP/IP Connections with GSSAPI Encryption #

[19.10.1. Basic Setup](gssapi-enc.html#GSSAPI-SETUP)

PostgreSQL also has native support for using GSSAPI to encrypt client/server
communications for increased security. Support requires that a GSSAPI
implementation (such as MIT Kerberos) is installed on both client and server
systems, and that support in PostgreSQL is enabled at build time (see [Chapter
17](installation.html "Chapter 17. Installation from Source Code")).

### 19.10.1. Basic Setup #

The PostgreSQL server will listen for both normal and GSSAPI-encrypted
connections on the same TCP port, and will negotiate with any connecting
client whether to use GSSAPI for encryption (and for authentication). By
default, this decision is up to the client (which means it can be downgraded
by an attacker); see [Section 21.1](auth-pg-hba-conf.html "21.1. The
pg_hba.conf File") about setting up the server to require the use of GSSAPI
for some or all connections.

When using GSSAPI for encryption, it is common to use GSSAPI for
authentication as well, since the underlying mechanism will determine both
client and server identities (according to the GSSAPI implementation) in any
case. But this is not required; another PostgreSQL authentication method can
be chosen to perform additional verification.

Other than configuration of the negotiation behavior, GSSAPI encryption
requires no setup beyond that which is necessary for GSSAPI authentication.
(For more information on configuring that, see [Section 21.6](gssapi-auth.html
"21.6. GSSAPI Authentication").)

* * *

[Prev](ssl-tcp.html "19.9. Secure TCP/IP Connections with SSL")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](ssh-tunnels.html "19.11. Secure TCP/IP Connections with SSH Tunnels")  
---|---|---  
19.9. Secure TCP/IP Connections with SSL  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.11. Secure TCP/IP Connections with SSH Tunnels  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gssapi-enc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

