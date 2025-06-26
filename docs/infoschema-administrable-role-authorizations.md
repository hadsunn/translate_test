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

Supported Versions: [Current](/docs/current/infoschema-administrable-role-
authorizations.html "PostgreSQL 17 -
37.4. administrable_role_​authorizations") ([17](/docs/17/infoschema-
administrable-role-authorizations.html "PostgreSQL 17 -
37.4. administrable_role_​authorizations")) / [16](/docs/16/infoschema-
administrable-role-authorizations.html "PostgreSQL 16 -
37.4. administrable_role_​authorizations") / [15](/docs/15/infoschema-
administrable-role-authorizations.html "PostgreSQL 15 -
37.4. administrable_role_​authorizations") / [14](/docs/14/infoschema-
administrable-role-authorizations.html "PostgreSQL 14 -
37.4. administrable_role_​authorizations") / [13](/docs/13/infoschema-
administrable-role-authorizations.html "PostgreSQL 13 -
37.4. administrable_role_​authorizations")

Development Versions: [18](/docs/18/infoschema-administrable-role-
authorizations.html "PostgreSQL 18 -
37.4. administrable_role_​authorizations") / [devel](/docs/devel/infoschema-
administrable-role-authorizations.html "PostgreSQL devel -
37.4. administrable_role_​authorizations")

Unsupported versions: [12](/docs/12/infoschema-administrable-role-
authorizations.html "PostgreSQL 12 -
37.4. administrable_role_​authorizations") / [11](/docs/11/infoschema-
administrable-role-authorizations.html "PostgreSQL 11 -
37.4. administrable_role_​authorizations") / [10](/docs/10/infoschema-
administrable-role-authorizations.html "PostgreSQL 10 -
37.4. administrable_role_​authorizations") / [9.6](/docs/9.6/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.6 -
37.4. administrable_role_​authorizations") / [9.5](/docs/9.5/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.5 -
37.4. administrable_role_​authorizations") / [9.4](/docs/9.4/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.4 -
37.4. administrable_role_​authorizations") / [9.3](/docs/9.3/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.3 -
37.4. administrable_role_​authorizations") / [9.2](/docs/9.2/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.2 -
37.4. administrable_role_​authorizations") / [9.1](/docs/9.1/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.1 -
37.4. administrable_role_​authorizations") / [9.0](/docs/9.0/infoschema-
administrable-role-authorizations.html "PostgreSQL 9.0 -
37.4. administrable_role_​authorizations") / [8.4](/docs/8.4/infoschema-
administrable-role-authorizations.html "PostgreSQL 8.4 -
37.4. administrable_role_​authorizations") / [8.3](/docs/8.3/infoschema-
administrable-role-authorizations.html "PostgreSQL 8.3 -
37.4. administrable_role_​authorizations") / [8.2](/docs/8.2/infoschema-
administrable-role-authorizations.html "PostgreSQL 8.2 -
37.4. administrable_role_​authorizations")

__

37.4. `administrable_role_​authorizations`  
---  
[Prev](infoschema-information-schema-catalog-name.html "37.3. information_schema_catalog_name")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-applicable-roles.html "37.5. applicable_roles")  
  
* * *

## 37.4. `administrable_role_​authorizations` #

The view `administrable_role_authorizations` identifies all roles that the
current user has the admin option for.

**Table  37.2. `administrable_role_authorizations` Columns**

Column Type Description  
---  
`grantee` `sql_identifier` Name of the role to which this role membership was
granted (can be the current user, or a different role in case of nested role
memberships)  
`role_name` `sql_identifier` Name of a role  
`is_grantable` `yes_or_no` Always `YES`  
  
  

* * *

[Prev](infoschema-information-schema-catalog-name.html "37.3. information_schema_catalog_name")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-applicable-roles.html "37.5. applicable_roles")  
---|---|---  
37.3. `information_schema_catalog_name`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.5. `applicable_roles`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-administrable-role-
authorizations.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

