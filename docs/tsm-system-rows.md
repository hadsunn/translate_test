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

Supported Versions: [Current](/docs/current/tsm-system-rows.html "PostgreSQL
17 - F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for TABLESAMPLE")
([17](/docs/17/tsm-system-rows.html "PostgreSQL 17 - F.46. tsm_system_rows —
the SYSTEM_ROWS sampling method for TABLESAMPLE")) / [16](/docs/16/tsm-system-
rows.html "PostgreSQL 16 - F.46. tsm_system_rows — the SYSTEM_ROWS sampling
method for TABLESAMPLE") / [15](/docs/15/tsm-system-rows.html "PostgreSQL 15 -
F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for TABLESAMPLE") /
[14](/docs/14/tsm-system-rows.html "PostgreSQL 14 - F.46. tsm_system_rows —
the SYSTEM_ROWS sampling method for TABLESAMPLE") / [13](/docs/13/tsm-system-
rows.html "PostgreSQL 13 - F.46. tsm_system_rows — the SYSTEM_ROWS sampling
method for TABLESAMPLE")

Development Versions: [18](/docs/18/tsm-system-rows.html "PostgreSQL 18 -
F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for TABLESAMPLE") /
[devel](/docs/devel/tsm-system-rows.html "PostgreSQL devel -
F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for TABLESAMPLE")

Unsupported versions: [12](/docs/12/tsm-system-rows.html "PostgreSQL 12 -
F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for TABLESAMPLE") /
[11](/docs/11/tsm-system-rows.html "PostgreSQL 11 - F.46. tsm_system_rows —
the SYSTEM_ROWS sampling method for TABLESAMPLE") / [10](/docs/10/tsm-system-
rows.html "PostgreSQL 10 - F.46. tsm_system_rows — the SYSTEM_ROWS sampling
method for TABLESAMPLE") / [9.6](/docs/9.6/tsm-system-rows.html "PostgreSQL
9.6 - F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for
TABLESAMPLE") / [9.5](/docs/9.5/tsm-system-rows.html "PostgreSQL 9.5 -
F.46. tsm_system_rows — the SYSTEM_ROWS sampling method for TABLESAMPLE")

__

F.46. tsm_system_rows — the `SYSTEM_ROWS` sampling method for `TABLESAMPLE`  
---  
[Prev](test-decoding.html "F.45. test_decoding — SQL-based test/example module for WAL logical decoding")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tsm-system-time.html "F.47. tsm_system_time —  the SYSTEM_TIME sampling method for TABLESAMPLE")  
  
* * *

## F.46. tsm_system_rows — the `SYSTEM_ROWS` sampling method for `TABLESAMPLE`
#

[F.46.1. Examples](tsm-system-rows.html#TSM-SYSTEM-ROWS-EXAMPLES)

The `tsm_system_rows` module provides the table sampling method `SYSTEM_ROWS`,
which can be used in the `TABLESAMPLE` clause of a [`SELECT`](sql-select.html
"SELECT") command.

This table sampling method accepts a single integer argument that is the
maximum number of rows to read. The resulting sample will always contain
exactly that many rows, unless the table does not contain enough rows, in
which case the whole table is selected.

Like the built-in `SYSTEM` sampling method, `SYSTEM_ROWS` performs block-level
sampling, so that the sample is not completely random but may be subject to
clustering effects, especially if only a small number of rows are requested.

`SYSTEM_ROWS` does not support the `REPEATABLE` clause.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.46.1. Examples #

Here is an example of selecting a sample of a table with `SYSTEM_ROWS`. First
install the extension:

    
    
    CREATE EXTENSION tsm_system_rows;
    

Then you can use it in a `SELECT` command, for instance:

    
    
    SELECT * FROM my_table TABLESAMPLE SYSTEM_ROWS(100);
    

This command will return a sample of 100 rows from the table `my_table`
(unless the table does not have 100 visible rows, in which case all its rows
are returned).

* * *

[Prev](test-decoding.html "F.45. test_decoding — SQL-based test/example module for WAL logical decoding")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](tsm-system-time.html "F.47. tsm_system_time —  the SYSTEM_TIME sampling method for TABLESAMPLE")  
---|---|---  
F.45. test_decoding — SQL-based test/example module for WAL logical decoding  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.47. tsm_system_time — the `SYSTEM_TIME` sampling method for `TABLESAMPLE`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tsm-system-rows.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

