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

Supported Versions: [Current](/docs/current/postgres-user.html "PostgreSQL 17
- 19.1. The PostgreSQL User Account") ([17](/docs/17/postgres-user.html
"PostgreSQL 17 - 19.1. The PostgreSQL User Account")) /
[16](/docs/16/postgres-user.html "PostgreSQL 16 - 19.1. The PostgreSQL User
Account") / [15](/docs/15/postgres-user.html "PostgreSQL 15 - 19.1. The
PostgreSQL User Account") / [14](/docs/14/postgres-user.html "PostgreSQL 14 -
19.1. The PostgreSQL User Account") / [13](/docs/13/postgres-user.html
"PostgreSQL 13 - 19.1. The PostgreSQL User Account")

Development Versions: [18](/docs/18/postgres-user.html "PostgreSQL 18 -
19.1. The PostgreSQL User Account") / [devel](/docs/devel/postgres-user.html
"PostgreSQL devel - 19.1. The PostgreSQL User Account")

Unsupported versions: [12](/docs/12/postgres-user.html "PostgreSQL 12 -
19.1. The PostgreSQL User Account") / [11](/docs/11/postgres-user.html
"PostgreSQL 11 - 19.1. The PostgreSQL User Account") / [10](/docs/10/postgres-
user.html "PostgreSQL 10 - 19.1. The PostgreSQL User Account") /
[9.6](/docs/9.6/postgres-user.html "PostgreSQL 9.6 - 19.1. The PostgreSQL User
Account") / [9.5](/docs/9.5/postgres-user.html "PostgreSQL 9.5 - 19.1. The
PostgreSQL User Account") / [9.4](/docs/9.4/postgres-user.html "PostgreSQL 9.4
- 19.1. The PostgreSQL User Account") / [9.3](/docs/9.3/postgres-user.html
"PostgreSQL 9.3 - 19.1. The PostgreSQL User Account") /
[9.2](/docs/9.2/postgres-user.html "PostgreSQL 9.2 - 19.1. The PostgreSQL User
Account") / [9.1](/docs/9.1/postgres-user.html "PostgreSQL 9.1 - 19.1. The
PostgreSQL User Account") / [9.0](/docs/9.0/postgres-user.html "PostgreSQL 9.0
- 19.1. The PostgreSQL User Account") / [8.4](/docs/8.4/postgres-user.html
"PostgreSQL 8.4 - 19.1. The PostgreSQL User Account") /
[8.3](/docs/8.3/postgres-user.html "PostgreSQL 8.3 - 19.1. The PostgreSQL User
Account") / [8.2](/docs/8.2/postgres-user.html "PostgreSQL 8.2 - 19.1. The
PostgreSQL User Account")

__

19.1. The PostgreSQL User Account  
---  
[Prev](runtime.html "Chapter 19. Server Setup and Operation")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](creating-cluster.html "19.2. Creating a Database Cluster")  
  
* * *

## 19.1. The PostgreSQL User Account #

As with any server daemon that is accessible to the outside world, it is
advisable to run PostgreSQL under a separate user account. This user account
should only own the data that is managed by the server, and should not be
shared with other daemons. (For example, using the user `nobody` is a bad
idea.) In particular, it is advisable that this user account not own the
PostgreSQL executable files, to ensure that a compromised server process could
not modify those executables.

Pre-packaged versions of PostgreSQL will typically create a suitable user
account automatically during package installation.

To add a Unix user account to your system, look for a command `useradd` or
`adduser`. The user name postgres is often used, and is assumed throughout
this book, but you can use another name if you like.

* * *

[Prev](runtime.html "Chapter 19. Server Setup and Operation")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](creating-cluster.html "19.2. Creating a Database Cluster")  
---|---|---  
Chapter 19. Server Setup and Operation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.2. Creating a Database Cluster  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/postgres-user.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

