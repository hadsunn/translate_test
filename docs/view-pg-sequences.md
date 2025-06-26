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

Supported Versions: [Current](/docs/current/view-pg-sequences.html "PostgreSQL
17 - 54.23. pg_sequences") ([17](/docs/17/view-pg-sequences.html "PostgreSQL
17 - 54.23. pg_sequences")) / [16](/docs/16/view-pg-sequences.html "PostgreSQL
16 - 54.23. pg_sequences") / [15](/docs/15/view-pg-sequences.html "PostgreSQL
15 - 54.23. pg_sequences") / [14](/docs/14/view-pg-sequences.html "PostgreSQL
14 - 54.23. pg_sequences") / [13](/docs/13/view-pg-sequences.html "PostgreSQL
13 - 54.23. pg_sequences")

Development Versions: [18](/docs/18/view-pg-sequences.html "PostgreSQL 18 -
54.23. pg_sequences") / [devel](/docs/devel/view-pg-sequences.html "PostgreSQL
devel - 54.23. pg_sequences")

Unsupported versions: [12](/docs/12/view-pg-sequences.html "PostgreSQL 12 -
54.23. pg_sequences") / [11](/docs/11/view-pg-sequences.html "PostgreSQL 11 -
54.23. pg_sequences") / [10](/docs/10/view-pg-sequences.html "PostgreSQL 10 -
54.23. pg_sequences")

__

54.23. `pg_sequences`  
---  
[Prev](view-pg-seclabels.html "54.22. pg_seclabels")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-settings.html "54.24. pg_settings")  
  
* * *

## 54.23. `pg_sequences` #

The view `pg_sequences` provides access to useful information about each
sequence in the database.

**Table  54.23. `pg_sequences` Columns**

Column Type Description  
---  
`schemaname` `name` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`nspname`) Name of schema containing sequence  
`sequencename` `name` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relname`) Name of sequence  
`sequenceowner` `name` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`rolname`) Name of sequence's owner  
`data_type` `regtype` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type of the sequence  
`start_value` `int8` Start value of the sequence  
`min_value` `int8` Minimum value of the sequence  
`max_value` `int8` Maximum value of the sequence  
`increment_by` `int8` Increment value of the sequence  
`cycle` `bool` Whether the sequence cycles  
`cache_size` `int8` Cache size of the sequence  
`last_value` `int8` The last sequence value written to disk. If caching is
used, this value can be greater than the last value handed out from the
sequence.  
  
  

The `last_value` column will read as null if any of the following are true:

  * The sequence has not been read from yet.

  * The current user does not have `USAGE` or `SELECT` privilege on the sequence.

  * The sequence is unlogged and the server is a standby.

* * *

[Prev](view-pg-seclabels.html "54.22. pg_seclabels")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-settings.html "54.24. pg_settings")  
---|---|---  
54.22. `pg_seclabels`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.24. `pg_settings`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-sequences.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

