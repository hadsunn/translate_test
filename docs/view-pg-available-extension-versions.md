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

Supported Versions: [Current](/docs/current/view-pg-available-extension-
versions.html "PostgreSQL 17 - 54.3. pg_available_extension_versions")
([17](/docs/17/view-pg-available-extension-versions.html "PostgreSQL 17 -
54.3. pg_available_extension_versions")) / [16](/docs/16/view-pg-available-
extension-versions.html "PostgreSQL 16 -
54.3. pg_available_extension_versions") / [15](/docs/15/view-pg-available-
extension-versions.html "PostgreSQL 15 -
54.3. pg_available_extension_versions") / [14](/docs/14/view-pg-available-
extension-versions.html "PostgreSQL 14 -
54.3. pg_available_extension_versions") / [13](/docs/13/view-pg-available-
extension-versions.html "PostgreSQL 13 -
54.3. pg_available_extension_versions")

Development Versions: [18](/docs/18/view-pg-available-extension-versions.html
"PostgreSQL 18 - 54.3. pg_available_extension_versions") /
[devel](/docs/devel/view-pg-available-extension-versions.html "PostgreSQL
devel - 54.3. pg_available_extension_versions")

Unsupported versions: [12](/docs/12/view-pg-available-extension-versions.html
"PostgreSQL 12 - 54.3. pg_available_extension_versions") / [11](/docs/11/view-
pg-available-extension-versions.html "PostgreSQL 11 -
54.3. pg_available_extension_versions") / [10](/docs/10/view-pg-available-
extension-versions.html "PostgreSQL 10 -
54.3. pg_available_extension_versions") / [9.6](/docs/9.6/view-pg-available-
extension-versions.html "PostgreSQL 9.6 -
54.3. pg_available_extension_versions") / [9.5](/docs/9.5/view-pg-available-
extension-versions.html "PostgreSQL 9.5 -
54.3. pg_available_extension_versions") / [9.4](/docs/9.4/view-pg-available-
extension-versions.html "PostgreSQL 9.4 -
54.3. pg_available_extension_versions") / [9.3](/docs/9.3/view-pg-available-
extension-versions.html "PostgreSQL 9.3 -
54.3. pg_available_extension_versions") / [9.2](/docs/9.2/view-pg-available-
extension-versions.html "PostgreSQL 9.2 -
54.3. pg_available_extension_versions") / [9.1](/docs/9.1/view-pg-available-
extension-versions.html "PostgreSQL 9.1 -
54.3. pg_available_extension_versions")

__

54.3. `pg_available_extension_versions`  
---  
[Prev](view-pg-available-extensions.html "54.2. pg_available_extensions")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-backend-memory-contexts.html "54.4. pg_backend_memory_contexts")  
  
* * *

## 54.3. `pg_available_extension_versions` #

The `pg_available_extension_versions` view lists the specific extension
versions that are available for installation. See also the
[`pg_extension`](catalog-pg-extension.html "53.22. pg_extension") catalog,
which shows the extensions currently installed.

**Table  54.3. `pg_available_extension_versions` Columns**

Column Type Description  
---  
`name` `name` Extension name  
`version` `text` Version name  
`installed` `bool` True if this version of this extension is currently
installed  
`superuser` `bool` True if only superusers are allowed to install this
extension (but see `trusted`)  
`trusted` `bool` True if the extension can be installed by non-superusers with
appropriate privileges  
`relocatable` `bool` True if extension can be relocated to another schema  
`schema` `name` Name of the schema that the extension must be installed into,
or `NULL` if partially or fully relocatable  
`requires` `name[]` Names of prerequisite extensions, or `NULL` if none  
`comment` `text` Comment string from the extension's control file  
  
  

The `pg_available_extension_versions` view is read-only.

* * *

[Prev](view-pg-available-extensions.html "54.2. pg_available_extensions")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-backend-memory-contexts.html "54.4. pg_backend_memory_contexts")  
---|---|---  
54.2. `pg_available_extensions`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.4. `pg_backend_memory_contexts`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-available-extension-
versions.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

