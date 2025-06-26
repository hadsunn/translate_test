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

Supported Versions: [Current](/docs/current/view-pg-cursors.html "PostgreSQL
17 - 54.6. pg_cursors") ([17](/docs/17/view-pg-cursors.html "PostgreSQL 17 -
54.6. pg_cursors")) / [16](/docs/16/view-pg-cursors.html "PostgreSQL 16 -
54.6. pg_cursors") / [15](/docs/15/view-pg-cursors.html "PostgreSQL 15 -
54.6. pg_cursors") / [14](/docs/14/view-pg-cursors.html "PostgreSQL 14 -
54.6. pg_cursors") / [13](/docs/13/view-pg-cursors.html "PostgreSQL 13 -
54.6. pg_cursors")

Development Versions: [18](/docs/18/view-pg-cursors.html "PostgreSQL 18 -
54.6. pg_cursors") / [devel](/docs/devel/view-pg-cursors.html "PostgreSQL
devel - 54.6. pg_cursors")

Unsupported versions: [12](/docs/12/view-pg-cursors.html "PostgreSQL 12 -
54.6. pg_cursors") / [11](/docs/11/view-pg-cursors.html "PostgreSQL 11 -
54.6. pg_cursors") / [10](/docs/10/view-pg-cursors.html "PostgreSQL 10 -
54.6. pg_cursors") / [9.6](/docs/9.6/view-pg-cursors.html "PostgreSQL 9.6 -
54.6. pg_cursors") / [9.5](/docs/9.5/view-pg-cursors.html "PostgreSQL 9.5 -
54.6. pg_cursors") / [9.4](/docs/9.4/view-pg-cursors.html "PostgreSQL 9.4 -
54.6. pg_cursors") / [9.3](/docs/9.3/view-pg-cursors.html "PostgreSQL 9.3 -
54.6. pg_cursors") / [9.2](/docs/9.2/view-pg-cursors.html "PostgreSQL 9.2 -
54.6. pg_cursors") / [9.1](/docs/9.1/view-pg-cursors.html "PostgreSQL 9.1 -
54.6. pg_cursors") / [9.0](/docs/9.0/view-pg-cursors.html "PostgreSQL 9.0 -
54.6. pg_cursors") / [8.4](/docs/8.4/view-pg-cursors.html "PostgreSQL 8.4 -
54.6. pg_cursors") / [8.3](/docs/8.3/view-pg-cursors.html "PostgreSQL 8.3 -
54.6. pg_cursors") / [8.2](/docs/8.2/view-pg-cursors.html "PostgreSQL 8.2 -
54.6. pg_cursors")

__

54.6. `pg_cursors`  
---  
[Prev](view-pg-config.html "54.5. pg_config")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-file-settings.html "54.7. pg_file_settings")  
  
* * *

## 54.6. `pg_cursors` #

The `pg_cursors` view lists the cursors that are currently available. Cursors
can be defined in several ways:

  * via the [`DECLARE`](sql-declare.html "DECLARE") statement in SQL

  * via the Bind message in the frontend/backend protocol, as described in [Section 55.2.3](protocol-flow.html#PROTOCOL-FLOW-EXT-QUERY "55.2.3. Extended Query")

  * via the Server Programming Interface (SPI), as described in [Section 47.1](spi-interface.html "47.1. Interface Functions")

The `pg_cursors` view displays cursors created by any of these means. Cursors
only exist for the duration of the transaction that defines them, unless they
have been declared `WITH HOLD`. Therefore non-holdable cursors are only
present in the view until the end of their creating transaction.

### Note

Cursors are used internally to implement some of the components of PostgreSQL,
such as procedural languages. Therefore, the `pg_cursors` view might include
cursors that have not been explicitly created by the user.

**Table  54.6. `pg_cursors` Columns**

Column Type Description  
---  
`name` `text` The name of the cursor  
`statement` `text` The verbatim query string submitted to declare this cursor  
`is_holdable` `bool` `true` if the cursor is holdable (that is, it can be
accessed after the transaction that declared the cursor has committed);
`false` otherwise  
`is_binary` `bool` `true` if the cursor was declared `BINARY`; `false`
otherwise  
`is_scrollable` `bool` `true` if the cursor is scrollable (that is, it allows
rows to be retrieved in a nonsequential manner); `false` otherwise  
`creation_time` `timestamptz` The time at which the cursor was declared  
  
  

The `pg_cursors` view is read-only.

* * *

[Prev](view-pg-config.html "54.5. pg_config")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-file-settings.html "54.7. pg_file_settings")  
---|---|---  
54.5. `pg_config`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.7. `pg_file_settings`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-cursors.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

