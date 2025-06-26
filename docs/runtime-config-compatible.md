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

Supported Versions: [Current](/docs/current/runtime-config-compatible.html
"PostgreSQL 17 - 20.13. Version and Platform Compatibility")
([17](/docs/17/runtime-config-compatible.html "PostgreSQL 17 - 20.13. Version
and Platform Compatibility")) / [16](/docs/16/runtime-config-compatible.html
"PostgreSQL 16 - 20.13. Version and Platform Compatibility") /
[15](/docs/15/runtime-config-compatible.html "PostgreSQL 15 - 20.13. Version
and Platform Compatibility") / [14](/docs/14/runtime-config-compatible.html
"PostgreSQL 14 - 20.13. Version and Platform Compatibility") /
[13](/docs/13/runtime-config-compatible.html "PostgreSQL 13 - 20.13. Version
and Platform Compatibility")

Development Versions: [18](/docs/18/runtime-config-compatible.html "PostgreSQL
18 - 20.13. Version and Platform Compatibility") /
[devel](/docs/devel/runtime-config-compatible.html "PostgreSQL devel -
20.13. Version and Platform Compatibility")

Unsupported versions: [12](/docs/12/runtime-config-compatible.html "PostgreSQL
12 - 20.13. Version and Platform Compatibility") / [11](/docs/11/runtime-
config-compatible.html "PostgreSQL 11 - 20.13. Version and Platform
Compatibility") / [10](/docs/10/runtime-config-compatible.html "PostgreSQL 10
- 20.13. Version and Platform Compatibility") / [9.6](/docs/9.6/runtime-
config-compatible.html "PostgreSQL 9.6 - 20.13. Version and Platform
Compatibility") / [9.5](/docs/9.5/runtime-config-compatible.html "PostgreSQL
9.5 - 20.13. Version and Platform Compatibility") / [9.4](/docs/9.4/runtime-
config-compatible.html "PostgreSQL 9.4 - 20.13. Version and Platform
Compatibility") / [9.3](/docs/9.3/runtime-config-compatible.html "PostgreSQL
9.3 - 20.13. Version and Platform Compatibility") / [9.2](/docs/9.2/runtime-
config-compatible.html "PostgreSQL 9.2 - 20.13. Version and Platform
Compatibility") / [9.1](/docs/9.1/runtime-config-compatible.html "PostgreSQL
9.1 - 20.13. Version and Platform Compatibility") / [9.0](/docs/9.0/runtime-
config-compatible.html "PostgreSQL 9.0 - 20.13. Version and Platform
Compatibility") / [8.4](/docs/8.4/runtime-config-compatible.html "PostgreSQL
8.4 - 20.13. Version and Platform Compatibility") / [8.3](/docs/8.3/runtime-
config-compatible.html "PostgreSQL 8.3 - 20.13. Version and Platform
Compatibility") / [8.2](/docs/8.2/runtime-config-compatible.html "PostgreSQL
8.2 - 20.13. Version and Platform Compatibility") / [8.1](/docs/8.1/runtime-
config-compatible.html "PostgreSQL 8.1 - 20.13. Version and Platform
Compatibility")

__

20.13. Version and Platform Compatibility  
---  
[Prev](runtime-config-locks.html "20.12. Lock Management")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-error-handling.html "20.14. Error Handling")  
  
* * *

## 20.13. Version and Platform Compatibility #

[20.13.1. Previous PostgreSQL Versions](runtime-config-
compatible.html#RUNTIME-CONFIG-COMPATIBLE-VERSION)

[20.13.2. Platform and Client Compatibility](runtime-config-
compatible.html#RUNTIME-CONFIG-COMPATIBLE-CLIENTS)

### 20.13.1. Previous PostgreSQL Versions #

`array_nulls` (`boolean`)  #

    

This controls whether the array input parser recognizes unquoted `NULL` as
specifying a null array element. By default, this is `on`, allowing array
values containing null values to be entered. However, PostgreSQL versions
before 8.2 did not support null values in arrays, and therefore would treat
`NULL` as specifying a normal array element with the string value “NULL”. For
backward compatibility with applications that require the old behavior, this
variable can be turned `off`.

Note that it is possible to create array values containing null values even
when this variable is `off`.

`backslash_quote` (`enum`)  #

    

This controls whether a quote mark can be represented by `\'` in a string
literal. The preferred, SQL-standard way to represent a quote mark is by
doubling it (`''`) but PostgreSQL has historically also accepted `\'`.
However, use of `\'` creates security risks because in some client character
set encodings, there are multibyte characters in which the last byte is
numerically equivalent to ASCII `\`. If client-side code does escaping
incorrectly then an SQL-injection attack is possible. This risk can be
prevented by making the server reject queries in which a quote mark appears to
be escaped by a backslash. The allowed values of `backslash_quote` are `on`
(allow `\'` always), `off` (reject always), and `safe_encoding` (allow only if
client encoding does not allow ASCII `\` within a multibyte character).
`safe_encoding` is the default setting.

Note that in a standard-conforming string literal, `\` just means `\` anyway.
This parameter only affects the handling of non-standard-conforming literals,
including escape string syntax (`E'...'`).

`escape_string_warning` (`boolean`)  #

    

When on, a warning is issued if a backslash (`\`) appears in an ordinary
string literal (`'...'` syntax) and `standard_conforming_strings` is off. The
default is `on`.

Applications that wish to use backslash as escape should be modified to use
escape string syntax (`E'...'`), because the default behavior of ordinary
strings is now to treat backslash as an ordinary character, per SQL standard.
This variable can be enabled to help locate code that needs to be changed.

`lo_compat_privileges` (`boolean`)  #

    

In PostgreSQL releases prior to 9.0, large objects did not have access
privileges and were, therefore, always readable and writable by all users.
Setting this variable to `on` disables the new privilege checks, for
compatibility with prior releases. The default is `off`. Only superusers and
users with the appropriate `SET` privilege can change this setting.

Setting this variable does not disable all security checks related to large
objects — only those for which the default behavior has changed in PostgreSQL
9.0.

`quote_all_identifiers` (`boolean`)  #

    

When the database generates SQL, force all identifiers to be quoted, even if
they are not (currently) keywords. This will affect the output of `EXPLAIN` as
well as the results of functions like `pg_get_viewdef`. See also the `--quote-
all-identifiers` option of [pg_dump](app-pgdump.html "pg_dump") and
[pg_dumpall](app-pg-dumpall.html "pg_dumpall").

`standard_conforming_strings` (`boolean`)  #

    

This controls whether ordinary string literals (`'...'`) treat backslashes
literally, as specified in the SQL standard. Beginning in PostgreSQL 9.1, the
default is `on` (prior releases defaulted to `off`). Applications can check
this parameter to determine how string literals will be processed. The
presence of this parameter can also be taken as an indication that the escape
string syntax (`E'...'`) is supported. Escape string syntax ([Section
4.1.2.2](sql-syntax-lexical.html#SQL-SYNTAX-STRINGS-ESCAPE "4.1.2.2. String
Constants with C-Style Escapes")) should be used if an application desires
backslashes to be treated as escape characters.

`synchronize_seqscans` (`boolean`)  #

    

This allows sequential scans of large tables to synchronize with each other,
so that concurrent scans read the same block at about the same time and hence
share the I/O workload. When this is enabled, a scan might start in the middle
of the table and then “wrap around” the end to cover all rows, so as to
synchronize with the activity of scans already in progress. This can result in
unpredictable changes in the row ordering returned by queries that have no
`ORDER BY` clause. Setting this parameter to `off` ensures the pre-8.3
behavior in which a sequential scan always starts from the beginning of the
table. The default is `on`.

### 20.13.2. Platform and Client Compatibility #

`transform_null_equals` (`boolean`)  #

    

When on, expressions of the form `_`expr`_ = NULL` (or `NULL = _`expr`_`) are
treated as `_`expr`_ IS NULL`, that is, they return true if _`expr`_ evaluates
to the null value, and false otherwise. The correct SQL-spec-compliant
behavior of `_`expr`_ = NULL` is to always return null (unknown). Therefore
this parameter defaults to `off`.

However, filtered forms in Microsoft Access generate queries that appear to
use `_`expr`_ = NULL` to test for null values, so if you use that interface to
access the database you might want to turn this option on. Since expressions
of the form `_`expr`_ = NULL` always return the null value (using the SQL
standard interpretation), they are not very useful and do not appear often in
normal applications so this option does little harm in practice. But new users
are frequently confused about the semantics of expressions involving null
values, so this option is off by default.

Note that this option only affects the exact form `= NULL`, not other
comparison operators or other expressions that are computationally equivalent
to some expression involving the equals operator (such as `IN`). Thus, this
option is not a general fix for bad programming.

Refer to [Section 9.2](functions-comparison.html "9.2. Comparison Functions
and Operators") for related information.

* * *

[Prev](runtime-config-locks.html "20.12. Lock Management")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-error-handling.html "20.14. Error Handling")  
---|---|---  
20.12. Lock Management  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.14. Error Handling  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-
compatible.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

