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

Supported Versions: [Current](/docs/current/auth-cert.html "PostgreSQL 17 -
21.12. Certificate Authentication") ([17](/docs/17/auth-cert.html "PostgreSQL
17 - 21.12. Certificate Authentication")) / [16](/docs/16/auth-cert.html
"PostgreSQL 16 - 21.12. Certificate Authentication") / [15](/docs/15/auth-
cert.html "PostgreSQL 15 - 21.12. Certificate Authentication") /
[14](/docs/14/auth-cert.html "PostgreSQL 14 - 21.12. Certificate
Authentication") / [13](/docs/13/auth-cert.html "PostgreSQL 13 -
21.12. Certificate Authentication")

Development Versions: [18](/docs/18/auth-cert.html "PostgreSQL 18 -
21.12. Certificate Authentication") / [devel](/docs/devel/auth-cert.html
"PostgreSQL devel - 21.12. Certificate Authentication")

Unsupported versions: [12](/docs/12/auth-cert.html "PostgreSQL 12 -
21.12. Certificate Authentication") / [11](/docs/11/auth-cert.html "PostgreSQL
11 - 21.12. Certificate Authentication")

__

21.12. Certificate Authentication  
---  
[Prev](auth-radius.html "21.11. RADIUS Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-pam.html "21.13. PAM Authentication")  
  
* * *

## 21.12. Certificate Authentication #

This authentication method uses SSL client certificates to perform
authentication. It is therefore only available for SSL connections; see
[Section 19.9.2](ssl-tcp.html#SSL-OPENSSL-CONFIG "19.9.2. OpenSSL
Configuration") for SSL configuration instructions. When using this
authentication method, the server will require that the client provide a
valid, trusted certificate. No password prompt will be sent to the client. The
`cn` (Common Name) attribute of the certificate will be compared to the
requested database user name, and if they match the login will be allowed.
User name mapping can be used to allow `cn` to be different from the database
user name.

The following configuration options are supported for SSL certificate
authentication:

`map`

    

Allows for mapping between system and database user names. See [Section
21.2](auth-username-maps.html "21.2. User Name Maps") for details.

It is redundant to use the `clientcert` option with `cert` authentication
because `cert` authentication is effectively `trust` authentication with
`clientcert=verify-full`.

* * *

[Prev](auth-radius.html "21.11. RADIUS Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-pam.html "21.13. PAM Authentication")  
---|---|---  
21.11. RADIUS Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.13. PAM Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-cert.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

