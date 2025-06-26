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

Supported Versions: [Current](/docs/current/view-pg-group.html "PostgreSQL 17
- 54.8. pg_group") ([17](/docs/17/view-pg-group.html "PostgreSQL 17 -
54.8. pg_group")) / [16](/docs/16/view-pg-group.html "PostgreSQL 16 -
54.8. pg_group") / [15](/docs/15/view-pg-group.html "PostgreSQL 15 -
54.8. pg_group") / [14](/docs/14/view-pg-group.html "PostgreSQL 14 -
54.8. pg_group") / [13](/docs/13/view-pg-group.html "PostgreSQL 13 -
54.8. pg_group")

Development Versions: [18](/docs/18/view-pg-group.html "PostgreSQL 18 -
54.8. pg_group") / [devel](/docs/devel/view-pg-group.html "PostgreSQL devel -
54.8. pg_group")

Unsupported versions: [12](/docs/12/view-pg-group.html "PostgreSQL 12 -
54.8. pg_group") / [11](/docs/11/view-pg-group.html "PostgreSQL 11 -
54.8. pg_group") / [10](/docs/10/view-pg-group.html "PostgreSQL 10 -
54.8. pg_group") / [9.6](/docs/9.6/view-pg-group.html "PostgreSQL 9.6 -
54.8. pg_group") / [9.5](/docs/9.5/view-pg-group.html "PostgreSQL 9.5 -
54.8. pg_group") / [9.4](/docs/9.4/view-pg-group.html "PostgreSQL 9.4 -
54.8. pg_group") / [9.3](/docs/9.3/view-pg-group.html "PostgreSQL 9.3 -
54.8. pg_group") / [9.2](/docs/9.2/view-pg-group.html "PostgreSQL 9.2 -
54.8. pg_group") / [9.1](/docs/9.1/view-pg-group.html "PostgreSQL 9.1 -
54.8. pg_group") / [9.0](/docs/9.0/view-pg-group.html "PostgreSQL 9.0 -
54.8. pg_group") / [8.4](/docs/8.4/view-pg-group.html "PostgreSQL 8.4 -
54.8. pg_group") / [8.3](/docs/8.3/view-pg-group.html "PostgreSQL 8.3 -
54.8. pg_group") / [8.2](/docs/8.2/view-pg-group.html "PostgreSQL 8.2 -
54.8. pg_group") / [8.1](/docs/8.1/view-pg-group.html "PostgreSQL 8.1 -
54.8. pg_group")

__

54.8. `pg_group`  
---  
[Prev](view-pg-file-settings.html "54.7. pg_file_settings")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-hba-file-rules.html "54.9. pg_hba_file_rules")  
  
* * *

## 54.8. `pg_group` #

The view `pg_group` exists for backwards compatibility: it emulates a catalog
that existed in PostgreSQL before version 8.1. It shows the names and members
of all roles that are marked as not `rolcanlogin`, which is an approximation
to the set of roles that are being used as groups.

**Table  54.8. `pg_group` Columns**

Column Type Description  
---  
`groname` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Name of the group  
`grosysid` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) ID of this group  
`grolist` `oid[]` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) An array containing the IDs of the roles in this
group  
  
  

* * *

[Prev](view-pg-file-settings.html "54.7. pg_file_settings")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-hba-file-rules.html "54.9. pg_hba_file_rules")  
---|---|---  
54.7. `pg_file_settings`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.9. `pg_hba_file_rules`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-group.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

