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

Supported Versions: [Current](/docs/current/tutorial-arch.html "PostgreSQL 17
- 1.2. Architectural Fundamentals") ([17](/docs/17/tutorial-arch.html
"PostgreSQL 17 - 1.2. Architectural Fundamentals")) / [16](/docs/16/tutorial-
arch.html "PostgreSQL 16 - 1.2. Architectural Fundamentals") /
[15](/docs/15/tutorial-arch.html "PostgreSQL 15 - 1.2. Architectural
Fundamentals") / [14](/docs/14/tutorial-arch.html "PostgreSQL 14 -
1.2. Architectural Fundamentals") / [13](/docs/13/tutorial-arch.html
"PostgreSQL 13 - 1.2. Architectural Fundamentals")

Development Versions: [18](/docs/18/tutorial-arch.html "PostgreSQL 18 -
1.2. Architectural Fundamentals") / [devel](/docs/devel/tutorial-arch.html
"PostgreSQL devel - 1.2. Architectural Fundamentals")

Unsupported versions: [12](/docs/12/tutorial-arch.html "PostgreSQL 12 -
1.2. Architectural Fundamentals") / [11](/docs/11/tutorial-arch.html
"PostgreSQL 11 - 1.2. Architectural Fundamentals") / [10](/docs/10/tutorial-
arch.html "PostgreSQL 10 - 1.2. Architectural Fundamentals") /
[9.6](/docs/9.6/tutorial-arch.html "PostgreSQL 9.6 - 1.2. Architectural
Fundamentals") / [9.5](/docs/9.5/tutorial-arch.html "PostgreSQL 9.5 -
1.2. Architectural Fundamentals") / [9.4](/docs/9.4/tutorial-arch.html
"PostgreSQL 9.4 - 1.2. Architectural Fundamentals") /
[9.3](/docs/9.3/tutorial-arch.html "PostgreSQL 9.3 - 1.2. Architectural
Fundamentals") / [9.2](/docs/9.2/tutorial-arch.html "PostgreSQL 9.2 -
1.2. Architectural Fundamentals") / [9.1](/docs/9.1/tutorial-arch.html
"PostgreSQL 9.1 - 1.2. Architectural Fundamentals") /
[9.0](/docs/9.0/tutorial-arch.html "PostgreSQL 9.0 - 1.2. Architectural
Fundamentals") / [8.4](/docs/8.4/tutorial-arch.html "PostgreSQL 8.4 -
1.2. Architectural Fundamentals") / [8.3](/docs/8.3/tutorial-arch.html
"PostgreSQL 8.3 - 1.2. Architectural Fundamentals") /
[8.2](/docs/8.2/tutorial-arch.html "PostgreSQL 8.2 - 1.2. Architectural
Fundamentals") / [8.1](/docs/8.1/tutorial-arch.html "PostgreSQL 8.1 -
1.2. Architectural Fundamentals") / [8.0](/docs/8.0/tutorial-arch.html
"PostgreSQL 8.0 - 1.2. Architectural Fundamentals") /
[7.4](/docs/7.4/tutorial-arch.html "PostgreSQL 7.4 - 1.2. Architectural
Fundamentals") / [7.3](/docs/7.3/tutorial-arch.html "PostgreSQL 7.3 -
1.2. Architectural Fundamentals") / [7.2](/docs/7.2/tutorial-arch.html
"PostgreSQL 7.2 - 1.2. Architectural Fundamentals")

__

1.2. Architectural Fundamentals  
---  
[Prev](tutorial-install.html "1.1. Installation")  | [Up](tutorial-start.html "Chapter 1. Getting Started") | Chapter 1. Getting Started | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-createdb.html "1.3. Creating a Database")  
  
* * *

## 1.2. Architectural Fundamentals #

Before we proceed, you should understand the basic PostgreSQL system
architecture. Understanding how the parts of PostgreSQL interact will make
this chapter somewhat clearer.

In database jargon, PostgreSQL uses a client/server model. A PostgreSQL
session consists of the following cooperating processes (programs):

  * A server process, which manages the database files, accepts connections to the database from client applications, and performs database actions on behalf of the clients. The database server program is called `postgres`. 

  * The user's client (frontend) application that wants to perform database operations. Client applications can be very diverse in nature: a client could be a text-oriented tool, a graphical application, a web server that accesses the database to display web pages, or a specialized database maintenance tool. Some client applications are supplied with the PostgreSQL distribution; most are developed by users.

As is typical of client/server applications, the client and the server can be
on different hosts. In that case they communicate over a TCP/IP network
connection. You should keep this in mind, because the files that can be
accessed on a client machine might not be accessible (or might only be
accessible using a different file name) on the database server machine.

The PostgreSQL server can handle multiple concurrent connections from clients.
To achieve this it starts (“forks”) a new process for each connection. From
that point on, the client and the new server process communicate without
intervention by the original `postgres` process. Thus, the supervisor server
process is always running, waiting for client connections, whereas client and
associated server processes come and go. (All of this is of course invisible
to the user. We only mention it here for completeness.)

* * *

[Prev](tutorial-install.html "1.1. Installation")  | [Up](tutorial-start.html "Chapter 1. Getting Started") |  [Next](tutorial-createdb.html "1.3. Creating a Database")  
---|---|---  
1.1. Installation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  1.3. Creating a Database  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-arch.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

