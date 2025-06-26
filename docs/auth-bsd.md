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

Supported Versions: [Current](/docs/current/auth-bsd.html "PostgreSQL 17 -
21.14. BSD Authentication") ([17](/docs/17/auth-bsd.html "PostgreSQL 17 -
21.14. BSD Authentication")) / [16](/docs/16/auth-bsd.html "PostgreSQL 16 -
21.14. BSD Authentication") / [15](/docs/15/auth-bsd.html "PostgreSQL 15 -
21.14. BSD Authentication") / [14](/docs/14/auth-bsd.html "PostgreSQL 14 -
21.14. BSD Authentication") / [13](/docs/13/auth-bsd.html "PostgreSQL 13 -
21.14. BSD Authentication")

Development Versions: [18](/docs/18/auth-bsd.html "PostgreSQL 18 - 21.14. BSD
Authentication") / [devel](/docs/devel/auth-bsd.html "PostgreSQL devel -
21.14. BSD Authentication")

Unsupported versions: [12](/docs/12/auth-bsd.html "PostgreSQL 12 - 21.14. BSD
Authentication") / [11](/docs/11/auth-bsd.html "PostgreSQL 11 - 21.14. BSD
Authentication")

__

21.14. BSD Authentication  
---  
[Prev](auth-pam.html "21.13. PAM Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](client-authentication-problems.html "21.15. Authentication Problems")  
  
* * *

## 21.14. BSD Authentication #

This authentication method operates similarly to `password` except that it
uses BSD Authentication to verify the password. BSD Authentication is used
only to validate user name/password pairs. Therefore the user's role must
already exist in the database before BSD Authentication can be used for
authentication. The BSD Authentication framework is currently only available
on OpenBSD.

BSD Authentication in PostgreSQL uses the `auth-postgresql` login type and
authenticates with the `postgresql` login class if that's defined in
`login.conf`. By default that login class does not exist, and PostgreSQL will
use the default login class.

### Note

To use BSD Authentication, the PostgreSQL user account (that is, the operating
system user running the server) must first be added to the `auth` group. The
`auth` group exists by default on OpenBSD systems.

* * *

[Prev](auth-pam.html "21.13. PAM Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](client-authentication-problems.html "21.15. Authentication Problems")  
---|---|---  
21.13. PAM Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.15. Authentication Problems  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-bsd.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

