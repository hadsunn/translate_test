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

Supported Versions: [Current](/docs/current/tutorial-update.html "PostgreSQL
17 - 2.8. Updates") ([17](/docs/17/tutorial-update.html "PostgreSQL 17 -
2.8. Updates")) / [16](/docs/16/tutorial-update.html "PostgreSQL 16 -
2.8. Updates") / [15](/docs/15/tutorial-update.html "PostgreSQL 15 -
2.8. Updates") / [14](/docs/14/tutorial-update.html "PostgreSQL 14 -
2.8. Updates") / [13](/docs/13/tutorial-update.html "PostgreSQL 13 -
2.8. Updates")

Development Versions: [18](/docs/18/tutorial-update.html "PostgreSQL 18 -
2.8. Updates") / [devel](/docs/devel/tutorial-update.html "PostgreSQL devel -
2.8. Updates")

Unsupported versions: [12](/docs/12/tutorial-update.html "PostgreSQL 12 -
2.8. Updates") / [11](/docs/11/tutorial-update.html "PostgreSQL 11 -
2.8. Updates") / [10](/docs/10/tutorial-update.html "PostgreSQL 10 -
2.8. Updates") / [9.6](/docs/9.6/tutorial-update.html "PostgreSQL 9.6 -
2.8. Updates") / [9.5](/docs/9.5/tutorial-update.html "PostgreSQL 9.5 -
2.8. Updates") / [9.4](/docs/9.4/tutorial-update.html "PostgreSQL 9.4 -
2.8. Updates") / [9.3](/docs/9.3/tutorial-update.html "PostgreSQL 9.3 -
2.8. Updates") / [9.2](/docs/9.2/tutorial-update.html "PostgreSQL 9.2 -
2.8. Updates") / [9.1](/docs/9.1/tutorial-update.html "PostgreSQL 9.1 -
2.8. Updates") / [9.0](/docs/9.0/tutorial-update.html "PostgreSQL 9.0 -
2.8. Updates") / [8.4](/docs/8.4/tutorial-update.html "PostgreSQL 8.4 -
2.8. Updates") / [8.3](/docs/8.3/tutorial-update.html "PostgreSQL 8.3 -
2.8. Updates") / [8.2](/docs/8.2/tutorial-update.html "PostgreSQL 8.2 -
2.8. Updates") / [8.1](/docs/8.1/tutorial-update.html "PostgreSQL 8.1 -
2.8. Updates") / [8.0](/docs/8.0/tutorial-update.html "PostgreSQL 8.0 -
2.8. Updates") / [7.4](/docs/7.4/tutorial-update.html "PostgreSQL 7.4 -
2.8. Updates") / [7.3](/docs/7.3/tutorial-update.html "PostgreSQL 7.3 -
2.8. Updates") / [7.2](/docs/7.2/tutorial-update.html "PostgreSQL 7.2 -
2.8. Updates")

__

2.8. Updates  
---  
[Prev](tutorial-agg.html "2.7. Aggregate Functions")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-delete.html "2.9. Deletions")  
  
* * *

## 2.8. Updates #

You can update existing rows using the `UPDATE` command. Suppose you discover
the temperature readings are all off by 2 degrees after November 28. You can
correct the data as follows:

    
    
    UPDATE weather
        SET temp_hi = temp_hi - 2,  temp_lo = temp_lo - 2
        WHERE date > '1994-11-28';
    

Look at the new state of the data:

    
    
    SELECT * FROM weather;
    
         city      | temp_lo | temp_hi | prcp |    date
    ---------------+---------+---------+------+------------
     San Francisco |      46 |      50 | 0.25 | 1994-11-27
     San Francisco |      41 |      55 |    0 | 1994-11-29
     Hayward       |      35 |      52 |      | 1994-11-29
    (3 rows)
    

* * *

[Prev](tutorial-agg.html "2.7. Aggregate Functions")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-delete.html "2.9. Deletions")  
---|---|---  
2.7. Aggregate Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.9. Deletions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-update.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

