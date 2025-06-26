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

Supported Versions: [Current](/docs/current/gssapi-auth.html "PostgreSQL 17 -
21.6. GSSAPI Authentication") ([17](/docs/17/gssapi-auth.html "PostgreSQL 17 -
21.6. GSSAPI Authentication")) / [16](/docs/16/gssapi-auth.html "PostgreSQL 16
- 21.6. GSSAPI Authentication") / [15](/docs/15/gssapi-auth.html "PostgreSQL
15 - 21.6. GSSAPI Authentication") / [14](/docs/14/gssapi-auth.html
"PostgreSQL 14 - 21.6. GSSAPI Authentication") / [13](/docs/13/gssapi-
auth.html "PostgreSQL 13 - 21.6. GSSAPI Authentication")

Development Versions: [18](/docs/18/gssapi-auth.html "PostgreSQL 18 -
21.6. GSSAPI Authentication") / [devel](/docs/devel/gssapi-auth.html
"PostgreSQL devel - 21.6. GSSAPI Authentication")

Unsupported versions: [12](/docs/12/gssapi-auth.html "PostgreSQL 12 -
21.6. GSSAPI Authentication") / [11](/docs/11/gssapi-auth.html "PostgreSQL 11
- 21.6. GSSAPI Authentication")

__

21.6. GSSAPI Authentication  
---  
[Prev](auth-password.html "21.5. Password Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sspi-auth.html "21.7. SSPI Authentication")  
  
* * *

## 21.6. GSSAPI Authentication #

GSSAPI is an industry-standard protocol for secure authentication defined in
[RFC 2743](https://datatracker.ietf.org/doc/html/rfc2743). PostgreSQL supports
GSSAPI for authentication, communications encryption, or both. GSSAPI provides
automatic authentication (single sign-on) for systems that support it. The
authentication itself is secure. If GSSAPI encryption or SSL encryption is
used, the data sent along the database connection will be encrypted;
otherwise, it will not.

GSSAPI support has to be enabled when PostgreSQL is built; see [Chapter
17](installation.html "Chapter 17. Installation from Source Code") for more
information.

When GSSAPI uses Kerberos, it uses a standard service principal
(authentication identity) name in the format `_`servicename`_ /_`hostname`_
@_`realm`_`. The principal name used by a particular installation is not
encoded in the PostgreSQL server in any way; rather it is specified in the
_keytab_ file that the server reads to determine its identity. If multiple
principals are listed in the keytab file, the server will accept any one of
them. The server's realm name is the preferred realm specified in the Kerberos
configuration file(s) accessible to the server.

When connecting, the client must know the principal name of the server it
intends to connect to. The _`servicename`_ part of the principal is ordinarily
`postgres`, but another value can be selected via libpq's [krbsrvname](libpq-
connect.html#LIBPQ-CONNECT-KRBSRVNAME) connection parameter. The _`hostname`_
part is the fully qualified host name that libpq is told to connect to. The
realm name is the preferred realm specified in the Kerberos configuration
file(s) accessible to the client.

The client will also have a principal name for its own identity (and it must
have a valid ticket for this principal). To use GSSAPI for authentication, the
client principal must be associated with a PostgreSQL database user name. The
`pg_ident.conf` configuration file can be used to map principals to user
names; for example, `pgusername@realm` could be mapped to just `pgusername`.
Alternatively, you can use the full `username@realm` principal as the role
name in PostgreSQL without any mapping.

PostgreSQL also supports mapping client principals to user names by just
stripping the realm from the principal. This method is supported for backwards
compatibility and is strongly discouraged as it is then impossible to
distinguish different users with the same user name but coming from different
realms. To enable this, set `include_realm` to 0. For simple single-realm
installations, doing that combined with setting the `krb_realm` parameter
(which checks that the principal's realm matches exactly what is in the
`krb_realm` parameter) is still secure; but this is a less capable approach
compared to specifying an explicit mapping in `pg_ident.conf`.

The location of the server's keytab file is specified by the
[krb_server_keyfile](runtime-config-connection.html#GUC-KRB-SERVER-KEYFILE)
configuration parameter. For security reasons, it is recommended to use a
separate keytab just for the PostgreSQL server rather than allowing the server
to read the system keytab file. Make sure that your server keytab file is
readable (and preferably only readable, not writable) by the PostgreSQL server
account. (See also [Section 19.1](postgres-user.html "19.1. The PostgreSQL
User Account").)

The keytab file is generated using the Kerberos software; see the Kerberos
documentation for details. The following example shows doing this using the
kadmin tool of MIT Kerberos:

    
    
    kadmin% **addprinc -randkey postgres/server.my.domain.org**
    kadmin% **ktadd -k krb5.keytab postgres/server.my.domain.org**
    

The following authentication options are supported for the GSSAPI
authentication method:

`include_realm`

    

If set to 0, the realm name from the authenticated user principal is stripped
off before being passed through the user name mapping ([Section 21.2](auth-
username-maps.html "21.2. User Name Maps")). This is discouraged and is
primarily available for backwards compatibility, as it is not secure in multi-
realm environments unless `krb_realm` is also used. It is recommended to leave
`include_realm` set to the default (1) and to provide an explicit mapping in
`pg_ident.conf` to convert principal names to PostgreSQL user names.

`map`

    

Allows mapping from client principals to database user names. See [Section
21.2](auth-username-maps.html "21.2. User Name Maps") for details. For a
GSSAPI/Kerberos principal, such as `username@EXAMPLE.COM` (or, less commonly,
`username/hostbased@EXAMPLE.COM`), the user name used for mapping is
`username@EXAMPLE.COM` (or `username/hostbased@EXAMPLE.COM`, respectively),
unless `include_realm` has been set to 0, in which case `username` (or
`username/hostbased`) is what is seen as the system user name when mapping.

`krb_realm`

    

Sets the realm to match user principal names against. If this parameter is
set, only users of that realm will be accepted. If it is not set, users of any
realm can connect, subject to whatever user name mapping is done.

In addition to these settings, which can be different for different
`pg_hba.conf` entries, there is the server-wide [krb_caseins_users](runtime-
config-connection.html#GUC-KRB-CASEINS-USERS) configuration parameter. If that
is set to true, client principals are matched to user map entries case-
insensitively. `krb_realm`, if set, is also matched case-insensitively.

* * *

[Prev](auth-password.html "21.5. Password Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](sspi-auth.html "21.7. SSPI Authentication")  
---|---|---  
21.5. Password Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.7. SSPI Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gssapi-auth.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

