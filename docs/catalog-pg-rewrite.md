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

Supported Versions: [Current](/docs/current/catalog-pg-rewrite.html
"PostgreSQL 17 - 53.45. pg_rewrite") ([17](/docs/17/catalog-pg-rewrite.html
"PostgreSQL 17 - 53.45. pg_rewrite")) / [16](/docs/16/catalog-pg-rewrite.html
"PostgreSQL 16 - 53.45. pg_rewrite") / [15](/docs/15/catalog-pg-rewrite.html
"PostgreSQL 15 - 53.45. pg_rewrite") / [14](/docs/14/catalog-pg-rewrite.html
"PostgreSQL 14 - 53.45. pg_rewrite") / [13](/docs/13/catalog-pg-rewrite.html
"PostgreSQL 13 - 53.45. pg_rewrite")

Development Versions: [18](/docs/18/catalog-pg-rewrite.html "PostgreSQL 18 -
53.45. pg_rewrite") / [devel](/docs/devel/catalog-pg-rewrite.html "PostgreSQL
devel - 53.45. pg_rewrite")

Unsupported versions: [12](/docs/12/catalog-pg-rewrite.html "PostgreSQL 12 -
53.45. pg_rewrite") / [11](/docs/11/catalog-pg-rewrite.html "PostgreSQL 11 -
53.45. pg_rewrite") / [10](/docs/10/catalog-pg-rewrite.html "PostgreSQL 10 -
53.45. pg_rewrite") / [9.6](/docs/9.6/catalog-pg-rewrite.html "PostgreSQL 9.6
- 53.45. pg_rewrite") / [9.5](/docs/9.5/catalog-pg-rewrite.html "PostgreSQL
9.5 - 53.45. pg_rewrite") / [9.4](/docs/9.4/catalog-pg-rewrite.html
"PostgreSQL 9.4 - 53.45. pg_rewrite") / [9.3](/docs/9.3/catalog-pg-
rewrite.html "PostgreSQL 9.3 - 53.45. pg_rewrite") / [9.2](/docs/9.2/catalog-
pg-rewrite.html "PostgreSQL 9.2 - 53.45. pg_rewrite") /
[9.1](/docs/9.1/catalog-pg-rewrite.html "PostgreSQL 9.1 - 53.45. pg_rewrite")
/ [9.0](/docs/9.0/catalog-pg-rewrite.html "PostgreSQL 9.0 -
53.45. pg_rewrite") / [8.4](/docs/8.4/catalog-pg-rewrite.html "PostgreSQL 8.4
- 53.45. pg_rewrite") / [8.3](/docs/8.3/catalog-pg-rewrite.html "PostgreSQL
8.3 - 53.45. pg_rewrite") / [8.2](/docs/8.2/catalog-pg-rewrite.html
"PostgreSQL 8.2 - 53.45. pg_rewrite") / [8.1](/docs/8.1/catalog-pg-
rewrite.html "PostgreSQL 8.1 - 53.45. pg_rewrite") / [8.0](/docs/8.0/catalog-
pg-rewrite.html "PostgreSQL 8.0 - 53.45. pg_rewrite") /
[7.4](/docs/7.4/catalog-pg-rewrite.html "PostgreSQL 7.4 - 53.45. pg_rewrite")
/ [7.3](/docs/7.3/catalog-pg-rewrite.html "PostgreSQL 7.3 -
53.45. pg_rewrite") / [7.2](/docs/7.2/catalog-pg-rewrite.html "PostgreSQL 7.2
- 53.45. pg_rewrite")

__

53.45. `pg_rewrite`  
---  
[Prev](catalog-pg-replication-origin.html "53.44. pg_replication_origin")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-seclabel.html "53.46. pg_seclabel")  
  
* * *

## 53.45. `pg_rewrite` #

The catalog `pg_rewrite` stores rewrite rules for tables and views.

**Table  53.45. `pg_rewrite` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`rulename` `name` Rule name  
`ev_class` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table this rule is for  
`ev_type` `char` Event type that the rule is for: 1 = [SELECT](sql-select.html
"SELECT"), 2 = [UPDATE](sql-update.html "UPDATE"), 3 = [INSERT](sql-
insert.html "INSERT"), 4 = [DELETE](sql-delete.html "DELETE")  
`ev_enabled` `char` Controls in which [session_replication_role](runtime-
config-client.html#GUC-SESSION-REPLICATION-ROLE) modes the rule fires. `O` =
rule fires in “origin” and “local” modes, `D` = rule is disabled, `R` = rule
fires in “replica” mode, `A` = rule fires always.  
`is_instead` `bool` True if the rule is an `INSTEAD` rule  
`ev_qual` `pg_node_tree` Expression tree (in the form of a `nodeToString()`
representation) for the rule's qualifying condition  
`ev_action` `pg_node_tree` Query tree (in the form of a `nodeToString()`
representation) for the rule's action  
  
  

### Note

`pg_class.relhasrules` must be true if a table has any rules in this catalog.

* * *

[Prev](catalog-pg-replication-origin.html "53.44. pg_replication_origin")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-seclabel.html "53.46. pg_seclabel")  
---|---|---  
53.44. `pg_replication_origin`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.46. `pg_seclabel`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-rewrite.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

