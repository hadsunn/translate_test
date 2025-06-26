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

Supported Versions: [Current](/docs/current/catalog-pg-language.html
"PostgreSQL 17 - 53.29. pg_language") ([17](/docs/17/catalog-pg-language.html
"PostgreSQL 17 - 53.29. pg_language")) / [16](/docs/16/catalog-pg-
language.html "PostgreSQL 16 - 53.29. pg_language") / [15](/docs/15/catalog-
pg-language.html "PostgreSQL 15 - 53.29. pg_language") /
[14](/docs/14/catalog-pg-language.html "PostgreSQL 14 - 53.29. pg_language") /
[13](/docs/13/catalog-pg-language.html "PostgreSQL 13 - 53.29. pg_language")

Development Versions: [18](/docs/18/catalog-pg-language.html "PostgreSQL 18 -
53.29. pg_language") / [devel](/docs/devel/catalog-pg-language.html
"PostgreSQL devel - 53.29. pg_language")

Unsupported versions: [12](/docs/12/catalog-pg-language.html "PostgreSQL 12 -
53.29. pg_language") / [11](/docs/11/catalog-pg-language.html "PostgreSQL 11 -
53.29. pg_language") / [10](/docs/10/catalog-pg-language.html "PostgreSQL 10 -
53.29. pg_language") / [9.6](/docs/9.6/catalog-pg-language.html "PostgreSQL
9.6 - 53.29. pg_language") / [9.5](/docs/9.5/catalog-pg-language.html
"PostgreSQL 9.5 - 53.29. pg_language") / [9.4](/docs/9.4/catalog-pg-
language.html "PostgreSQL 9.4 - 53.29. pg_language") /
[9.3](/docs/9.3/catalog-pg-language.html "PostgreSQL 9.3 -
53.29. pg_language") / [9.2](/docs/9.2/catalog-pg-language.html "PostgreSQL
9.2 - 53.29. pg_language") / [9.1](/docs/9.1/catalog-pg-language.html
"PostgreSQL 9.1 - 53.29. pg_language") / [9.0](/docs/9.0/catalog-pg-
language.html "PostgreSQL 9.0 - 53.29. pg_language") /
[8.4](/docs/8.4/catalog-pg-language.html "PostgreSQL 8.4 -
53.29. pg_language") / [8.3](/docs/8.3/catalog-pg-language.html "PostgreSQL
8.3 - 53.29. pg_language") / [8.2](/docs/8.2/catalog-pg-language.html
"PostgreSQL 8.2 - 53.29. pg_language") / [8.1](/docs/8.1/catalog-pg-
language.html "PostgreSQL 8.1 - 53.29. pg_language") /
[8.0](/docs/8.0/catalog-pg-language.html "PostgreSQL 8.0 -
53.29. pg_language") / [7.4](/docs/7.4/catalog-pg-language.html "PostgreSQL
7.4 - 53.29. pg_language") / [7.3](/docs/7.3/catalog-pg-language.html
"PostgreSQL 7.3 - 53.29. pg_language") / [7.2](/docs/7.2/catalog-pg-
language.html "PostgreSQL 7.2 - 53.29. pg_language") /
[7.1](/docs/7.1/catalog-pg-language.html "PostgreSQL 7.1 -
53.29. pg_language")

__

53.29. `pg_language`  
---  
[Prev](catalog-pg-init-privs.html "53.28. pg_init_privs")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-largeobject.html "53.30. pg_largeobject")  
  
* * *

## 53.29. `pg_language` #

The catalog `pg_language` registers languages in which you can write functions
or stored procedures. See [CREATE LANGUAGE](sql-createlanguage.html "CREATE
LANGUAGE") and [Chapter 42](xplang.html "Chapter 42. Procedural Languages")
for more information about language handlers.

**Table  53.29. `pg_language` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`lanname` `name` Name of the language  
`lanowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the language  
`lanispl` `bool` This is false for internal languages (such as SQL) and true
for user-defined languages. Currently, pg_dump still uses this to determine
which languages need to be dumped, but this might be replaced by a different
mechanism in the future.  
`lanpltrusted` `bool` True if this is a trusted language, which means that it
is believed not to grant access to anything outside the normal SQL execution
environment. Only superusers can create functions in untrusted languages.  
`lanplcallfoid` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) For noninternal languages this references the
language handler, which is a special function that is responsible for
executing all functions that are written in the particular language. Zero for
internal languages.  
`laninline` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) This references a function that is responsible for
executing “inline” anonymous code blocks ([DO](sql-do.html "DO") blocks). Zero
if inline blocks are not supported.  
`lanvalidator` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) This references a language validator function that is
responsible for checking the syntax and validity of new functions when they
are created. Zero if no validator is provided.  
`lanacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

* * *

[Prev](catalog-pg-init-privs.html "53.28. pg_init_privs")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-largeobject.html "53.30. pg_largeobject")  
---|---|---  
53.28. `pg_init_privs`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.30. `pg_largeobject`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-language.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

