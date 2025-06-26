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

Supported Versions: [Current](/docs/current/tutorial-inheritance.html
"PostgreSQL 17 - 3.6. Inheritance") ([17](/docs/17/tutorial-inheritance.html
"PostgreSQL 17 - 3.6. Inheritance")) / [16](/docs/16/tutorial-inheritance.html
"PostgreSQL 16 - 3.6. Inheritance") / [15](/docs/15/tutorial-inheritance.html
"PostgreSQL 15 - 3.6. Inheritance") / [14](/docs/14/tutorial-inheritance.html
"PostgreSQL 14 - 3.6. Inheritance") / [13](/docs/13/tutorial-inheritance.html
"PostgreSQL 13 - 3.6. Inheritance")

Development Versions: [18](/docs/18/tutorial-inheritance.html "PostgreSQL 18 -
3.6. Inheritance") / [devel](/docs/devel/tutorial-inheritance.html "PostgreSQL
devel - 3.6. Inheritance")

Unsupported versions: [12](/docs/12/tutorial-inheritance.html "PostgreSQL 12 -
3.6. Inheritance") / [11](/docs/11/tutorial-inheritance.html "PostgreSQL 11 -
3.6. Inheritance") / [10](/docs/10/tutorial-inheritance.html "PostgreSQL 10 -
3.6. Inheritance") / [9.6](/docs/9.6/tutorial-inheritance.html "PostgreSQL 9.6
- 3.6. Inheritance") / [9.5](/docs/9.5/tutorial-inheritance.html "PostgreSQL
9.5 - 3.6. Inheritance") / [9.4](/docs/9.4/tutorial-inheritance.html
"PostgreSQL 9.4 - 3.6. Inheritance") / [9.3](/docs/9.3/tutorial-
inheritance.html "PostgreSQL 9.3 - 3.6. Inheritance") /
[9.2](/docs/9.2/tutorial-inheritance.html "PostgreSQL 9.2 - 3.6. Inheritance")
/ [9.1](/docs/9.1/tutorial-inheritance.html "PostgreSQL 9.1 -
3.6. Inheritance") / [9.0](/docs/9.0/tutorial-inheritance.html "PostgreSQL 9.0
- 3.6. Inheritance") / [8.4](/docs/8.4/tutorial-inheritance.html "PostgreSQL
8.4 - 3.6. Inheritance") / [8.3](/docs/8.3/tutorial-inheritance.html
"PostgreSQL 8.3 - 3.6. Inheritance") / [8.2](/docs/8.2/tutorial-
inheritance.html "PostgreSQL 8.2 - 3.6. Inheritance") /
[8.1](/docs/8.1/tutorial-inheritance.html "PostgreSQL 8.1 - 3.6. Inheritance")
/ [8.0](/docs/8.0/tutorial-inheritance.html "PostgreSQL 8.0 -
3.6. Inheritance") / [7.4](/docs/7.4/tutorial-inheritance.html "PostgreSQL 7.4
- 3.6. Inheritance") / [7.3](/docs/7.3/tutorial-inheritance.html "PostgreSQL
7.3 - 3.6. Inheritance") / [7.2](/docs/7.2/tutorial-inheritance.html
"PostgreSQL 7.2 - 3.6. Inheritance")

__

3.6. Inheritance  
---  
[Prev](tutorial-window.html "3.5. Window Functions")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") | Chapter 3. Advanced Features | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-conclusion.html "3.7. Conclusion")  
  
* * *

## 3.6. Inheritance #

Inheritance is a concept from object-oriented databases. It opens up
interesting new possibilities of database design.

Let's create two tables: A table `cities` and a table `capitals`. Naturally,
capitals are also cities, so you want some way to show the capitals implicitly
when you list all cities. If you're really clever you might invent some scheme
like this:

    
    
    CREATE TABLE capitals (
      name       text,
      population real,
      elevation  int,    -- (in ft)
      state      char(2)
    );
    
    CREATE TABLE non_capitals (
      name       text,
      population real,
      elevation  int     -- (in ft)
    );
    
    CREATE VIEW cities AS
      SELECT name, population, elevation FROM capitals
        UNION
      SELECT name, population, elevation FROM non_capitals;
    

This works OK as far as querying goes, but it gets ugly when you need to
update several rows, for one thing.

A better solution is this:

    
    
    CREATE TABLE cities (
      name       text,
      population real,
      elevation  int     -- (in ft)
    );
    
    CREATE TABLE capitals (
      state      char(2) UNIQUE NOT NULL
    ) INHERITS (cities);
    

In this case, a row of `capitals` _inherits_ all columns (`name`,
`population`, and `elevation`) from its _parent_ , `cities`. The type of the
column `name` is `text`, a native PostgreSQL type for variable length
character strings. The `capitals` table has an additional column, `state`,
which shows its state abbreviation. In PostgreSQL, a table can inherit from
zero or more other tables.

For example, the following query finds the names of all cities, including
state capitals, that are located at an elevation over 500 feet:

    
    
    SELECT name, elevation
      FROM cities
      WHERE elevation > 500;
    

which returns:

    
    
       name    | elevation
    -----------+-----------
     Las Vegas |      2174
     Mariposa  |      1953
     Madison   |       845
    (3 rows)
    

On the other hand, the following query finds all the cities that are not state
capitals and are situated at an elevation over 500 feet:

    
    
    SELECT name, elevation
        FROM ONLY cities
        WHERE elevation > 500;
    
    
    
       name    | elevation
    -----------+-----------
     Las Vegas |      2174
     Mariposa  |      1953
    (2 rows)
    

Here the `ONLY` before `cities` indicates that the query should be run over
only the `cities` table, and not tables below `cities` in the inheritance
hierarchy. Many of the commands that we have already discussed — `SELECT`,
`UPDATE`, and `DELETE` — support this `ONLY` notation.

### Note

Although inheritance is frequently useful, it has not been integrated with
unique constraints or foreign keys, which limits its usefulness. See [Section
5.10](ddl-inherit.html "5.10. Inheritance") for more detail.

* * *

[Prev](tutorial-window.html "3.5. Window Functions")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") |  [Next](tutorial-conclusion.html "3.7. Conclusion")  
---|---|---  
3.5. Window Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  3.7. Conclusion  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-inheritance.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

