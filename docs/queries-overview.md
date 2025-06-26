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

Supported Versions: [Current](/docs/current/queries-overview.html "PostgreSQL
17 - 7.1. Overview") ([17](/docs/17/queries-overview.html "PostgreSQL 17 -
7.1. Overview")) / [16](/docs/16/queries-overview.html "PostgreSQL 16 -
7.1. Overview") / [15](/docs/15/queries-overview.html "PostgreSQL 15 -
7.1. Overview") / [14](/docs/14/queries-overview.html "PostgreSQL 14 -
7.1. Overview") / [13](/docs/13/queries-overview.html "PostgreSQL 13 -
7.1. Overview")

Development Versions: [18](/docs/18/queries-overview.html "PostgreSQL 18 -
7.1. Overview") / [devel](/docs/devel/queries-overview.html "PostgreSQL devel
- 7.1. Overview")

Unsupported versions: [12](/docs/12/queries-overview.html "PostgreSQL 12 -
7.1. Overview") / [11](/docs/11/queries-overview.html "PostgreSQL 11 -
7.1. Overview") / [10](/docs/10/queries-overview.html "PostgreSQL 10 -
7.1. Overview") / [9.6](/docs/9.6/queries-overview.html "PostgreSQL 9.6 -
7.1. Overview") / [9.5](/docs/9.5/queries-overview.html "PostgreSQL 9.5 -
7.1. Overview") / [9.4](/docs/9.4/queries-overview.html "PostgreSQL 9.4 -
7.1. Overview") / [9.3](/docs/9.3/queries-overview.html "PostgreSQL 9.3 -
7.1. Overview") / [9.2](/docs/9.2/queries-overview.html "PostgreSQL 9.2 -
7.1. Overview") / [9.1](/docs/9.1/queries-overview.html "PostgreSQL 9.1 -
7.1. Overview") / [9.0](/docs/9.0/queries-overview.html "PostgreSQL 9.0 -
7.1. Overview") / [8.4](/docs/8.4/queries-overview.html "PostgreSQL 8.4 -
7.1. Overview") / [8.3](/docs/8.3/queries-overview.html "PostgreSQL 8.3 -
7.1. Overview") / [8.2](/docs/8.2/queries-overview.html "PostgreSQL 8.2 -
7.1. Overview")

__

7.1. Overview  
---  
[Prev](queries.html "Chapter 7. Queries")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-table-expressions.html "7.2. Table Expressions")  
  
* * *

## 7.1. Overview #

The process of retrieving or the command to retrieve data from a database is
called a _query_. In SQL the [`SELECT`](sql-select.html "SELECT") command is
used to specify queries. The general syntax of the `SELECT` command is

    
    
    [WITH _with_queries_] SELECT _select_list_ FROM _table_expression_ [_sort_specification_]
    

The following sections describe the details of the select list, the table
expression, and the sort specification. `WITH` queries are treated last since
they are an advanced feature.

A simple kind of query has the form:

    
    
    SELECT * FROM table1;
    

Assuming that there is a table called `table1`, this command would retrieve
all rows and all user-defined columns from `table1`. (The method of retrieval
depends on the client application. For example, the psql program will display
an ASCII-art table on the screen, while client libraries will offer functions
to extract individual values from the query result.) The select list
specification `*` means all columns that the table expression happens to
provide. A select list can also select a subset of the available columns or
make calculations using the columns. For example, if `table1` has columns
named `a`, `b`, and `c` (and perhaps others) you can make the following query:

    
    
    SELECT a, b + c FROM table1;
    

(assuming that `b` and `c` are of a numerical data type). See [Section
7.3](queries-select-lists.html "7.3. Select Lists") for more details.

`FROM table1` is a simple kind of table expression: it reads just one table.
In general, table expressions can be complex constructs of base tables, joins,
and subqueries. But you can also omit the table expression entirely and use
the `SELECT` command as a calculator:

    
    
    SELECT 3 * 4;
    

This is more useful if the expressions in the select list return varying
results. For example, you could call a function this way:

    
    
    SELECT random();
    

* * *

[Prev](queries.html "Chapter 7. Queries")  | [Up](queries.html "Chapter 7. Queries") |  [Next](queries-table-expressions.html "7.2. Table Expressions")  
---|---|---  
Chapter 7. Queries  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.2. Table Expressions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-overview.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

