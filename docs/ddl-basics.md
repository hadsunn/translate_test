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

Supported Versions: [Current](/docs/current/ddl-basics.html "PostgreSQL 17 -
5.1. Table Basics") ([17](/docs/17/ddl-basics.html "PostgreSQL 17 - 5.1. Table
Basics")) / [16](/docs/16/ddl-basics.html "PostgreSQL 16 - 5.1. Table Basics")
/ [15](/docs/15/ddl-basics.html "PostgreSQL 15 - 5.1. Table Basics") /
[14](/docs/14/ddl-basics.html "PostgreSQL 14 - 5.1. Table Basics") /
[13](/docs/13/ddl-basics.html "PostgreSQL 13 - 5.1. Table Basics")

Development Versions: [18](/docs/18/ddl-basics.html "PostgreSQL 18 -
5.1. Table Basics") / [devel](/docs/devel/ddl-basics.html "PostgreSQL devel -
5.1. Table Basics")

Unsupported versions: [12](/docs/12/ddl-basics.html "PostgreSQL 12 -
5.1. Table Basics") / [11](/docs/11/ddl-basics.html "PostgreSQL 11 -
5.1. Table Basics") / [10](/docs/10/ddl-basics.html "PostgreSQL 10 -
5.1. Table Basics") / [9.6](/docs/9.6/ddl-basics.html "PostgreSQL 9.6 -
5.1. Table Basics") / [9.5](/docs/9.5/ddl-basics.html "PostgreSQL 9.5 -
5.1. Table Basics") / [9.4](/docs/9.4/ddl-basics.html "PostgreSQL 9.4 -
5.1. Table Basics") / [9.3](/docs/9.3/ddl-basics.html "PostgreSQL 9.3 -
5.1. Table Basics") / [9.2](/docs/9.2/ddl-basics.html "PostgreSQL 9.2 -
5.1. Table Basics") / [9.1](/docs/9.1/ddl-basics.html "PostgreSQL 9.1 -
5.1. Table Basics") / [9.0](/docs/9.0/ddl-basics.html "PostgreSQL 9.0 -
5.1. Table Basics") / [8.4](/docs/8.4/ddl-basics.html "PostgreSQL 8.4 -
5.1. Table Basics") / [8.3](/docs/8.3/ddl-basics.html "PostgreSQL 8.3 -
5.1. Table Basics") / [8.2](/docs/8.2/ddl-basics.html "PostgreSQL 8.2 -
5.1. Table Basics")

__

5.1. Table Basics  
---  
[Prev](ddl.html "Chapter 5. Data Definition")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-default.html "5.2. Default Values")  
  
* * *

## 5.1. Table Basics #

A table in a relational database is much like a table on paper: It consists of
rows and columns. The number and order of the columns is fixed, and each
column has a name. The number of rows is variable — it reflects how much data
is stored at a given moment. SQL does not make any guarantees about the order
of the rows in a table. When a table is read, the rows will appear in an
unspecified order, unless sorting is explicitly requested. This is covered in
[Chapter 7](queries.html "Chapter 7. Queries"). Furthermore, SQL does not
assign unique identifiers to rows, so it is possible to have several
completely identical rows in a table. This is a consequence of the
mathematical model that underlies SQL but is usually not desirable. Later in
this chapter we will see how to deal with this issue.

Each column has a data type. The data type constrains the set of possible
values that can be assigned to a column and assigns semantics to the data
stored in the column so that it can be used for computations. For instance, a
column declared to be of a numerical type will not accept arbitrary text
strings, and the data stored in such a column can be used for mathematical
computations. By contrast, a column declared to be of a character string type
will accept almost any kind of data but it does not lend itself to
mathematical calculations, although other operations such as string
concatenation are available.

PostgreSQL includes a sizable set of built-in data types that fit many
applications. Users can also define their own data types. Most built-in data
types have obvious names and semantics, so we defer a detailed explanation to
[Chapter 8](datatype.html "Chapter 8. Data Types"). Some of the frequently
used data types are `integer` for whole numbers, `numeric` for possibly
fractional numbers, `text` for character strings, `date` for dates, `time` for
time-of-day values, and `timestamp` for values containing both date and time.

To create a table, you use the aptly named [CREATE TABLE](sql-createtable.html
"CREATE TABLE") command. In this command you specify at least a name for the
new table, the names of the columns and the data type of each column. For
example:

    
    
    CREATE TABLE my_first_table (
        first_column text,
        second_column integer
    );
    

This creates a table named `my_first_table` with two columns. The first column
is named `first_column` and has a data type of `text`; the second column has
the name `second_column` and the type `integer`. The table and column names
follow the identifier syntax explained in [Section 4.1.1](sql-syntax-
lexical.html#SQL-SYNTAX-IDENTIFIERS "4.1.1. Identifiers and Key Words"). The
type names are usually also identifiers, but there are some exceptions. Note
that the column list is comma-separated and surrounded by parentheses.

Of course, the previous example was heavily contrived. Normally, you would
give names to your tables and columns that convey what kind of data they
store. So let's look at a more realistic example:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric
    );
    

(The `numeric` type can store fractional components, as would be typical of
monetary amounts.)

### Tip

When you create many interrelated tables it is wise to choose a consistent
naming pattern for the tables and columns. For instance, there is a choice of
using singular or plural nouns for table names, both of which are favored by
some theorist or other.

There is a limit on how many columns a table can contain. Depending on the
column types, it is between 250 and 1600. However, defining a table with
anywhere near this many columns is highly unusual and often a questionable
design.

If you no longer need a table, you can remove it using the [DROP TABLE](sql-
droptable.html "DROP TABLE") command. For example:

    
    
    DROP TABLE my_first_table;
    DROP TABLE products;
    

Attempting to drop a table that does not exist is an error. Nevertheless, it
is common in SQL script files to unconditionally try to drop each table before
creating it, ignoring any error messages, so that the script works whether or
not the table exists. (If you like, you can use the `DROP TABLE IF EXISTS`
variant to avoid the error messages, but this is not standard SQL.)

If you need to modify a table that already exists, see [Section 5.6](ddl-
alter.html "5.6. Modifying Tables") later in this chapter.

With the tools discussed so far you can create fully functional tables. The
remainder of this chapter is concerned with adding features to the table
definition to ensure data integrity, security, or convenience. If you are
eager to fill your tables with data now you can skip ahead to [Chapter
6](dml.html "Chapter 6. Data Manipulation") and read the rest of this chapter
later.

* * *

[Prev](ddl.html "Chapter 5. Data Definition")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-default.html "5.2. Default Values")  
---|---|---  
Chapter 5. Data Definition  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.2. Default Values  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-basics.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

