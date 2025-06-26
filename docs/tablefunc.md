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

Supported Versions: [Current](/docs/current/tablefunc.html "PostgreSQL 17 -
F.43. tablefunc — functions that return tables \(crosstab and others\)")
([17](/docs/17/tablefunc.html "PostgreSQL 17 - F.43. tablefunc — functions
that return tables \(crosstab and others\)")) / [16](/docs/16/tablefunc.html
"PostgreSQL 16 - F.43. tablefunc — functions that return tables \(crosstab and
others\)") / [15](/docs/15/tablefunc.html "PostgreSQL 15 - F.43. tablefunc —
functions that return tables \(crosstab and others\)") /
[14](/docs/14/tablefunc.html "PostgreSQL 14 - F.43. tablefunc — functions that
return tables \(crosstab and others\)") / [13](/docs/13/tablefunc.html
"PostgreSQL 13 - F.43. tablefunc — functions that return tables \(crosstab and
others\)")

Development Versions: [18](/docs/18/tablefunc.html "PostgreSQL 18 -
F.43. tablefunc — functions that return tables \(crosstab and others\)") /
[devel](/docs/devel/tablefunc.html "PostgreSQL devel - F.43. tablefunc —
functions that return tables \(crosstab and others\)")

Unsupported versions: [12](/docs/12/tablefunc.html "PostgreSQL 12 -
F.43. tablefunc — functions that return tables \(crosstab and others\)") /
[11](/docs/11/tablefunc.html "PostgreSQL 11 - F.43. tablefunc — functions that
return tables \(crosstab and others\)") / [10](/docs/10/tablefunc.html
"PostgreSQL 10 - F.43. tablefunc — functions that return tables \(crosstab and
others\)") / [9.6](/docs/9.6/tablefunc.html "PostgreSQL 9.6 - F.43. tablefunc
— functions that return tables \(crosstab and others\)") /
[9.5](/docs/9.5/tablefunc.html "PostgreSQL 9.5 - F.43. tablefunc — functions
that return tables \(crosstab and others\)") / [9.4](/docs/9.4/tablefunc.html
"PostgreSQL 9.4 - F.43. tablefunc — functions that return tables \(crosstab
and others\)") / [9.3](/docs/9.3/tablefunc.html "PostgreSQL 9.3 -
F.43. tablefunc — functions that return tables \(crosstab and others\)") /
[9.2](/docs/9.2/tablefunc.html "PostgreSQL 9.2 - F.43. tablefunc — functions
that return tables \(crosstab and others\)") / [9.1](/docs/9.1/tablefunc.html
"PostgreSQL 9.1 - F.43. tablefunc — functions that return tables \(crosstab
and others\)") / [9.0](/docs/9.0/tablefunc.html "PostgreSQL 9.0 -
F.43. tablefunc — functions that return tables \(crosstab and others\)") /
[8.4](/docs/8.4/tablefunc.html "PostgreSQL 8.4 - F.43. tablefunc — functions
that return tables \(crosstab and others\)") / [8.3](/docs/8.3/tablefunc.html
"PostgreSQL 8.3 - F.43. tablefunc — functions that return tables \(crosstab
and others\)")

__

F.43. tablefunc — functions that return tables (`crosstab` and others)  
---  
[Prev](sslinfo.html "F.42. sslinfo — obtain client SSL information")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tcn.html "F.44. tcn — a trigger function to notify listeners of changes to table content")  
  
* * *

## F.43. tablefunc — functions that return tables (`crosstab` and others) #

[F.43.1. Functions Provided](tablefunc.html#TABLEFUNC-FUNCTIONS-SECT)

[F.43.2. Author](tablefunc.html#TABLEFUNC-AUTHOR)

The `tablefunc` module includes various functions that return tables (that is,
multiple rows). These functions are useful both in their own right and as
examples of how to write C functions that return multiple rows.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.43.1. Functions Provided #

[Table F.32](tablefunc.html#TABLEFUNC-FUNCTIONS "Table F.32. tablefunc
Functions") summarizes the functions provided by the `tablefunc` module.

**Table  F.32. `tablefunc` Functions**

Function Description  
---  
`normal_rand` ( _`numvals`_ `integer`, _`mean`_ `float8`, _`stddev`_ `float8`
) → `setof float8` Produces a set of normally distributed random values.  
`crosstab` ( _`sql`_ `text` ) → `setof record` Produces a “pivot table”
containing row names plus _`N`_ value columns, where _`N`_ is determined by
the row type specified in the calling query.  
`crosstab _`N`_` ( _`sql`_ `text` ) → `setof table_crosstab__`N`_` Produces a
“pivot table” containing row names plus _`N`_ value columns. `crosstab2`,
`crosstab3`, and `crosstab4` are predefined, but you can create additional
`crosstab _`N`_` functions as described below.  
`crosstab` ( _`source_sql`_ `text`, _`category_sql`_ `text` ) → `setof record`
Produces a “pivot table” with the value columns specified by a second query.  
`crosstab` ( _`sql`_ `text`, _`N`_ `integer` ) → `setof record` Obsolete
version of `crosstab(text)`. The parameter _`N`_ is now ignored, since the
number of value columns is always determined by the calling query.  
`connectby` ( _`relname`_ `text`, _`keyid_fld`_ `text`, _`parent_keyid_fld`_
`text` [, _`orderby_fld`_ `text` ], _`start_with`_ `text`, _`max_depth`_
`integer` [, _`branch_delim`_ `text` ] ) → `setof record` Produces a
representation of a hierarchical tree structure.  
  
  

#### F.43.1.1. `normal_rand` #

    
    
    normal_rand(int numvals, float8 mean, float8 stddev) returns setof float8
    

`normal_rand` produces a set of normally distributed random values (Gaussian
distribution).

_`numvals`_ is the number of values to be returned from the function. _`mean`_
is the mean of the normal distribution of values and _`stddev`_ is the
standard deviation of the normal distribution of values.

For example, this call requests 1000 values with a mean of 5 and a standard
deviation of 3:

    
    
    test=# SELECT * FROM normal_rand(1000, 5, 3);
         normal_rand
    ----------------------
         1.56556322244898
         9.10040991424657
         5.36957140345079
       -0.369151492880995
        0.283600703686639
           .
           .
           .
         4.82992125404908
         9.71308014517282
         2.49639286969028
    (1000 rows)
    

#### F.43.1.2. `crosstab(text)` #

    
    
    crosstab(text sql)
    crosstab(text sql, int N)
    

The `crosstab` function is used to produce “pivot” displays, wherein data is
listed across the page rather than down. For example, we might have data like

    
    
    row1    val11
    row1    val12
    row1    val13
    ...
    row2    val21
    row2    val22
    row2    val23
    ...
    

which we wish to display like

    
    
    row1    val11   val12   val13   ...
    row2    val21   val22   val23   ...
    ...
    

The `crosstab` function takes a text parameter that is an SQL query producing
raw data formatted in the first way, and produces a table formatted in the
second way.

The _`sql`_ parameter is an SQL statement that produces the source set of
data. This statement must return one `row_name` column, one `category` column,
and one `value` column. _`N`_ is an obsolete parameter, ignored if supplied
(formerly this had to match the number of output value columns, but now that
is determined by the calling query).

For example, the provided query might produce a set something like:

    
    
     row_name    cat    value
    ----------+-------+-------
      row1      cat1    val1
      row1      cat2    val2
      row1      cat3    val3
      row1      cat4    val4
      row2      cat1    val5
      row2      cat2    val6
      row2      cat3    val7
      row2      cat4    val8
    

The `crosstab` function is declared to return `setof record`, so the actual
names and types of the output columns must be defined in the `FROM` clause of
the calling `SELECT` statement, for example:

    
    
    SELECT * FROM crosstab('...') AS ct(row_name text, category_1 text, category_2 text);
    

This example produces a set something like:

    
    
               <== value  columns  ==>
     row_name   category_1   category_2
    ----------+------------+------------
      row1        val1         val2
      row2        val5         val6
    

The `FROM` clause must define the output as one `row_name` column (of the same
data type as the first result column of the SQL query) followed by N `value`
columns (all of the same data type as the third result column of the SQL
query). You can set up as many output value columns as you wish. The names of
the output columns are up to you.

The `crosstab` function produces one output row for each consecutive group of
input rows with the same `row_name` value. It fills the output `value`
columns, left to right, with the `value` fields from these rows. If there are
fewer rows in a group than there are output `value` columns, the extra output
columns are filled with nulls; if there are more rows, the extra input rows
are skipped.

In practice the SQL query should always specify `ORDER BY 1,2` to ensure that
the input rows are properly ordered, that is, values with the same `row_name`
are brought together and correctly ordered within the row. Notice that
`crosstab` itself does not pay any attention to the second column of the query
result; it's just there to be ordered by, to control the order in which the
third-column values appear across the page.

Here is a complete example:

    
    
    CREATE TABLE ct(id SERIAL, rowid TEXT, attribute TEXT, value TEXT);
    INSERT INTO ct(rowid, attribute, value) VALUES('test1','att1','val1');
    INSERT INTO ct(rowid, attribute, value) VALUES('test1','att2','val2');
    INSERT INTO ct(rowid, attribute, value) VALUES('test1','att3','val3');
    INSERT INTO ct(rowid, attribute, value) VALUES('test1','att4','val4');
    INSERT INTO ct(rowid, attribute, value) VALUES('test2','att1','val5');
    INSERT INTO ct(rowid, attribute, value) VALUES('test2','att2','val6');
    INSERT INTO ct(rowid, attribute, value) VALUES('test2','att3','val7');
    INSERT INTO ct(rowid, attribute, value) VALUES('test2','att4','val8');
    
    SELECT *
    FROM crosstab(
      'select rowid, attribute, value
       from ct
       where attribute = ''att2'' or attribute = ''att3''
       order by 1,2')
    AS ct(row_name text, category_1 text, category_2 text, category_3 text);
    
     row_name | category_1 | category_2 | category_3
    ----------+------------+------------+------------
     test1    | val2       | val3       |
     test2    | val6       | val7       |
    (2 rows)
    

You can avoid always having to write out a `FROM` clause to define the output
columns, by setting up a custom crosstab function that has the desired output
row type wired into its definition. This is described in the next section.
Another possibility is to embed the required `FROM` clause in a view
definition.

### Note

See also the `[\crosstabview](app-psql.html#APP-PSQL-META-COMMANDS-
CROSSTABVIEW)` command in psql, which provides functionality similar to
`crosstab()`.

#### F.43.1.3. `crosstab _`N`_(text)` #

    
    
    crosstab _N_(text sql)
    

The `crosstab _`N`_` functions are examples of how to set up custom wrappers
for the general `crosstab` function, so that you need not write out column
names and types in the calling `SELECT` query. The `tablefunc` module includes
`crosstab2`, `crosstab3`, and `crosstab4`, whose output row types are defined
as

    
    
    CREATE TYPE tablefunc_crosstab_N AS (
        row_name TEXT,
        category_1 TEXT,
        category_2 TEXT,
            .
            .
            .
        category_N TEXT
    );
    

Thus, these functions can be used directly when the input query produces
`row_name` and `value` columns of type `text`, and you want 2, 3, or 4 output
values columns. In all other ways they behave exactly as described above for
the general `crosstab` function.

For instance, the example given in the previous section would also work as

    
    
    SELECT *
    FROM crosstab3(
      'select rowid, attribute, value
       from ct
       where attribute = ''att2'' or attribute = ''att3''
       order by 1,2');
    

These functions are provided mostly for illustration purposes. You can create
your own return types and functions based on the underlying `crosstab()`
function. There are two ways to do it:

  * Create a composite type describing the desired output columns, similar to the examples in `contrib/tablefunc/tablefunc--1.0.sql`. Then define a unique function name accepting one `text` parameter and returning `setof your_type_name`, but linking to the same underlying `crosstab` C function. For example, if your source data produces row names that are `text`, and values that are `float8`, and you want 5 value columns:
        
        CREATE TYPE my_crosstab_float8_5_cols AS (
            my_row_name text,
            my_category_1 float8,
            my_category_2 float8,
            my_category_3 float8,
            my_category_4 float8,
            my_category_5 float8
        );
        
        CREATE OR REPLACE FUNCTION crosstab_float8_5_cols(text)
            RETURNS setof my_crosstab_float8_5_cols
            AS '$libdir/tablefunc','crosstab' LANGUAGE C STABLE STRICT;
        

  * Use `OUT` parameters to define the return type implicitly. The same example could also be done this way:
        
        CREATE OR REPLACE FUNCTION crosstab_float8_5_cols(
            IN text,
            OUT my_row_name text,
            OUT my_category_1 float8,
            OUT my_category_2 float8,
            OUT my_category_3 float8,
            OUT my_category_4 float8,
            OUT my_category_5 float8)
          RETURNS setof record
          AS '$libdir/tablefunc','crosstab' LANGUAGE C STABLE STRICT;
        

#### F.43.1.4. `crosstab(text, text)` #

    
    
    crosstab(text source_sql, text category_sql)
    

The main limitation of the single-parameter form of `crosstab` is that it
treats all values in a group alike, inserting each value into the first
available column. If you want the value columns to correspond to specific
categories of data, and some groups might not have data for some of the
categories, that doesn't work well. The two-parameter form of `crosstab`
handles this case by providing an explicit list of the categories
corresponding to the output columns.

_`source_sql`_ is an SQL statement that produces the source set of data. This
statement must return one `row_name` column, one `category` column, and one
`value` column. It may also have one or more “extra” columns. The `row_name`
column must be first. The `category` and `value` columns must be the last two
columns, in that order. Any columns between `row_name` and `category` are
treated as “extra”. The “extra” columns are expected to be the same for all
rows with the same `row_name` value.

For example, _`source_sql`_ might produce a set something like:

    
    
    SELECT row_name, extra_col, cat, value FROM foo ORDER BY 1;
    
     row_name    extra_col   cat    value
    ----------+------------+-----+---------
      row1         extra1    cat1    val1
      row1         extra1    cat2    val2
      row1         extra1    cat4    val4
      row2         extra2    cat1    val5
      row2         extra2    cat2    val6
      row2         extra2    cat3    val7
      row2         extra2    cat4    val8
    

_`category_sql`_ is an SQL statement that produces the set of categories. This
statement must return only one column. It must produce at least one row, or an
error will be generated. Also, it must not produce duplicate values, or an
error will be generated. _`category_sql`_ might be something like:

    
    
    SELECT DISTINCT cat FROM foo ORDER BY 1;
        cat
      -------
        cat1
        cat2
        cat3
        cat4
    

The `crosstab` function is declared to return `setof record`, so the actual
names and types of the output columns must be defined in the `FROM` clause of
the calling `SELECT` statement, for example:

    
    
    SELECT * FROM crosstab('...', '...')
        AS ct(row_name text, extra text, cat1 text, cat2 text, cat3 text, cat4 text);
    

This will produce a result something like:

    
    
                      <==  value  columns   ==>
    row_name   extra   cat1   cat2   cat3   cat4
    ---------+-------+------+------+------+------
      row1     extra1  val1   val2          val4
      row2     extra2  val5   val6   val7   val8
    

The `FROM` clause must define the proper number of output columns of the
proper data types. If there are _`N`_ columns in the _`source_sql`_ query's
result, the first _`N`_ -2 of them must match up with the first _`N`_ -2
output columns. The remaining output columns must have the type of the last
column of the _`source_sql`_ query's result, and there must be exactly as many
of them as there are rows in the _`category_sql`_ query's result.

The `crosstab` function produces one output row for each consecutive group of
input rows with the same `row_name` value. The output `row_name` column, plus
any “extra” columns, are copied from the first row of the group. The output
`value` columns are filled with the `value` fields from rows having matching
`category` values. If a row's `category` does not match any output of the
_`category_sql`_ query, its `value` is ignored. Output columns whose matching
category is not present in any input row of the group are filled with nulls.

In practice the _`source_sql`_ query should always specify `ORDER BY 1` to
ensure that values with the same `row_name` are brought together. However,
ordering of the categories within a group is not important. Also, it is
essential to be sure that the order of the _`category_sql`_ query's output
matches the specified output column order.

Here are two complete examples:

    
    
    create table sales(year int, month int, qty int);
    insert into sales values(2007, 1, 1000);
    insert into sales values(2007, 2, 1500);
    insert into sales values(2007, 7, 500);
    insert into sales values(2007, 11, 1500);
    insert into sales values(2007, 12, 2000);
    insert into sales values(2008, 1, 1000);
    
    select * from crosstab(
      'select year, month, qty from sales order by 1',
      'select m from generate_series(1,12) m'
    ) as (
      year int,
      "Jan" int,
      "Feb" int,
      "Mar" int,
      "Apr" int,
      "May" int,
      "Jun" int,
      "Jul" int,
      "Aug" int,
      "Sep" int,
      "Oct" int,
      "Nov" int,
      "Dec" int
    );
     year | Jan  | Feb  | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov  | Dec
    ------+------+------+-----+-----+-----+-----+-----+-----+-----+-----+------+------
     2007 | 1000 | 1500 |     |     |     |     | 500 |     |     |     | 1500 | 2000
     2008 | 1000 |      |     |     |     |     |     |     |     |     |      |
    (2 rows)
    
    
    
    CREATE TABLE cth(rowid text, rowdt timestamp, attribute text, val text);
    INSERT INTO cth VALUES('test1','01 March 2003','temperature','42');
    INSERT INTO cth VALUES('test1','01 March 2003','test_result','PASS');
    INSERT INTO cth VALUES('test1','01 March 2003','volts','2.6987');
    INSERT INTO cth VALUES('test2','02 March 2003','temperature','53');
    INSERT INTO cth VALUES('test2','02 March 2003','test_result','FAIL');
    INSERT INTO cth VALUES('test2','02 March 2003','test_startdate','01 March 2003');
    INSERT INTO cth VALUES('test2','02 March 2003','volts','3.1234');
    
    SELECT * FROM crosstab
    (
      'SELECT rowid, rowdt, attribute, val FROM cth ORDER BY 1',
      'SELECT DISTINCT attribute FROM cth ORDER BY 1'
    )
    AS
    (
           rowid text,
           rowdt timestamp,
           temperature int4,
           test_result text,
           test_startdate timestamp,
           volts float8
    );
     rowid |          rowdt           | temperature | test_result |      test_startdate      | volts
    -------+--------------------------+-------------+-------------+--------------------------+--------
     test1 | Sat Mar 01 00:00:00 2003 |          42 | PASS        |                          | 2.6987
     test2 | Sun Mar 02 00:00:00 2003 |          53 | FAIL        | Sat Mar 01 00:00:00 2003 | 3.1234
    (2 rows)
    

You can create predefined functions to avoid having to write out the result
column names and types in each query. See the examples in the previous
section. The underlying C function for this form of `crosstab` is named
`crosstab_hash`.

#### F.43.1.5. `connectby` #

    
    
    connectby(text relname, text keyid_fld, text parent_keyid_fld
              [, text orderby_fld ], text start_with, int max_depth
              [, text branch_delim ])
    

The `connectby` function produces a display of hierarchical data that is
stored in a table. The table must have a key field that uniquely identifies
rows, and a parent-key field that references the parent (if any) of each row.
`connectby` can display the sub-tree descending from any row.

[Table F.33](tablefunc.html#TABLEFUNC-CONNECTBY-PARAMETERS
"Table F.33. connectby Parameters") explains the parameters.

**Table  F.33. `connectby` Parameters**

Parameter | Description  
---|---  
_`relname`_ | Name of the source relation  
_`keyid_fld`_ | Name of the key field  
_`parent_keyid_fld`_ | Name of the parent-key field  
_`orderby_fld`_ | Name of the field to order siblings by (optional)  
_`start_with`_ | Key value of the row to start at  
_`max_depth`_ | Maximum depth to descend to, or zero for unlimited depth  
_`branch_delim`_ | String to separate keys with in branch output (optional)  
  
  

The key and parent-key fields can be any data type, but they must be the same
type. Note that the _`start_with`_ value must be entered as a text string,
regardless of the type of the key field.

The `connectby` function is declared to return `setof record`, so the actual
names and types of the output columns must be defined in the `FROM` clause of
the calling `SELECT` statement, for example:

    
    
    SELECT * FROM connectby('connectby_tree', 'keyid', 'parent_keyid', 'pos', 'row2', 0, '~')
        AS t(keyid text, parent_keyid text, level int, branch text, pos int);
    

The first two output columns are used for the current row's key and its parent
row's key; they must match the type of the table's key field. The third output
column is the depth in the tree and must be of type `integer`. If a
_`branch_delim`_ parameter was given, the next output column is the branch
display and must be of type `text`. Finally, if an _`orderby_fld`_ parameter
was given, the last output column is a serial number, and must be of type
`integer`.

The “branch” output column shows the path of keys taken to reach the current
row. The keys are separated by the specified _`branch_delim`_ string. If no
branch display is wanted, omit both the _`branch_delim`_ parameter and the
branch column in the output column list.

If the ordering of siblings of the same parent is important, include the
_`orderby_fld`_ parameter to specify which field to order siblings by. This
field can be of any sortable data type. The output column list must include a
final integer serial-number column, if and only if _`orderby_fld`_ is
specified.

The parameters representing table and field names are copied as-is into the
SQL queries that `connectby` generates internally. Therefore, include double
quotes if the names are mixed-case or contain special characters. You may also
need to schema-qualify the table name.

In large tables, performance will be poor unless there is an index on the
parent-key field.

It is important that the _`branch_delim`_ string not appear in any key values,
else `connectby` may incorrectly report an infinite-recursion error. Note that
if _`branch_delim`_ is not provided, a default value of `~` is used for
recursion detection purposes.

Here is an example:

    
    
    CREATE TABLE connectby_tree(keyid text, parent_keyid text, pos int);
    
    INSERT INTO connectby_tree VALUES('row1',NULL, 0);
    INSERT INTO connectby_tree VALUES('row2','row1', 0);
    INSERT INTO connectby_tree VALUES('row3','row1', 0);
    INSERT INTO connectby_tree VALUES('row4','row2', 1);
    INSERT INTO connectby_tree VALUES('row5','row2', 0);
    INSERT INTO connectby_tree VALUES('row6','row4', 0);
    INSERT INTO connectby_tree VALUES('row7','row3', 0);
    INSERT INTO connectby_tree VALUES('row8','row6', 0);
    INSERT INTO connectby_tree VALUES('row9','row5', 0);
    
    -- with branch, without orderby_fld (order of results is not guaranteed)
    SELECT * FROM connectby('connectby_tree', 'keyid', 'parent_keyid', 'row2', 0, '~')
     AS t(keyid text, parent_keyid text, level int, branch text);
     keyid | parent_keyid | level |       branch
    -------+--------------+-------+---------------------
     row2  |              |     0 | row2
     row4  | row2         |     1 | row2~row4
     row6  | row4         |     2 | row2~row4~row6
     row8  | row6         |     3 | row2~row4~row6~row8
     row5  | row2         |     1 | row2~row5
     row9  | row5         |     2 | row2~row5~row9
    (6 rows)
    
    -- without branch, without orderby_fld (order of results is not guaranteed)
    SELECT * FROM connectby('connectby_tree', 'keyid', 'parent_keyid', 'row2', 0)
     AS t(keyid text, parent_keyid text, level int);
     keyid | parent_keyid | level
    -------+--------------+-------
     row2  |              |     0
     row4  | row2         |     1
     row6  | row4         |     2
     row8  | row6         |     3
     row5  | row2         |     1
     row9  | row5         |     2
    (6 rows)
    
    -- with branch, with orderby_fld (notice that row5 comes before row4)
    SELECT * FROM connectby('connectby_tree', 'keyid', 'parent_keyid', 'pos', 'row2', 0, '~')
     AS t(keyid text, parent_keyid text, level int, branch text, pos int);
     keyid | parent_keyid | level |       branch        | pos
    -------+--------------+-------+---------------------+-----
     row2  |              |     0 | row2                |   1
     row5  | row2         |     1 | row2~row5           |   2
     row9  | row5         |     2 | row2~row5~row9      |   3
     row4  | row2         |     1 | row2~row4           |   4
     row6  | row4         |     2 | row2~row4~row6      |   5
     row8  | row6         |     3 | row2~row4~row6~row8 |   6
    (6 rows)
    
    -- without branch, with orderby_fld (notice that row5 comes before row4)
    SELECT * FROM connectby('connectby_tree', 'keyid', 'parent_keyid', 'pos', 'row2', 0)
     AS t(keyid text, parent_keyid text, level int, pos int);
     keyid | parent_keyid | level | pos
    -------+--------------+-------+-----
     row2  |              |     0 |   1
     row5  | row2         |     1 |   2
     row9  | row5         |     2 |   3
     row4  | row2         |     1 |   4
     row6  | row4         |     2 |   5
     row8  | row6         |     3 |   6
    (6 rows)
    

### F.43.2. Author #

Joe Conway

* * *

[Prev](sslinfo.html "F.42. sslinfo — obtain client SSL information")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](tcn.html "F.44. tcn — a trigger function to notify listeners of changes to table content")  
---|---|---  
F.42. sslinfo — obtain client SSL information  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.44. tcn — a trigger function to notify listeners of changes to table content  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tablefunc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

