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

Supported Versions: [Current](/docs/current/ddl-default.html "PostgreSQL 17 -
5.2. Default Values") ([17](/docs/17/ddl-default.html "PostgreSQL 17 -
5.2. Default Values")) / [16](/docs/16/ddl-default.html "PostgreSQL 16 -
5.2. Default Values") / [15](/docs/15/ddl-default.html "PostgreSQL 15 -
5.2. Default Values") / [14](/docs/14/ddl-default.html "PostgreSQL 14 -
5.2. Default Values") / [13](/docs/13/ddl-default.html "PostgreSQL 13 -
5.2. Default Values")

Development Versions: [18](/docs/18/ddl-default.html "PostgreSQL 18 -
5.2. Default Values") / [devel](/docs/devel/ddl-default.html "PostgreSQL devel
- 5.2. Default Values")

Unsupported versions: [12](/docs/12/ddl-default.html "PostgreSQL 12 -
5.2. Default Values") / [11](/docs/11/ddl-default.html "PostgreSQL 11 -
5.2. Default Values") / [10](/docs/10/ddl-default.html "PostgreSQL 10 -
5.2. Default Values") / [9.6](/docs/9.6/ddl-default.html "PostgreSQL 9.6 -
5.2. Default Values") / [9.5](/docs/9.5/ddl-default.html "PostgreSQL 9.5 -
5.2. Default Values") / [9.4](/docs/9.4/ddl-default.html "PostgreSQL 9.4 -
5.2. Default Values") / [9.3](/docs/9.3/ddl-default.html "PostgreSQL 9.3 -
5.2. Default Values") / [9.2](/docs/9.2/ddl-default.html "PostgreSQL 9.2 -
5.2. Default Values") / [9.1](/docs/9.1/ddl-default.html "PostgreSQL 9.1 -
5.2. Default Values") / [9.0](/docs/9.0/ddl-default.html "PostgreSQL 9.0 -
5.2. Default Values") / [8.4](/docs/8.4/ddl-default.html "PostgreSQL 8.4 -
5.2. Default Values") / [8.3](/docs/8.3/ddl-default.html "PostgreSQL 8.3 -
5.2. Default Values") / [8.2](/docs/8.2/ddl-default.html "PostgreSQL 8.2 -
5.2. Default Values") / [8.1](/docs/8.1/ddl-default.html "PostgreSQL 8.1 -
5.2. Default Values") / [8.0](/docs/8.0/ddl-default.html "PostgreSQL 8.0 -
5.2. Default Values") / [7.4](/docs/7.4/ddl-default.html "PostgreSQL 7.4 -
5.2. Default Values")

__

5.2. Default Values  
---  
[Prev](ddl-basics.html "5.1. Table Basics")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-generated-columns.html "5.3. Generated Columns")  
  
* * *

## 5.2. Default Values #

A column can be assigned a default value. When a new row is created and no
values are specified for some of the columns, those columns will be filled
with their respective default values. A data manipulation command can also
request explicitly that a column be set to its default value, without having
to know what that value is. (Details about data manipulation commands are in
[Chapter 6](dml.html "Chapter 6. Data Manipulation").)

If no default value is declared explicitly, the default value is the null
value. This usually makes sense because a null value can be considered to
represent unknown data.

In a table definition, default values are listed after the column data type.
For example:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric **DEFAULT 9.99**
    );
    

The default value can be an expression, which will be evaluated whenever the
default value is inserted (_not_ when the table is created). A common example
is for a `timestamp` column to have a default of `CURRENT_TIMESTAMP`, so that
it gets set to the time of row insertion. Another common example is generating
a “serial number” for each row. In PostgreSQL this is typically done by
something like:

    
    
    CREATE TABLE products (
        product_no integer **DEFAULT nextval('products_product_no_seq')** ,
        ...
    );
    

where the `nextval()` function supplies successive values from a _sequence
object_ (see [Section 9.17](functions-sequence.html "9.17. Sequence
Manipulation Functions")). This arrangement is sufficiently common that
there's a special shorthand for it:

    
    
    CREATE TABLE products (
        product_no **SERIAL** ,
        ...
    );
    

The `SERIAL` shorthand is discussed further in [Section 8.1.4](datatype-
numeric.html#DATATYPE-SERIAL "8.1.4. Serial Types").

* * *

[Prev](ddl-basics.html "5.1. Table Basics")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-generated-columns.html "5.3. Generated Columns")  
---|---|---  
5.1. Table Basics  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.3. Generated Columns  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-default.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

