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

Supported Versions: [Current](/docs/current/tutorial-views.html "PostgreSQL 17
- 3.2. Views") ([17](/docs/17/tutorial-views.html "PostgreSQL 17 -
3.2. Views")) / [16](/docs/16/tutorial-views.html "PostgreSQL 16 -
3.2. Views") / [15](/docs/15/tutorial-views.html "PostgreSQL 15 - 3.2. Views")
/ [14](/docs/14/tutorial-views.html "PostgreSQL 14 - 3.2. Views") /
[13](/docs/13/tutorial-views.html "PostgreSQL 13 - 3.2. Views")

Development Versions: [18](/docs/18/tutorial-views.html "PostgreSQL 18 -
3.2. Views") / [devel](/docs/devel/tutorial-views.html "PostgreSQL devel -
3.2. Views")

Unsupported versions: [12](/docs/12/tutorial-views.html "PostgreSQL 12 -
3.2. Views") / [11](/docs/11/tutorial-views.html "PostgreSQL 11 - 3.2. Views")
/ [10](/docs/10/tutorial-views.html "PostgreSQL 10 - 3.2. Views") /
[9.6](/docs/9.6/tutorial-views.html "PostgreSQL 9.6 - 3.2. Views") /
[9.5](/docs/9.5/tutorial-views.html "PostgreSQL 9.5 - 3.2. Views") /
[9.4](/docs/9.4/tutorial-views.html "PostgreSQL 9.4 - 3.2. Views") /
[9.3](/docs/9.3/tutorial-views.html "PostgreSQL 9.3 - 3.2. Views") /
[9.2](/docs/9.2/tutorial-views.html "PostgreSQL 9.2 - 3.2. Views") /
[9.1](/docs/9.1/tutorial-views.html "PostgreSQL 9.1 - 3.2. Views") /
[9.0](/docs/9.0/tutorial-views.html "PostgreSQL 9.0 - 3.2. Views") /
[8.4](/docs/8.4/tutorial-views.html "PostgreSQL 8.4 - 3.2. Views") /
[8.3](/docs/8.3/tutorial-views.html "PostgreSQL 8.3 - 3.2. Views") /
[8.2](/docs/8.2/tutorial-views.html "PostgreSQL 8.2 - 3.2. Views") /
[8.1](/docs/8.1/tutorial-views.html "PostgreSQL 8.1 - 3.2. Views") /
[8.0](/docs/8.0/tutorial-views.html "PostgreSQL 8.0 - 3.2. Views") /
[7.4](/docs/7.4/tutorial-views.html "PostgreSQL 7.4 - 3.2. Views") /
[7.3](/docs/7.3/tutorial-views.html "PostgreSQL 7.3 - 3.2. Views") /
[7.2](/docs/7.2/tutorial-views.html "PostgreSQL 7.2 - 3.2. Views")

__

3.2. Views  
---  
[Prev](tutorial-advanced-intro.html "3.1. Introduction")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") | Chapter 3. Advanced Features | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-fk.html "3.3. Foreign Keys")  
  
* * *

## 3.2. Views #

Refer back to the queries in [Section 2.6](tutorial-join.html "2.6. Joins
Between Tables"). Suppose the combined listing of weather records and city
location is of particular interest to your application, but you do not want to
type the query each time you need it. You can create a _view_ over the query,
which gives a name to the query that you can refer to like an ordinary table:

    
    
    CREATE VIEW myview AS
        SELECT name, temp_lo, temp_hi, prcp, date, location
            FROM weather, cities
            WHERE city = name;
    
    SELECT * FROM myview;
    

Making liberal use of views is a key aspect of good SQL database design. Views
allow you to encapsulate the details of the structure of your tables, which
might change as your application evolves, behind consistent interfaces.

Views can be used in almost any place a real table can be used. Building views
upon other views is not uncommon.

* * *

[Prev](tutorial-advanced-intro.html "3.1. Introduction")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") |  [Next](tutorial-fk.html "3.3. Foreign Keys")  
---|---|---  
3.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  3.3. Foreign Keys  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-views.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

