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

Supported Versions: [Current](/docs/current/catalog-pg-default-acl.html
"PostgreSQL 17 - 53.17. pg_default_acl") ([17](/docs/17/catalog-pg-default-
acl.html "PostgreSQL 17 - 53.17. pg_default_acl")) / [16](/docs/16/catalog-pg-
default-acl.html "PostgreSQL 16 - 53.17. pg_default_acl") /
[15](/docs/15/catalog-pg-default-acl.html "PostgreSQL 15 -
53.17. pg_default_acl") / [14](/docs/14/catalog-pg-default-acl.html
"PostgreSQL 14 - 53.17. pg_default_acl") / [13](/docs/13/catalog-pg-default-
acl.html "PostgreSQL 13 - 53.17. pg_default_acl")

Development Versions: [18](/docs/18/catalog-pg-default-acl.html "PostgreSQL 18
- 53.17. pg_default_acl") / [devel](/docs/devel/catalog-pg-default-acl.html
"PostgreSQL devel - 53.17. pg_default_acl")

Unsupported versions: [12](/docs/12/catalog-pg-default-acl.html "PostgreSQL 12
- 53.17. pg_default_acl") / [11](/docs/11/catalog-pg-default-acl.html
"PostgreSQL 11 - 53.17. pg_default_acl") / [10](/docs/10/catalog-pg-default-
acl.html "PostgreSQL 10 - 53.17. pg_default_acl") / [9.6](/docs/9.6/catalog-
pg-default-acl.html "PostgreSQL 9.6 - 53.17. pg_default_acl") /
[9.5](/docs/9.5/catalog-pg-default-acl.html "PostgreSQL 9.5 -
53.17. pg_default_acl") / [9.4](/docs/9.4/catalog-pg-default-acl.html
"PostgreSQL 9.4 - 53.17. pg_default_acl") / [9.3](/docs/9.3/catalog-pg-
default-acl.html "PostgreSQL 9.3 - 53.17. pg_default_acl") /
[9.2](/docs/9.2/catalog-pg-default-acl.html "PostgreSQL 9.2 -
53.17. pg_default_acl") / [9.1](/docs/9.1/catalog-pg-default-acl.html
"PostgreSQL 9.1 - 53.17. pg_default_acl") / [9.0](/docs/9.0/catalog-pg-
default-acl.html "PostgreSQL 9.0 - 53.17. pg_default_acl")

__

53.17. `pg_default_acl`  
---  
[Prev](catalog-pg-db-role-setting.html "53.16. pg_db_role_setting")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-depend.html "53.18. pg_depend")  
  
* * *

## 53.17. `pg_default_acl` #

The catalog `pg_default_acl` stores initial privileges to be assigned to newly
created objects.

**Table  53.17. `pg_default_acl` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`defaclrole` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) The OID of the role associated with this entry  
`defaclnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace associated with this
entry, or zero if none  
`defaclobjtype` `char` Type of object this entry is for: `r` = relation
(table, view), `S` = sequence, `f` = function, `T` = type, `n` = schema  
`defaclacl` `aclitem[]` Access privileges that this type of object should have
on creation  
  
  

A `pg_default_acl` entry shows the initial privileges to be assigned to an
object belonging to the indicated user. There are currently two types of
entry: “global” entries with `defaclnamespace` = zero, and “per-schema”
entries that reference a particular schema. If a global entry is present then
it _overrides_ the normal hard-wired default privileges for the object type. A
per-schema entry, if present, represents privileges to be _added to_ the
global or hard-wired default privileges.

Note that when an ACL entry in another catalog is null, it is taken to
represent the hard-wired default privileges for its object, _not_ whatever
might be in `pg_default_acl` at the moment. `pg_default_acl` is only consulted
during object creation.

* * *

[Prev](catalog-pg-db-role-setting.html "53.16. pg_db_role_setting")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-depend.html "53.18. pg_depend")  
---|---|---  
53.16. `pg_db_role_setting`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.18. `pg_depend`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-default-acl.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

