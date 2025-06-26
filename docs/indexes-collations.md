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

Supported Versions: [Current](/docs/current/indexes-collations.html
"PostgreSQL 17 - 11.11. Indexes and Collations") ([17](/docs/17/indexes-
collations.html "PostgreSQL 17 - 11.11. Indexes and Collations")) /
[16](/docs/16/indexes-collations.html "PostgreSQL 16 - 11.11. Indexes and
Collations") / [15](/docs/15/indexes-collations.html "PostgreSQL 15 -
11.11. Indexes and Collations") / [14](/docs/14/indexes-collations.html
"PostgreSQL 14 - 11.11. Indexes and Collations") / [13](/docs/13/indexes-
collations.html "PostgreSQL 13 - 11.11. Indexes and Collations")

Development Versions: [18](/docs/18/indexes-collations.html "PostgreSQL 18 -
11.11. Indexes and Collations") / [devel](/docs/devel/indexes-collations.html
"PostgreSQL devel - 11.11. Indexes and Collations")

Unsupported versions: [12](/docs/12/indexes-collations.html "PostgreSQL 12 -
11.11. Indexes and Collations") / [11](/docs/11/indexes-collations.html
"PostgreSQL 11 - 11.11. Indexes and Collations") / [10](/docs/10/indexes-
collations.html "PostgreSQL 10 - 11.11. Indexes and Collations") /
[9.6](/docs/9.6/indexes-collations.html "PostgreSQL 9.6 - 11.11. Indexes and
Collations") / [9.5](/docs/9.5/indexes-collations.html "PostgreSQL 9.5 -
11.11. Indexes and Collations") / [9.4](/docs/9.4/indexes-collations.html
"PostgreSQL 9.4 - 11.11. Indexes and Collations") / [9.3](/docs/9.3/indexes-
collations.html "PostgreSQL 9.3 - 11.11. Indexes and Collations") /
[9.2](/docs/9.2/indexes-collations.html "PostgreSQL 9.2 - 11.11. Indexes and
Collations") / [9.1](/docs/9.1/indexes-collations.html "PostgreSQL 9.1 -
11.11. Indexes and Collations")

__

11.11. Indexes and Collations  
---  
[Prev](indexes-opclass.html "11.10. Operator Classes and Operator Families")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-examine.html "11.12. Examining Index Usage")  
  
* * *

## 11.11. Indexes and Collations #

An index can support only one collation per index column. If multiple
collations are of interest, multiple indexes may be needed.

Consider these statements:

    
    
    CREATE TABLE test1c (
        id integer,
        content varchar COLLATE "x"
    );
    
    CREATE INDEX test1c_content_index ON test1c (content);
    

The index automatically uses the collation of the underlying column. So a
query of the form

    
    
    SELECT * FROM test1c WHERE content > _constant_ ;
    

could use the index, because the comparison will by default use the collation
of the column. However, this index cannot accelerate queries that involve some
other collation. So if queries of the form, say,

    
    
    SELECT * FROM test1c WHERE content > _constant_ COLLATE "y";
    

are also of interest, an additional index could be created that supports the
`"y"` collation, like this:

    
    
    CREATE INDEX test1c_content_y_index ON test1c (content COLLATE "y");
    

* * *

[Prev](indexes-opclass.html "11.10. Operator Classes and Operator Families")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-examine.html "11.12. Examining Index Usage")  
---|---|---  
11.10. Operator Classes and Operator Families  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.12. Examining Index Usage  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-collations.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

