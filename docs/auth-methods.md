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

Supported Versions: [Current](/docs/current/auth-methods.html "PostgreSQL 17 -
21.3. Authentication Methods") ([17](/docs/17/auth-methods.html "PostgreSQL 17
- 21.3. Authentication Methods")) / [16](/docs/16/auth-methods.html
"PostgreSQL 16 - 21.3. Authentication Methods") / [15](/docs/15/auth-
methods.html "PostgreSQL 15 - 21.3. Authentication Methods") /
[14](/docs/14/auth-methods.html "PostgreSQL 14 - 21.3. Authentication
Methods") / [13](/docs/13/auth-methods.html "PostgreSQL 13 -
21.3. Authentication Methods")

Development Versions: [18](/docs/18/auth-methods.html "PostgreSQL 18 -
21.3. Authentication Methods") / [devel](/docs/devel/auth-methods.html
"PostgreSQL devel - 21.3. Authentication Methods")

Unsupported versions: [12](/docs/12/auth-methods.html "PostgreSQL 12 -
21.3. Authentication Methods") / [11](/docs/11/auth-methods.html "PostgreSQL
11 - 21.3. Authentication Methods") / [10](/docs/10/auth-methods.html
"PostgreSQL 10 - 21.3. Authentication Methods") / [9.6](/docs/9.6/auth-
methods.html "PostgreSQL 9.6 - 21.3. Authentication Methods") /
[9.5](/docs/9.5/auth-methods.html "PostgreSQL 9.5 - 21.3. Authentication
Methods") / [9.4](/docs/9.4/auth-methods.html "PostgreSQL 9.4 -
21.3. Authentication Methods") / [9.3](/docs/9.3/auth-methods.html "PostgreSQL
9.3 - 21.3. Authentication Methods") / [9.2](/docs/9.2/auth-methods.html
"PostgreSQL 9.2 - 21.3. Authentication Methods") / [9.1](/docs/9.1/auth-
methods.html "PostgreSQL 9.1 - 21.3. Authentication Methods") /
[9.0](/docs/9.0/auth-methods.html "PostgreSQL 9.0 - 21.3. Authentication
Methods") / [8.4](/docs/8.4/auth-methods.html "PostgreSQL 8.4 -
21.3. Authentication Methods") / [8.3](/docs/8.3/auth-methods.html "PostgreSQL
8.3 - 21.3. Authentication Methods") / [8.2](/docs/8.2/auth-methods.html
"PostgreSQL 8.2 - 21.3. Authentication Methods") / [8.1](/docs/8.1/auth-
methods.html "PostgreSQL 8.1 - 21.3. Authentication Methods") /
[8.0](/docs/8.0/auth-methods.html "PostgreSQL 8.0 - 21.3. Authentication
Methods") / [7.4](/docs/7.4/auth-methods.html "PostgreSQL 7.4 -
21.3. Authentication Methods") / [7.3](/docs/7.3/auth-methods.html "PostgreSQL
7.3 - 21.3. Authentication Methods") / [7.2](/docs/7.2/auth-methods.html
"PostgreSQL 7.2 - 21.3. Authentication Methods") / [7.1](/docs/7.1/auth-
methods.html "PostgreSQL 7.1 - 21.3. Authentication Methods")

__

21.3. Authentication Methods  
---  
[Prev](auth-username-maps.html "21.2. User Name Maps")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-trust.html "21.4. Trust Authentication")  
  
* * *

## 21.3. Authentication Methods #

PostgreSQL provides various methods for authenticating users:

  * [Trust authentication](auth-trust.html "21.4. Trust Authentication"), which simply trusts that users are who they say they are.

  * [Password authentication](auth-password.html "21.5. Password Authentication"), which requires that users send a password.

  * [GSSAPI authentication](gssapi-auth.html "21.6. GSSAPI Authentication"), which relies on a GSSAPI-compatible security library. Typically this is used to access an authentication server such as a Kerberos or Microsoft Active Directory server.

  * [SSPI authentication](sspi-auth.html "21.7. SSPI Authentication"), which uses a Windows-specific protocol similar to GSSAPI.

  * [Ident authentication](auth-ident.html "21.8. Ident Authentication"), which relies on an “Identification Protocol” ([RFC 1413](https://datatracker.ietf.org/doc/html/rfc1413)) service on the client's machine. (On local Unix-socket connections, this is treated as peer authentication.)

  * [Peer authentication](auth-peer.html "21.9. Peer Authentication"), which relies on operating system facilities to identify the process at the other end of a local connection. This is not supported for remote connections.

  * [LDAP authentication](auth-ldap.html "21.10. LDAP Authentication"), which relies on an LDAP authentication server.

  * [RADIUS authentication](auth-radius.html "21.11. RADIUS Authentication"), which relies on a RADIUS authentication server.

  * [Certificate authentication](auth-cert.html "21.12. Certificate Authentication"), which requires an SSL connection and authenticates users by checking the SSL certificate they send.

  * [PAM authentication](auth-pam.html "21.13. PAM Authentication"), which relies on a PAM (Pluggable Authentication Modules) library.

  * [BSD authentication](auth-bsd.html "21.14. BSD Authentication"), which relies on the BSD Authentication framework (currently available only on OpenBSD).

Peer authentication is usually recommendable for local connections, though
trust authentication might be sufficient in some circumstances. Password
authentication is the easiest choice for remote connections. All the other
options require some kind of external security infrastructure (usually an
authentication server or a certificate authority for issuing SSL
certificates), or are platform-specific.

The following sections describe each of these authentication methods in more
detail.

* * *

[Prev](auth-username-maps.html "21.2. User Name Maps")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-trust.html "21.4. Trust Authentication")  
---|---|---  
21.2. User Name Maps  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.4. Trust Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-methods.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

