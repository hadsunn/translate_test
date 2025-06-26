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

Supported Versions: [Current](/docs/current/view-pg-timezone-names.html
"PostgreSQL 17 - 54.32. pg_timezone_names") ([17](/docs/17/view-pg-timezone-
names.html "PostgreSQL 17 - 54.32. pg_timezone_names")) / [16](/docs/16/view-
pg-timezone-names.html "PostgreSQL 16 - 54.32. pg_timezone_names") /
[15](/docs/15/view-pg-timezone-names.html "PostgreSQL 15 -
54.32. pg_timezone_names") / [14](/docs/14/view-pg-timezone-names.html
"PostgreSQL 14 - 54.32. pg_timezone_names") / [13](/docs/13/view-pg-timezone-
names.html "PostgreSQL 13 - 54.32. pg_timezone_names")

Development Versions: [18](/docs/18/view-pg-timezone-names.html "PostgreSQL 18
- 54.32. pg_timezone_names") / [devel](/docs/devel/view-pg-timezone-names.html
"PostgreSQL devel - 54.32. pg_timezone_names")

Unsupported versions: [12](/docs/12/view-pg-timezone-names.html "PostgreSQL 12
- 54.32. pg_timezone_names") / [11](/docs/11/view-pg-timezone-names.html
"PostgreSQL 11 - 54.32. pg_timezone_names") / [10](/docs/10/view-pg-timezone-
names.html "PostgreSQL 10 - 54.32. pg_timezone_names") / [9.6](/docs/9.6/view-
pg-timezone-names.html "PostgreSQL 9.6 - 54.32. pg_timezone_names") /
[9.5](/docs/9.5/view-pg-timezone-names.html "PostgreSQL 9.5 -
54.32. pg_timezone_names") / [9.4](/docs/9.4/view-pg-timezone-names.html
"PostgreSQL 9.4 - 54.32. pg_timezone_names") / [9.3](/docs/9.3/view-pg-
timezone-names.html "PostgreSQL 9.3 - 54.32. pg_timezone_names") /
[9.2](/docs/9.2/view-pg-timezone-names.html "PostgreSQL 9.2 -
54.32. pg_timezone_names") / [9.1](/docs/9.1/view-pg-timezone-names.html
"PostgreSQL 9.1 - 54.32. pg_timezone_names") / [9.0](/docs/9.0/view-pg-
timezone-names.html "PostgreSQL 9.0 - 54.32. pg_timezone_names") /
[8.4](/docs/8.4/view-pg-timezone-names.html "PostgreSQL 8.4 -
54.32. pg_timezone_names") / [8.3](/docs/8.3/view-pg-timezone-names.html
"PostgreSQL 8.3 - 54.32. pg_timezone_names") / [8.2](/docs/8.2/view-pg-
timezone-names.html "PostgreSQL 8.2 - 54.32. pg_timezone_names")

__

54.32. `pg_timezone_names`  
---  
[Prev](view-pg-timezone-abbrevs.html "54.31. pg_timezone_abbrevs")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-user.html "54.33. pg_user")  
  
* * *

## 54.32. `pg_timezone_names` #

The view `pg_timezone_names` provides a list of time zone names that are
recognized by `SET TIMEZONE`, along with their associated abbreviations, UTC
offsets, and daylight-savings status. (Technically, PostgreSQL does not use
UTC because leap seconds are not handled.) Unlike the abbreviations shown in
[`pg_timezone_abbrevs`](view-pg-timezone-abbrevs.html
"54.31. pg_timezone_abbrevs"), many of these names imply a set of daylight-
savings transition date rules. Therefore, the associated information changes
across local DST boundaries. The displayed information is computed based on
the current value of `CURRENT_TIMESTAMP`.

**Table  54.32. `pg_timezone_names` Columns**

Column Type Description  
---  
`name` `text` Time zone name  
`abbrev` `text` Time zone abbreviation  
`utc_offset` `interval` Offset from UTC (positive means east of Greenwich)  
`is_dst` `bool` True if currently observing daylight savings  
  
  

* * *

[Prev](view-pg-timezone-abbrevs.html "54.31. pg_timezone_abbrevs")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-user.html "54.33. pg_user")  
---|---|---  
54.31. `pg_timezone_abbrevs`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.33. `pg_user`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-timezone-names.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

