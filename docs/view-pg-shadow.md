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

Supported Versions: [Current](/docs/current/view-pg-shadow.html "PostgreSQL 17
- 54.25. pg_shadow") ([17](/docs/17/view-pg-shadow.html "PostgreSQL 17 -
54.25. pg_shadow")) / [16](/docs/16/view-pg-shadow.html "PostgreSQL 16 -
54.25. pg_shadow") / [15](/docs/15/view-pg-shadow.html "PostgreSQL 15 -
54.25. pg_shadow") / [14](/docs/14/view-pg-shadow.html "PostgreSQL 14 -
54.25. pg_shadow") / [13](/docs/13/view-pg-shadow.html "PostgreSQL 13 -
54.25. pg_shadow")

Development Versions: [18](/docs/18/view-pg-shadow.html "PostgreSQL 18 -
54.25. pg_shadow") / [devel](/docs/devel/view-pg-shadow.html "PostgreSQL devel
- 54.25. pg_shadow")

Unsupported versions: [12](/docs/12/view-pg-shadow.html "PostgreSQL 12 -
54.25. pg_shadow") / [11](/docs/11/view-pg-shadow.html "PostgreSQL 11 -
54.25. pg_shadow") / [10](/docs/10/view-pg-shadow.html "PostgreSQL 10 -
54.25. pg_shadow") / [9.6](/docs/9.6/view-pg-shadow.html "PostgreSQL 9.6 -
54.25. pg_shadow") / [9.5](/docs/9.5/view-pg-shadow.html "PostgreSQL 9.5 -
54.25. pg_shadow") / [9.4](/docs/9.4/view-pg-shadow.html "PostgreSQL 9.4 -
54.25. pg_shadow") / [9.3](/docs/9.3/view-pg-shadow.html "PostgreSQL 9.3 -
54.25. pg_shadow") / [9.2](/docs/9.2/view-pg-shadow.html "PostgreSQL 9.2 -
54.25. pg_shadow") / [9.1](/docs/9.1/view-pg-shadow.html "PostgreSQL 9.1 -
54.25. pg_shadow") / [9.0](/docs/9.0/view-pg-shadow.html "PostgreSQL 9.0 -
54.25. pg_shadow") / [8.4](/docs/8.4/view-pg-shadow.html "PostgreSQL 8.4 -
54.25. pg_shadow") / [8.3](/docs/8.3/view-pg-shadow.html "PostgreSQL 8.3 -
54.25. pg_shadow") / [8.2](/docs/8.2/view-pg-shadow.html "PostgreSQL 8.2 -
54.25. pg_shadow") / [8.1](/docs/8.1/view-pg-shadow.html "PostgreSQL 8.1 -
54.25. pg_shadow")

__

54.25. `pg_shadow`  
---  
[Prev](view-pg-settings.html "54.24. pg_settings")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-shmem-allocations.html "54.26. pg_shmem_allocations")  
  
* * *

## 54.25. `pg_shadow` #

The view `pg_shadow` exists for backwards compatibility: it emulates a catalog
that existed in PostgreSQL before version 8.1. It shows properties of all
roles that are marked as `rolcanlogin` in [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").

The name stems from the fact that this table should not be readable by the
public since it contains passwords. [`pg_user`](view-pg-user.html
"54.33. pg_user") is a publicly readable view on `pg_shadow` that blanks out
the password field.

**Table  54.25. `pg_shadow` Columns**

Column Type Description  
---  
`usename` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) User name  
`usesysid` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) ID of this user  
`usecreatedb` `bool` User can create databases  
`usesuper` `bool` User is a superuser  
`userepl` `bool` User can initiate streaming replication and put the system in
and out of backup mode.  
`usebypassrls` `bool` User bypasses every row-level security policy, see
[Section 5.8](ddl-rowsecurity.html "5.8. Row Security Policies") for more
information.  
`passwd` `text` Password (possibly encrypted); null if none. See
[`pg_authid`](catalog-pg-authid.html "53.8. pg_authid") for details of how
encrypted passwords are stored.  
`valuntil` `timestamptz` Password expiry time (only used for password
authentication)  
`useconfig` `text[]` Session defaults for run-time configuration variables  
  
  

* * *

[Prev](view-pg-settings.html "54.24. pg_settings")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-shmem-allocations.html "54.26. pg_shmem_allocations")  
---|---|---  
54.24. `pg_settings`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.26. `pg_shmem_allocations`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-shadow.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

