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

Supported Versions: [Current](/docs/current/tutorial-concepts.html "PostgreSQL
17 - 2.2. Concepts") ([17](/docs/17/tutorial-concepts.html "PostgreSQL 17 -
2.2. Concepts")) / [16](/docs/16/tutorial-concepts.html "PostgreSQL 16 -
2.2. Concepts") / [15](/docs/15/tutorial-concepts.html "PostgreSQL 15 -
2.2. Concepts") / [14](/docs/14/tutorial-concepts.html "PostgreSQL 14 -
2.2. Concepts") / [13](/docs/13/tutorial-concepts.html "PostgreSQL 13 -
2.2. Concepts")

Development Versions: [18](/docs/18/tutorial-concepts.html "PostgreSQL 18 -
2.2. Concepts") / [devel](/docs/devel/tutorial-concepts.html "PostgreSQL devel
- 2.2. Concepts")

Unsupported versions: [12](/docs/12/tutorial-concepts.html "PostgreSQL 12 -
2.2. Concepts") / [11](/docs/11/tutorial-concepts.html "PostgreSQL 11 -
2.2. Concepts") / [10](/docs/10/tutorial-concepts.html "PostgreSQL 10 -
2.2. Concepts") / [9.6](/docs/9.6/tutorial-concepts.html "PostgreSQL 9.6 -
2.2. Concepts") / [9.5](/docs/9.5/tutorial-concepts.html "PostgreSQL 9.5 -
2.2. Concepts") / [9.4](/docs/9.4/tutorial-concepts.html "PostgreSQL 9.4 -
2.2. Concepts") / [9.3](/docs/9.3/tutorial-concepts.html "PostgreSQL 9.3 -
2.2. Concepts") / [9.2](/docs/9.2/tutorial-concepts.html "PostgreSQL 9.2 -
2.2. Concepts") / [9.1](/docs/9.1/tutorial-concepts.html "PostgreSQL 9.1 -
2.2. Concepts") / [9.0](/docs/9.0/tutorial-concepts.html "PostgreSQL 9.0 -
2.2. Concepts") / [8.4](/docs/8.4/tutorial-concepts.html "PostgreSQL 8.4 -
2.2. Concepts") / [8.3](/docs/8.3/tutorial-concepts.html "PostgreSQL 8.3 -
2.2. Concepts") / [8.2](/docs/8.2/tutorial-concepts.html "PostgreSQL 8.2 -
2.2. Concepts") / [8.1](/docs/8.1/tutorial-concepts.html "PostgreSQL 8.1 -
2.2. Concepts") / [8.0](/docs/8.0/tutorial-concepts.html "PostgreSQL 8.0 -
2.2. Concepts") / [7.4](/docs/7.4/tutorial-concepts.html "PostgreSQL 7.4 -
2.2. Concepts") / [7.3](/docs/7.3/tutorial-concepts.html "PostgreSQL 7.3 -
2.2. Concepts") / [7.2](/docs/7.2/tutorial-concepts.html "PostgreSQL 7.2 -
2.2. Concepts")

__

2.2. Concepts  
---  
[Prev](tutorial-sql-intro.html "2.1. Introduction")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-table.html "2.3. Creating a New Table")  
  
* * *

## 2.2. Concepts #

PostgreSQL is a _relational database management system_ (RDBMS). That means it
is a system for managing data stored in _relations_. Relation is essentially a
mathematical term for _table_. The notion of storing data in tables is so
commonplace today that it might seem inherently obvious, but there are a
number of other ways of organizing databases. Files and directories on Unix-
like operating systems form an example of a hierarchical database. A more
modern development is the object-oriented database.

Each table is a named collection of _rows_. Each row of a given table has the
same set of named _columns_ , and each column is of a specific data type.
Whereas columns have a fixed order in each row, it is important to remember
that SQL does not guarantee the order of the rows within the table in any way
(although they can be explicitly sorted for display).

Tables are grouped into databases, and a collection of databases managed by a
single PostgreSQL server instance constitutes a database _cluster_.

* * *

[Prev](tutorial-sql-intro.html "2.1. Introduction")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-table.html "2.3. Creating a New Table")  
---|---|---  
2.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.3. Creating a New Table  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-concepts.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

