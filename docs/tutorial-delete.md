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

Supported Versions: [Current](/docs/current/tutorial-delete.html "PostgreSQL
17 - 2.9. Deletions") ([17](/docs/17/tutorial-delete.html "PostgreSQL 17 -
2.9. Deletions")) / [16](/docs/16/tutorial-delete.html "PostgreSQL 16 -
2.9. Deletions") / [15](/docs/15/tutorial-delete.html "PostgreSQL 15 -
2.9. Deletions") / [14](/docs/14/tutorial-delete.html "PostgreSQL 14 -
2.9. Deletions") / [13](/docs/13/tutorial-delete.html "PostgreSQL 13 -
2.9. Deletions")

Development Versions: [18](/docs/18/tutorial-delete.html "PostgreSQL 18 -
2.9. Deletions") / [devel](/docs/devel/tutorial-delete.html "PostgreSQL devel
- 2.9. Deletions")

Unsupported versions: [12](/docs/12/tutorial-delete.html "PostgreSQL 12 -
2.9. Deletions") / [11](/docs/11/tutorial-delete.html "PostgreSQL 11 -
2.9. Deletions") / [10](/docs/10/tutorial-delete.html "PostgreSQL 10 -
2.9. Deletions") / [9.6](/docs/9.6/tutorial-delete.html "PostgreSQL 9.6 -
2.9. Deletions") / [9.5](/docs/9.5/tutorial-delete.html "PostgreSQL 9.5 -
2.9. Deletions") / [9.4](/docs/9.4/tutorial-delete.html "PostgreSQL 9.4 -
2.9. Deletions") / [9.3](/docs/9.3/tutorial-delete.html "PostgreSQL 9.3 -
2.9. Deletions") / [9.2](/docs/9.2/tutorial-delete.html "PostgreSQL 9.2 -
2.9. Deletions") / [9.1](/docs/9.1/tutorial-delete.html "PostgreSQL 9.1 -
2.9. Deletions") / [9.0](/docs/9.0/tutorial-delete.html "PostgreSQL 9.0 -
2.9. Deletions") / [8.4](/docs/8.4/tutorial-delete.html "PostgreSQL 8.4 -
2.9. Deletions") / [8.3](/docs/8.3/tutorial-delete.html "PostgreSQL 8.3 -
2.9. Deletions") / [8.2](/docs/8.2/tutorial-delete.html "PostgreSQL 8.2 -
2.9. Deletions") / [8.1](/docs/8.1/tutorial-delete.html "PostgreSQL 8.1 -
2.9. Deletions") / [8.0](/docs/8.0/tutorial-delete.html "PostgreSQL 8.0 -
2.9. Deletions") / [7.4](/docs/7.4/tutorial-delete.html "PostgreSQL 7.4 -
2.9. Deletions") / [7.3](/docs/7.3/tutorial-delete.html "PostgreSQL 7.3 -
2.9. Deletions") / [7.2](/docs/7.2/tutorial-delete.html "PostgreSQL 7.2 -
2.9. Deletions")

__

2.9. Deletions  
---  
[Prev](tutorial-update.html "2.8. Updates")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-advanced.html "Chapter 3. Advanced Features")  
  
* * *

## 2.9. Deletions #

Rows can be removed from a table using the `DELETE` command. Suppose you are
no longer interested in the weather of Hayward. Then you can do the following
to delete those rows from the table:

    
    
    DELETE FROM weather WHERE city = 'Hayward';
    

All weather records belonging to Hayward are removed.

    
    
    SELECT * FROM weather;
    
    
    
         city      | temp_lo | temp_hi | prcp |    date
    ---------------+---------+---------+------+------------
     San Francisco |      46 |      50 | 0.25 | 1994-11-27
     San Francisco |      41 |      55 |    0 | 1994-11-29
    (2 rows)
    

One should be wary of statements of the form

    
    
    DELETE FROM _tablename_ ;
    

Without a qualification, `DELETE` will remove _all_ rows from the given table,
leaving it empty. The system will not request confirmation before doing this!

* * *

[Prev](tutorial-update.html "2.8. Updates")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-advanced.html "Chapter 3. Advanced Features")  
---|---|---  
2.8. Updates  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 3. Advanced Features  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-delete.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

