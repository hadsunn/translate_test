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

Supported Versions: [Current](/docs/current/view-pg-prepared-statements.html
"PostgreSQL 17 - 54.15. pg_prepared_statements") ([17](/docs/17/view-pg-
prepared-statements.html "PostgreSQL 17 - 54.15. pg_prepared_statements")) /
[16](/docs/16/view-pg-prepared-statements.html "PostgreSQL 16 -
54.15. pg_prepared_statements") / [15](/docs/15/view-pg-prepared-
statements.html "PostgreSQL 15 - 54.15. pg_prepared_statements") /
[14](/docs/14/view-pg-prepared-statements.html "PostgreSQL 14 -
54.15. pg_prepared_statements") / [13](/docs/13/view-pg-prepared-
statements.html "PostgreSQL 13 - 54.15. pg_prepared_statements")

Development Versions: [18](/docs/18/view-pg-prepared-statements.html
"PostgreSQL 18 - 54.15. pg_prepared_statements") / [devel](/docs/devel/view-
pg-prepared-statements.html "PostgreSQL devel -
54.15. pg_prepared_statements")

Unsupported versions: [12](/docs/12/view-pg-prepared-statements.html
"PostgreSQL 12 - 54.15. pg_prepared_statements") / [11](/docs/11/view-pg-
prepared-statements.html "PostgreSQL 11 - 54.15. pg_prepared_statements") /
[10](/docs/10/view-pg-prepared-statements.html "PostgreSQL 10 -
54.15. pg_prepared_statements") / [9.6](/docs/9.6/view-pg-prepared-
statements.html "PostgreSQL 9.6 - 54.15. pg_prepared_statements") /
[9.5](/docs/9.5/view-pg-prepared-statements.html "PostgreSQL 9.5 -
54.15. pg_prepared_statements") / [9.4](/docs/9.4/view-pg-prepared-
statements.html "PostgreSQL 9.4 - 54.15. pg_prepared_statements") /
[9.3](/docs/9.3/view-pg-prepared-statements.html "PostgreSQL 9.3 -
54.15. pg_prepared_statements") / [9.2](/docs/9.2/view-pg-prepared-
statements.html "PostgreSQL 9.2 - 54.15. pg_prepared_statements") /
[9.1](/docs/9.1/view-pg-prepared-statements.html "PostgreSQL 9.1 -
54.15. pg_prepared_statements") / [9.0](/docs/9.0/view-pg-prepared-
statements.html "PostgreSQL 9.0 - 54.15. pg_prepared_statements") /
[8.4](/docs/8.4/view-pg-prepared-statements.html "PostgreSQL 8.4 -
54.15. pg_prepared_statements") / [8.3](/docs/8.3/view-pg-prepared-
statements.html "PostgreSQL 8.3 - 54.15. pg_prepared_statements") /
[8.2](/docs/8.2/view-pg-prepared-statements.html "PostgreSQL 8.2 -
54.15. pg_prepared_statements")

__

54.15. `pg_prepared_statements`  
---  
[Prev](view-pg-policies.html "54.14. pg_policies")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-prepared-xacts.html "54.16. pg_prepared_xacts")  
  
* * *

## 54.15. `pg_prepared_statements` #

The `pg_prepared_statements` view displays all the prepared statements that
are available in the current session. See [PREPARE](sql-prepare.html
"PREPARE") for more information about prepared statements.

`pg_prepared_statements` contains one row for each prepared statement. Rows
are added to the view when a new prepared statement is created and removed
when a prepared statement is released (for example, via the
[`DEALLOCATE`](sql-deallocate.html "DEALLOCATE") command).

**Table  54.15. `pg_prepared_statements` Columns**

Column Type Description  
---  
`name` `text` The identifier of the prepared statement  
`statement` `text` The query string submitted by the client to create this
prepared statement. For prepared statements created via SQL, this is the
`PREPARE` statement submitted by the client. For prepared statements created
via the frontend/backend protocol, this is the text of the prepared statement
itself.  
`prepare_time` `timestamptz` The time at which the prepared statement was
created  
`parameter_types` `regtype[]` The expected parameter types for the prepared
statement in the form of an array of `regtype`. The OID corresponding to an
element of this array can be obtained by casting the `regtype` value to `oid`.  
`result_types` `regtype[]` The types of the columns returned by the prepared
statement in the form of an array of `regtype`. The OID corresponding to an
element of this array can be obtained by casting the `regtype` value to `oid`.
If the prepared statement does not provide a result (e.g., a DML statement),
then this field will be null.  
`from_sql` `bool` `true` if the prepared statement was created via the
`PREPARE` SQL command; `false` if the statement was prepared via the
frontend/backend protocol  
`generic_plans` `int8` Number of times generic plan was chosen  
`custom_plans` `int8` Number of times custom plan was chosen  
  
  

The `pg_prepared_statements` view is read-only.

* * *

[Prev](view-pg-policies.html "54.14. pg_policies")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-prepared-xacts.html "54.16. pg_prepared_xacts")  
---|---|---  
54.14. `pg_policies`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.16. `pg_prepared_xacts`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-prepared-
statements.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

