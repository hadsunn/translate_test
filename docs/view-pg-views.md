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

Supported Versions: [Current](/docs/current/view-pg-views.html "PostgreSQL 17
- 54.35. pg_views") ([17](/docs/17/view-pg-views.html "PostgreSQL 17 -
54.35. pg_views")) / [16](/docs/16/view-pg-views.html "PostgreSQL 16 -
54.35. pg_views") / [15](/docs/15/view-pg-views.html "PostgreSQL 15 -
54.35. pg_views") / [14](/docs/14/view-pg-views.html "PostgreSQL 14 -
54.35. pg_views") / [13](/docs/13/view-pg-views.html "PostgreSQL 13 -
54.35. pg_views")

Development Versions: [18](/docs/18/view-pg-views.html "PostgreSQL 18 -
54.35. pg_views") / [devel](/docs/devel/view-pg-views.html "PostgreSQL devel -
54.35. pg_views")

Unsupported versions: [12](/docs/12/view-pg-views.html "PostgreSQL 12 -
54.35. pg_views") / [11](/docs/11/view-pg-views.html "PostgreSQL 11 -
54.35. pg_views") / [10](/docs/10/view-pg-views.html "PostgreSQL 10 -
54.35. pg_views") / [9.6](/docs/9.6/view-pg-views.html "PostgreSQL 9.6 -
54.35. pg_views") / [9.5](/docs/9.5/view-pg-views.html "PostgreSQL 9.5 -
54.35. pg_views") / [9.4](/docs/9.4/view-pg-views.html "PostgreSQL 9.4 -
54.35. pg_views") / [9.3](/docs/9.3/view-pg-views.html "PostgreSQL 9.3 -
54.35. pg_views") / [9.2](/docs/9.2/view-pg-views.html "PostgreSQL 9.2 -
54.35. pg_views") / [9.1](/docs/9.1/view-pg-views.html "PostgreSQL 9.1 -
54.35. pg_views") / [9.0](/docs/9.0/view-pg-views.html "PostgreSQL 9.0 -
54.35. pg_views") / [8.4](/docs/8.4/view-pg-views.html "PostgreSQL 8.4 -
54.35. pg_views") / [8.3](/docs/8.3/view-pg-views.html "PostgreSQL 8.3 -
54.35. pg_views") / [8.2](/docs/8.2/view-pg-views.html "PostgreSQL 8.2 -
54.35. pg_views") / [8.1](/docs/8.1/view-pg-views.html "PostgreSQL 8.1 -
54.35. pg_views") / [8.0](/docs/8.0/view-pg-views.html "PostgreSQL 8.0 -
54.35. pg_views") / [7.4](/docs/7.4/view-pg-views.html "PostgreSQL 7.4 -
54.35. pg_views")

__

54.35. `pg_views`  
---  
[Prev](view-pg-user-mappings.html "54.34. pg_user_mappings")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](protocol.html "Chapter 55. Frontend/Backend Protocol")  
  
* * *

## 54.35. `pg_views` #

The view `pg_views` provides access to useful information about each view in
the database.

**Table  54.35. `pg_views` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing view  
`viewname` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of view  
`viewowner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Name of view's owner  
`definition` `text` View definition (a reconstructed [SELECT](sql-select.html
"SELECT") query)  
  
  

* * *

[Prev](view-pg-user-mappings.html "54.34. pg_user_mappings")  | [Up](views.html "Chapter 54. System Views") |  [Next](protocol.html "Chapter 55. Frontend/Backend Protocol")  
---|---|---  
54.34. `pg_user_mappings`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 55. Frontend/Backend Protocol  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-views.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

