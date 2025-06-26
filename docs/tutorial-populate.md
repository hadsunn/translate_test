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

Supported Versions: [Current](/docs/current/tutorial-populate.html "PostgreSQL
17 - 2.4. Populating a Table With Rows") ([17](/docs/17/tutorial-populate.html
"PostgreSQL 17 - 2.4. Populating a Table With Rows")) /
[16](/docs/16/tutorial-populate.html "PostgreSQL 16 - 2.4. Populating a Table
With Rows") / [15](/docs/15/tutorial-populate.html "PostgreSQL 15 -
2.4. Populating a Table With Rows") / [14](/docs/14/tutorial-populate.html
"PostgreSQL 14 - 2.4. Populating a Table With Rows") / [13](/docs/13/tutorial-
populate.html "PostgreSQL 13 - 2.4. Populating a Table With Rows")

Development Versions: [18](/docs/18/tutorial-populate.html "PostgreSQL 18 -
2.4. Populating a Table With Rows") / [devel](/docs/devel/tutorial-
populate.html "PostgreSQL devel - 2.4. Populating a Table With Rows")

Unsupported versions: [12](/docs/12/tutorial-populate.html "PostgreSQL 12 -
2.4. Populating a Table With Rows") / [11](/docs/11/tutorial-populate.html
"PostgreSQL 11 - 2.4. Populating a Table With Rows") / [10](/docs/10/tutorial-
populate.html "PostgreSQL 10 - 2.4. Populating a Table With Rows") /
[9.6](/docs/9.6/tutorial-populate.html "PostgreSQL 9.6 - 2.4. Populating a
Table With Rows") / [9.5](/docs/9.5/tutorial-populate.html "PostgreSQL 9.5 -
2.4. Populating a Table With Rows") / [9.4](/docs/9.4/tutorial-populate.html
"PostgreSQL 9.4 - 2.4. Populating a Table With Rows") /
[9.3](/docs/9.3/tutorial-populate.html "PostgreSQL 9.3 - 2.4. Populating a
Table With Rows") / [9.2](/docs/9.2/tutorial-populate.html "PostgreSQL 9.2 -
2.4. Populating a Table With Rows") / [9.1](/docs/9.1/tutorial-populate.html
"PostgreSQL 9.1 - 2.4. Populating a Table With Rows") /
[9.0](/docs/9.0/tutorial-populate.html "PostgreSQL 9.0 - 2.4. Populating a
Table With Rows") / [8.4](/docs/8.4/tutorial-populate.html "PostgreSQL 8.4 -
2.4. Populating a Table With Rows") / [8.3](/docs/8.3/tutorial-populate.html
"PostgreSQL 8.3 - 2.4. Populating a Table With Rows") /
[8.2](/docs/8.2/tutorial-populate.html "PostgreSQL 8.2 - 2.4. Populating a
Table With Rows") / [8.1](/docs/8.1/tutorial-populate.html "PostgreSQL 8.1 -
2.4. Populating a Table With Rows") / [8.0](/docs/8.0/tutorial-populate.html
"PostgreSQL 8.0 - 2.4. Populating a Table With Rows") /
[7.4](/docs/7.4/tutorial-populate.html "PostgreSQL 7.4 - 2.4. Populating a
Table With Rows") / [7.3](/docs/7.3/tutorial-populate.html "PostgreSQL 7.3 -
2.4. Populating a Table With Rows") / [7.2](/docs/7.2/tutorial-populate.html
"PostgreSQL 7.2 - 2.4. Populating a Table With Rows")

__

2.4. Populating a Table With Rows  
---  
[Prev](tutorial-table.html "2.3. Creating a New Table")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-select.html "2.5. Querying a Table")  
  
* * *

## 2.4. Populating a Table With Rows #

The `INSERT` statement is used to populate a table with rows:

    
    
    INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');
    

Note that all data types use rather obvious input formats. Constants that are
not simple numeric values usually must be surrounded by single quotes (`'`),
as in the example. The `date` type is actually quite flexible in what it
accepts, but for this tutorial we will stick to the unambiguous format shown
here.

The `point` type requires a coordinate pair as input, as shown here:

    
    
    INSERT INTO cities VALUES ('San Francisco', '(-194.0, 53.0)');
    

The syntax used so far requires you to remember the order of the columns. An
alternative syntax allows you to list the columns explicitly:

    
    
    INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
        VALUES ('San Francisco', 43, 57, 0.0, '1994-11-29');
    

You can list the columns in a different order if you wish or even omit some
columns, e.g., if the precipitation is unknown:

    
    
    INSERT INTO weather (date, city, temp_hi, temp_lo)
        VALUES ('1994-11-29', 'Hayward', 54, 37);
    

Many developers consider explicitly listing the columns better style than
relying on the order implicitly.

Please enter all the commands shown above so you have some data to work with
in the following sections.

You could also have used `COPY` to load large amounts of data from flat-text
files. This is usually faster because the `COPY` command is optimized for this
application while allowing less flexibility than `INSERT`. An example would
be:

    
    
    COPY weather FROM '/home/user/weather.txt';
    

where the file name for the source file must be available on the machine
running the backend process, not the client, since the backend process reads
the file directly. You can read more about the `COPY` command in [COPY](sql-
copy.html "COPY").

* * *

[Prev](tutorial-table.html "2.3. Creating a New Table")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-select.html "2.5. Querying a Table")  
---|---|---  
2.3. Creating a New Table  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.5. Querying a Table  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-populate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

