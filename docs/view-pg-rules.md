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

Supported Versions: [Current](/docs/current/view-pg-rules.html "PostgreSQL 17
- 54.21. pg_rules") ([17](/docs/17/view-pg-rules.html "PostgreSQL 17 -
54.21. pg_rules")) / [16](/docs/16/view-pg-rules.html "PostgreSQL 16 -
54.21. pg_rules") / [15](/docs/15/view-pg-rules.html "PostgreSQL 15 -
54.21. pg_rules") / [14](/docs/14/view-pg-rules.html "PostgreSQL 14 -
54.21. pg_rules") / [13](/docs/13/view-pg-rules.html "PostgreSQL 13 -
54.21. pg_rules")

Development Versions: [18](/docs/18/view-pg-rules.html "PostgreSQL 18 -
54.21. pg_rules") / [devel](/docs/devel/view-pg-rules.html "PostgreSQL devel -
54.21. pg_rules")

Unsupported versions: [12](/docs/12/view-pg-rules.html "PostgreSQL 12 -
54.21. pg_rules") / [11](/docs/11/view-pg-rules.html "PostgreSQL 11 -
54.21. pg_rules") / [10](/docs/10/view-pg-rules.html "PostgreSQL 10 -
54.21. pg_rules") / [9.6](/docs/9.6/view-pg-rules.html "PostgreSQL 9.6 -
54.21. pg_rules") / [9.5](/docs/9.5/view-pg-rules.html "PostgreSQL 9.5 -
54.21. pg_rules") / [9.4](/docs/9.4/view-pg-rules.html "PostgreSQL 9.4 -
54.21. pg_rules") / [9.3](/docs/9.3/view-pg-rules.html "PostgreSQL 9.3 -
54.21. pg_rules") / [9.2](/docs/9.2/view-pg-rules.html "PostgreSQL 9.2 -
54.21. pg_rules") / [9.1](/docs/9.1/view-pg-rules.html "PostgreSQL 9.1 -
54.21. pg_rules") / [9.0](/docs/9.0/view-pg-rules.html "PostgreSQL 9.0 -
54.21. pg_rules") / [8.4](/docs/8.4/view-pg-rules.html "PostgreSQL 8.4 -
54.21. pg_rules") / [8.3](/docs/8.3/view-pg-rules.html "PostgreSQL 8.3 -
54.21. pg_rules") / [8.2](/docs/8.2/view-pg-rules.html "PostgreSQL 8.2 -
54.21. pg_rules") / [8.1](/docs/8.1/view-pg-rules.html "PostgreSQL 8.1 -
54.21. pg_rules") / [8.0](/docs/8.0/view-pg-rules.html "PostgreSQL 8.0 -
54.21. pg_rules") / [7.4](/docs/7.4/view-pg-rules.html "PostgreSQL 7.4 -
54.21. pg_rules")

__

54.21. `pg_rules`  
---  
[Prev](view-pg-roles.html "54.20. pg_roles")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-seclabels.html "54.22. pg_seclabels")  
  
* * *

## 54.21. `pg_rules` #

The view `pg_rules` provides access to useful information about query rewrite
rules.

**Table  54.21. `pg_rules` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table the rule is for  
`rulename` `name` (references [`pg_rewrite`](catalog-pg-rewrite.html
"53.45. pg_rewrite").`rulename`) Name of rule  
`definition` `text` Rule definition (a reconstructed creation command)  
  
  

The `pg_rules` view excludes the `ON SELECT` rules of views and materialized
views; those can be seen in [`pg_views`](view-pg-views.html "54.35. pg_views")
and [`pg_matviews`](view-pg-matviews.html "54.13. pg_matviews").

* * *

[Prev](view-pg-roles.html "54.20. pg_roles")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-seclabels.html "54.22. pg_seclabels")  
---|---|---  
54.20. `pg_roles`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.22. `pg_seclabels`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-rules.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

