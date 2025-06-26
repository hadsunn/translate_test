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

Supported Versions: [Current](/docs/current/view-pg-seclabels.html "PostgreSQL
17 - 54.22. pg_seclabels") ([17](/docs/17/view-pg-seclabels.html "PostgreSQL
17 - 54.22. pg_seclabels")) / [16](/docs/16/view-pg-seclabels.html "PostgreSQL
16 - 54.22. pg_seclabels") / [15](/docs/15/view-pg-seclabels.html "PostgreSQL
15 - 54.22. pg_seclabels") / [14](/docs/14/view-pg-seclabels.html "PostgreSQL
14 - 54.22. pg_seclabels") / [13](/docs/13/view-pg-seclabels.html "PostgreSQL
13 - 54.22. pg_seclabels")

Development Versions: [18](/docs/18/view-pg-seclabels.html "PostgreSQL 18 -
54.22. pg_seclabels") / [devel](/docs/devel/view-pg-seclabels.html "PostgreSQL
devel - 54.22. pg_seclabels")

Unsupported versions: [12](/docs/12/view-pg-seclabels.html "PostgreSQL 12 -
54.22. pg_seclabels") / [11](/docs/11/view-pg-seclabels.html "PostgreSQL 11 -
54.22. pg_seclabels") / [10](/docs/10/view-pg-seclabels.html "PostgreSQL 10 -
54.22. pg_seclabels") / [9.6](/docs/9.6/view-pg-seclabels.html "PostgreSQL 9.6
- 54.22. pg_seclabels") / [9.5](/docs/9.5/view-pg-seclabels.html "PostgreSQL
9.5 - 54.22. pg_seclabels") / [9.4](/docs/9.4/view-pg-seclabels.html
"PostgreSQL 9.4 - 54.22. pg_seclabels") / [9.3](/docs/9.3/view-pg-
seclabels.html "PostgreSQL 9.3 - 54.22. pg_seclabels") / [9.2](/docs/9.2/view-
pg-seclabels.html "PostgreSQL 9.2 - 54.22. pg_seclabels") /
[9.1](/docs/9.1/view-pg-seclabels.html "PostgreSQL 9.1 - 54.22. pg_seclabels")

__

54.22. `pg_seclabels`  
---  
[Prev](view-pg-rules.html "54.21. pg_rules")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-sequences.html "54.23. pg_sequences")  
  
* * *

## 54.22. `pg_seclabels` #

The view `pg_seclabels` provides information about security labels. It as an
easier-to-query version of the [`pg_seclabel`](catalog-pg-seclabel.html
"53.46. pg_seclabel") catalog.

**Table  54.22. `pg_seclabels` Columns**

Column Type Description  
---  
`objoid` `oid` (references any OID column) The OID of the object this security
label pertains to  
`classoid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog this object appears in  
`objsubid` `int4` For a security label on a table column, this is the column
number (the `objoid` and `classoid` refer to the table itself). For all other
object types, this column is zero.  
`objtype` `text` The type of object to which this label applies, as text.  
`objnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace for this object, if
applicable; otherwise NULL.  
`objname` `text` The name of the object to which this label applies, as text.  
`provider` `text` (references [`pg_seclabel`](catalog-pg-seclabel.html
"53.46. pg_seclabel").`provider`) The label provider associated with this
label.  
`label` `text` (references [`pg_seclabel`](catalog-pg-seclabel.html
"53.46. pg_seclabel").`label`) The security label applied to this object.  
  
  

* * *

[Prev](view-pg-rules.html "54.21. pg_rules")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-sequences.html "54.23. pg_sequences")  
---|---|---  
54.21. `pg_rules`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.23. `pg_sequences`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-seclabels.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

