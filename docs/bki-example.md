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

Supported Versions: [Current](/docs/current/bki-example.html "PostgreSQL 17 -
75.6. BKI Example") ([17](/docs/17/bki-example.html "PostgreSQL 17 - 75.6. BKI
Example")) / [16](/docs/16/bki-example.html "PostgreSQL 16 - 75.6. BKI
Example") / [15](/docs/15/bki-example.html "PostgreSQL 15 - 75.6. BKI
Example") / [14](/docs/14/bki-example.html "PostgreSQL 14 - 75.6. BKI
Example") / [13](/docs/13/bki-example.html "PostgreSQL 13 - 75.6. BKI
Example")

Development Versions: [18](/docs/18/bki-example.html "PostgreSQL 18 -
75.6. BKI Example") / [devel](/docs/devel/bki-example.html "PostgreSQL devel -
75.6. BKI Example")

Unsupported versions: [12](/docs/12/bki-example.html "PostgreSQL 12 -
75.6. BKI Example") / [11](/docs/11/bki-example.html "PostgreSQL 11 -
75.6. BKI Example") / [10](/docs/10/bki-example.html "PostgreSQL 10 -
75.6. BKI Example") / [9.6](/docs/9.6/bki-example.html "PostgreSQL 9.6 -
75.6. BKI Example") / [9.5](/docs/9.5/bki-example.html "PostgreSQL 9.5 -
75.6. BKI Example") / [9.4](/docs/9.4/bki-example.html "PostgreSQL 9.4 -
75.6. BKI Example") / [9.3](/docs/9.3/bki-example.html "PostgreSQL 9.3 -
75.6. BKI Example") / [9.2](/docs/9.2/bki-example.html "PostgreSQL 9.2 -
75.6. BKI Example") / [9.1](/docs/9.1/bki-example.html "PostgreSQL 9.1 -
75.6. BKI Example") / [9.0](/docs/9.0/bki-example.html "PostgreSQL 9.0 -
75.6. BKI Example") / [8.4](/docs/8.4/bki-example.html "PostgreSQL 8.4 -
75.6. BKI Example") / [8.3](/docs/8.3/bki-example.html "PostgreSQL 8.3 -
75.6. BKI Example") / [8.2](/docs/8.2/bki-example.html "PostgreSQL 8.2 -
75.6. BKI Example") / [8.1](/docs/8.1/bki-example.html "PostgreSQL 8.1 -
75.6. BKI Example") / [8.0](/docs/8.0/bki-example.html "PostgreSQL 8.0 -
75.6. BKI Example") / [7.4](/docs/7.4/bki-example.html "PostgreSQL 7.4 -
75.6. BKI Example") / [7.3](/docs/7.3/bki-example.html "PostgreSQL 7.3 -
75.6. BKI Example") / [7.2](/docs/7.2/bki-example.html "PostgreSQL 7.2 -
75.6. BKI Example") / [7.1](/docs/7.1/bki-example.html "PostgreSQL 7.1 -
75.6. BKI Example")

__

75.6. BKI Example  
---  
[Prev](bki-structure.html "75.5. Structure of the Bootstrap BKI File")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") | Chapter 75. System Catalog Declarations and Initial Contents | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](planner-stats-details.html "Chapter 76. How the Planner Uses Statistics")  
  
* * *

## 75.6. BKI Example #

The following sequence of commands will create the table `test_table` with OID
420, having three columns `oid`, `cola` and `colb` of type `oid`, `int4` and
`text`, respectively, and insert two rows into the table:

    
    
    create test_table 420 (oid = oid, cola = int4, colb = text)
    open test_table
    insert ( 421 1 'value 1' )
    insert ( 422 2 _null_ )
    close test_table
    

* * *

[Prev](bki-structure.html "75.5. Structure of the Bootstrap BKI File")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") |  [Next](planner-stats-details.html "Chapter 76. How the Planner Uses Statistics")  
---|---|---  
75.5. Structure of the Bootstrap BKI File  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 76. How the Planner Uses Statistics  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/bki-example.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

