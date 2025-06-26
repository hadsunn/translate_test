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

Supported Versions: [Current](/docs/current/perm-functions.html "PostgreSQL 17
- 22.6. Function Security") ([17](/docs/17/perm-functions.html "PostgreSQL 17
- 22.6. Function Security")) / [16](/docs/16/perm-functions.html "PostgreSQL
16 - 22.6. Function Security") / [15](/docs/15/perm-functions.html "PostgreSQL
15 - 22.6. Function Security") / [14](/docs/14/perm-functions.html "PostgreSQL
14 - 22.6. Function Security") / [13](/docs/13/perm-functions.html "PostgreSQL
13 - 22.6. Function Security")

Development Versions: [18](/docs/18/perm-functions.html "PostgreSQL 18 -
22.6. Function Security") / [devel](/docs/devel/perm-functions.html
"PostgreSQL devel - 22.6. Function Security")

Unsupported versions: [12](/docs/12/perm-functions.html "PostgreSQL 12 -
22.6. Function Security") / [11](/docs/11/perm-functions.html "PostgreSQL 11 -
22.6. Function Security") / [10](/docs/10/perm-functions.html "PostgreSQL 10 -
22.6. Function Security") / [9.6](/docs/9.6/perm-functions.html "PostgreSQL
9.6 - 22.6. Function Security") / [9.5](/docs/9.5/perm-functions.html
"PostgreSQL 9.5 - 22.6. Function Security") / [9.4](/docs/9.4/perm-
functions.html "PostgreSQL 9.4 - 22.6. Function Security") /
[9.3](/docs/9.3/perm-functions.html "PostgreSQL 9.3 - 22.6. Function
Security") / [9.2](/docs/9.2/perm-functions.html "PostgreSQL 9.2 -
22.6. Function Security") / [9.1](/docs/9.1/perm-functions.html "PostgreSQL
9.1 - 22.6. Function Security") / [9.0](/docs/9.0/perm-functions.html
"PostgreSQL 9.0 - 22.6. Function Security") / [8.4](/docs/8.4/perm-
functions.html "PostgreSQL 8.4 - 22.6. Function Security") /
[8.3](/docs/8.3/perm-functions.html "PostgreSQL 8.3 - 22.6. Function
Security") / [8.2](/docs/8.2/perm-functions.html "PostgreSQL 8.2 -
22.6. Function Security") / [8.1](/docs/8.1/perm-functions.html "PostgreSQL
8.1 - 22.6. Function Security") / [8.0](/docs/8.0/perm-functions.html
"PostgreSQL 8.0 - 22.6. Function Security") / [7.4](/docs/7.4/perm-
functions.html "PostgreSQL 7.4 - 22.6. Function Security") /
[7.3](/docs/7.3/perm-functions.html "PostgreSQL 7.3 - 22.6. Function
Security") / [7.2](/docs/7.2/perm-functions.html "PostgreSQL 7.2 -
22.6. Function Security") / [7.1](/docs/7.1/perm-functions.html "PostgreSQL
7.1 - 22.6. Function Security")

__

22.6. Function Security  
---  
[Prev](predefined-roles.html "22.5. Predefined Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") | Chapter 22. Database Roles | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](managing-databases.html "Chapter 23. Managing Databases")  
  
* * *

## 22.6. Function Security #

Functions, triggers and row-level security policies allow users to insert code
into the backend server that other users might execute unintentionally. Hence,
these mechanisms permit users to “Trojan horse” others with relative ease. The
strongest protection is tight control over who can define objects. Where that
is infeasible, write queries referring only to objects having trusted owners.
Remove from `search_path` any schemas that permit untrusted users to create
objects.

Functions run inside the backend server process with the operating system
permissions of the database server daemon. If the programming language used
for the function allows unchecked memory accesses, it is possible to change
the server's internal data structures. Hence, among many other things, such
functions can circumvent any system access controls. Function languages that
allow such access are considered “untrusted”, and PostgreSQL allows only
superusers to create functions written in those languages.

* * *

[Prev](predefined-roles.html "22.5. Predefined Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") |  [Next](managing-databases.html "Chapter 23. Managing Databases")  
---|---|---  
22.5. Predefined Roles  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 23. Managing Databases  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/perm-functions.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

