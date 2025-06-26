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

Supported Versions: [Current](/docs/current/catalog-pg-policy.html "PostgreSQL
17 - 53.38. pg_policy") ([17](/docs/17/catalog-pg-policy.html "PostgreSQL 17 -
53.38. pg_policy")) / [16](/docs/16/catalog-pg-policy.html "PostgreSQL 16 -
53.38. pg_policy") / [15](/docs/15/catalog-pg-policy.html "PostgreSQL 15 -
53.38. pg_policy") / [14](/docs/14/catalog-pg-policy.html "PostgreSQL 14 -
53.38. pg_policy") / [13](/docs/13/catalog-pg-policy.html "PostgreSQL 13 -
53.38. pg_policy")

Development Versions: [18](/docs/18/catalog-pg-policy.html "PostgreSQL 18 -
53.38. pg_policy") / [devel](/docs/devel/catalog-pg-policy.html "PostgreSQL
devel - 53.38. pg_policy")

Unsupported versions: [12](/docs/12/catalog-pg-policy.html "PostgreSQL 12 -
53.38. pg_policy") / [11](/docs/11/catalog-pg-policy.html "PostgreSQL 11 -
53.38. pg_policy") / [10](/docs/10/catalog-pg-policy.html "PostgreSQL 10 -
53.38. pg_policy") / [9.6](/docs/9.6/catalog-pg-policy.html "PostgreSQL 9.6 -
53.38. pg_policy") / [9.5](/docs/9.5/catalog-pg-policy.html "PostgreSQL 9.5 -
53.38. pg_policy")

__

53.38. `pg_policy`  
---  
[Prev](catalog-pg-partitioned-table.html "53.37. pg_partitioned_table")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-proc.html "53.39. pg_proc")  
  
* * *

## 53.38. `pg_policy` #

The catalog `pg_policy` stores row-level security policies for tables. A
policy includes the kind of command that it applies to (possibly all
commands), the roles that it applies to, the expression to be added as a
security-barrier qualification to queries that include the table, and the
expression to be added as a `WITH CHECK` option for queries that attempt to
add new records to the table.

**Table  53.38. `pg_policy` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`polname` `name` The name of the policy  
`polrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table to which the policy applies  
`polcmd` `char` The command type to which the policy is applied: `r` for
[SELECT](sql-select.html "SELECT"), `a` for [INSERT](sql-insert.html
"INSERT"), `w` for [UPDATE](sql-update.html "UPDATE"), `d` for [DELETE](sql-
delete.html "DELETE"), or `*` for all  
`polpermissive` `bool` Is the policy permissive or restrictive?  
`polroles` `oid[]` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) The roles to which the policy is applied; zero means
`PUBLIC` (and normally appears alone in the array)  
`polqual` `pg_node_tree` The expression tree to be added to the security
barrier qualifications for queries that use the table  
`polwithcheck` `pg_node_tree` The expression tree to be added to the WITH
CHECK qualifications for queries that attempt to add rows to the table  
  
  

### Note

Policies stored in `pg_policy` are applied only when [`pg_class`](catalog-pg-
class.html "53.11. pg_class").`relrowsecurity` is set for their table.

* * *

[Prev](catalog-pg-partitioned-table.html "53.37. pg_partitioned_table")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-proc.html "53.39. pg_proc")  
---|---|---  
53.37. `pg_partitioned_table`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.39. `pg_proc`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-policy.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

