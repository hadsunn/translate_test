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

Supported Versions: [Current](/docs/current/tsm-system-time.html "PostgreSQL
17 - F.47. tsm_system_time — the SYSTEM_TIME sampling method for TABLESAMPLE")
([17](/docs/17/tsm-system-time.html "PostgreSQL 17 - F.47. tsm_system_time —
the SYSTEM_TIME sampling method for TABLESAMPLE")) / [16](/docs/16/tsm-system-
time.html "PostgreSQL 16 - F.47. tsm_system_time — the SYSTEM_TIME sampling
method for TABLESAMPLE") / [15](/docs/15/tsm-system-time.html "PostgreSQL 15 -
F.47. tsm_system_time — the SYSTEM_TIME sampling method for TABLESAMPLE") /
[14](/docs/14/tsm-system-time.html "PostgreSQL 14 - F.47. tsm_system_time —
the SYSTEM_TIME sampling method for TABLESAMPLE") / [13](/docs/13/tsm-system-
time.html "PostgreSQL 13 - F.47. tsm_system_time — the SYSTEM_TIME sampling
method for TABLESAMPLE")

Development Versions: [18](/docs/18/tsm-system-time.html "PostgreSQL 18 -
F.47. tsm_system_time — the SYSTEM_TIME sampling method for TABLESAMPLE") /
[devel](/docs/devel/tsm-system-time.html "PostgreSQL devel -
F.47. tsm_system_time — the SYSTEM_TIME sampling method for TABLESAMPLE")

Unsupported versions: [12](/docs/12/tsm-system-time.html "PostgreSQL 12 -
F.47. tsm_system_time — the SYSTEM_TIME sampling method for TABLESAMPLE") /
[11](/docs/11/tsm-system-time.html "PostgreSQL 11 - F.47. tsm_system_time —
the SYSTEM_TIME sampling method for TABLESAMPLE") / [10](/docs/10/tsm-system-
time.html "PostgreSQL 10 - F.47. tsm_system_time — the SYSTEM_TIME sampling
method for TABLESAMPLE") / [9.6](/docs/9.6/tsm-system-time.html "PostgreSQL
9.6 - F.47. tsm_system_time — the SYSTEM_TIME sampling method for
TABLESAMPLE") / [9.5](/docs/9.5/tsm-system-time.html "PostgreSQL 9.5 -
F.47. tsm_system_time — the SYSTEM_TIME sampling method for TABLESAMPLE")

__

F.47. tsm_system_time — the `SYSTEM_TIME` sampling method for `TABLESAMPLE`  
---  
[Prev](tsm-system-rows.html "F.46. tsm_system_rows —  the SYSTEM_ROWS sampling method for TABLESAMPLE")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](unaccent.html "F.48. unaccent — a text search dictionary which removes diacritics")  
  
* * *

## F.47. tsm_system_time — the `SYSTEM_TIME` sampling method for `TABLESAMPLE`
#

[F.47.1. Examples](tsm-system-time.html#TSM-SYSTEM-TIME-EXAMPLES)

The `tsm_system_time` module provides the table sampling method `SYSTEM_TIME`,
which can be used in the `TABLESAMPLE` clause of a [`SELECT`](sql-select.html
"SELECT") command.

This table sampling method accepts a single floating-point argument that is
the maximum number of milliseconds to spend reading the table. This gives you
direct control over how long the query takes, at the price that the size of
the sample becomes hard to predict. The resulting sample will contain as many
rows as could be read in the specified time, unless the whole table has been
read first.

Like the built-in `SYSTEM` sampling method, `SYSTEM_TIME` performs block-level
sampling, so that the sample is not completely random but may be subject to
clustering effects, especially if only a small number of rows are selected.

`SYSTEM_TIME` does not support the `REPEATABLE` clause.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.47.1. Examples #

Here is an example of selecting a sample of a table with `SYSTEM_TIME`. First
install the extension:

    
    
    CREATE EXTENSION tsm_system_time;
    

Then you can use it in a `SELECT` command, for instance:

    
    
    SELECT * FROM my_table TABLESAMPLE SYSTEM_TIME(1000);
    

This command will return as large a sample of `my_table` as it can read in 1
second (1000 milliseconds). Of course, if the whole table can be read in under
1 second, all its rows will be returned.

* * *

[Prev](tsm-system-rows.html "F.46. tsm_system_rows —  the SYSTEM_ROWS sampling method for TABLESAMPLE")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](unaccent.html "F.48. unaccent — a text search dictionary which removes diacritics")  
---|---|---  
F.46. tsm_system_rows — the `SYSTEM_ROWS` sampling method for `TABLESAMPLE`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.48. unaccent — a text search dictionary which removes diacritics  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tsm-system-time.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

