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

Supported Versions: [Current](/docs/current/view-pg-available-extensions.html
"PostgreSQL 17 - 54.2. pg_available_extensions") ([17](/docs/17/view-pg-
available-extensions.html "PostgreSQL 17 - 54.2. pg_available_extensions")) /
[16](/docs/16/view-pg-available-extensions.html "PostgreSQL 16 -
54.2. pg_available_extensions") / [15](/docs/15/view-pg-available-
extensions.html "PostgreSQL 15 - 54.2. pg_available_extensions") /
[14](/docs/14/view-pg-available-extensions.html "PostgreSQL 14 -
54.2. pg_available_extensions") / [13](/docs/13/view-pg-available-
extensions.html "PostgreSQL 13 - 54.2. pg_available_extensions")

Development Versions: [18](/docs/18/view-pg-available-extensions.html
"PostgreSQL 18 - 54.2. pg_available_extensions") / [devel](/docs/devel/view-
pg-available-extensions.html "PostgreSQL devel -
54.2. pg_available_extensions")

Unsupported versions: [12](/docs/12/view-pg-available-extensions.html
"PostgreSQL 12 - 54.2. pg_available_extensions") / [11](/docs/11/view-pg-
available-extensions.html "PostgreSQL 11 - 54.2. pg_available_extensions") /
[10](/docs/10/view-pg-available-extensions.html "PostgreSQL 10 -
54.2. pg_available_extensions") / [9.6](/docs/9.6/view-pg-available-
extensions.html "PostgreSQL 9.6 - 54.2. pg_available_extensions") /
[9.5](/docs/9.5/view-pg-available-extensions.html "PostgreSQL 9.5 -
54.2. pg_available_extensions") / [9.4](/docs/9.4/view-pg-available-
extensions.html "PostgreSQL 9.4 - 54.2. pg_available_extensions") /
[9.3](/docs/9.3/view-pg-available-extensions.html "PostgreSQL 9.3 -
54.2. pg_available_extensions") / [9.2](/docs/9.2/view-pg-available-
extensions.html "PostgreSQL 9.2 - 54.2. pg_available_extensions") /
[9.1](/docs/9.1/view-pg-available-extensions.html "PostgreSQL 9.1 -
54.2. pg_available_extensions")

__

54.2. `pg_available_extensions`  
---  
[Prev](views-overview.html "54.1. Overview")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-available-extension-versions.html "54.3. pg_available_extension_versions")  
  
* * *

## 54.2. `pg_available_extensions` #

The `pg_available_extensions` view lists the extensions that are available for
installation. See also the [`pg_extension`](catalog-pg-extension.html
"53.22. pg_extension") catalog, which shows the extensions currently
installed.

**Table  54.2. `pg_available_extensions` Columns**

Column Type Description  
---  
`name` `name` Extension name  
`default_version` `text` Name of default version, or `NULL` if none is
specified  
`installed_version` `text` Currently installed version of the extension, or
`NULL` if not installed  
`comment` `text` Comment string from the extension's control file  
  
  

The `pg_available_extensions` view is read-only.

* * *

[Prev](views-overview.html "54.1. Overview")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-available-extension-versions.html "54.3. pg_available_extension_versions")  
---|---|---  
54.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.3. `pg_available_extension_versions`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-available-
extensions.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

