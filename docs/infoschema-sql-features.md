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

Supported Versions: [Current](/docs/current/infoschema-sql-features.html
"PostgreSQL 17 - 37.48. sql_features") ([17](/docs/17/infoschema-sql-
features.html "PostgreSQL 17 - 37.48. sql_features")) /
[16](/docs/16/infoschema-sql-features.html "PostgreSQL 16 -
37.48. sql_features") / [15](/docs/15/infoschema-sql-features.html "PostgreSQL
15 - 37.48. sql_features") / [14](/docs/14/infoschema-sql-features.html
"PostgreSQL 14 - 37.48. sql_features") / [13](/docs/13/infoschema-sql-
features.html "PostgreSQL 13 - 37.48. sql_features")

Development Versions: [18](/docs/18/infoschema-sql-features.html "PostgreSQL
18 - 37.48. sql_features") / [devel](/docs/devel/infoschema-sql-features.html
"PostgreSQL devel - 37.48. sql_features")

Unsupported versions: [12](/docs/12/infoschema-sql-features.html "PostgreSQL
12 - 37.48. sql_features") / [11](/docs/11/infoschema-sql-features.html
"PostgreSQL 11 - 37.48. sql_features") / [10](/docs/10/infoschema-sql-
features.html "PostgreSQL 10 - 37.48. sql_features") /
[9.6](/docs/9.6/infoschema-sql-features.html "PostgreSQL 9.6 -
37.48. sql_features") / [9.5](/docs/9.5/infoschema-sql-features.html
"PostgreSQL 9.5 - 37.48. sql_features") / [9.4](/docs/9.4/infoschema-sql-
features.html "PostgreSQL 9.4 - 37.48. sql_features") /
[9.3](/docs/9.3/infoschema-sql-features.html "PostgreSQL 9.3 -
37.48. sql_features") / [9.2](/docs/9.2/infoschema-sql-features.html
"PostgreSQL 9.2 - 37.48. sql_features") / [9.1](/docs/9.1/infoschema-sql-
features.html "PostgreSQL 9.1 - 37.48. sql_features") /
[9.0](/docs/9.0/infoschema-sql-features.html "PostgreSQL 9.0 -
37.48. sql_features") / [8.4](/docs/8.4/infoschema-sql-features.html
"PostgreSQL 8.4 - 37.48. sql_features") / [8.3](/docs/8.3/infoschema-sql-
features.html "PostgreSQL 8.3 - 37.48. sql_features") /
[8.2](/docs/8.2/infoschema-sql-features.html "PostgreSQL 8.2 -
37.48. sql_features") / [8.1](/docs/8.1/infoschema-sql-features.html
"PostgreSQL 8.1 - 37.48. sql_features") / [8.0](/docs/8.0/infoschema-sql-
features.html "PostgreSQL 8.0 - 37.48. sql_features") /
[7.4](/docs/7.4/infoschema-sql-features.html "PostgreSQL 7.4 -
37.48. sql_features")

__

37.48. `sql_features`  
---  
[Prev](infoschema-sequences.html "37.47. sequences")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-sql-implementation-info.html "37.49. sql_implementation_info")  
  
* * *

## 37.48. `sql_features` #

The table `sql_features` contains information about which formal features
defined in the SQL standard are supported by PostgreSQL. This is the same
information that is presented in [Appendix D](features.html "Appendix D. SQL
Conformance"). There you can also find some additional background information.

**Table  37.46. `sql_features` Columns**

Column Type Description  
---  
`feature_id` `character_data` Identifier string of the feature  
`feature_name` `character_data` Descriptive name of the feature  
`sub_feature_id` `character_data` Identifier string of the subfeature, or a
zero-length string if not a subfeature  
`sub_feature_name` `character_data` Descriptive name of the subfeature, or a
zero-length string if not a subfeature  
`is_supported` `yes_or_no` `YES` if the feature is fully supported by the
current version of PostgreSQL, `NO` if not  
`is_verified_by` `character_data` Always null, since the PostgreSQL
development group does not perform formal testing of feature conformance  
`comments` `character_data` Possibly a comment about the supported status of
the feature  
  
  

* * *

[Prev](infoschema-sequences.html "37.47. sequences")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-sql-implementation-info.html "37.49. sql_implementation_info")  
---|---|---  
37.47. `sequences`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.49. `sql_implementation_info`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-sql-features.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

