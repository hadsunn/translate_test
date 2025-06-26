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

Supported Versions: [Current](/docs/current/dml-delete.html "PostgreSQL 17 -
6.3. Deleting Data") ([17](/docs/17/dml-delete.html "PostgreSQL 17 -
6.3. Deleting Data")) / [16](/docs/16/dml-delete.html "PostgreSQL 16 -
6.3. Deleting Data") / [15](/docs/15/dml-delete.html "PostgreSQL 15 -
6.3. Deleting Data") / [14](/docs/14/dml-delete.html "PostgreSQL 14 -
6.3. Deleting Data") / [13](/docs/13/dml-delete.html "PostgreSQL 13 -
6.3. Deleting Data")

Development Versions: [18](/docs/18/dml-delete.html "PostgreSQL 18 -
6.3. Deleting Data") / [devel](/docs/devel/dml-delete.html "PostgreSQL devel -
6.3. Deleting Data")

Unsupported versions: [12](/docs/12/dml-delete.html "PostgreSQL 12 -
6.3. Deleting Data") / [11](/docs/11/dml-delete.html "PostgreSQL 11 -
6.3. Deleting Data") / [10](/docs/10/dml-delete.html "PostgreSQL 10 -
6.3. Deleting Data") / [9.6](/docs/9.6/dml-delete.html "PostgreSQL 9.6 -
6.3. Deleting Data") / [9.5](/docs/9.5/dml-delete.html "PostgreSQL 9.5 -
6.3. Deleting Data") / [9.4](/docs/9.4/dml-delete.html "PostgreSQL 9.4 -
6.3. Deleting Data") / [9.3](/docs/9.3/dml-delete.html "PostgreSQL 9.3 -
6.3. Deleting Data") / [9.2](/docs/9.2/dml-delete.html "PostgreSQL 9.2 -
6.3. Deleting Data") / [9.1](/docs/9.1/dml-delete.html "PostgreSQL 9.1 -
6.3. Deleting Data") / [9.0](/docs/9.0/dml-delete.html "PostgreSQL 9.0 -
6.3. Deleting Data") / [8.4](/docs/8.4/dml-delete.html "PostgreSQL 8.4 -
6.3. Deleting Data") / [8.3](/docs/8.3/dml-delete.html "PostgreSQL 8.3 -
6.3. Deleting Data") / [8.2](/docs/8.2/dml-delete.html "PostgreSQL 8.2 -
6.3. Deleting Data") / [8.1](/docs/8.1/dml-delete.html "PostgreSQL 8.1 -
6.3. Deleting Data") / [8.0](/docs/8.0/dml-delete.html "PostgreSQL 8.0 -
6.3. Deleting Data") / [7.4](/docs/7.4/dml-delete.html "PostgreSQL 7.4 -
6.3. Deleting Data") / [7.3](/docs/7.3/dml-delete.html "PostgreSQL 7.3 -
6.3. Deleting Data")

__

6.3. Deleting Data  
---  
[Prev](dml-update.html "6.2. Updating Data")  | [Up](dml.html "Chapter 6. Data Manipulation") | Chapter 6. Data Manipulation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](dml-returning.html "6.4. Returning Data from Modified Rows")  
  
* * *

## 6.3. Deleting Data #

So far we have explained how to add data to tables and how to change data.
What remains is to discuss how to remove data that is no longer needed. Just
as adding data is only possible in whole rows, you can only remove entire rows
from a table. In the previous section we explained that SQL does not provide a
way to directly address individual rows. Therefore, removing rows can only be
done by specifying conditions that the rows to be removed have to match. If
you have a primary key in the table then you can specify the exact row. But
you can also remove groups of rows matching a condition, or you can remove all
rows in the table at once.

You use the [DELETE](sql-delete.html "DELETE") command to remove rows; the
syntax is very similar to the [UPDATE](sql-update.html "UPDATE") command. For
instance, to remove all rows from the products table that have a price of 10,
use:

    
    
    DELETE FROM products WHERE price = 10;
    

If you simply write:

    
    
    DELETE FROM products;
    

then all rows in the table will be deleted! Caveat programmer.

* * *

[Prev](dml-update.html "6.2. Updating Data")  | [Up](dml.html "Chapter 6. Data Manipulation") |  [Next](dml-returning.html "6.4. Returning Data from Modified Rows")  
---|---|---  
6.2. Updating Data  | [Home](index.html "PostgreSQL 16.9 Documentation") |  6.4. Returning Data from Modified Rows  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dml-delete.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

