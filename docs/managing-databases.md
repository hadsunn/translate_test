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

Supported Versions: [Current](/docs/current/managing-databases.html
"PostgreSQL 17 - Chapter 23. Managing Databases") ([17](/docs/17/managing-
databases.html "PostgreSQL 17 - Chapter 23. Managing Databases")) /
[16](/docs/16/managing-databases.html "PostgreSQL 16 - Chapter 23. Managing
Databases") / [15](/docs/15/managing-databases.html "PostgreSQL 15 -
Chapter 23. Managing Databases") / [14](/docs/14/managing-databases.html
"PostgreSQL 14 - Chapter 23. Managing Databases") / [13](/docs/13/managing-
databases.html "PostgreSQL 13 - Chapter 23. Managing Databases")

Development Versions: [18](/docs/18/managing-databases.html "PostgreSQL 18 -
Chapter 23. Managing Databases") / [devel](/docs/devel/managing-databases.html
"PostgreSQL devel - Chapter 23. Managing Databases")

Unsupported versions: [12](/docs/12/managing-databases.html "PostgreSQL 12 -
Chapter 23. Managing Databases") / [11](/docs/11/managing-databases.html
"PostgreSQL 11 - Chapter 23. Managing Databases") / [10](/docs/10/managing-
databases.html "PostgreSQL 10 - Chapter 23. Managing Databases") /
[9.6](/docs/9.6/managing-databases.html "PostgreSQL 9.6 - Chapter 23. Managing
Databases") / [9.5](/docs/9.5/managing-databases.html "PostgreSQL 9.5 -
Chapter 23. Managing Databases") / [9.4](/docs/9.4/managing-databases.html
"PostgreSQL 9.4 - Chapter 23. Managing Databases") / [9.3](/docs/9.3/managing-
databases.html "PostgreSQL 9.3 - Chapter 23. Managing Databases") /
[9.2](/docs/9.2/managing-databases.html "PostgreSQL 9.2 - Chapter 23. Managing
Databases") / [9.1](/docs/9.1/managing-databases.html "PostgreSQL 9.1 -
Chapter 23. Managing Databases") / [9.0](/docs/9.0/managing-databases.html
"PostgreSQL 9.0 - Chapter 23. Managing Databases") / [8.4](/docs/8.4/managing-
databases.html "PostgreSQL 8.4 - Chapter 23. Managing Databases") /
[8.3](/docs/8.3/managing-databases.html "PostgreSQL 8.3 - Chapter 23. Managing
Databases") / [8.2](/docs/8.2/managing-databases.html "PostgreSQL 8.2 -
Chapter 23. Managing Databases") / [8.1](/docs/8.1/managing-databases.html
"PostgreSQL 8.1 - Chapter 23. Managing Databases") / [8.0](/docs/8.0/managing-
databases.html "PostgreSQL 8.0 - Chapter 23. Managing Databases") /
[7.4](/docs/7.4/managing-databases.html "PostgreSQL 7.4 - Chapter 23. Managing
Databases") / [7.3](/docs/7.3/managing-databases.html "PostgreSQL 7.3 -
Chapter 23. Managing Databases") / [7.2](/docs/7.2/managing-databases.html
"PostgreSQL 7.2 - Chapter 23. Managing Databases") / [7.1](/docs/7.1/managing-
databases.html "PostgreSQL 7.1 - Chapter 23. Managing Databases")

__

Chapter 23. Managing Databases  
---  
[Prev](perm-functions.html "22.6. Function Security")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](manage-ag-overview.html "23.1. Overview")  
  
* * *

## Chapter 23. Managing Databases

**Table of Contents**

[23.1. Overview](manage-ag-overview.html)

[23.2. Creating a Database](manage-ag-createdb.html)

[23.3. Template Databases](manage-ag-templatedbs.html)

[23.4. Database Configuration](manage-ag-config.html)

[23.5. Destroying a Database](manage-ag-dropdb.html)

[23.6. Tablespaces](manage-ag-tablespaces.html)

Every instance of a running PostgreSQL server manages one or more databases.
Databases are therefore the topmost hierarchical level for organizing SQL
objects (“database objects”). This chapter describes the properties of
databases, and how to create, manage, and destroy them.

* * *

[Prev](perm-functions.html "22.6. Function Security")  | [Up](admin.html "Part III. Server Administration") |  [Next](manage-ag-overview.html "23.1. Overview")  
---|---|---  
22.6. Function Security  | [Home](index.html "PostgreSQL 16.9 Documentation") |  23.1. Overview  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/managing-databases.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

