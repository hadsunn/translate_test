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

Supported Versions: [Current](/docs/current/view-pg-user-mappings.html
"PostgreSQL 17 - 54.34. pg_user_mappings") ([17](/docs/17/view-pg-user-
mappings.html "PostgreSQL 17 - 54.34. pg_user_mappings")) /
[16](/docs/16/view-pg-user-mappings.html "PostgreSQL 16 -
54.34. pg_user_mappings") / [15](/docs/15/view-pg-user-mappings.html
"PostgreSQL 15 - 54.34. pg_user_mappings") / [14](/docs/14/view-pg-user-
mappings.html "PostgreSQL 14 - 54.34. pg_user_mappings") / [13](/docs/13/view-
pg-user-mappings.html "PostgreSQL 13 - 54.34. pg_user_mappings")

Development Versions: [18](/docs/18/view-pg-user-mappings.html "PostgreSQL 18
- 54.34. pg_user_mappings") / [devel](/docs/devel/view-pg-user-mappings.html
"PostgreSQL devel - 54.34. pg_user_mappings")

Unsupported versions: [12](/docs/12/view-pg-user-mappings.html "PostgreSQL 12
- 54.34. pg_user_mappings") / [11](/docs/11/view-pg-user-mappings.html
"PostgreSQL 11 - 54.34. pg_user_mappings") / [10](/docs/10/view-pg-user-
mappings.html "PostgreSQL 10 - 54.34. pg_user_mappings") /
[9.6](/docs/9.6/view-pg-user-mappings.html "PostgreSQL 9.6 -
54.34. pg_user_mappings") / [9.5](/docs/9.5/view-pg-user-mappings.html
"PostgreSQL 9.5 - 54.34. pg_user_mappings") / [9.4](/docs/9.4/view-pg-user-
mappings.html "PostgreSQL 9.4 - 54.34. pg_user_mappings") /
[9.3](/docs/9.3/view-pg-user-mappings.html "PostgreSQL 9.3 -
54.34. pg_user_mappings") / [9.2](/docs/9.2/view-pg-user-mappings.html
"PostgreSQL 9.2 - 54.34. pg_user_mappings") / [9.1](/docs/9.1/view-pg-user-
mappings.html "PostgreSQL 9.1 - 54.34. pg_user_mappings") /
[9.0](/docs/9.0/view-pg-user-mappings.html "PostgreSQL 9.0 -
54.34. pg_user_mappings") / [8.4](/docs/8.4/view-pg-user-mappings.html
"PostgreSQL 8.4 - 54.34. pg_user_mappings")

__

54.34. `pg_user_mappings`  
---  
[Prev](view-pg-user.html "54.33. pg_user")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-views.html "54.35. pg_views")  
  
* * *

## 54.34. `pg_user_mappings` #

The view `pg_user_mappings` provides access to information about user
mappings. This is essentially a publicly readable view of
[`pg_user_mapping`](catalog-pg-user-mapping.html "53.65. pg_user_mapping")
that leaves out the options field if the user has no rights to use it.

**Table  54.34. `pg_user_mappings` Columns**

Column Type Description  
---  
`umid` `oid` (references [`pg_user_mapping`](catalog-pg-user-mapping.html
"53.65. pg_user_mapping").`oid`) OID of the user mapping  
`srvid` `oid` (references [`pg_foreign_server`](catalog-pg-foreign-server.html
"53.24. pg_foreign_server").`oid`) The OID of the foreign server that contains
this mapping  
`srvname` `name` (references [`pg_foreign_server`](catalog-pg-foreign-
server.html "53.24. pg_foreign_server").`srvname`) Name of the foreign server  
`umuser` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) OID of the local role being mapped, or zero if the
user mapping is public  
`usename` `name` Name of the local user to be mapped  
`umoptions` `text[]` User mapping specific options, as “keyword=value” strings  
  
  

To protect password information stored as a user mapping option, the
`umoptions` column will read as null unless one of the following applies:

  * current user is the user being mapped, and owns the server or holds `USAGE` privilege on it

  * current user is the server owner and mapping is for `PUBLIC`

  * current user is a superuser

* * *

[Prev](view-pg-user.html "54.33. pg_user")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-views.html "54.35. pg_views")  
---|---|---  
54.33. `pg_user`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.35. `pg_views`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-user-mappings.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

