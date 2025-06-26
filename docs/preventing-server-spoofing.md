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

Supported Versions: [Current](/docs/current/preventing-server-spoofing.html
"PostgreSQL 17 - 19.7. Preventing Server Spoofing") ([17](/docs/17/preventing-
server-spoofing.html "PostgreSQL 17 - 19.7. Preventing Server Spoofing")) /
[16](/docs/16/preventing-server-spoofing.html "PostgreSQL 16 -
19.7. Preventing Server Spoofing") / [15](/docs/15/preventing-server-
spoofing.html "PostgreSQL 15 - 19.7. Preventing Server Spoofing") /
[14](/docs/14/preventing-server-spoofing.html "PostgreSQL 14 -
19.7. Preventing Server Spoofing") / [13](/docs/13/preventing-server-
spoofing.html "PostgreSQL 13 - 19.7. Preventing Server Spoofing")

Development Versions: [18](/docs/18/preventing-server-spoofing.html
"PostgreSQL 18 - 19.7. Preventing Server Spoofing") /
[devel](/docs/devel/preventing-server-spoofing.html "PostgreSQL devel -
19.7. Preventing Server Spoofing")

Unsupported versions: [12](/docs/12/preventing-server-spoofing.html
"PostgreSQL 12 - 19.7. Preventing Server Spoofing") /
[11](/docs/11/preventing-server-spoofing.html "PostgreSQL 11 -
19.7. Preventing Server Spoofing") / [10](/docs/10/preventing-server-
spoofing.html "PostgreSQL 10 - 19.7. Preventing Server Spoofing") /
[9.6](/docs/9.6/preventing-server-spoofing.html "PostgreSQL 9.6 -
19.7. Preventing Server Spoofing") / [9.5](/docs/9.5/preventing-server-
spoofing.html "PostgreSQL 9.5 - 19.7. Preventing Server Spoofing") /
[9.4](/docs/9.4/preventing-server-spoofing.html "PostgreSQL 9.4 -
19.7. Preventing Server Spoofing") / [9.3](/docs/9.3/preventing-server-
spoofing.html "PostgreSQL 9.3 - 19.7. Preventing Server Spoofing") /
[9.2](/docs/9.2/preventing-server-spoofing.html "PostgreSQL 9.2 -
19.7. Preventing Server Spoofing") / [9.1](/docs/9.1/preventing-server-
spoofing.html "PostgreSQL 9.1 - 19.7. Preventing Server Spoofing") /
[9.0](/docs/9.0/preventing-server-spoofing.html "PostgreSQL 9.0 -
19.7. Preventing Server Spoofing") / [8.4](/docs/8.4/preventing-server-
spoofing.html "PostgreSQL 8.4 - 19.7. Preventing Server Spoofing") /
[8.3](/docs/8.3/preventing-server-spoofing.html "PostgreSQL 8.3 -
19.7. Preventing Server Spoofing")

__

19.7. Preventing Server Spoofing  
---  
[Prev](upgrading.html "19.6. Upgrading a PostgreSQL Cluster")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](encryption-options.html "19.8. Encryption Options")  
  
* * *

## 19.7. Preventing Server Spoofing #

While the server is running, it is not possible for a malicious user to take
the place of the normal database server. However, when the server is down, it
is possible for a local user to spoof the normal server by starting their own
server. The spoof server could read passwords and queries sent by clients, but
could not return any data because the `PGDATA` directory would still be secure
because of directory permissions. Spoofing is possible because any user can
start a database server; a client cannot identify an invalid server unless it
is specially configured.

One way to prevent spoofing of `local` connections is to use a Unix domain
socket directory ([unix_socket_directories](runtime-config-
connection.html#GUC-UNIX-SOCKET-DIRECTORIES)) that has write permission only
for a trusted local user. This prevents a malicious user from creating their
own socket file in that directory. If you are concerned that some applications
might still reference `/tmp` for the socket file and hence be vulnerable to
spoofing, during operating system startup create a symbolic link
`/tmp/.s.PGSQL.5432` that points to the relocated socket file. You also might
need to modify your `/tmp` cleanup script to prevent removal of the symbolic
link.

Another option for `local` connections is for clients to use
[`requirepeer`](libpq-connect.html#LIBPQ-CONNECT-REQUIREPEER) to specify the
required owner of the server process connected to the socket.

To prevent spoofing on TCP connections, either use SSL certificates and make
sure that clients check the server's certificate, or use GSSAPI encryption (or
both, if they're on separate connections).

To prevent spoofing with SSL, the server must be configured to accept only
`hostssl` connections ([Section 21.1](auth-pg-hba-conf.html "21.1. The
pg_hba.conf File")) and have SSL key and certificate files ([Section
19.9](ssl-tcp.html "19.9. Secure TCP/IP Connections with SSL")). The TCP
client must connect using `sslmode=verify-ca` or `verify-full` and have the
appropriate root certificate file installed ([Section 34.19.1](libpq-
ssl.html#LIBQ-SSL-CERTIFICATES "34.19.1. Client Verification of Server
Certificates")). Alternatively the [system CA pool](libpq-connect.html#LIBPQ-
CONNECT-SSLROOTCERT), as defined by the SSL implementation, can be used using
`sslrootcert=system`; in this case, `sslmode=verify-full` is forced for
safety, since it is generally trivial to obtain certificates which are signed
by a public CA.

To prevent server spoofing from occurring when using [scram-sha-256](auth-
password.html "21.5. Password Authentication") password authentication over a
network, you should ensure that you connect to the server using SSL and with
one of the anti-spoofing methods described in the previous paragraph.
Additionally, the SCRAM implementation in libpq cannot protect the entire
authentication exchange, but using the `channel_binding=require` connection
parameter provides a mitigation against server spoofing. An attacker that uses
a rogue server to intercept a SCRAM exchange can use offline analysis to
potentially determine the hashed password from the client.

To prevent spoofing with GSSAPI, the server must be configured to accept only
`hostgssenc` connections ([Section 21.1](auth-pg-hba-conf.html "21.1. The
pg_hba.conf File")) and use `gss` authentication with them. The TCP client
must connect using `gssencmode=require`.

* * *

[Prev](upgrading.html "19.6. Upgrading a PostgreSQL Cluster")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](encryption-options.html "19.8. Encryption Options")  
---|---|---  
19.6. Upgrading a PostgreSQL Cluster  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.8. Encryption Options  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/preventing-server-
spoofing.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

