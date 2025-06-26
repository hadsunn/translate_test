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

Supported Versions: [Current](/docs/current/connect-estab.html "PostgreSQL 17
- 52.2. How Connections Are Established") ([17](/docs/17/connect-estab.html
"PostgreSQL 17 - 52.2. How Connections Are Established")) /
[16](/docs/16/connect-estab.html "PostgreSQL 16 - 52.2. How Connections Are
Established") / [15](/docs/15/connect-estab.html "PostgreSQL 15 - 52.2. How
Connections Are Established") / [14](/docs/14/connect-estab.html "PostgreSQL
14 - 52.2. How Connections Are Established") / [13](/docs/13/connect-
estab.html "PostgreSQL 13 - 52.2. How Connections Are Established")

Development Versions: [18](/docs/18/connect-estab.html "PostgreSQL 18 -
52.2. How Connections Are Established") / [devel](/docs/devel/connect-
estab.html "PostgreSQL devel - 52.2. How Connections Are Established")

Unsupported versions: [12](/docs/12/connect-estab.html "PostgreSQL 12 -
52.2. How Connections Are Established") / [11](/docs/11/connect-estab.html
"PostgreSQL 11 - 52.2. How Connections Are Established") /
[10](/docs/10/connect-estab.html "PostgreSQL 10 - 52.2. How Connections Are
Established") / [9.6](/docs/9.6/connect-estab.html "PostgreSQL 9.6 - 52.2. How
Connections Are Established") / [9.5](/docs/9.5/connect-estab.html "PostgreSQL
9.5 - 52.2. How Connections Are Established") / [9.4](/docs/9.4/connect-
estab.html "PostgreSQL 9.4 - 52.2. How Connections Are Established") /
[9.3](/docs/9.3/connect-estab.html "PostgreSQL 9.3 - 52.2. How Connections Are
Established") / [9.2](/docs/9.2/connect-estab.html "PostgreSQL 9.2 - 52.2. How
Connections Are Established") / [9.1](/docs/9.1/connect-estab.html "PostgreSQL
9.1 - 52.2. How Connections Are Established") / [9.0](/docs/9.0/connect-
estab.html "PostgreSQL 9.0 - 52.2. How Connections Are Established") /
[8.4](/docs/8.4/connect-estab.html "PostgreSQL 8.4 - 52.2. How Connections Are
Established") / [8.3](/docs/8.3/connect-estab.html "PostgreSQL 8.3 - 52.2. How
Connections Are Established") / [8.2](/docs/8.2/connect-estab.html "PostgreSQL
8.2 - 52.2. How Connections Are Established") / [8.1](/docs/8.1/connect-
estab.html "PostgreSQL 8.1 - 52.2. How Connections Are Established") /
[8.0](/docs/8.0/connect-estab.html "PostgreSQL 8.0 - 52.2. How Connections Are
Established") / [7.4](/docs/7.4/connect-estab.html "PostgreSQL 7.4 - 52.2. How
Connections Are Established") / [7.3](/docs/7.3/connect-estab.html "PostgreSQL
7.3 - 52.2. How Connections Are Established") / [7.2](/docs/7.2/connect-
estab.html "PostgreSQL 7.2 - 52.2. How Connections Are Established") /
[7.1](/docs/7.1/connect-estab.html "PostgreSQL 7.1 - 52.2. How Connections Are
Established")

__

52.2. How Connections Are Established  
---  
[Prev](query-path.html "52.1. The Path of a Query")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") | Chapter 52. Overview of PostgreSQL Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](parser-stage.html "52.3. The Parser Stage")  
  
* * *

## 52.2. How Connections Are Established #

PostgreSQL implements a “process per user” client/server model. In this model,
every [](glossary.html#GLOSSARY-CLIENT)[client
process](glossary.html#GLOSSARY-CLIENT "Client \(process\)") connects to
exactly one [](glossary.html#GLOSSARY-BACKEND)[backend
process](glossary.html#GLOSSARY-BACKEND "Backend \(process\)"). As we do not
know ahead of time how many connections will be made, we have to use a
“supervisor process” that spawns a new backend process every time a connection
is requested. This supervisor process is called [](glossary.html#GLOSSARY-
POSTMASTER)[postmaster](glossary.html#GLOSSARY-POSTMASTER "Postmaster
\(process\)") and listens at a specified TCP/IP port for incoming connections.
Whenever it detects a request for a connection, it spawns a new backend
process. Those backend processes communicate with each other and with other
processes of the [](glossary.html#GLOSSARY-
INSTANCE)[instance](glossary.html#GLOSSARY-INSTANCE "Instance") using
_semaphores_ and [](glossary.html#GLOSSARY-SHARED-MEMORY)[shared
memory](glossary.html#GLOSSARY-SHARED-MEMORY "Shared memory") to ensure data
integrity throughout concurrent data access.

The client process can be any program that understands the PostgreSQL protocol
described in [Chapter 55](protocol.html "Chapter 55. Frontend/Backend
Protocol"). Many clients are based on the C-language library libpq, but
several independent implementations of the protocol exist, such as the Java
JDBC driver.

Once a connection is established, the client process can send a query to the
backend process it's connected to. The query is transmitted using plain text,
i.e., there is no parsing done in the client. The backend process parses the
query, creates an _execution plan_ , executes the plan, and returns the
retrieved rows to the client by transmitting them over the established
connection.

* * *

[Prev](query-path.html "52.1. The Path of a Query")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") |  [Next](parser-stage.html "52.3. The Parser Stage")  
---|---|---  
52.1. The Path of a Query  | [Home](index.html "PostgreSQL 16.9 Documentation") |  52.3. The Parser Stage  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/connect-estab.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

