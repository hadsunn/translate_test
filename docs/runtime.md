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

Supported Versions: [Current](/docs/current/runtime.html "PostgreSQL 17 -
Chapter 19. Server Setup and Operation") ([17](/docs/17/runtime.html
"PostgreSQL 17 - Chapter 19. Server Setup and Operation")) /
[16](/docs/16/runtime.html "PostgreSQL 16 - Chapter 19. Server Setup and
Operation") / [15](/docs/15/runtime.html "PostgreSQL 15 - Chapter 19. Server
Setup and Operation") / [14](/docs/14/runtime.html "PostgreSQL 14 -
Chapter 19. Server Setup and Operation") / [13](/docs/13/runtime.html
"PostgreSQL 13 - Chapter 19. Server Setup and Operation")

Development Versions: [18](/docs/18/runtime.html "PostgreSQL 18 -
Chapter 19. Server Setup and Operation") / [devel](/docs/devel/runtime.html
"PostgreSQL devel - Chapter 19. Server Setup and Operation")

Unsupported versions: [12](/docs/12/runtime.html "PostgreSQL 12 -
Chapter 19. Server Setup and Operation") / [11](/docs/11/runtime.html
"PostgreSQL 11 - Chapter 19. Server Setup and Operation") /
[10](/docs/10/runtime.html "PostgreSQL 10 - Chapter 19. Server Setup and
Operation") / [9.6](/docs/9.6/runtime.html "PostgreSQL 9.6 -
Chapter 19. Server Setup and Operation") / [9.5](/docs/9.5/runtime.html
"PostgreSQL 9.5 - Chapter 19. Server Setup and Operation") /
[9.4](/docs/9.4/runtime.html "PostgreSQL 9.4 - Chapter 19. Server Setup and
Operation") / [9.3](/docs/9.3/runtime.html "PostgreSQL 9.3 -
Chapter 19. Server Setup and Operation") / [9.2](/docs/9.2/runtime.html
"PostgreSQL 9.2 - Chapter 19. Server Setup and Operation") /
[9.1](/docs/9.1/runtime.html "PostgreSQL 9.1 - Chapter 19. Server Setup and
Operation") / [9.0](/docs/9.0/runtime.html "PostgreSQL 9.0 -
Chapter 19. Server Setup and Operation") / [8.4](/docs/8.4/runtime.html
"PostgreSQL 8.4 - Chapter 19. Server Setup and Operation") /
[8.3](/docs/8.3/runtime.html "PostgreSQL 8.3 - Chapter 19. Server Setup and
Operation") / [8.2](/docs/8.2/runtime.html "PostgreSQL 8.2 -
Chapter 19. Server Setup and Operation") / [8.1](/docs/8.1/runtime.html
"PostgreSQL 8.1 - Chapter 19. Server Setup and Operation") /
[8.0](/docs/8.0/runtime.html "PostgreSQL 8.0 - Chapter 19. Server Setup and
Operation") / [7.4](/docs/7.4/runtime.html "PostgreSQL 7.4 -
Chapter 19. Server Setup and Operation") / [7.3](/docs/7.3/runtime.html
"PostgreSQL 7.3 - Chapter 19. Server Setup and Operation") /
[7.2](/docs/7.2/runtime.html "PostgreSQL 7.2 - Chapter 19. Server Setup and
Operation") / [7.1](/docs/7.1/runtime.html "PostgreSQL 7.1 -
Chapter 19. Server Setup and Operation")

__

Chapter 19. Server Setup and Operation  
---  
[Prev](install-windows-full.html "18.1. Building with Visual C++ or the  Microsoft Windows SDK")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](postgres-user.html "19.1. The PostgreSQL User Account")  
  
* * *

## Chapter 19. Server Setup and Operation

**Table of Contents**

[19.1. The PostgreSQL User Account](postgres-user.html)

[19.2. Creating a Database Cluster](creating-cluster.html)

    

[19.2.1. Use of Secondary File Systems](creating-cluster.html#CREATING-
CLUSTER-MOUNT-POINTS)

[19.2.2. File Systems](creating-cluster.html#CREATING-CLUSTER-FILESYSTEM)

[19.3. Starting the Database Server](server-start.html)

    

[19.3.1. Server Start-up Failures](server-start.html#SERVER-START-FAILURES)

[19.3.2. Client Connection Problems](server-start.html#CLIENT-CONNECTION-
PROBLEMS)

[19.4. Managing Kernel Resources](kernel-resources.html)

    

[19.4.1. Shared Memory and Semaphores](kernel-resources.html#SYSVIPC)

[19.4.2. systemd RemoveIPC](kernel-resources.html#SYSTEMD-REMOVEIPC)

[19.4.3. Resource Limits](kernel-resources.html#KERNEL-RESOURCES-LIMITS)

[19.4.4. Linux Memory Overcommit](kernel-resources.html#LINUX-MEMORY-
OVERCOMMIT)

[19.4.5. Linux Huge Pages](kernel-resources.html#LINUX-HUGE-PAGES)

[19.5. Shutting Down the Server](server-shutdown.html)

[19.6. Upgrading a PostgreSQL Cluster](upgrading.html)

    

[19.6.1. Upgrading Data via pg_dumpall](upgrading.html#UPGRADING-VIA-
PGDUMPALL)

[19.6.2. Upgrading Data via pg_upgrade](upgrading.html#UPGRADING-VIA-PG-
UPGRADE)

[19.6.3. Upgrading Data via Replication](upgrading.html#UPGRADING-VIA-
REPLICATION)

[19.7. Preventing Server Spoofing](preventing-server-spoofing.html)

[19.8. Encryption Options](encryption-options.html)

[19.9. Secure TCP/IP Connections with SSL](ssl-tcp.html)

    

[19.9.1. Basic Setup](ssl-tcp.html#SSL-SETUP)

[19.9.2. OpenSSL Configuration](ssl-tcp.html#SSL-OPENSSL-CONFIG)

[19.9.3. Using Client Certificates](ssl-tcp.html#SSL-CLIENT-CERTIFICATES)

[19.9.4. SSL Server File Usage](ssl-tcp.html#SSL-SERVER-FILES)

[19.9.5. Creating Certificates](ssl-tcp.html#SSL-CERTIFICATE-CREATION)

[19.10. Secure TCP/IP Connections with GSSAPI Encryption](gssapi-enc.html)

    

[19.10.1. Basic Setup](gssapi-enc.html#GSSAPI-SETUP)

[19.11. Secure TCP/IP Connections with SSH Tunnels](ssh-tunnels.html)

[19.12. Registering Event Log on Windows](event-log-registration.html)

This chapter discusses how to set up and run the database server, and its
interactions with the operating system.

The directions in this chapter assume that you are working with plain
PostgreSQL without any additional infrastructure, for example a copy that you
built from source according to the directions in the preceding chapters. If
you are working with a pre-packaged or vendor-supplied version of PostgreSQL,
it is likely that the packager has made special provisions for installing and
starting the database server according to your system's conventions. Consult
the package-level documentation for details.

* * *

[Prev](install-windows-full.html "18.1. Building with Visual C++ or the  Microsoft Windows SDK")  | [Up](admin.html "Part III. Server Administration") |  [Next](postgres-user.html "19.1. The PostgreSQL User Account")  
---|---|---  
18.1. Building with Visual C++ or the Microsoft Windows SDK  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.1. The PostgreSQL User Account  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

