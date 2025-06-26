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

Supported Versions: [Current](/docs/current/view-pg-policies.html "PostgreSQL
17 - 54.14. pg_policies") ([17](/docs/17/view-pg-policies.html "PostgreSQL 17
- 54.14. pg_policies")) / [16](/docs/16/view-pg-policies.html "PostgreSQL 16 -
54.14. pg_policies") / [15](/docs/15/view-pg-policies.html "PostgreSQL 15 -
54.14. pg_policies") / [14](/docs/14/view-pg-policies.html "PostgreSQL 14 -
54.14. pg_policies") / [13](/docs/13/view-pg-policies.html "PostgreSQL 13 -
54.14. pg_policies")

Development Versions: [18](/docs/18/view-pg-policies.html "PostgreSQL 18 -
54.14. pg_policies") / [devel](/docs/devel/view-pg-policies.html "PostgreSQL
devel - 54.14. pg_policies")

Unsupported versions: [12](/docs/12/view-pg-policies.html "PostgreSQL 12 -
54.14. pg_policies") / [11](/docs/11/view-pg-policies.html "PostgreSQL 11 -
54.14. pg_policies") / [10](/docs/10/view-pg-policies.html "PostgreSQL 10 -
54.14. pg_policies") / [9.6](/docs/9.6/view-pg-policies.html "PostgreSQL 9.6 -
54.14. pg_policies") / [9.5](/docs/9.5/view-pg-policies.html "PostgreSQL 9.5 -
54.14. pg_policies")

__

54.14. `pg_policies`  
---  
[Prev](view-pg-matviews.html "54.13. pg_matviews")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-prepared-statements.html "54.15. pg_prepared_statements")  
  
* * *

## 54.14. `pg_policies` #

The view `pg_policies` provides access to useful information about each row-
level security policy in the database.

**Table  54.14. `pg_policies` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing table policy is on  
`tablename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of table policy is on  
`policyname` `name` (references [`pg_policy`](catalog-pg-policy.html
"53.38. pg_policy").`polname`) Name of policy  
`permissive` `text` Is the policy permissive or restrictive?  
`roles` `name[]` The roles to which this policy applies  
`cmd` `text` The command type to which the policy is applied  
`qual` `text` The expression added to the security barrier qualifications for
queries that this policy applies to  
`with_check` `text` The expression added to the WITH CHECK qualifications for
queries that attempt to add rows to this table  
  
  

* * *

[Prev](view-pg-matviews.html "54.13. pg_matviews")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-prepared-statements.html "54.15. pg_prepared_statements")  
---|---|---  
54.13. `pg_matviews`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.15. `pg_prepared_statements`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-policies.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

