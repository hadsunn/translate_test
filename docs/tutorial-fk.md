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

Supported Versions: [Current](/docs/current/tutorial-fk.html "PostgreSQL 17 -
3.3. Foreign Keys") ([17](/docs/17/tutorial-fk.html "PostgreSQL 17 -
3.3. Foreign Keys")) / [16](/docs/16/tutorial-fk.html "PostgreSQL 16 -
3.3. Foreign Keys") / [15](/docs/15/tutorial-fk.html "PostgreSQL 15 -
3.3. Foreign Keys") / [14](/docs/14/tutorial-fk.html "PostgreSQL 14 -
3.3. Foreign Keys") / [13](/docs/13/tutorial-fk.html "PostgreSQL 13 -
3.3. Foreign Keys")

Development Versions: [18](/docs/18/tutorial-fk.html "PostgreSQL 18 -
3.3. Foreign Keys") / [devel](/docs/devel/tutorial-fk.html "PostgreSQL devel -
3.3. Foreign Keys")

Unsupported versions: [12](/docs/12/tutorial-fk.html "PostgreSQL 12 -
3.3. Foreign Keys") / [11](/docs/11/tutorial-fk.html "PostgreSQL 11 -
3.3. Foreign Keys") / [10](/docs/10/tutorial-fk.html "PostgreSQL 10 -
3.3. Foreign Keys") / [9.6](/docs/9.6/tutorial-fk.html "PostgreSQL 9.6 -
3.3. Foreign Keys") / [9.5](/docs/9.5/tutorial-fk.html "PostgreSQL 9.5 -
3.3. Foreign Keys") / [9.4](/docs/9.4/tutorial-fk.html "PostgreSQL 9.4 -
3.3. Foreign Keys") / [9.3](/docs/9.3/tutorial-fk.html "PostgreSQL 9.3 -
3.3. Foreign Keys") / [9.2](/docs/9.2/tutorial-fk.html "PostgreSQL 9.2 -
3.3. Foreign Keys") / [9.1](/docs/9.1/tutorial-fk.html "PostgreSQL 9.1 -
3.3. Foreign Keys") / [9.0](/docs/9.0/tutorial-fk.html "PostgreSQL 9.0 -
3.3. Foreign Keys") / [8.4](/docs/8.4/tutorial-fk.html "PostgreSQL 8.4 -
3.3. Foreign Keys") / [8.3](/docs/8.3/tutorial-fk.html "PostgreSQL 8.3 -
3.3. Foreign Keys") / [8.2](/docs/8.2/tutorial-fk.html "PostgreSQL 8.2 -
3.3. Foreign Keys") / [8.1](/docs/8.1/tutorial-fk.html "PostgreSQL 8.1 -
3.3. Foreign Keys") / [8.0](/docs/8.0/tutorial-fk.html "PostgreSQL 8.0 -
3.3. Foreign Keys") / [7.4](/docs/7.4/tutorial-fk.html "PostgreSQL 7.4 -
3.3. Foreign Keys") / [7.3](/docs/7.3/tutorial-fk.html "PostgreSQL 7.3 -
3.3. Foreign Keys") / [7.2](/docs/7.2/tutorial-fk.html "PostgreSQL 7.2 -
3.3. Foreign Keys")

__

3.3. Foreign Keys  
---  
[Prev](tutorial-views.html "3.2. Views")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") | Chapter 3. Advanced Features | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-transactions.html "3.4. Transactions")  
  
* * *

## 3.3. Foreign Keys #

Recall the `weather` and `cities` tables from [Chapter 2](tutorial-sql.html
"Chapter 2. The SQL Language"). Consider the following problem: You want to
make sure that no one can insert rows in the `weather` table that do not have
a matching entry in the `cities` table. This is called maintaining the
_referential integrity_ of your data. In simplistic database systems this
would be implemented (if at all) by first looking at the `cities` table to
check if a matching record exists, and then inserting or rejecting the new
`weather` records. This approach has a number of problems and is very
inconvenient, so PostgreSQL can do this for you.

The new declaration of the tables would look like this:

    
    
    CREATE TABLE cities (
            name     varchar(80) primary key,
            location point
    );
    
    CREATE TABLE weather (
            city      varchar(80) references cities(name),
            temp_lo   int,
            temp_hi   int,
            prcp      real,
            date      date
    );
    

Now try inserting an invalid record:

    
    
    INSERT INTO weather VALUES ('Berkeley', 45, 53, 0.0, '1994-11-28');
    
    
    
    ERROR:  insert or update on table "weather" violates foreign key constraint "weather_city_fkey"
    DETAIL:  Key (city)=(Berkeley) is not present in table "cities".
    

The behavior of foreign keys can be finely tuned to your application. We will
not go beyond this simple example in this tutorial, but just refer you to
[Chapter 5](ddl.html "Chapter 5. Data Definition") for more information.
Making correct use of foreign keys will definitely improve the quality of your
database applications, so you are strongly encouraged to learn about them.

* * *

[Prev](tutorial-views.html "3.2. Views")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") |  [Next](tutorial-transactions.html "3.4. Transactions")  
---|---|---  
3.2. Views  | [Home](index.html "PostgreSQL 16.9 Documentation") |  3.4. Transactions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-fk.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

