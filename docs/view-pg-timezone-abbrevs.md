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

Supported Versions: [Current](/docs/current/view-pg-timezone-abbrevs.html
"PostgreSQL 17 - 54.31. pg_timezone_abbrevs") ([17](/docs/17/view-pg-timezone-
abbrevs.html "PostgreSQL 17 - 54.31. pg_timezone_abbrevs")) /
[16](/docs/16/view-pg-timezone-abbrevs.html "PostgreSQL 16 -
54.31. pg_timezone_abbrevs") / [15](/docs/15/view-pg-timezone-abbrevs.html
"PostgreSQL 15 - 54.31. pg_timezone_abbrevs") / [14](/docs/14/view-pg-
timezone-abbrevs.html "PostgreSQL 14 - 54.31. pg_timezone_abbrevs") /
[13](/docs/13/view-pg-timezone-abbrevs.html "PostgreSQL 13 -
54.31. pg_timezone_abbrevs")

Development Versions: [18](/docs/18/view-pg-timezone-abbrevs.html "PostgreSQL
18 - 54.31. pg_timezone_abbrevs") / [devel](/docs/devel/view-pg-timezone-
abbrevs.html "PostgreSQL devel - 54.31. pg_timezone_abbrevs")

Unsupported versions: [12](/docs/12/view-pg-timezone-abbrevs.html "PostgreSQL
12 - 54.31. pg_timezone_abbrevs") / [11](/docs/11/view-pg-timezone-
abbrevs.html "PostgreSQL 11 - 54.31. pg_timezone_abbrevs") /
[10](/docs/10/view-pg-timezone-abbrevs.html "PostgreSQL 10 -
54.31. pg_timezone_abbrevs") / [9.6](/docs/9.6/view-pg-timezone-abbrevs.html
"PostgreSQL 9.6 - 54.31. pg_timezone_abbrevs") / [9.5](/docs/9.5/view-pg-
timezone-abbrevs.html "PostgreSQL 9.5 - 54.31. pg_timezone_abbrevs") /
[9.4](/docs/9.4/view-pg-timezone-abbrevs.html "PostgreSQL 9.4 -
54.31. pg_timezone_abbrevs") / [9.3](/docs/9.3/view-pg-timezone-abbrevs.html
"PostgreSQL 9.3 - 54.31. pg_timezone_abbrevs") / [9.2](/docs/9.2/view-pg-
timezone-abbrevs.html "PostgreSQL 9.2 - 54.31. pg_timezone_abbrevs") /
[9.1](/docs/9.1/view-pg-timezone-abbrevs.html "PostgreSQL 9.1 -
54.31. pg_timezone_abbrevs") / [9.0](/docs/9.0/view-pg-timezone-abbrevs.html
"PostgreSQL 9.0 - 54.31. pg_timezone_abbrevs") / [8.4](/docs/8.4/view-pg-
timezone-abbrevs.html "PostgreSQL 8.4 - 54.31. pg_timezone_abbrevs") /
[8.3](/docs/8.3/view-pg-timezone-abbrevs.html "PostgreSQL 8.3 -
54.31. pg_timezone_abbrevs") / [8.2](/docs/8.2/view-pg-timezone-abbrevs.html
"PostgreSQL 8.2 - 54.31. pg_timezone_abbrevs")

__

54.31. `pg_timezone_abbrevs`  
---  
[Prev](view-pg-tables.html "54.30. pg_tables")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-timezone-names.html "54.32. pg_timezone_names")  
  
* * *

## 54.31. `pg_timezone_abbrevs` #

The view `pg_timezone_abbrevs` provides a list of time zone abbreviations that
are currently recognized by the datetime input routines. The contents of this
view change when the [timezone_abbreviations](runtime-config-client.html#GUC-
TIMEZONE-ABBREVIATIONS) run-time parameter is modified.

**Table  54.31. `pg_timezone_abbrevs` Columns**

Column Type Description  
---  
`abbrev` `text` Time zone abbreviation  
`utc_offset` `interval` Offset from UTC (positive means east of Greenwich)  
`is_dst` `bool` True if this is a daylight-savings abbreviation  
  
  

While most timezone abbreviations represent fixed offsets from UTC, there are
some that have historically varied in value (see [Section B.4](datetime-
config-files.html "B.4. Date/Time Configuration Files") for more information).
In such cases this view presents their current meaning.

* * *

[Prev](view-pg-tables.html "54.30. pg_tables")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-timezone-names.html "54.32. pg_timezone_names")  
---|---|---  
54.30. `pg_tables`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.32. `pg_timezone_names`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-timezone-
abbrevs.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

