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

Supported Versions: [Current](/docs/current/view-pg-roles.html "PostgreSQL 17
- 54.20. pg_roles") ([17](/docs/17/view-pg-roles.html "PostgreSQL 17 -
54.20. pg_roles")) / [16](/docs/16/view-pg-roles.html "PostgreSQL 16 -
54.20. pg_roles") / [15](/docs/15/view-pg-roles.html "PostgreSQL 15 -
54.20. pg_roles") / [14](/docs/14/view-pg-roles.html "PostgreSQL 14 -
54.20. pg_roles") / [13](/docs/13/view-pg-roles.html "PostgreSQL 13 -
54.20. pg_roles")

Development Versions: [18](/docs/18/view-pg-roles.html "PostgreSQL 18 -
54.20. pg_roles") / [devel](/docs/devel/view-pg-roles.html "PostgreSQL devel -
54.20. pg_roles")

Unsupported versions: [12](/docs/12/view-pg-roles.html "PostgreSQL 12 -
54.20. pg_roles") / [11](/docs/11/view-pg-roles.html "PostgreSQL 11 -
54.20. pg_roles") / [10](/docs/10/view-pg-roles.html "PostgreSQL 10 -
54.20. pg_roles") / [9.6](/docs/9.6/view-pg-roles.html "PostgreSQL 9.6 -
54.20. pg_roles") / [9.5](/docs/9.5/view-pg-roles.html "PostgreSQL 9.5 -
54.20. pg_roles") / [9.4](/docs/9.4/view-pg-roles.html "PostgreSQL 9.4 -
54.20. pg_roles") / [9.3](/docs/9.3/view-pg-roles.html "PostgreSQL 9.3 -
54.20. pg_roles") / [9.2](/docs/9.2/view-pg-roles.html "PostgreSQL 9.2 -
54.20. pg_roles") / [9.1](/docs/9.1/view-pg-roles.html "PostgreSQL 9.1 -
54.20. pg_roles") / [9.0](/docs/9.0/view-pg-roles.html "PostgreSQL 9.0 -
54.20. pg_roles") / [8.4](/docs/8.4/view-pg-roles.html "PostgreSQL 8.4 -
54.20. pg_roles") / [8.3](/docs/8.3/view-pg-roles.html "PostgreSQL 8.3 -
54.20. pg_roles") / [8.2](/docs/8.2/view-pg-roles.html "PostgreSQL 8.2 -
54.20. pg_roles") / [8.1](/docs/8.1/view-pg-roles.html "PostgreSQL 8.1 -
54.20. pg_roles")

__

54.20. `pg_roles`  
---  
[Prev](view-pg-replication-slots.html "54.19. pg_replication_slots")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-rules.html "54.21. pg_rules")  
  
* * *

## 54.20. `pg_roles` #

The view `pg_roles` provides access to information about database roles. This
is simply a publicly readable view of [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid") that blanks out the password field.

**Table  54.20. `pg_roles` Columns**

Column Type Description  
---  
`rolname` `name` Role name  
`rolsuper` `bool` Role has superuser privileges  
`rolinherit` `bool` Role automatically inherits privileges of roles it is a
member of  
`rolcreaterole` `bool` Role can create more roles  
`rolcreatedb` `bool` Role can create databases  
`rolcanlogin` `bool` Role can log in. That is, this role can be given as the
initial session authorization identifier  
`rolreplication` `bool` Role is a replication role. A replication role can
initiate replication connections and create and drop replication slots.  
`rolconnlimit` `int4` For roles that can log in, this sets maximum number of
concurrent connections this role can make. -1 means no limit.  
`rolpassword` `text` Not the password (always reads as `********`)  
`rolvaliduntil` `timestamptz` Password expiry time (only used for password
authentication); null if no expiration  
`rolbypassrls` `bool` Role bypasses every row-level security policy, see
[Section 5.8](ddl-rowsecurity.html "5.8. Row Security Policies") for more
information.  
`rolconfig` `text[]` Role-specific defaults for run-time configuration
variables  
`oid` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) ID of role  
  
  

* * *

[Prev](view-pg-replication-slots.html "54.19. pg_replication_slots")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-rules.html "54.21. pg_rules")  
---|---|---  
54.19. `pg_replication_slots`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.21. `pg_rules`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-roles.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

