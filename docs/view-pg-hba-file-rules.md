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

Supported Versions: [Current](/docs/current/view-pg-hba-file-rules.html
"PostgreSQL 17 - 54.9. pg_hba_file_rules") ([17](/docs/17/view-pg-hba-file-
rules.html "PostgreSQL 17 - 54.9. pg_hba_file_rules")) / [16](/docs/16/view-
pg-hba-file-rules.html "PostgreSQL 16 - 54.9. pg_hba_file_rules") /
[15](/docs/15/view-pg-hba-file-rules.html "PostgreSQL 15 -
54.9. pg_hba_file_rules") / [14](/docs/14/view-pg-hba-file-rules.html
"PostgreSQL 14 - 54.9. pg_hba_file_rules") / [13](/docs/13/view-pg-hba-file-
rules.html "PostgreSQL 13 - 54.9. pg_hba_file_rules")

Development Versions: [18](/docs/18/view-pg-hba-file-rules.html "PostgreSQL 18
- 54.9. pg_hba_file_rules") / [devel](/docs/devel/view-pg-hba-file-rules.html
"PostgreSQL devel - 54.9. pg_hba_file_rules")

Unsupported versions: [12](/docs/12/view-pg-hba-file-rules.html "PostgreSQL 12
- 54.9. pg_hba_file_rules") / [11](/docs/11/view-pg-hba-file-rules.html
"PostgreSQL 11 - 54.9. pg_hba_file_rules") / [10](/docs/10/view-pg-hba-file-
rules.html "PostgreSQL 10 - 54.9. pg_hba_file_rules")

__

54.9. `pg_hba_file_rules`  
---  
[Prev](view-pg-group.html "54.8. pg_group")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-ident-file-mappings.html "54.10. pg_ident_file_mappings")  
  
* * *

## 54.9. `pg_hba_file_rules` #

The view `pg_hba_file_rules` provides a summary of the contents of the client
authentication configuration file, [`pg_hba.conf`](auth-pg-hba-conf.html
"21.1. The pg_hba.conf File"). A row appears in this view for each non-empty,
non-comment line in the file, with annotations indicating whether the rule
could be applied successfully.

This view can be helpful for checking whether planned changes in the
authentication configuration file will work, or for diagnosing a previous
failure. Note that this view reports on the _current_ contents of the file,
not on what was last loaded by the server.

By default, the `pg_hba_file_rules` view can be read only by superusers.

**Table  54.9. `pg_hba_file_rules` Columns**

Column Type Description  
---  
`rule_number` `int4` Number of this rule, if valid, otherwise `NULL`. This
indicates the order in which each rule is considered until a match is found
during authentication.  
`file_name` `text` Name of the file containing this rule  
`line_number` `int4` Line number of this rule in `file_name`  
`type` `text` Type of connection  
`database` `text[]` List of database name(s) to which this rule applies  
`user_name` `text[]` List of user and group name(s) to which this rule applies  
`address` `text` Host name or IP address, or one of `all`, `samehost`, or
`samenet`, or null for local connections  
`netmask` `text` IP address mask, or null if not applicable  
`auth_method` `text` Authentication method  
`options` `text[]` Options specified for authentication method, if any  
`error` `text` If not null, an error message indicating why this line could
not be processed  
  
  

Usually, a row reflecting an incorrect entry will have values for only the
`line_number` and `error` fields.

See [Chapter 21](client-authentication.html "Chapter 21. Client
Authentication") for more information about client authentication
configuration.

* * *

[Prev](view-pg-group.html "54.8. pg_group")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-ident-file-mappings.html "54.10. pg_ident_file_mappings")  
---|---|---  
54.8. `pg_group`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.10. `pg_ident_file_mappings`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-hba-file-rules.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

