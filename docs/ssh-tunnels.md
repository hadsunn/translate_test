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

Supported Versions: [Current](/docs/current/ssh-tunnels.html "PostgreSQL 17 -
19.11. Secure TCP/IP Connections with SSH Tunnels") ([17](/docs/17/ssh-
tunnels.html "PostgreSQL 17 - 19.11. Secure TCP/IP Connections with SSH
Tunnels")) / [16](/docs/16/ssh-tunnels.html "PostgreSQL 16 - 19.11. Secure
TCP/IP Connections with SSH Tunnels") / [15](/docs/15/ssh-tunnels.html
"PostgreSQL 15 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[14](/docs/14/ssh-tunnels.html "PostgreSQL 14 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [13](/docs/13/ssh-tunnels.html "PostgreSQL 13
- 19.11. Secure TCP/IP Connections with SSH Tunnels")

Development Versions: [18](/docs/18/ssh-tunnels.html "PostgreSQL 18 -
19.11. Secure TCP/IP Connections with SSH Tunnels") / [devel](/docs/devel/ssh-
tunnels.html "PostgreSQL devel - 19.11. Secure TCP/IP Connections with SSH
Tunnels")

Unsupported versions: [12](/docs/12/ssh-tunnels.html "PostgreSQL 12 -
19.11. Secure TCP/IP Connections with SSH Tunnels") / [11](/docs/11/ssh-
tunnels.html "PostgreSQL 11 - 19.11. Secure TCP/IP Connections with SSH
Tunnels") / [10](/docs/10/ssh-tunnels.html "PostgreSQL 10 - 19.11. Secure
TCP/IP Connections with SSH Tunnels") / [9.6](/docs/9.6/ssh-tunnels.html
"PostgreSQL 9.6 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[9.5](/docs/9.5/ssh-tunnels.html "PostgreSQL 9.5 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [9.4](/docs/9.4/ssh-tunnels.html "PostgreSQL
9.4 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[9.3](/docs/9.3/ssh-tunnels.html "PostgreSQL 9.3 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [9.2](/docs/9.2/ssh-tunnels.html "PostgreSQL
9.2 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[9.1](/docs/9.1/ssh-tunnels.html "PostgreSQL 9.1 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [9.0](/docs/9.0/ssh-tunnels.html "PostgreSQL
9.0 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[8.4](/docs/8.4/ssh-tunnels.html "PostgreSQL 8.4 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [8.3](/docs/8.3/ssh-tunnels.html "PostgreSQL
8.3 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[8.2](/docs/8.2/ssh-tunnels.html "PostgreSQL 8.2 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [8.1](/docs/8.1/ssh-tunnels.html "PostgreSQL
8.1 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[8.0](/docs/8.0/ssh-tunnels.html "PostgreSQL 8.0 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [7.4](/docs/7.4/ssh-tunnels.html "PostgreSQL
7.4 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[7.3](/docs/7.3/ssh-tunnels.html "PostgreSQL 7.3 - 19.11. Secure TCP/IP
Connections with SSH Tunnels") / [7.2](/docs/7.2/ssh-tunnels.html "PostgreSQL
7.2 - 19.11. Secure TCP/IP Connections with SSH Tunnels") /
[7.1](/docs/7.1/ssh-tunnels.html "PostgreSQL 7.1 - 19.11. Secure TCP/IP
Connections with SSH Tunnels")

__

19.11. Secure TCP/IP Connections with SSH Tunnels  
---  
[Prev](gssapi-enc.html "19.10. Secure TCP/IP Connections with GSSAPI Encryption")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-log-registration.html "19.12. Registering Event Log on Windows")  
  
* * *

## 19.11. Secure TCP/IP Connections with SSH Tunnels #

It is possible to use SSH to encrypt the network connection between clients
and a PostgreSQL server. Done properly, this provides an adequately secure
network connection, even for non-SSL-capable clients.

First make sure that an SSH server is running properly on the same machine as
the PostgreSQL server and that you can log in using `ssh` as some user; you
then can establish a secure tunnel to the remote server. A secure tunnel
listens on a local port and forwards all traffic to a port on the remote
machine. Traffic sent to the remote port can arrive on its `localhost`
address, or different bind address if desired; it does not appear as coming
from your local machine. This command creates a secure tunnel from the client
machine to the remote machine `foo.com`:

    
    
    ssh -L 63333:localhost:5432 joe@foo.com
    

The first number in the `-L` argument, 63333, is the local port number of the
tunnel; it can be any unused port. (IANA reserves ports 49152 through 65535
for private use.) The name or IP address after this is the remote bind address
you are connecting to, i.e., `localhost`, which is the default. The second
number, 5432, is the remote end of the tunnel, e.g., the port number your
database server is using. In order to connect to the database server using
this tunnel, you connect to port 63333 on the local machine:

    
    
    psql -h localhost -p 63333 postgres
    

To the database server it will then look as though you are user `joe` on host
`foo.com` connecting to the `localhost` bind address, and it will use whatever
authentication procedure was configured for connections by that user to that
bind address. Note that the server will not think the connection is SSL-
encrypted, since in fact it is not encrypted between the SSH server and the
PostgreSQL server. This should not pose any extra security risk because they
are on the same machine.

In order for the tunnel setup to succeed you must be allowed to connect via
`ssh` as `joe@foo.com`, just as if you had attempted to use `ssh` to create a
terminal session.

You could also have set up port forwarding as

    
    
    ssh -L 63333:foo.com:5432 joe@foo.com
    

but then the database server will see the connection as coming in on its
`foo.com` bind address, which is not opened by the default setting
`listen_addresses = 'localhost'`. This is usually not what you want.

If you have to “hop” to the database server via some login host, one possible
setup could look like this:

    
    
    ssh -L 63333:db.foo.com:5432 joe@shell.foo.com
    

Note that this way the connection from `shell.foo.com` to `db.foo.com` will
not be encrypted by the SSH tunnel. SSH offers quite a few configuration
possibilities when the network is restricted in various ways. Please refer to
the SSH documentation for details.

### Tip

Several other applications exist that can provide secure tunnels using a
procedure similar in concept to the one just described.

* * *

[Prev](gssapi-enc.html "19.10. Secure TCP/IP Connections with GSSAPI Encryption")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](event-log-registration.html "19.12. Registering Event Log on Windows")  
---|---|---  
19.10. Secure TCP/IP Connections with GSSAPI Encryption  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.12. Registering Event Log on Windows  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ssh-tunnels.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

