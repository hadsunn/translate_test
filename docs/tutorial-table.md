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

Supported Versions: [Current](/docs/current/tutorial-table.html "PostgreSQL 17
- 2.3. Creating a New Table") ([17](/docs/17/tutorial-table.html "PostgreSQL
17 - 2.3. Creating a New Table")) / [16](/docs/16/tutorial-table.html
"PostgreSQL 16 - 2.3. Creating a New Table") / [15](/docs/15/tutorial-
table.html "PostgreSQL 15 - 2.3. Creating a New Table") /
[14](/docs/14/tutorial-table.html "PostgreSQL 14 - 2.3. Creating a New Table")
/ [13](/docs/13/tutorial-table.html "PostgreSQL 13 - 2.3. Creating a New
Table")

Development Versions: [18](/docs/18/tutorial-table.html "PostgreSQL 18 -
2.3. Creating a New Table") / [devel](/docs/devel/tutorial-table.html
"PostgreSQL devel - 2.3. Creating a New Table")

Unsupported versions: [12](/docs/12/tutorial-table.html "PostgreSQL 12 -
2.3. Creating a New Table") / [11](/docs/11/tutorial-table.html "PostgreSQL 11
- 2.3. Creating a New Table") / [10](/docs/10/tutorial-table.html "PostgreSQL
10 - 2.3. Creating a New Table") / [9.6](/docs/9.6/tutorial-table.html
"PostgreSQL 9.6 - 2.3. Creating a New Table") / [9.5](/docs/9.5/tutorial-
table.html "PostgreSQL 9.5 - 2.3. Creating a New Table") /
[9.4](/docs/9.4/tutorial-table.html "PostgreSQL 9.4 - 2.3. Creating a New
Table") / [9.3](/docs/9.3/tutorial-table.html "PostgreSQL 9.3 - 2.3. Creating
a New Table") / [9.2](/docs/9.2/tutorial-table.html "PostgreSQL 9.2 -
2.3. Creating a New Table") / [9.1](/docs/9.1/tutorial-table.html "PostgreSQL
9.1 - 2.3. Creating a New Table") / [9.0](/docs/9.0/tutorial-table.html
"PostgreSQL 9.0 - 2.3. Creating a New Table") / [8.4](/docs/8.4/tutorial-
table.html "PostgreSQL 8.4 - 2.3. Creating a New Table") /
[8.3](/docs/8.3/tutorial-table.html "PostgreSQL 8.3 - 2.3. Creating a New
Table") / [8.2](/docs/8.2/tutorial-table.html "PostgreSQL 8.2 - 2.3. Creating
a New Table") / [8.1](/docs/8.1/tutorial-table.html "PostgreSQL 8.1 -
2.3. Creating a New Table") / [8.0](/docs/8.0/tutorial-table.html "PostgreSQL
8.0 - 2.3. Creating a New Table") / [7.4](/docs/7.4/tutorial-table.html
"PostgreSQL 7.4 - 2.3. Creating a New Table") / [7.3](/docs/7.3/tutorial-
table.html "PostgreSQL 7.3 - 2.3. Creating a New Table") /
[7.2](/docs/7.2/tutorial-table.html "PostgreSQL 7.2 - 2.3. Creating a New
Table")

__

2.3. Creating a New Table  
---  
[Prev](tutorial-concepts.html "2.2. Concepts")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-populate.html "2.4. Populating a Table With Rows")  
  
* * *

## 2.3. Creating a New Table #

You can create a new table by specifying the table name, along with all column
names and their types:

    
    
    CREATE TABLE weather (
        city            varchar(80),
        temp_lo         int,           -- low temperature
        temp_hi         int,           -- high temperature
        prcp            real,          -- precipitation
        date            date
    );
    

You can enter this into `psql` with the line breaks. `psql` will recognize
that the command is not terminated until the semicolon.

White space (i.e., spaces, tabs, and newlines) can be used freely in SQL
commands. That means you can type the command aligned differently than above,
or even all on one line. Two dashes (“`--`”) introduce comments. Whatever
follows them is ignored up to the end of the line. SQL is case-insensitive
about key words and identifiers, except when identifiers are double-quoted to
preserve the case (not done above).

`varchar(80)` specifies a data type that can store arbitrary character strings
up to 80 characters in length. `int` is the normal integer type. `real` is a
type for storing single precision floating-point numbers. `date` should be
self-explanatory. (Yes, the column of type `date` is also named `date`. This
might be convenient or confusing — you choose.)

PostgreSQL supports the standard SQL types `int`, `smallint`, `real`, `double
precision`, `char(_`N`_)`, `varchar(_`N`_)`, `date`, `time`, `timestamp`, and
`interval`, as well as other types of general utility and a rich set of
geometric types. PostgreSQL can be customized with an arbitrary number of
user-defined data types. Consequently, type names are not key words in the
syntax, except where required to support special cases in the SQL standard.

The second example will store cities and their associated geographical
location:

    
    
    CREATE TABLE cities (
        name            varchar(80),
        location        point
    );
    

The `point` type is an example of a PostgreSQL-specific data type.

Finally, it should be mentioned that if you don't need a table any longer or
want to recreate it differently you can remove it using the following command:

    
    
    DROP TABLE _tablename_ ;
    

* * *

[Prev](tutorial-concepts.html "2.2. Concepts")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-populate.html "2.4. Populating a Table With Rows")  
---|---|---  
2.2. Concepts  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.4. Populating a Table With Rows  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-table.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

