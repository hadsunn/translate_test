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

Supported Versions: [Current](/docs/current/dml-returning.html "PostgreSQL 17
- 6.4. Returning Data from Modified Rows") ([17](/docs/17/dml-returning.html
"PostgreSQL 17 - 6.4. Returning Data from Modified Rows")) /
[16](/docs/16/dml-returning.html "PostgreSQL 16 - 6.4. Returning Data from
Modified Rows") / [15](/docs/15/dml-returning.html "PostgreSQL 15 -
6.4. Returning Data from Modified Rows") / [14](/docs/14/dml-returning.html
"PostgreSQL 14 - 6.4. Returning Data from Modified Rows") / [13](/docs/13/dml-
returning.html "PostgreSQL 13 - 6.4. Returning Data from Modified Rows")

Development Versions: [18](/docs/18/dml-returning.html "PostgreSQL 18 -
6.4. Returning Data from Modified Rows") / [devel](/docs/devel/dml-
returning.html "PostgreSQL devel - 6.4. Returning Data from Modified Rows")

Unsupported versions: [12](/docs/12/dml-returning.html "PostgreSQL 12 -
6.4. Returning Data from Modified Rows") / [11](/docs/11/dml-returning.html
"PostgreSQL 11 - 6.4. Returning Data from Modified Rows") / [10](/docs/10/dml-
returning.html "PostgreSQL 10 - 6.4. Returning Data from Modified Rows") /
[9.6](/docs/9.6/dml-returning.html "PostgreSQL 9.6 - 6.4. Returning Data from
Modified Rows") / [9.5](/docs/9.5/dml-returning.html "PostgreSQL 9.5 -
6.4. Returning Data from Modified Rows") / [9.4](/docs/9.4/dml-returning.html
"PostgreSQL 9.4 - 6.4. Returning Data from Modified Rows") /
[9.3](/docs/9.3/dml-returning.html "PostgreSQL 9.3 - 6.4. Returning Data from
Modified Rows") / [9.2](/docs/9.2/dml-returning.html "PostgreSQL 9.2 -
6.4. Returning Data from Modified Rows")

__

6.4. Returning Data from Modified Rows  
---  
[Prev](dml-delete.html "6.3. Deleting Data")  | [Up](dml.html "Chapter 6. Data Manipulation") | Chapter 6. Data Manipulation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries.html "Chapter 7. Queries")  
  
* * *

## 6.4. Returning Data from Modified Rows #

Sometimes it is useful to obtain data from modified rows while they are being
manipulated. The `INSERT`, `UPDATE`, and `DELETE` commands all have an
optional `RETURNING` clause that supports this. Use of `RETURNING` avoids
performing an extra database query to collect the data, and is especially
valuable when it would otherwise be difficult to identify the modified rows
reliably.

The allowed contents of a `RETURNING` clause are the same as a `SELECT`
command's output list (see [Section 7.3](queries-select-lists.html
"7.3. Select Lists")). It can contain column names of the command's target
table, or value expressions using those columns. A common shorthand is
`RETURNING *`, which selects all columns of the target table in order.

In an `INSERT`, the data available to `RETURNING` is the row as it was
inserted. This is not so useful in trivial inserts, since it would just repeat
the data provided by the client. But it can be very handy when relying on
computed default values. For example, when using a [`serial`](datatype-
numeric.html#DATATYPE-SERIAL "8.1.4. Serial Types") column to provide unique
identifiers, `RETURNING` can return the ID assigned to a new row:

    
    
    CREATE TABLE users (firstname text, lastname text, id serial primary key);
    
    INSERT INTO users (firstname, lastname) VALUES ('Joe', 'Cool') RETURNING id;
    

The `RETURNING` clause is also very useful with `INSERT ... SELECT`.

In an `UPDATE`, the data available to `RETURNING` is the new content of the
modified row. For example:

    
    
    UPDATE products SET price = price * 1.10
      WHERE price <= 99.99
      RETURNING name, price AS new_price;
    

In a `DELETE`, the data available to `RETURNING` is the content of the deleted
row. For example:

    
    
    DELETE FROM products
      WHERE obsoletion_date = 'today'
      RETURNING *;
    

If there are triggers ([Chapter 39](triggers.html "Chapter 39. Triggers")) on
the target table, the data available to `RETURNING` is the row as modified by
the triggers. Thus, inspecting columns computed by triggers is another common
use-case for `RETURNING`.

* * *

[Prev](dml-delete.html "6.3. Deleting Data")  | [Up](dml.html "Chapter 6. Data Manipulation") |  [Next](queries.html "Chapter 7. Queries")  
---|---|---  
6.3. Deleting Data  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 7. Queries  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dml-returning.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

