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

Supported Versions: [Current](/docs/current/infoschema-applicable-roles.html
"PostgreSQL 17 - 37.5. applicable_roles") ([17](/docs/17/infoschema-
applicable-roles.html "PostgreSQL 17 - 37.5. applicable_roles")) /
[16](/docs/16/infoschema-applicable-roles.html "PostgreSQL 16 -
37.5. applicable_roles") / [15](/docs/15/infoschema-applicable-roles.html
"PostgreSQL 15 - 37.5. applicable_roles") / [14](/docs/14/infoschema-
applicable-roles.html "PostgreSQL 14 - 37.5. applicable_roles") /
[13](/docs/13/infoschema-applicable-roles.html "PostgreSQL 13 -
37.5. applicable_roles")

Development Versions: [18](/docs/18/infoschema-applicable-roles.html
"PostgreSQL 18 - 37.5. applicable_roles") / [devel](/docs/devel/infoschema-
applicable-roles.html "PostgreSQL devel - 37.5. applicable_roles")

Unsupported versions: [12](/docs/12/infoschema-applicable-roles.html
"PostgreSQL 12 - 37.5. applicable_roles") / [11](/docs/11/infoschema-
applicable-roles.html "PostgreSQL 11 - 37.5. applicable_roles") /
[10](/docs/10/infoschema-applicable-roles.html "PostgreSQL 10 -
37.5. applicable_roles") / [9.6](/docs/9.6/infoschema-applicable-roles.html
"PostgreSQL 9.6 - 37.5. applicable_roles") / [9.5](/docs/9.5/infoschema-
applicable-roles.html "PostgreSQL 9.5 - 37.5. applicable_roles") /
[9.4](/docs/9.4/infoschema-applicable-roles.html "PostgreSQL 9.4 -
37.5. applicable_roles") / [9.3](/docs/9.3/infoschema-applicable-roles.html
"PostgreSQL 9.3 - 37.5. applicable_roles") / [9.2](/docs/9.2/infoschema-
applicable-roles.html "PostgreSQL 9.2 - 37.5. applicable_roles") /
[9.1](/docs/9.1/infoschema-applicable-roles.html "PostgreSQL 9.1 -
37.5. applicable_roles") / [9.0](/docs/9.0/infoschema-applicable-roles.html
"PostgreSQL 9.0 - 37.5. applicable_roles") / [8.4](/docs/8.4/infoschema-
applicable-roles.html "PostgreSQL 8.4 - 37.5. applicable_roles") /
[8.3](/docs/8.3/infoschema-applicable-roles.html "PostgreSQL 8.3 -
37.5. applicable_roles") / [8.2](/docs/8.2/infoschema-applicable-roles.html
"PostgreSQL 8.2 - 37.5. applicable_roles") / [8.1](/docs/8.1/infoschema-
applicable-roles.html "PostgreSQL 8.1 - 37.5. applicable_roles") /
[8.0](/docs/8.0/infoschema-applicable-roles.html "PostgreSQL 8.0 -
37.5. applicable_roles") / [7.4](/docs/7.4/infoschema-applicable-roles.html
"PostgreSQL 7.4 - 37.5. applicable_roles")

__

37.5. `applicable_roles`  
---  
[Prev](infoschema-administrable-role-authorizations.html "37.4. administrable_role_​authorizations")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-attributes.html "37.6. attributes")  
  
* * *

## 37.5. `applicable_roles` #

The view `applicable_roles` identifies all roles whose privileges the current
user can use. This means there is some chain of role grants from the current
user to the role in question. The current user itself is also an applicable
role. The set of applicable roles is generally used for permission checking.

**Table  37.3. `applicable_roles` Columns**

Column Type Description  
---  
`grantee` `sql_identifier` Name of the role to which this role membership was
granted (can be the current user, or a different role in case of nested role
memberships)  
`role_name` `sql_identifier` Name of a role  
`is_grantable` `yes_or_no` `YES` if the grantee has the admin option on the
role, `NO` if not  
  
  

* * *

[Prev](infoschema-administrable-role-authorizations.html "37.4. administrable_role_​authorizations")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-attributes.html "37.6. attributes")  
---|---|---  
37.4. `administrable_role_​authorizations`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.6. `attributes`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-applicable-
roles.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

