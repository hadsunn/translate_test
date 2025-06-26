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

Supported Versions: [Current](/docs/current/indexes-unique.html "PostgreSQL 17
- 11.6. Unique Indexes") ([17](/docs/17/indexes-unique.html "PostgreSQL 17 -
11.6. Unique Indexes")) / [16](/docs/16/indexes-unique.html "PostgreSQL 16 -
11.6. Unique Indexes") / [15](/docs/15/indexes-unique.html "PostgreSQL 15 -
11.6. Unique Indexes") / [14](/docs/14/indexes-unique.html "PostgreSQL 14 -
11.6. Unique Indexes") / [13](/docs/13/indexes-unique.html "PostgreSQL 13 -
11.6. Unique Indexes")

Development Versions: [18](/docs/18/indexes-unique.html "PostgreSQL 18 -
11.6. Unique Indexes") / [devel](/docs/devel/indexes-unique.html "PostgreSQL
devel - 11.6. Unique Indexes")

Unsupported versions: [12](/docs/12/indexes-unique.html "PostgreSQL 12 -
11.6. Unique Indexes") / [11](/docs/11/indexes-unique.html "PostgreSQL 11 -
11.6. Unique Indexes") / [10](/docs/10/indexes-unique.html "PostgreSQL 10 -
11.6. Unique Indexes") / [9.6](/docs/9.6/indexes-unique.html "PostgreSQL 9.6 -
11.6. Unique Indexes") / [9.5](/docs/9.5/indexes-unique.html "PostgreSQL 9.5 -
11.6. Unique Indexes") / [9.4](/docs/9.4/indexes-unique.html "PostgreSQL 9.4 -
11.6. Unique Indexes") / [9.3](/docs/9.3/indexes-unique.html "PostgreSQL 9.3 -
11.6. Unique Indexes") / [9.2](/docs/9.2/indexes-unique.html "PostgreSQL 9.2 -
11.6. Unique Indexes") / [9.1](/docs/9.1/indexes-unique.html "PostgreSQL 9.1 -
11.6. Unique Indexes") / [9.0](/docs/9.0/indexes-unique.html "PostgreSQL 9.0 -
11.6. Unique Indexes") / [8.4](/docs/8.4/indexes-unique.html "PostgreSQL 8.4 -
11.6. Unique Indexes") / [8.3](/docs/8.3/indexes-unique.html "PostgreSQL 8.3 -
11.6. Unique Indexes") / [8.2](/docs/8.2/indexes-unique.html "PostgreSQL 8.2 -
11.6. Unique Indexes") / [8.1](/docs/8.1/indexes-unique.html "PostgreSQL 8.1 -
11.6. Unique Indexes") / [8.0](/docs/8.0/indexes-unique.html "PostgreSQL 8.0 -
11.6. Unique Indexes") / [7.4](/docs/7.4/indexes-unique.html "PostgreSQL 7.4 -
11.6. Unique Indexes") / [7.3](/docs/7.3/indexes-unique.html "PostgreSQL 7.3 -
11.6. Unique Indexes") / [7.2](/docs/7.2/indexes-unique.html "PostgreSQL 7.2 -
11.6. Unique Indexes")

__

11.6. Unique Indexes  
---  
[Prev](indexes-bitmap-scans.html "11.5. Combining Multiple Indexes")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-expressional.html "11.7. Indexes on Expressions")  
  
* * *

## 11.6. Unique Indexes #

Indexes can also be used to enforce uniqueness of a column's value, or the
uniqueness of the combined values of more than one column.

    
    
    CREATE UNIQUE INDEX _name_ ON _table_ (_column_ [, ...]) [ NULLS [ NOT ] DISTINCT ];
    

Currently, only B-tree indexes can be declared unique.

When an index is declared unique, multiple table rows with equal indexed
values are not allowed. By default, null values in a unique column are not
considered equal, allowing multiple nulls in the column. The `NULLS NOT
DISTINCT` option modifies this and causes the index to treat nulls as equal. A
multicolumn unique index will only reject cases where all indexed columns are
equal in multiple rows.

PostgreSQL automatically creates a unique index when a unique constraint or
primary key is defined for a table. The index covers the columns that make up
the primary key or unique constraint (a multicolumn index, if appropriate),
and is the mechanism that enforces the constraint.

### Note

There's no need to manually create indexes on unique columns; doing so would
just duplicate the automatically-created index.

* * *

[Prev](indexes-bitmap-scans.html "11.5. Combining Multiple Indexes")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-expressional.html "11.7. Indexes on Expressions")  
---|---|---  
11.5. Combining Multiple Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.7. Indexes on Expressions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-unique.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

