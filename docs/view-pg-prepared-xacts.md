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

Supported Versions: [Current](/docs/current/view-pg-prepared-xacts.html
"PostgreSQL 17 - 54.16. pg_prepared_xacts") ([17](/docs/17/view-pg-prepared-
xacts.html "PostgreSQL 17 - 54.16. pg_prepared_xacts")) / [16](/docs/16/view-
pg-prepared-xacts.html "PostgreSQL 16 - 54.16. pg_prepared_xacts") /
[15](/docs/15/view-pg-prepared-xacts.html "PostgreSQL 15 -
54.16. pg_prepared_xacts") / [14](/docs/14/view-pg-prepared-xacts.html
"PostgreSQL 14 - 54.16. pg_prepared_xacts") / [13](/docs/13/view-pg-prepared-
xacts.html "PostgreSQL 13 - 54.16. pg_prepared_xacts")

Development Versions: [18](/docs/18/view-pg-prepared-xacts.html "PostgreSQL 18
- 54.16. pg_prepared_xacts") / [devel](/docs/devel/view-pg-prepared-xacts.html
"PostgreSQL devel - 54.16. pg_prepared_xacts")

Unsupported versions: [12](/docs/12/view-pg-prepared-xacts.html "PostgreSQL 12
- 54.16. pg_prepared_xacts") / [11](/docs/11/view-pg-prepared-xacts.html
"PostgreSQL 11 - 54.16. pg_prepared_xacts") / [10](/docs/10/view-pg-prepared-
xacts.html "PostgreSQL 10 - 54.16. pg_prepared_xacts") / [9.6](/docs/9.6/view-
pg-prepared-xacts.html "PostgreSQL 9.6 - 54.16. pg_prepared_xacts") /
[9.5](/docs/9.5/view-pg-prepared-xacts.html "PostgreSQL 9.5 -
54.16. pg_prepared_xacts") / [9.4](/docs/9.4/view-pg-prepared-xacts.html
"PostgreSQL 9.4 - 54.16. pg_prepared_xacts") / [9.3](/docs/9.3/view-pg-
prepared-xacts.html "PostgreSQL 9.3 - 54.16. pg_prepared_xacts") /
[9.2](/docs/9.2/view-pg-prepared-xacts.html "PostgreSQL 9.2 -
54.16. pg_prepared_xacts") / [9.1](/docs/9.1/view-pg-prepared-xacts.html
"PostgreSQL 9.1 - 54.16. pg_prepared_xacts") / [9.0](/docs/9.0/view-pg-
prepared-xacts.html "PostgreSQL 9.0 - 54.16. pg_prepared_xacts") /
[8.4](/docs/8.4/view-pg-prepared-xacts.html "PostgreSQL 8.4 -
54.16. pg_prepared_xacts") / [8.3](/docs/8.3/view-pg-prepared-xacts.html
"PostgreSQL 8.3 - 54.16. pg_prepared_xacts") / [8.2](/docs/8.2/view-pg-
prepared-xacts.html "PostgreSQL 8.2 - 54.16. pg_prepared_xacts") /
[8.1](/docs/8.1/view-pg-prepared-xacts.html "PostgreSQL 8.1 -
54.16. pg_prepared_xacts")

__

54.16. `pg_prepared_xacts`  
---  
[Prev](view-pg-prepared-statements.html "54.15. pg_prepared_statements")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-publication-tables.html "54.17. pg_publication_tables")  
  
* * *

## 54.16. `pg_prepared_xacts` #

The view `pg_prepared_xacts` displays information about transactions that are
currently prepared for two-phase commit (see [PREPARE TRANSACTION](sql-
prepare-transaction.html "PREPARE TRANSACTION") for details).

`pg_prepared_xacts` contains one row per prepared transaction. An entry is
removed when the transaction is committed or rolled back.

**Table  54.16. `pg_prepared_xacts` Columns**

Column Type Description  
---  
`transaction` `xid` Numeric transaction identifier of the prepared transaction  
`gid` `text` Global transaction identifier that was assigned to the
transaction  
`prepared` `timestamptz` Time at which the transaction was prepared for commit  
`owner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Name of the user that executed the transaction  
`database` `name` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`datname`) Name of the database in which the transaction
was executed  
  
  

When the `pg_prepared_xacts` view is accessed, the internal transaction
manager data structures are momentarily locked, and a copy is made for the
view to display. This ensures that the view produces a consistent set of
results, while not blocking normal operations longer than necessary.
Nonetheless there could be some impact on database performance if this view is
frequently accessed.

* * *

[Prev](view-pg-prepared-statements.html "54.15. pg_prepared_statements")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-publication-tables.html "54.17. pg_publication_tables")  
---|---|---  
54.15. `pg_prepared_statements`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.17. `pg_publication_tables`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-prepared-xacts.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

