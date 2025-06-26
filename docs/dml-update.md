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

Supported Versions: [Current](/docs/current/dml-update.html "PostgreSQL 17 -
6.2. Updating Data") ([17](/docs/17/dml-update.html "PostgreSQL 17 -
6.2. Updating Data")) / [16](/docs/16/dml-update.html "PostgreSQL 16 -
6.2. Updating Data") / [15](/docs/15/dml-update.html "PostgreSQL 15 -
6.2. Updating Data") / [14](/docs/14/dml-update.html "PostgreSQL 14 -
6.2. Updating Data") / [13](/docs/13/dml-update.html "PostgreSQL 13 -
6.2. Updating Data")

Development Versions: [18](/docs/18/dml-update.html "PostgreSQL 18 -
6.2. Updating Data") / [devel](/docs/devel/dml-update.html "PostgreSQL devel -
6.2. Updating Data")

Unsupported versions: [12](/docs/12/dml-update.html "PostgreSQL 12 -
6.2. Updating Data") / [11](/docs/11/dml-update.html "PostgreSQL 11 -
6.2. Updating Data") / [10](/docs/10/dml-update.html "PostgreSQL 10 -
6.2. Updating Data") / [9.6](/docs/9.6/dml-update.html "PostgreSQL 9.6 -
6.2. Updating Data") / [9.5](/docs/9.5/dml-update.html "PostgreSQL 9.5 -
6.2. Updating Data") / [9.4](/docs/9.4/dml-update.html "PostgreSQL 9.4 -
6.2. Updating Data") / [9.3](/docs/9.3/dml-update.html "PostgreSQL 9.3 -
6.2. Updating Data") / [9.2](/docs/9.2/dml-update.html "PostgreSQL 9.2 -
6.2. Updating Data") / [9.1](/docs/9.1/dml-update.html "PostgreSQL 9.1 -
6.2. Updating Data") / [9.0](/docs/9.0/dml-update.html "PostgreSQL 9.0 -
6.2. Updating Data") / [8.4](/docs/8.4/dml-update.html "PostgreSQL 8.4 -
6.2. Updating Data") / [8.3](/docs/8.3/dml-update.html "PostgreSQL 8.3 -
6.2. Updating Data") / [8.2](/docs/8.2/dml-update.html "PostgreSQL 8.2 -
6.2. Updating Data") / [8.1](/docs/8.1/dml-update.html "PostgreSQL 8.1 -
6.2. Updating Data") / [8.0](/docs/8.0/dml-update.html "PostgreSQL 8.0 -
6.2. Updating Data") / [7.4](/docs/7.4/dml-update.html "PostgreSQL 7.4 -
6.2. Updating Data") / [7.3](/docs/7.3/dml-update.html "PostgreSQL 7.3 -
6.2. Updating Data")

__

6.2. Updating Data  
---  
[Prev](dml-insert.html "6.1. Inserting Data")  | [Up](dml.html "Chapter 6. Data Manipulation") | Chapter 6. Data Manipulation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](dml-delete.html "6.3. Deleting Data")  
  
* * *

## 6.2. Updating Data #

The modification of data that is already in the database is referred to as
updating. You can update individual rows, all the rows in a table, or a subset
of all rows. Each column can be updated separately; the other columns are not
affected.

To update existing rows, use the [UPDATE](sql-update.html "UPDATE") command.
This requires three pieces of information:

  1. The name of the table and column to update

  2. The new value of the column

  3. Which row(s) to update

Recall from [Chapter 5](ddl.html "Chapter 5. Data Definition") that SQL does
not, in general, provide a unique identifier for rows. Therefore it is not
always possible to directly specify which row to update. Instead, you specify
which conditions a row must meet in order to be updated. Only if you have a
primary key in the table (independent of whether you declared it or not) can
you reliably address individual rows by choosing a condition that matches the
primary key. Graphical database access tools rely on this fact to allow you to
update rows individually.

For example, this command updates all products that have a price of 5 to have
a price of 10:

    
    
    UPDATE products SET price = 10 WHERE price = 5;
    

This might cause zero, one, or many rows to be updated. It is not an error to
attempt an update that does not match any rows.

Let's look at that command in detail. First is the key word `UPDATE` followed
by the table name. As usual, the table name can be schema-qualified, otherwise
it is looked up in the path. Next is the key word `SET` followed by the column
name, an equal sign, and the new column value. The new column value can be any
scalar expression, not just a constant. For example, if you want to raise the
price of all products by 10% you could use:

    
    
    UPDATE products SET price = price * 1.10;
    

As you see, the expression for the new value can refer to the existing
value(s) in the row. We also left out the `WHERE` clause. If it is omitted, it
means that all rows in the table are updated. If it is present, only those
rows that match the `WHERE` condition are updated. Note that the equals sign
in the `SET` clause is an assignment while the one in the `WHERE` clause is a
comparison, but this does not create any ambiguity. Of course, the `WHERE`
condition does not have to be an equality test. Many other operators are
available (see [Chapter 9](functions.html "Chapter 9. Functions and
Operators")). But the expression needs to evaluate to a Boolean result.

You can update more than one column in an `UPDATE` command by listing more
than one assignment in the `SET` clause. For example:

    
    
    UPDATE mytable SET a = 5, b = 3, c = 1 WHERE a > 0;
    

* * *

[Prev](dml-insert.html "6.1. Inserting Data")  | [Up](dml.html "Chapter 6. Data Manipulation") |  [Next](dml-delete.html "6.3. Deleting Data")  
---|---|---  
6.1. Inserting Data  | [Home](index.html "PostgreSQL 16.9 Documentation") |  6.3. Deleting Data  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dml-update.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

