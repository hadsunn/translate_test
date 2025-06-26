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

Supported Versions: [Current](/docs/current/auth-pam.html "PostgreSQL 17 -
21.13. PAM Authentication") ([17](/docs/17/auth-pam.html "PostgreSQL 17 -
21.13. PAM Authentication")) / [16](/docs/16/auth-pam.html "PostgreSQL 16 -
21.13. PAM Authentication") / [15](/docs/15/auth-pam.html "PostgreSQL 15 -
21.13. PAM Authentication") / [14](/docs/14/auth-pam.html "PostgreSQL 14 -
21.13. PAM Authentication") / [13](/docs/13/auth-pam.html "PostgreSQL 13 -
21.13. PAM Authentication")

Development Versions: [18](/docs/18/auth-pam.html "PostgreSQL 18 - 21.13. PAM
Authentication") / [devel](/docs/devel/auth-pam.html "PostgreSQL devel -
21.13. PAM Authentication")

Unsupported versions: [12](/docs/12/auth-pam.html "PostgreSQL 12 - 21.13. PAM
Authentication") / [11](/docs/11/auth-pam.html "PostgreSQL 11 - 21.13. PAM
Authentication")

__

21.13. PAM Authentication  
---  
[Prev](auth-cert.html "21.12. Certificate Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-bsd.html "21.14. BSD Authentication")  
  
* * *

## 21.13. PAM Authentication #

This authentication method operates similarly to `password` except that it
uses PAM (Pluggable Authentication Modules) as the authentication mechanism.
The default PAM service name is `postgresql`. PAM is used only to validate
user name/password pairs and optionally the connected remote host name or IP
address. Therefore the user must already exist in the database before PAM can
be used for authentication. For more information about PAM, please read the
[Linux-PAM Page](https://www.kernel.org/pub/linux/libs/pam/).

The following configuration options are supported for PAM:

`pamservice`

    

PAM service name.

`pam_use_hostname`

    

Determines whether the remote IP address or the host name is provided to PAM
modules through the `PAM_RHOST` item. By default, the IP address is used. Set
this option to 1 to use the resolved host name instead. Host name resolution
can lead to login delays. (Most PAM configurations don't use this information,
so it is only necessary to consider this setting if a PAM configuration was
specifically created to make use of it.)

### Note

If PAM is set up to read `/etc/shadow`, authentication will fail because the
PostgreSQL server is started by a non-root user. However, this is not an issue
when PAM is configured to use LDAP or other authentication methods.

* * *

[Prev](auth-cert.html "21.12. Certificate Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-bsd.html "21.14. BSD Authentication")  
---|---|---  
21.12. Certificate Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.14. BSD Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-pam.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

