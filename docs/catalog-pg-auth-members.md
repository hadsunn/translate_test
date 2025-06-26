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

Supported Versions: [Current](/docs/current/catalog-pg-auth-members.html
"PostgreSQL 17 - 53.9. pg_auth_members") ([17](/docs/17/catalog-pg-auth-
members.html "PostgreSQL 17 - 53.9. pg_auth_members")) /
[16](/docs/16/catalog-pg-auth-members.html "PostgreSQL 16 -
53.9. pg_auth_members") / [15](/docs/15/catalog-pg-auth-members.html
"PostgreSQL 15 - 53.9. pg_auth_members") / [14](/docs/14/catalog-pg-auth-
members.html "PostgreSQL 14 - 53.9. pg_auth_members") / [13](/docs/13/catalog-
pg-auth-members.html "PostgreSQL 13 - 53.9. pg_auth_members")

Development Versions: [18](/docs/18/catalog-pg-auth-members.html "PostgreSQL
18 - 53.9. pg_auth_members") / [devel](/docs/devel/catalog-pg-auth-
members.html "PostgreSQL devel - 53.9. pg_auth_members")

Unsupported versions: [12](/docs/12/catalog-pg-auth-members.html "PostgreSQL
12 - 53.9. pg_auth_members") / [11](/docs/11/catalog-pg-auth-members.html
"PostgreSQL 11 - 53.9. pg_auth_members") / [10](/docs/10/catalog-pg-auth-
members.html "PostgreSQL 10 - 53.9. pg_auth_members") /
[9.6](/docs/9.6/catalog-pg-auth-members.html "PostgreSQL 9.6 -
53.9. pg_auth_members") / [9.5](/docs/9.5/catalog-pg-auth-members.html
"PostgreSQL 9.5 - 53.9. pg_auth_members") / [9.4](/docs/9.4/catalog-pg-auth-
members.html "PostgreSQL 9.4 - 53.9. pg_auth_members") /
[9.3](/docs/9.3/catalog-pg-auth-members.html "PostgreSQL 9.3 -
53.9. pg_auth_members") / [9.2](/docs/9.2/catalog-pg-auth-members.html
"PostgreSQL 9.2 - 53.9. pg_auth_members") / [9.1](/docs/9.1/catalog-pg-auth-
members.html "PostgreSQL 9.1 - 53.9. pg_auth_members") /
[9.0](/docs/9.0/catalog-pg-auth-members.html "PostgreSQL 9.0 -
53.9. pg_auth_members") / [8.4](/docs/8.4/catalog-pg-auth-members.html
"PostgreSQL 8.4 - 53.9. pg_auth_members") / [8.3](/docs/8.3/catalog-pg-auth-
members.html "PostgreSQL 8.3 - 53.9. pg_auth_members") /
[8.2](/docs/8.2/catalog-pg-auth-members.html "PostgreSQL 8.2 -
53.9. pg_auth_members") / [8.1](/docs/8.1/catalog-pg-auth-members.html
"PostgreSQL 8.1 - 53.9. pg_auth_members")

__

53.9. `pg_auth_members`  
---  
[Prev](catalog-pg-authid.html "53.8. pg_authid")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-cast.html "53.10. pg_cast")  
  
* * *

## 53.9. `pg_auth_members` #

The catalog `pg_auth_members` shows the membership relations between roles.
Any non-circular set of relationships is allowed.

Because user identities are cluster-wide, `pg_auth_members` is shared across
all databases of a cluster: there is only one copy of `pg_auth_members` per
cluster, not one per database.

**Table  53.9. `pg_auth_members` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`roleid` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) ID of a role that has a member  
`member` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) ID of a role that is a member of `roleid`  
`grantor` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) ID of the role that granted this membership  
`admin_option` `bool` True if `member` can grant membership in `roleid` to
others  
`inherit_option` `bool` True if the member automatically inherits the
privileges of the granted role  
`set_option` `bool` True if the member can [`SET ROLE`](sql-set-role.html "SET
ROLE") to the granted role  
  
  

* * *

[Prev](catalog-pg-authid.html "53.8. pg_authid")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-cast.html "53.10. pg_cast")  
---|---|---  
53.8. `pg_authid`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.10. `pg_cast`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-auth-members.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

