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

Supported Versions: [Current](/docs/current/dml-insert.html "PostgreSQL 17 -
6.1. Inserting Data") ([17](/docs/17/dml-insert.html "PostgreSQL 17 -
6.1. Inserting Data")) / [16](/docs/16/dml-insert.html "PostgreSQL 16 -
6.1. Inserting Data") / [15](/docs/15/dml-insert.html "PostgreSQL 15 -
6.1. Inserting Data") / [14](/docs/14/dml-insert.html "PostgreSQL 14 -
6.1. Inserting Data") / [13](/docs/13/dml-insert.html "PostgreSQL 13 -
6.1. Inserting Data")

Development Versions: [18](/docs/18/dml-insert.html "PostgreSQL 18 -
6.1. Inserting Data") / [devel](/docs/devel/dml-insert.html "PostgreSQL devel
- 6.1. Inserting Data")

Unsupported versions: [12](/docs/12/dml-insert.html "PostgreSQL 12 -
6.1. Inserting Data") / [11](/docs/11/dml-insert.html "PostgreSQL 11 -
6.1. Inserting Data") / [10](/docs/10/dml-insert.html "PostgreSQL 10 -
6.1. Inserting Data") / [9.6](/docs/9.6/dml-insert.html "PostgreSQL 9.6 -
6.1. Inserting Data") / [9.5](/docs/9.5/dml-insert.html "PostgreSQL 9.5 -
6.1. Inserting Data") / [9.4](/docs/9.4/dml-insert.html "PostgreSQL 9.4 -
6.1. Inserting Data") / [9.3](/docs/9.3/dml-insert.html "PostgreSQL 9.3 -
6.1. Inserting Data") / [9.2](/docs/9.2/dml-insert.html "PostgreSQL 9.2 -
6.1. Inserting Data") / [9.1](/docs/9.1/dml-insert.html "PostgreSQL 9.1 -
6.1. Inserting Data") / [9.0](/docs/9.0/dml-insert.html "PostgreSQL 9.0 -
6.1. Inserting Data") / [8.4](/docs/8.4/dml-insert.html "PostgreSQL 8.4 -
6.1. Inserting Data") / [8.3](/docs/8.3/dml-insert.html "PostgreSQL 8.3 -
6.1. Inserting Data") / [8.2](/docs/8.2/dml-insert.html "PostgreSQL 8.2 -
6.1. Inserting Data")

__

6.1. Inserting Data  
---  
[Prev](dml.html "Chapter 6. Data Manipulation")  | [Up](dml.html "Chapter 6. Data Manipulation") | Chapter 6. Data Manipulation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](dml-update.html "6.2. Updating Data")  
  
* * *

## 6.1. Inserting Data #

When a table is created, it contains no data. The first thing to do before a
database can be of much use is to insert data. Data is inserted one row at a
time. You can also insert more than one row in a single command, but it is not
possible to insert something that is not a complete row. Even if you know only
some column values, a complete row must be created.

To create a new row, use the [INSERT](sql-insert.html "INSERT") command. The
command requires the table name and column values. For example, consider the
products table from [Chapter 5](ddl.html "Chapter 5. Data Definition"):

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric
    );
    

An example command to insert a row would be:

    
    
    INSERT INTO products VALUES (1, 'Cheese', 9.99);
    

The data values are listed in the order in which the columns appear in the
table, separated by commas. Usually, the data values will be literals
(constants), but scalar expressions are also allowed.

The above syntax has the drawback that you need to know the order of the
columns in the table. To avoid this you can also list the columns explicitly.
For example, both of the following commands have the same effect as the one
above:

    
    
    INSERT INTO products (product_no, name, price) VALUES (1, 'Cheese', 9.99);
    INSERT INTO products (name, price, product_no) VALUES ('Cheese', 9.99, 1);
    

Many users consider it good practice to always list the column names.

If you don't have values for all the columns, you can omit some of them. In
that case, the columns will be filled with their default values. For example:

    
    
    INSERT INTO products (product_no, name) VALUES (1, 'Cheese');
    INSERT INTO products VALUES (1, 'Cheese');
    

The second form is a PostgreSQL extension. It fills the columns from the left
with as many values as are given, and the rest will be defaulted.

For clarity, you can also request default values explicitly, for individual
columns or for the entire row:

    
    
    INSERT INTO products (product_no, name, price) VALUES (1, 'Cheese', DEFAULT);
    INSERT INTO products DEFAULT VALUES;
    

You can insert multiple rows in a single command:

    
    
    INSERT INTO products (product_no, name, price) VALUES
        (1, 'Cheese', 9.99),
        (2, 'Bread', 1.99),
        (3, 'Milk', 2.99);
    

It is also possible to insert the result of a query (which might be no rows,
one row, or many rows):

    
    
    INSERT INTO products (product_no, name, price)
      SELECT product_no, name, price FROM new_products
        WHERE release_date = 'today';
    

This provides the full power of the SQL query mechanism ([Chapter
7](queries.html "Chapter 7. Queries")) for computing the rows to be inserted.

### Tip

When inserting a lot of data at the same time, consider using the [COPY](sql-
copy.html "COPY") command. It is not as flexible as the [INSERT](sql-
insert.html "INSERT") command, but is more efficient. Refer to [Section
14.4](populate.html "14.4. Populating a Database") for more information on
improving bulk loading performance.

* * *

[Prev](dml.html "Chapter 6. Data Manipulation")  | [Up](dml.html "Chapter 6. Data Manipulation") |  [Next](dml-update.html "6.2. Updating Data")  
---|---|---  
Chapter 6. Data Manipulation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  6.2. Updating Data  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dml-insert.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

