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

Supported Versions: [Current](/docs/current/view-pg-user.html "PostgreSQL 17 -
54.33. pg_user") ([17](/docs/17/view-pg-user.html "PostgreSQL 17 -
54.33. pg_user")) / [16](/docs/16/view-pg-user.html "PostgreSQL 16 -
54.33. pg_user") / [15](/docs/15/view-pg-user.html "PostgreSQL 15 -
54.33. pg_user") / [14](/docs/14/view-pg-user.html "PostgreSQL 14 -
54.33. pg_user") / [13](/docs/13/view-pg-user.html "PostgreSQL 13 -
54.33. pg_user")

Development Versions: [18](/docs/18/view-pg-user.html "PostgreSQL 18 -
54.33. pg_user") / [devel](/docs/devel/view-pg-user.html "PostgreSQL devel -
54.33. pg_user")

Unsupported versions: [12](/docs/12/view-pg-user.html "PostgreSQL 12 -
54.33. pg_user") / [11](/docs/11/view-pg-user.html "PostgreSQL 11 -
54.33. pg_user") / [10](/docs/10/view-pg-user.html "PostgreSQL 10 -
54.33. pg_user") / [9.6](/docs/9.6/view-pg-user.html "PostgreSQL 9.6 -
54.33. pg_user") / [9.5](/docs/9.5/view-pg-user.html "PostgreSQL 9.5 -
54.33. pg_user") / [9.4](/docs/9.4/view-pg-user.html "PostgreSQL 9.4 -
54.33. pg_user") / [9.3](/docs/9.3/view-pg-user.html "PostgreSQL 9.3 -
54.33. pg_user") / [9.2](/docs/9.2/view-pg-user.html "PostgreSQL 9.2 -
54.33. pg_user") / [9.1](/docs/9.1/view-pg-user.html "PostgreSQL 9.1 -
54.33. pg_user") / [9.0](/docs/9.0/view-pg-user.html "PostgreSQL 9.0 -
54.33. pg_user") / [8.4](/docs/8.4/view-pg-user.html "PostgreSQL 8.4 -
54.33. pg_user") / [8.3](/docs/8.3/view-pg-user.html "PostgreSQL 8.3 -
54.33. pg_user") / [8.2](/docs/8.2/view-pg-user.html "PostgreSQL 8.2 -
54.33. pg_user") / [8.1](/docs/8.1/view-pg-user.html "PostgreSQL 8.1 -
54.33. pg_user") / [8.0](/docs/8.0/view-pg-user.html "PostgreSQL 8.0 -
54.33. pg_user") / [7.4](/docs/7.4/view-pg-user.html "PostgreSQL 7.4 -
54.33. pg_user")

__

54.33. `pg_user`  
---  
[Prev](view-pg-timezone-names.html "54.32. pg_timezone_names")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-user-mappings.html "54.34. pg_user_mappings")  
  
* * *

## 54.33. `pg_user` #

The view `pg_user` provides access to information about database users. This
is simply a publicly readable view of [`pg_shadow`](view-pg-shadow.html
"54.25. pg_shadow") that blanks out the password field.

**Table  54.33. `pg_user` Columns**

Column Type Description  
---  
`usename` `name` User name  
`usesysid` `oid` ID of this user  
`usecreatedb` `bool` User can create databases  
`usesuper` `bool` User is a superuser  
`userepl` `bool` User can initiate streaming replication and put the system in
and out of backup mode.  
`usebypassrls` `bool` User bypasses every row-level security policy, see
[Section 5.8](ddl-rowsecurity.html "5.8. Row Security Policies") for more
information.  
`passwd` `text` Not the password (always reads as `********`)  
`valuntil` `timestamptz` Password expiry time (only used for password
authentication)  
`useconfig` `text[]` Session defaults for run-time configuration variables  
  
  

* * *

[Prev](view-pg-timezone-names.html "54.32. pg_timezone_names")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-user-mappings.html "54.34. pg_user_mappings")  
---|---|---  
54.32. `pg_timezone_names`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.34. `pg_user_mappings`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-user.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

