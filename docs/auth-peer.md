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

Supported Versions: [Current](/docs/current/auth-peer.html "PostgreSQL 17 -
21.9. Peer Authentication") ([17](/docs/17/auth-peer.html "PostgreSQL 17 -
21.9. Peer Authentication")) / [16](/docs/16/auth-peer.html "PostgreSQL 16 -
21.9. Peer Authentication") / [15](/docs/15/auth-peer.html "PostgreSQL 15 -
21.9. Peer Authentication") / [14](/docs/14/auth-peer.html "PostgreSQL 14 -
21.9. Peer Authentication") / [13](/docs/13/auth-peer.html "PostgreSQL 13 -
21.9. Peer Authentication")

Development Versions: [18](/docs/18/auth-peer.html "PostgreSQL 18 - 21.9. Peer
Authentication") / [devel](/docs/devel/auth-peer.html "PostgreSQL devel -
21.9. Peer Authentication")

Unsupported versions: [12](/docs/12/auth-peer.html "PostgreSQL 12 - 21.9. Peer
Authentication") / [11](/docs/11/auth-peer.html "PostgreSQL 11 - 21.9. Peer
Authentication")

__

21.9. Peer Authentication  
---  
[Prev](auth-ident.html "21.8. Ident Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-ldap.html "21.10. LDAP Authentication")  
  
* * *

## 21.9. Peer Authentication #

The peer authentication method works by obtaining the client's operating
system user name from the kernel and using it as the allowed database user
name (with optional user name mapping). This method is only supported on local
connections.

The following configuration options are supported for `peer`:

`map`

    

Allows for mapping between system and database user names. See [Section
21.2](auth-username-maps.html "21.2. User Name Maps") for details.

Peer authentication is only available on operating systems providing the
`getpeereid()` function, the `SO_PEERCRED` socket parameter, or similar
mechanisms. Currently that includes Linux, most flavors of BSD including
macOS, and Solaris.

* * *

[Prev](auth-ident.html "21.8. Ident Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-ldap.html "21.10. LDAP Authentication")  
---|---|---  
21.8. Ident Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.10. LDAP Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-peer.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

