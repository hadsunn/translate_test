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

Supported Versions: [Current](/docs/current/catalog-pg-sequence.html
"PostgreSQL 17 - 53.47. pg_sequence") ([17](/docs/17/catalog-pg-sequence.html
"PostgreSQL 17 - 53.47. pg_sequence")) / [16](/docs/16/catalog-pg-
sequence.html "PostgreSQL 16 - 53.47. pg_sequence") / [15](/docs/15/catalog-
pg-sequence.html "PostgreSQL 15 - 53.47. pg_sequence") /
[14](/docs/14/catalog-pg-sequence.html "PostgreSQL 14 - 53.47. pg_sequence") /
[13](/docs/13/catalog-pg-sequence.html "PostgreSQL 13 - 53.47. pg_sequence")

Development Versions: [18](/docs/18/catalog-pg-sequence.html "PostgreSQL 18 -
53.47. pg_sequence") / [devel](/docs/devel/catalog-pg-sequence.html
"PostgreSQL devel - 53.47. pg_sequence")

Unsupported versions: [12](/docs/12/catalog-pg-sequence.html "PostgreSQL 12 -
53.47. pg_sequence") / [11](/docs/11/catalog-pg-sequence.html "PostgreSQL 11 -
53.47. pg_sequence") / [10](/docs/10/catalog-pg-sequence.html "PostgreSQL 10 -
53.47. pg_sequence")

__

53.47. `pg_sequence`  
---  
[Prev](catalog-pg-seclabel.html "53.46. pg_seclabel")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-shdepend.html "53.48. pg_shdepend")  
  
* * *

## 53.47. `pg_sequence` #

The catalog `pg_sequence` contains information about sequences. Some of the
information about sequences, such as the name and the schema, is in
[`pg_class`](catalog-pg-class.html "53.11. pg_class")

**Table  53.47. `pg_sequence` Columns**

Column Type Description  
---  
`seqrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry for this sequence  
`seqtypid` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type of the sequence  
`seqstart` `int8` Start value of the sequence  
`seqincrement` `int8` Increment value of the sequence  
`seqmax` `int8` Maximum value of the sequence  
`seqmin` `int8` Minimum value of the sequence  
`seqcache` `int8` Cache size of the sequence  
`seqcycle` `bool` Whether the sequence cycles  
  
  

* * *

[Prev](catalog-pg-seclabel.html "53.46. pg_seclabel")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-shdepend.html "53.48. pg_shdepend")  
---|---|---  
53.46. `pg_seclabel`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.48. `pg_shdepend`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-sequence.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

