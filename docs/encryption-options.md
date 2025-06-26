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

Supported Versions: [Current](/docs/current/encryption-options.html
"PostgreSQL 17 - 19.8. Encryption Options") ([17](/docs/17/encryption-
options.html "PostgreSQL 17 - 19.8. Encryption Options")) /
[16](/docs/16/encryption-options.html "PostgreSQL 16 - 19.8. Encryption
Options") / [15](/docs/15/encryption-options.html "PostgreSQL 15 -
19.8. Encryption Options") / [14](/docs/14/encryption-options.html "PostgreSQL
14 - 19.8. Encryption Options") / [13](/docs/13/encryption-options.html
"PostgreSQL 13 - 19.8. Encryption Options")

Development Versions: [18](/docs/18/encryption-options.html "PostgreSQL 18 -
19.8. Encryption Options") / [devel](/docs/devel/encryption-options.html
"PostgreSQL devel - 19.8. Encryption Options")

Unsupported versions: [12](/docs/12/encryption-options.html "PostgreSQL 12 -
19.8. Encryption Options") / [11](/docs/11/encryption-options.html "PostgreSQL
11 - 19.8. Encryption Options") / [10](/docs/10/encryption-options.html
"PostgreSQL 10 - 19.8. Encryption Options") / [9.6](/docs/9.6/encryption-
options.html "PostgreSQL 9.6 - 19.8. Encryption Options") /
[9.5](/docs/9.5/encryption-options.html "PostgreSQL 9.5 - 19.8. Encryption
Options") / [9.4](/docs/9.4/encryption-options.html "PostgreSQL 9.4 -
19.8. Encryption Options") / [9.3](/docs/9.3/encryption-options.html
"PostgreSQL 9.3 - 19.8. Encryption Options") / [9.2](/docs/9.2/encryption-
options.html "PostgreSQL 9.2 - 19.8. Encryption Options") /
[9.1](/docs/9.1/encryption-options.html "PostgreSQL 9.1 - 19.8. Encryption
Options") / [9.0](/docs/9.0/encryption-options.html "PostgreSQL 9.0 -
19.8. Encryption Options") / [8.4](/docs/8.4/encryption-options.html
"PostgreSQL 8.4 - 19.8. Encryption Options") / [8.3](/docs/8.3/encryption-
options.html "PostgreSQL 8.3 - 19.8. Encryption Options") /
[8.2](/docs/8.2/encryption-options.html "PostgreSQL 8.2 - 19.8. Encryption
Options") / [8.1](/docs/8.1/encryption-options.html "PostgreSQL 8.1 -
19.8. Encryption Options") / [8.0](/docs/8.0/encryption-options.html
"PostgreSQL 8.0 - 19.8. Encryption Options")

__

19.8. Encryption Options  
---  
[Prev](preventing-server-spoofing.html "19.7. Preventing Server Spoofing")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ssl-tcp.html "19.9. Secure TCP/IP Connections with SSL")  
  
* * *

## 19.8. Encryption Options #

PostgreSQL offers encryption at several levels, and provides flexibility in
protecting data from disclosure due to database server theft, unscrupulous
administrators, and insecure networks. Encryption might also be required to
secure sensitive data such as medical records or financial transactions.

Password Encryption

    

Database user passwords are stored as hashes (determined by the setting
[password_encryption](runtime-config-connection.html#GUC-PASSWORD-
ENCRYPTION)), so the administrator cannot determine the actual password
assigned to the user. If SCRAM or MD5 encryption is used for client
authentication, the unencrypted password is never even temporarily present on
the server because the client encrypts it before being sent across the
network. SCRAM is preferred, because it is an Internet standard and is more
secure than the PostgreSQL-specific MD5 authentication protocol.

Encryption For Specific Columns

    

The [pgcrypto](pgcrypto.html "F.28. pgcrypto — cryptographic functions")
module allows certain fields to be stored encrypted. This is useful if only
some of the data is sensitive. The client supplies the decryption key and the
data is decrypted on the server and then sent to the client.

The decrypted data and the decryption key are present on the server for a
brief time while it is being decrypted and communicated between the client and
server. This presents a brief moment where the data and keys can be
intercepted by someone with complete access to the database server, such as
the system administrator.

Data Partition Encryption

    

Storage encryption can be performed at the file system level or the block
level. Linux file system encryption options include eCryptfs and EncFS, while
FreeBSD uses PEFS. Block level or full disk encryption options include dm-
crypt + LUKS on Linux and GEOM modules geli and gbde on FreeBSD. Many other
operating systems support this functionality, including Windows.

This mechanism prevents unencrypted data from being read from the drives if
the drives or the entire computer is stolen. This does not protect against
attacks while the file system is mounted, because when mounted, the operating
system provides an unencrypted view of the data. However, to mount the file
system, you need some way for the encryption key to be passed to the operating
system, and sometimes the key is stored somewhere on the host that mounts the
disk.

Encrypting Data Across A Network

    

SSL connections encrypt all data sent across the network: the password, the
queries, and the data returned. The `pg_hba.conf` file allows administrators
to specify which hosts can use non-encrypted connections (`host`) and which
require SSL-encrypted connections (`hostssl`). Also, clients can specify that
they connect to servers only via SSL.

GSSAPI-encrypted connections encrypt all data sent across the network,
including queries and data returned. (No password is sent across the network.)
The `pg_hba.conf` file allows administrators to specify which hosts can use
non-encrypted connections (`host`) and which require GSSAPI-encrypted
connections (`hostgssenc`). Also, clients can specify that they connect to
servers only on GSSAPI-encrypted connections (`gssencmode=require`).

Stunnel or SSH can also be used to encrypt transmissions.

SSL Host Authentication

    

It is possible for both the client and server to provide SSL certificates to
each other. It takes some extra configuration on each side, but this provides
stronger verification of identity than the mere use of passwords. It prevents
a computer from pretending to be the server just long enough to read the
password sent by the client. It also helps prevent “man in the middle” attacks
where a computer between the client and server pretends to be the server and
reads and passes all data between the client and server.

Client-Side Encryption

    

If the system administrator for the server's machine cannot be trusted, it is
necessary for the client to encrypt the data; this way, unencrypted data never
appears on the database server. Data is encrypted on the client before being
sent to the server, and database results have to be decrypted on the client
before being used.

* * *

[Prev](preventing-server-spoofing.html "19.7. Preventing Server Spoofing")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](ssl-tcp.html "19.9. Secure TCP/IP Connections with SSL")  
---|---|---  
19.7. Preventing Server Spoofing  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.9. Secure TCP/IP Connections with SSL  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/encryption-options.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

