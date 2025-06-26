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

Supported Versions: [Current](/docs/current/auth-radius.html "PostgreSQL 17 -
21.11. RADIUS Authentication") ([17](/docs/17/auth-radius.html "PostgreSQL 17
- 21.11. RADIUS Authentication")) / [16](/docs/16/auth-radius.html "PostgreSQL
16 - 21.11. RADIUS Authentication") / [15](/docs/15/auth-radius.html
"PostgreSQL 15 - 21.11. RADIUS Authentication") / [14](/docs/14/auth-
radius.html "PostgreSQL 14 - 21.11. RADIUS Authentication") /
[13](/docs/13/auth-radius.html "PostgreSQL 13 - 21.11. RADIUS Authentication")

Development Versions: [18](/docs/18/auth-radius.html "PostgreSQL 18 -
21.11. RADIUS Authentication") / [devel](/docs/devel/auth-radius.html
"PostgreSQL devel - 21.11. RADIUS Authentication")

Unsupported versions: [12](/docs/12/auth-radius.html "PostgreSQL 12 -
21.11. RADIUS Authentication") / [11](/docs/11/auth-radius.html "PostgreSQL 11
- 21.11. RADIUS Authentication")

__

21.11. RADIUS Authentication  
---  
[Prev](auth-ldap.html "21.10. LDAP Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-cert.html "21.12. Certificate Authentication")  
  
* * *

## 21.11. RADIUS Authentication #

This authentication method operates similarly to `password` except that it
uses RADIUS as the password verification method. RADIUS is used only to
validate the user name/password pairs. Therefore the user must already exist
in the database before RADIUS can be used for authentication.

When using RADIUS authentication, an Access Request message will be sent to
the configured RADIUS server. This request will be of type `Authenticate
Only`, and include parameters for `user name`, `password` (encrypted) and `NAS
Identifier`. The request will be encrypted using a secret shared with the
server. The RADIUS server will respond to this request with either `Access
Accept` or `Access Reject`. There is no support for RADIUS accounting.

Multiple RADIUS servers can be specified, in which case they will be tried
sequentially. If a negative response is received from a server, the
authentication will fail. If no response is received, the next server in the
list will be tried. To specify multiple servers, separate the server names
with commas and surround the list with double quotes. If multiple servers are
specified, the other RADIUS options can also be given as comma-separated
lists, to provide individual values for each server. They can also be
specified as a single value, in which case that value will apply to all
servers.

The following configuration options are supported for RADIUS:

`radiusservers`

    

The DNS names or IP addresses of the RADIUS servers to connect to. This
parameter is required.

`radiussecrets`

    

The shared secrets used when talking securely to the RADIUS servers. This must
have exactly the same value on the PostgreSQL and RADIUS servers. It is
recommended that this be a string of at least 16 characters. This parameter is
required.

### Note

The encryption vector used will only be cryptographically strong if PostgreSQL
is built with support for OpenSSL. In other cases, the transmission to the
RADIUS server should only be considered obfuscated, not secured, and external
security measures should be applied if necessary.

`radiusports`

    

The port numbers to connect to on the RADIUS servers. If no port is specified,
the default RADIUS port (`1812`) will be used.

`radiusidentifiers`

    

The strings to be used as `NAS Identifier` in the RADIUS requests. This
parameter can be used, for example, to identify which database cluster the
user is attempting to connect to, which can be useful for policy matching on
the RADIUS server. If no identifier is specified, the default `postgresql`
will be used.

If it is necessary to have a comma or whitespace in a RADIUS parameter value,
that can be done by putting double quotes around the value, but it is tedious
because two layers of double-quoting are now required. An example of putting
whitespace into RADIUS secret strings is:

    
    
    host ... radius radiusservers="server1,server2" radiussecrets="""secret one"",""secret two"""
    

* * *

[Prev](auth-ldap.html "21.10. LDAP Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-cert.html "21.12. Certificate Authentication")  
---|---|---  
21.10. LDAP Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.12. Certificate Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-radius.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

