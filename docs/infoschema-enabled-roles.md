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

Supported Versions: [Current](/docs/current/infoschema-enabled-roles.html
"PostgreSQL 17 - 37.25. enabled_roles") ([17](/docs/17/infoschema-enabled-
roles.html "PostgreSQL 17 - 37.25. enabled_roles")) /
[16](/docs/16/infoschema-enabled-roles.html "PostgreSQL 16 -
37.25. enabled_roles") / [15](/docs/15/infoschema-enabled-roles.html
"PostgreSQL 15 - 37.25. enabled_roles") / [14](/docs/14/infoschema-enabled-
roles.html "PostgreSQL 14 - 37.25. enabled_roles") / [13](/docs/13/infoschema-
enabled-roles.html "PostgreSQL 13 - 37.25. enabled_roles")

Development Versions: [18](/docs/18/infoschema-enabled-roles.html "PostgreSQL
18 - 37.25. enabled_roles") / [devel](/docs/devel/infoschema-enabled-
roles.html "PostgreSQL devel - 37.25. enabled_roles")

Unsupported versions: [12](/docs/12/infoschema-enabled-roles.html "PostgreSQL
12 - 37.25. enabled_roles") / [11](/docs/11/infoschema-enabled-roles.html
"PostgreSQL 11 - 37.25. enabled_roles") / [10](/docs/10/infoschema-enabled-
roles.html "PostgreSQL 10 - 37.25. enabled_roles") /
[9.6](/docs/9.6/infoschema-enabled-roles.html "PostgreSQL 9.6 -
37.25. enabled_roles") / [9.5](/docs/9.5/infoschema-enabled-roles.html
"PostgreSQL 9.5 - 37.25. enabled_roles") / [9.4](/docs/9.4/infoschema-enabled-
roles.html "PostgreSQL 9.4 - 37.25. enabled_roles") /
[9.3](/docs/9.3/infoschema-enabled-roles.html "PostgreSQL 9.3 -
37.25. enabled_roles") / [9.2](/docs/9.2/infoschema-enabled-roles.html
"PostgreSQL 9.2 - 37.25. enabled_roles") / [9.1](/docs/9.1/infoschema-enabled-
roles.html "PostgreSQL 9.1 - 37.25. enabled_roles") /
[9.0](/docs/9.0/infoschema-enabled-roles.html "PostgreSQL 9.0 -
37.25. enabled_roles") / [8.4](/docs/8.4/infoschema-enabled-roles.html
"PostgreSQL 8.4 - 37.25. enabled_roles") / [8.3](/docs/8.3/infoschema-enabled-
roles.html "PostgreSQL 8.3 - 37.25. enabled_roles") /
[8.2](/docs/8.2/infoschema-enabled-roles.html "PostgreSQL 8.2 -
37.25. enabled_roles") / [8.1](/docs/8.1/infoschema-enabled-roles.html
"PostgreSQL 8.1 - 37.25. enabled_roles") / [8.0](/docs/8.0/infoschema-enabled-
roles.html "PostgreSQL 8.0 - 37.25. enabled_roles") /
[7.4](/docs/7.4/infoschema-enabled-roles.html "PostgreSQL 7.4 -
37.25. enabled_roles")

__

37.25. `enabled_roles`  
---  
[Prev](infoschema-element-types.html "37.24. element_types")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-foreign-data-wrapper-options.html "37.26. foreign_data_wrapper_options")  
  
* * *

## 37.25. `enabled_roles` #

The view `enabled_roles` identifies the currently “enabled roles”. The enabled
roles are recursively defined as the current user together with all roles that
have been granted to the enabled roles with automatic inheritance. In other
words, these are all roles that the current user has direct or indirect,
automatically inheriting membership in.

For permission checking, the set of “applicable roles” is applied, which can
be broader than the set of enabled roles. So generally, it is better to use
the view `applicable_roles` instead of this one; See [Section
37.5](infoschema-applicable-roles.html "37.5. applicable_roles") for details
on `applicable_roles` view.

**Table  37.23. `enabled_roles` Columns**

Column Type Description  
---  
`role_name` `sql_identifier` Name of a role  
  
  

* * *

[Prev](infoschema-element-types.html "37.24. element_types")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-foreign-data-wrapper-options.html "37.26. foreign_data_wrapper_options")  
---|---|---  
37.24. `element_types`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.26. `foreign_data_wrapper_options`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-enabled-
roles.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

