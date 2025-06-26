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

Supported Versions: [Current](/docs/current/queries-table-expressions.html
"PostgreSQL 17 - 7.2. Table Expressions") ([17](/docs/17/queries-table-
expressions.html "PostgreSQL 17 - 7.2. Table Expressions")) /
[16](/docs/16/queries-table-expressions.html "PostgreSQL 16 - 7.2. Table
Expressions") / [15](/docs/15/queries-table-expressions.html "PostgreSQL 15 -
7.2. Table Expressions") / [14](/docs/14/queries-table-expressions.html
"PostgreSQL 14 - 7.2. Table Expressions") / [13](/docs/13/queries-table-
expressions.html "PostgreSQL 13 - 7.2. Table Expressions")

Development Versions: [18](/docs/18/queries-table-expressions.html "PostgreSQL
18 - 7.2. Table Expressions") / [devel](/docs/devel/queries-table-
expressions.html "PostgreSQL devel - 7.2. Table Expressions")

Unsupported versions: [12](/docs/12/queries-table-expressions.html "PostgreSQL
12 - 7.2. Table Expressions") / [11](/docs/11/queries-table-expressions.html
"PostgreSQL 11 - 7.2. Table Expressions") / [10](/docs/10/queries-table-
expressions.html "PostgreSQL 10 - 7.2. Table Expressions") /
[9.6](/docs/9.6/queries-table-expressions.html "PostgreSQL 9.6 - 7.2. Table
Expressions") / [9.5](/docs/9.5/queries-table-expressions.html "PostgreSQL 9.5
- 7.2. Table Expressions") / [9.4](/docs/9.4/queries-table-expressions.html
"PostgreSQL 9.4 - 7.2. Table Expressions") / [9.3](/docs/9.3/queries-table-
expressions.html "PostgreSQL 9.3 - 7.2. Table Expressions") /
[9.2](/docs/9.2/queries-table-expressions.html "PostgreSQL 9.2 - 7.2. Table
Expressions") / [9.1](/docs/9.1/queries-table-expressions.html "PostgreSQL 9.1
- 7.2. Table Expressions") / [9.0](/docs/9.0/queries-table-expressions.html
"PostgreSQL 9.0 - 7.2. Table Expressions") / [8.4](/docs/8.4/queries-table-
expressions.html "PostgreSQL 8.4 - 7.2. Table Expressions") /
[8.3](/docs/8.3/queries-table-expressions.html "PostgreSQL 8.3 - 7.2. Table
Expressions") / [8.2](/docs/8.2/queries-table-expressions.html "PostgreSQL 8.2
- 7.2. Table Expressions") / [8.1](/docs/8.1/queries-table-expressions.html
"PostgreSQL 8.1 - 7.2. Table Expressions") / [8.0](/docs/8.0/queries-table-
expressions.html "PostgreSQL 8.0 - 7.2. Table Expressions") /
[7.4](/docs/7.4/queries-table-expressions.html "PostgreSQL 7.4 - 7.2. Table
Expressions") / [7.3](/docs/7.3/queries-table-expressions.html "PostgreSQL 7.3
- 7.2. Table Expressions") / [7.2](/docs/7.2/queries-table-expressions.html
"PostgreSQL 7.2 - 7.2. Table Expressions")

__

7.2. Table Expressions  
---  
[Prev](queries-overview.html "7.1. Overview")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-select-lists.html "7.3. Select Lists")  
  
* * *

## 7.2. Table Expressions #

[7.2.1. The `FROM` Clause](queries-table-expressions.html#QUERIES-FROM)

[7.2.2. The `WHERE` Clause](queries-table-expressions.html#QUERIES-WHERE)

[7.2.3. The `GROUP BY` and `HAVING` Clauses](queries-table-
expressions.html#QUERIES-GROUP)

[7.2.4. `GROUPING SETS`, `CUBE`, and `ROLLUP`](queries-table-
expressions.html#QUERIES-GROUPING-SETS)

[7.2.5. Window Function Processing](queries-table-expressions.html#QUERIES-
WINDOW)

A _table expression_ computes a table. The table expression contains a `FROM`
clause that is optionally followed by `WHERE`, `GROUP BY`, and `HAVING`
clauses. Trivial table expressions simply refer to a table on disk, a so-
called base table, but more complex expressions can be used to modify or
combine base tables in various ways.

The optional `WHERE`, `GROUP BY`, and `HAVING` clauses in the table expression
specify a pipeline of successive transformations performed on the table
derived in the `FROM` clause. All these transformations produce a virtual
table that provides the rows that are passed to the select list to compute the
output rows of the query.

### 7.2.1. The `FROM` Clause #

The [`FROM`](sql-select.html#SQL-FROM "FROM Clause") clause derives a table
from one or more other tables given in a comma-separated table reference list.

    
    
    FROM _table_reference_ [, _table_reference_ [, ...]]
    

A table reference can be a table name (possibly schema-qualified), or a
derived table such as a subquery, a `JOIN` construct, or complex combinations
of these. If more than one table reference is listed in the `FROM` clause, the
tables are cross-joined (that is, the Cartesian product of their rows is
formed; see below). The result of the `FROM` list is an intermediate virtual
table that can then be subject to transformations by the `WHERE`, `GROUP BY`,
and `HAVING` clauses and is finally the result of the overall table
expression.

When a table reference names a table that is the parent of a table inheritance
hierarchy, the table reference produces rows of not only that table but all of
its descendant tables, unless the key word `ONLY` precedes the table name.
However, the reference produces only the columns that appear in the named
table — any columns added in subtables are ignored.

Instead of writing `ONLY` before the table name, you can write `*` after the
table name to explicitly specify that descendant tables are included. There is
no real reason to use this syntax any more, because searching descendant
tables is now always the default behavior. However, it is supported for
compatibility with older releases.

#### 7.2.1.1. Joined Tables #

A joined table is a table derived from two other (real or derived) tables
according to the rules of the particular join type. Inner, outer, and cross-
joins are available. The general syntax of a joined table is

    
    
    _T1_ _join_type_ _T2_ [ _join_condition_ ]
    

Joins of all types can be chained together, or nested: either or both _`T1`_
and _`T2`_ can be joined tables. Parentheses can be used around `JOIN` clauses
to control the join order. In the absence of parentheses, `JOIN` clauses nest
left-to-right.

**Join Types**

Cross join

    
    
    
    _T1_ CROSS JOIN _T2_
    

For every possible combination of rows from _`T1`_ and _`T2`_ (i.e., a
Cartesian product), the joined table will contain a row consisting of all
columns in _`T1`_ followed by all columns in _`T2`_. If the tables have N and
M rows respectively, the joined table will have N * M rows.

`FROM _`T1`_ CROSS JOIN _`T2`_` is equivalent to `FROM _`T1`_ INNER JOIN
_`T2`_ ON TRUE` (see below). It is also equivalent to `FROM _`T1`_ , _`T2`_`.

### Note

This latter equivalence does not hold exactly when more than two tables
appear, because `JOIN` binds more tightly than comma. For example `FROM _`T1`_
CROSS JOIN _`T2`_ INNER JOIN _`T3`_ ON _`condition`_` is not the same as `FROM
_`T1`_ , _`T2`_ INNER JOIN _`T3`_ ON _`condition`_` because the _`condition`_
can reference _`T1`_ in the first case but not the second.

Qualified joins

    
    
    
    _T1_ { [INNER] | { LEFT | RIGHT | FULL } [OUTER] } JOIN _T2_ ON _boolean_expression_
    _T1_ { [INNER] | { LEFT | RIGHT | FULL } [OUTER] } JOIN _T2_ USING ( _join column list_ )
    _T1_ NATURAL { [INNER] | { LEFT | RIGHT | FULL } [OUTER] } JOIN _T2_
    

The words `INNER` and `OUTER` are optional in all forms. `INNER` is the
default; `LEFT`, `RIGHT`, and `FULL` imply an outer join.

The _join condition_ is specified in the `ON` or `USING` clause, or implicitly
by the word `NATURAL`. The join condition determines which rows from the two
source tables are considered to “match”, as explained in detail below.

The possible types of qualified join are:

`INNER JOIN`

    

For each row R1 of T1, the joined table has a row for each row in T2 that
satisfies the join condition with R1.

`LEFT OUTER JOIN`

    

First, an inner join is performed. Then, for each row in T1 that does not
satisfy the join condition with any row in T2, a joined row is added with null
values in columns of T2. Thus, the joined table always has at least one row
for each row in T1.

`RIGHT OUTER JOIN`

    

First, an inner join is performed. Then, for each row in T2 that does not
satisfy the join condition with any row in T1, a joined row is added with null
values in columns of T1. This is the converse of a left join: the result table
will always have a row for each row in T2.

`FULL OUTER JOIN`

    

First, an inner join is performed. Then, for each row in T1 that does not
satisfy the join condition with any row in T2, a joined row is added with null
values in columns of T2. Also, for each row of T2 that does not satisfy the
join condition with any row in T1, a joined row with null values in the
columns of T1 is added.

The `ON` clause is the most general kind of join condition: it takes a Boolean
value expression of the same kind as is used in a `WHERE` clause. A pair of
rows from _`T1`_ and _`T2`_ match if the `ON` expression evaluates to true.

The `USING` clause is a shorthand that allows you to take advantage of the
specific situation where both sides of the join use the same name for the
joining column(s). It takes a comma-separated list of the shared column names
and forms a join condition that includes an equality comparison for each one.
For example, joining _`T1`_ and _`T2`_ with `USING (a, b)` produces the join
condition `ON _`T1`_.a = _`T2`_.a AND _`T1`_.b = _`T2`_.b`.

Furthermore, the output of `JOIN USING` suppresses redundant columns: there is
no need to print both of the matched columns, since they must have equal
values. While `JOIN ON` produces all columns from _`T1`_ followed by all
columns from _`T2`_ , `JOIN USING` produces one output column for each of the
listed column pairs (in the listed order), followed by any remaining columns
from _`T1`_ , followed by any remaining columns from _`T2`_.

Finally, `NATURAL` is a shorthand form of `USING`: it forms a `USING` list
consisting of all column names that appear in both input tables. As with
`USING`, these columns appear only once in the output table. If there are no
common column names, `NATURAL JOIN` behaves like `JOIN ... ON TRUE`, producing
a cross-product join.

### Note

`USING` is reasonably safe from column changes in the joined relations since
only the listed columns are combined. `NATURAL` is considerably more risky
since any schema changes to either relation that cause a new matching column
name to be present will cause the join to combine that new column as well.

To put this together, assume we have tables `t1`:

    
    
     num | name
    -----+------
       1 | a
       2 | b
       3 | c
    

and `t2`:

    
    
     num | value
    -----+-------
       1 | xxx
       3 | yyy
       5 | zzz
    

then we get the following results for the various joins:

    
    
    => **SELECT * FROM t1 CROSS JOIN t2;**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
       1 | a    |   3 | yyy
       1 | a    |   5 | zzz
       2 | b    |   1 | xxx
       2 | b    |   3 | yyy
       2 | b    |   5 | zzz
       3 | c    |   1 | xxx
       3 | c    |   3 | yyy
       3 | c    |   5 | zzz
    (9 rows)
    
    => **SELECT * FROM t1 INNER JOIN t2 ON t1.num = t2.num;**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
       3 | c    |   3 | yyy
    (2 rows)
    
    => **SELECT * FROM t1 INNER JOIN t2 USING (num);**
     num | name | value
    -----+------+-------
       1 | a    | xxx
       3 | c    | yyy
    (2 rows)
    
    => **SELECT * FROM t1 NATURAL INNER JOIN t2;**
     num | name | value
    -----+------+-------
       1 | a    | xxx
       3 | c    | yyy
    (2 rows)
    
    => **SELECT * FROM t1 LEFT JOIN t2 ON t1.num = t2.num;**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
       2 | b    |     |
       3 | c    |   3 | yyy
    (3 rows)
    
    => **SELECT * FROM t1 LEFT JOIN t2 USING (num);**
     num | name | value
    -----+------+-------
       1 | a    | xxx
       2 | b    |
       3 | c    | yyy
    (3 rows)
    
    => **SELECT * FROM t1 RIGHT JOIN t2 ON t1.num = t2.num;**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
       3 | c    |   3 | yyy
         |      |   5 | zzz
    (3 rows)
    
    => **SELECT * FROM t1 FULL JOIN t2 ON t1.num = t2.num;**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
       2 | b    |     |
       3 | c    |   3 | yyy
         |      |   5 | zzz
    (4 rows)
    

The join condition specified with `ON` can also contain conditions that do not
relate directly to the join. This can prove useful for some queries but needs
to be thought out carefully. For example:

    
    
    => **SELECT * FROM t1 LEFT JOIN t2 ON t1.num = t2.num AND t2.value = 'xxx';**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
       2 | b    |     |
       3 | c    |     |
    (3 rows)
    

Notice that placing the restriction in the `WHERE` clause produces a different
result:

    
    
    => **SELECT * FROM t1 LEFT JOIN t2 ON t1.num = t2.num WHERE t2.value = 'xxx';**
     num | name | num | value
    -----+------+-----+-------
       1 | a    |   1 | xxx
    (1 row)
    

This is because a restriction placed in the `ON` clause is processed _before_
the join, while a restriction placed in the `WHERE` clause is processed
_after_ the join. That does not matter with inner joins, but it matters a lot
with outer joins.

#### 7.2.1.2. Table and Column Aliases #

A temporary name can be given to tables and complex table references to be
used for references to the derived table in the rest of the query. This is
called a _table alias_.

To create a table alias, write

    
    
    FROM _table_reference_ AS _alias_
    

or

    
    
    FROM _table_reference_ _alias_
    

The `AS` key word is optional noise. _`alias`_ can be any identifier.

A typical application of table aliases is to assign short identifiers to long
table names to keep the join clauses readable. For example:

    
    
    SELECT * FROM some_very_long_table_name s JOIN another_fairly_long_name a ON s.id = a.num;
    

The alias becomes the new name of the table reference so far as the current
query is concerned — it is not allowed to refer to the table by the original
name elsewhere in the query. Thus, this is not valid:

    
    
    SELECT * FROM my_table AS m WHERE my_table.a > 5;    -- wrong
    

Table aliases are mainly for notational convenience, but it is necessary to
use them when joining a table to itself, e.g.:

    
    
    SELECT * FROM people AS mother JOIN people AS child ON mother.id = child.mother_id;
    

Parentheses are used to resolve ambiguities. In the following example, the
first statement assigns the alias `b` to the second instance of `my_table`,
but the second statement assigns the alias to the result of the join:

    
    
    SELECT * FROM my_table AS a CROSS JOIN my_table AS b ...
    SELECT * FROM (my_table AS a CROSS JOIN my_table) AS b ...
    

Another form of table aliasing gives temporary names to the columns of the
table, as well as the table itself:

    
    
    FROM _table_reference_ [AS] _alias_ ( _column1_ [, _column2_ [, ...]] )
    

If fewer column aliases are specified than the actual table has columns, the
remaining columns are not renamed. This syntax is especially useful for self-
joins or subqueries.

When an alias is applied to the output of a `JOIN` clause, the alias hides the
original name(s) within the `JOIN`. For example:

    
    
    SELECT a.* FROM my_table AS a JOIN your_table AS b ON ...
    

is valid SQL, but:

    
    
    SELECT a.* FROM (my_table AS a JOIN your_table AS b ON ...) AS c
    

is not valid; the table alias `a` is not visible outside the alias `c`.

#### 7.2.1.3. Subqueries #

Subqueries specifying a derived table must be enclosed in parentheses. They
may be assigned a table alias name, and optionally column alias names (as in
[Section 7.2.1.2](queries-table-expressions.html#QUERIES-TABLE-ALIASES
"7.2.1.2. Table and Column Aliases")). For example:

    
    
    FROM (SELECT * FROM table1) AS alias_name
    

This example is equivalent to `FROM table1 AS alias_name`. More interesting
cases, which cannot be reduced to a plain join, arise when the subquery
involves grouping or aggregation.

A subquery can also be a `VALUES` list:

    
    
    FROM (VALUES ('anne', 'smith'), ('bob', 'jones'), ('joe', 'blow'))
         AS names(first, last)
    

Again, a table alias is optional. Assigning alias names to the columns of the
`VALUES` list is optional, but is good practice. For more information see
[Section 7.7](queries-values.html "7.7. VALUES Lists").

According to the SQL standard, a table alias name must be supplied for a
subquery. PostgreSQL allows `AS` and the alias to be omitted, but writing one
is good practice in SQL code that might be ported to another system.

#### 7.2.1.4. Table Functions #

Table functions are functions that produce a set of rows, made up of either
base data types (scalar types) or composite data types (table rows). They are
used like a table, view, or subquery in the `FROM` clause of a query. Columns
returned by table functions can be included in `SELECT`, `JOIN`, or `WHERE`
clauses in the same manner as columns of a table, view, or subquery.

Table functions may also be combined using the `ROWS FROM` syntax, with the
results returned in parallel columns; the number of result rows in this case
is that of the largest function result, with smaller results padded with null
values to match.

    
    
    _function_call_ [WITH ORDINALITY] [[AS] _table_alias_ [(_column_alias_ [, ... ])]]
    ROWS FROM( _function_call_ [, ... ] ) [WITH ORDINALITY] [[AS] _table_alias_ [(_column_alias_ [, ... ])]]
    

If the `WITH ORDINALITY` clause is specified, an additional column of type
`bigint` will be added to the function result columns. This column numbers the
rows of the function result set, starting from 1. (This is a generalization of
the SQL-standard syntax for `UNNEST ... WITH ORDINALITY`.) By default, the
ordinal column is called `ordinality`, but a different column name can be
assigned to it using an `AS` clause.

The special table function `UNNEST` may be called with any number of array
parameters, and it returns a corresponding number of columns, as if `UNNEST`
([Section 9.19](functions-array.html "9.19. Array Functions and Operators"))
had been called on each parameter separately and combined using the `ROWS
FROM` construct.

    
    
    UNNEST( _array_expression_ [, ... ] ) [WITH ORDINALITY] [[AS] _table_alias_ [(_column_alias_ [, ... ])]]
    

If no _`table_alias`_ is specified, the function name is used as the table
name; in the case of a `ROWS FROM()` construct, the first function's name is
used.

If column aliases are not supplied, then for a function returning a base data
type, the column name is also the same as the function name. For a function
returning a composite type, the result columns get the names of the individual
attributes of the type.

Some examples:

    
    
    CREATE TABLE foo (fooid int, foosubid int, fooname text);
    
    CREATE FUNCTION getfoo(int) RETURNS SETOF foo AS $$
        SELECT * FROM foo WHERE fooid = $1;
    $$ LANGUAGE SQL;
    
    SELECT * FROM getfoo(1) AS t1;
    
    SELECT * FROM foo
        WHERE foosubid IN (
                            SELECT foosubid
                            FROM getfoo(foo.fooid) z
                            WHERE z.fooid = foo.fooid
                          );
    
    CREATE VIEW vw_getfoo AS SELECT * FROM getfoo(1);
    
    SELECT * FROM vw_getfoo;
    

In some cases it is useful to define table functions that can return different
column sets depending on how they are invoked. To support this, the table
function can be declared as returning the pseudo-type `record` with no `OUT`
parameters. When such a function is used in a query, the expected row
structure must be specified in the query itself, so that the system can know
how to parse and plan the query. This syntax looks like:

    
    
    _function_call_ [AS] _alias_ (_column_definition_ [, ... ])
    _function_call_ AS [_alias_] (_column_definition_ [, ... ])
    ROWS FROM( ... _function_call_ AS (_column_definition_ [, ... ]) [, ... ] )
    

When not using the `ROWS FROM()` syntax, the _`column_definition`_ list
replaces the column alias list that could otherwise be attached to the `FROM`
item; the names in the column definitions serve as column aliases. When using
the `ROWS FROM()` syntax, a _`column_definition`_ list can be attached to each
member function separately; or if there is only one member function and no
`WITH ORDINALITY` clause, a _`column_definition`_ list can be written in place
of a column alias list following `ROWS FROM()`.

Consider this example:

    
    
    SELECT *
        FROM dblink('dbname=mydb', 'SELECT proname, prosrc FROM pg_proc')
          AS t1(proname name, prosrc text)
        WHERE proname LIKE 'bytea%';
    

The [dblink](contrib-dblink-function.html "dblink") function (part of the
[dblink](dblink.html "F.12. dblink — connect to other PostgreSQL databases")
module) executes a remote query. It is declared to return `record` since it
might be used for any kind of query. The actual column set must be specified
in the calling query so that the parser knows, for example, what `*` should
expand to.

This example uses `ROWS FROM`:

    
    
    SELECT *
    FROM ROWS FROM
        (
            json_to_recordset('[{"a":40,"b":"foo"},{"a":"100","b":"bar"}]')
                AS (a INTEGER, b TEXT),
            generate_series(1, 3)
        ) AS x (p, q, s)
    ORDER BY p;
    
      p  |  q  | s
    -----+-----+---
      40 | foo | 1
     100 | bar | 2
         |     | 3
    

It joins two functions into a single `FROM` target. `json_to_recordset()` is
instructed to return two columns, the first `integer` and the second `text`.
The result of `generate_series()` is used directly. The `ORDER BY` clause
sorts the column values as integers.

#### 7.2.1.5. `LATERAL` Subqueries #

Subqueries appearing in `FROM` can be preceded by the key word `LATERAL`. This
allows them to reference columns provided by preceding `FROM` items. (Without
`LATERAL`, each subquery is evaluated independently and so cannot cross-
reference any other `FROM` item.)

Table functions appearing in `FROM` can also be preceded by the key word
`LATERAL`, but for functions the key word is optional; the function's
arguments can contain references to columns provided by preceding `FROM` items
in any case.

A `LATERAL` item can appear at the top level in the `FROM` list, or within a
`JOIN` tree. In the latter case it can also refer to any items that are on the
left-hand side of a `JOIN` that it is on the right-hand side of.

When a `FROM` item contains `LATERAL` cross-references, evaluation proceeds as
follows: for each row of the `FROM` item providing the cross-referenced
column(s), or set of rows of multiple `FROM` items providing the columns, the
`LATERAL` item is evaluated using that row or row set's values of the columns.
The resulting row(s) are joined as usual with the rows they were computed
from. This is repeated for each row or set of rows from the column source
table(s).

A trivial example of `LATERAL` is

    
    
    SELECT * FROM foo, LATERAL (SELECT * FROM bar WHERE bar.id = foo.bar_id) ss;
    

This is not especially useful since it has exactly the same result as the more
conventional

    
    
    SELECT * FROM foo, bar WHERE bar.id = foo.bar_id;
    

`LATERAL` is primarily useful when the cross-referenced column is necessary
for computing the row(s) to be joined. A common application is providing an
argument value for a set-returning function. For example, supposing that
`vertices(polygon)` returns the set of vertices of a polygon, we could
identify close-together vertices of polygons stored in a table with:

    
    
    SELECT p1.id, p2.id, v1, v2
    FROM polygons p1, polygons p2,
         LATERAL vertices(p1.poly) v1,
         LATERAL vertices(p2.poly) v2
    WHERE (v1 <-> v2) < 10 AND p1.id != p2.id;
    

This query could also be written

    
    
    SELECT p1.id, p2.id, v1, v2
    FROM polygons p1 CROSS JOIN LATERAL vertices(p1.poly) v1,
         polygons p2 CROSS JOIN LATERAL vertices(p2.poly) v2
    WHERE (v1 <-> v2) < 10 AND p1.id != p2.id;
    

or in several other equivalent formulations. (As already mentioned, the
`LATERAL` key word is unnecessary in this example, but we use it for clarity.)

It is often particularly handy to `LEFT JOIN` to a `LATERAL` subquery, so that
source rows will appear in the result even if the `LATERAL` subquery produces
no rows for them. For example, if `get_product_names()` returns the names of
products made by a manufacturer, but some manufacturers in our table currently
produce no products, we could find out which ones those are like this:

    
    
    SELECT m.name
    FROM manufacturers m LEFT JOIN LATERAL get_product_names(m.id) pname ON true
    WHERE pname IS NULL;
    

### 7.2.2. The `WHERE` Clause #

The syntax of the [`WHERE`](sql-select.html#SQL-WHERE "WHERE Clause") clause
is

    
    
    WHERE _search_condition_
    

where _`search_condition`_ is any value expression (see [Section 4.2](sql-
expressions.html "4.2. Value Expressions")) that returns a value of type
`boolean`.

After the processing of the `FROM` clause is done, each row of the derived
virtual table is checked against the search condition. If the result of the
condition is true, the row is kept in the output table, otherwise (i.e., if
the result is false or null) it is discarded. The search condition typically
references at least one column of the table generated in the `FROM` clause;
this is not required, but otherwise the `WHERE` clause will be fairly useless.

### Note

The join condition of an inner join can be written either in the `WHERE`
clause or in the `JOIN` clause. For example, these table expressions are
equivalent:

    
    
    FROM a, b WHERE a.id = b.id AND b.val > 5
    

and:

    
    
    FROM a INNER JOIN b ON (a.id = b.id) WHERE b.val > 5
    

or perhaps even:

    
    
    FROM a NATURAL JOIN b WHERE b.val > 5
    

Which one of these you use is mainly a matter of style. The `JOIN` syntax in
the `FROM` clause is probably not as portable to other SQL database management
systems, even though it is in the SQL standard. For outer joins there is no
choice: they must be done in the `FROM` clause. The `ON` or `USING` clause of
an outer join is _not_ equivalent to a `WHERE` condition, because it results
in the addition of rows (for unmatched input rows) as well as the removal of
rows in the final result.

Here are some examples of `WHERE` clauses:

    
    
    SELECT ... FROM fdt WHERE c1 > 5
    
    SELECT ... FROM fdt WHERE c1 IN (1, 2, 3)
    
    SELECT ... FROM fdt WHERE c1 IN (SELECT c1 FROM t2)
    
    SELECT ... FROM fdt WHERE c1 IN (SELECT c3 FROM t2 WHERE c2 = fdt.c1 + 10)
    
    SELECT ... FROM fdt WHERE c1 BETWEEN (SELECT c3 FROM t2 WHERE c2 = fdt.c1 + 10) AND 100
    
    SELECT ... FROM fdt WHERE EXISTS (SELECT c1 FROM t2 WHERE c2 > fdt.c1)
    

`fdt` is the table derived in the `FROM` clause. Rows that do not meet the
search condition of the `WHERE` clause are eliminated from `fdt`. Notice the
use of scalar subqueries as value expressions. Just like any other query, the
subqueries can employ complex table expressions. Notice also how `fdt` is
referenced in the subqueries. Qualifying `c1` as `fdt.c1` is only necessary if
`c1` is also the name of a column in the derived input table of the subquery.
But qualifying the column name adds clarity even when it is not needed. This
example shows how the column naming scope of an outer query extends into its
inner queries.

### 7.2.3. The `GROUP BY` and `HAVING` Clauses #

After passing the `WHERE` filter, the derived input table might be subject to
grouping, using the `GROUP BY` clause, and elimination of group rows using the
`HAVING` clause.

    
    
    SELECT _select_list_
        FROM ...
        [WHERE ...]
        GROUP BY _grouping_column_reference_ [, _grouping_column_reference_]...
    

The [`GROUP BY`](sql-select.html#SQL-GROUPBY "GROUP BY Clause") clause is used
to group together those rows in a table that have the same values in all the
columns listed. The order in which the columns are listed does not matter. The
effect is to combine each set of rows having common values into one group row
that represents all rows in the group. This is done to eliminate redundancy in
the output and/or compute aggregates that apply to these groups. For instance:

    
    
    => **SELECT * FROM test1;**
     x | y
    ---+---
     a | 3
     c | 2
     b | 5
     a | 1
    (4 rows)
    
    => **SELECT x FROM test1 GROUP BY x;**
     x
    ---
     a
     b
     c
    (3 rows)
    

In the second query, we could not have written `SELECT * FROM test1 GROUP BY
x`, because there is no single value for the column `y` that could be
associated with each group. The grouped-by columns can be referenced in the
select list since they have a single value in each group.

In general, if a table is grouped, columns that are not listed in `GROUP BY`
cannot be referenced except in aggregate expressions. An example with
aggregate expressions is:

    
    
    => **SELECT x, sum(y) FROM test1 GROUP BY x;**
     x | sum
    ---+-----
     a |   4
     b |   5
     c |   2
    (3 rows)
    

Here `sum` is an aggregate function that computes a single value over the
entire group. More information about the available aggregate functions can be
found in [Section 9.21](functions-aggregate.html "9.21. Aggregate Functions").

### Tip

Grouping without aggregate expressions effectively calculates the set of
distinct values in a column. This can also be achieved using the `DISTINCT`
clause (see [Section 7.3.3](queries-select-lists.html#QUERIES-DISTINCT
"7.3.3. DISTINCT")).

Here is another example: it calculates the total sales for each product
(rather than the total sales of all products):

    
    
    SELECT product_id, p.name, (sum(s.units) * p.price) AS sales
        FROM products p LEFT JOIN sales s USING (product_id)
        GROUP BY product_id, p.name, p.price;
    

In this example, the columns `product_id`, `p.name`, and `p.price` must be in
the `GROUP BY` clause since they are referenced in the query select list (but
see below). The column `s.units` does not have to be in the `GROUP BY` list
since it is only used in an aggregate expression (`sum(...)`), which
represents the sales of a product. For each product, the query returns a
summary row about all sales of the product.

If the products table is set up so that, say, `product_id` is the primary key,
then it would be enough to group by `product_id` in the above example, since
name and price would be _functionally dependent_ on the product ID, and so
there would be no ambiguity about which name and price value to return for
each product ID group.

In strict SQL, `GROUP BY` can only group by columns of the source table but
PostgreSQL extends this to also allow `GROUP BY` to group by columns in the
select list. Grouping by value expressions instead of simple column names is
also allowed.

If a table has been grouped using `GROUP BY`, but only certain groups are of
interest, the `HAVING` clause can be used, much like a `WHERE` clause, to
eliminate groups from the result. The syntax is:

    
    
    SELECT _select_list_ FROM ... [WHERE ...] GROUP BY ... HAVING _boolean_expression_
    

Expressions in the `HAVING` clause can refer both to grouped expressions and
to ungrouped expressions (which necessarily involve an aggregate function).

Example:

    
    
    => **SELECT x, sum(y) FROM test1 GROUP BY x HAVING sum(y)> 3;**
     x | sum
    ---+-----
     a |   4
     b |   5
    (2 rows)
    
    => **SELECT x, sum(y) FROM test1 GROUP BY x HAVING x< 'c';**
     x | sum
    ---+-----
     a |   4
     b |   5
    (2 rows)
    

Again, a more realistic example:

    
    
    SELECT product_id, p.name, (sum(s.units) * (p.price - p.cost)) AS profit
        FROM products p LEFT JOIN sales s USING (product_id)
        WHERE s.date > CURRENT_DATE - INTERVAL '4 weeks'
        GROUP BY product_id, p.name, p.price, p.cost
        HAVING sum(p.price * s.units) > 5000;
    

In the example above, the `WHERE` clause is selecting rows by a column that is
not grouped (the expression is only true for sales during the last four
weeks), while the `HAVING` clause restricts the output to groups with total
gross sales over 5000. Note that the aggregate expressions do not necessarily
need to be the same in all parts of the query.

If a query contains aggregate function calls, but no `GROUP BY` clause,
grouping still occurs: the result is a single group row (or perhaps no rows at
all, if the single row is then eliminated by `HAVING`). The same is true if it
contains a `HAVING` clause, even without any aggregate function calls or
`GROUP BY` clause.

### 7.2.4. `GROUPING SETS`, `CUBE`, and `ROLLUP` #

More complex grouping operations than those described above are possible using
the concept of _grouping sets_. The data selected by the `FROM` and `WHERE`
clauses is grouped separately by each specified grouping set, aggregates
computed for each group just as for simple `GROUP BY` clauses, and then the
results returned. For example:

    
    
    => **SELECT * FROM items_sold;**
     brand | size | sales
    -------+------+-------
     Foo   | L    |  10
     Foo   | M    |  20
     Bar   | M    |  15
     Bar   | L    |  5
    (4 rows)
    
    => **SELECT brand, size, sum(sales) FROM items_sold GROUP BY GROUPING SETS ((brand), (size), ());**
     brand | size | sum
    -------+------+-----
     Foo   |      |  30
     Bar   |      |  20
           | L    |  15
           | M    |  35
           |      |  50
    (5 rows)
    

Each sublist of `GROUPING SETS` may specify zero or more columns or
expressions and is interpreted the same way as though it were directly in the
`GROUP BY` clause. An empty grouping set means that all rows are aggregated
down to a single group (which is output even if no input rows were present),
as described above for the case of aggregate functions with no `GROUP BY`
clause.

References to the grouping columns or expressions are replaced by null values
in result rows for grouping sets in which those columns do not appear. To
distinguish which grouping a particular output row resulted from, see [Table
9.63](functions-aggregate.html#FUNCTIONS-GROUPING-TABLE "Table 9.63. Grouping
Operations").

A shorthand notation is provided for specifying two common types of grouping
set. A clause of the form

    
    
    ROLLUP ( _e1_ , _e2_ , _e3_ , ... )
    

represents the given list of expressions and all prefixes of the list
including the empty list; thus it is equivalent to

    
    
    GROUPING SETS (
        ( _e1_ , _e2_ , _e3_ , ... ),
        ...
        ( _e1_ , _e2_ ),
        ( _e1_ ),
        ( )
    )
    

This is commonly used for analysis over hierarchical data; e.g., total salary
by department, division, and company-wide total.

A clause of the form

    
    
    CUBE ( _e1_ , _e2_ , ... )
    

represents the given list and all of its possible subsets (i.e., the power
set). Thus

    
    
    CUBE ( a, b, c )
    

is equivalent to

    
    
    GROUPING SETS (
        ( a, b, c ),
        ( a, b    ),
        ( a,    c ),
        ( a       ),
        (    b, c ),
        (    b    ),
        (       c ),
        (         )
    )
    

The individual elements of a `CUBE` or `ROLLUP` clause may be either
individual expressions, or sublists of elements in parentheses. In the latter
case, the sublists are treated as single units for the purposes of generating
the individual grouping sets. For example:

    
    
    CUBE ( (a, b), (c, d) )
    

is equivalent to

    
    
    GROUPING SETS (
        ( a, b, c, d ),
        ( a, b       ),
        (       c, d ),
        (            )
    )
    

and

    
    
    ROLLUP ( a, (b, c), d )
    

is equivalent to

    
    
    GROUPING SETS (
        ( a, b, c, d ),
        ( a, b, c    ),
        ( a          ),
        (            )
    )
    

The `CUBE` and `ROLLUP` constructs can be used either directly in the `GROUP
BY` clause, or nested inside a `GROUPING SETS` clause. If one `GROUPING SETS`
clause is nested inside another, the effect is the same as if all the elements
of the inner clause had been written directly in the outer clause.

If multiple grouping items are specified in a single `GROUP BY` clause, then
the final list of grouping sets is the cross product of the individual items.
For example:

    
    
    GROUP BY a, CUBE (b, c), GROUPING SETS ((d), (e))
    

is equivalent to

    
    
    GROUP BY GROUPING SETS (
        (a, b, c, d), (a, b, c, e),
        (a, b, d),    (a, b, e),
        (a, c, d),    (a, c, e),
        (a, d),       (a, e)
    )
    

When specifying multiple grouping items together, the final set of grouping
sets might contain duplicates. For example:

    
    
    GROUP BY ROLLUP (a, b), ROLLUP (a, c)
    

is equivalent to

    
    
    GROUP BY GROUPING SETS (
        (a, b, c),
        (a, b),
        (a, b),
        (a, c),
        (a),
        (a),
        (a, c),
        (a),
        ()
    )
    

If these duplicates are undesirable, they can be removed using the `DISTINCT`
clause directly on the `GROUP BY`. Therefore:

    
    
    GROUP BY **DISTINCT** ROLLUP (a, b), ROLLUP (a, c)
    

is equivalent to

    
    
    GROUP BY GROUPING SETS (
        (a, b, c),
        (a, b),
        (a, c),
        (a),
        ()
    )
    

This is not the same as using `SELECT DISTINCT` because the output rows may
still contain duplicates. If any of the ungrouped columns contains NULL, it
will be indistinguishable from the NULL used when that same column is grouped.

### Note

The construct `(a, b)` is normally recognized in expressions as a [row
constructor](sql-expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS "4.2.13. Row
Constructors"). Within the `GROUP BY` clause, this does not apply at the top
levels of expressions, and `(a, b)` is parsed as a list of expressions as
described above. If for some reason you _need_ a row constructor in a grouping
expression, use `ROW(a, b)`.

### 7.2.5. Window Function Processing #

If the query contains any window functions (see [Section 3.5](tutorial-
window.html "3.5. Window Functions"), [Section 9.22](functions-window.html
"9.22. Window Functions") and [Section 4.2.8](sql-expressions.html#SYNTAX-
WINDOW-FUNCTIONS "4.2.8. Window Function Calls")), these functions are
evaluated after any grouping, aggregation, and `HAVING` filtering is
performed. That is, if the query uses any aggregates, `GROUP BY`, or `HAVING`,
then the rows seen by the window functions are the group rows instead of the
original table rows from `FROM`/`WHERE`.

When multiple window functions are used, all the window functions having
equivalent `PARTITION BY` and `ORDER BY` clauses in their window definitions
are guaranteed to see the same ordering of the input rows, even if the `ORDER
BY` does not uniquely determine the ordering. However, no guarantees are made
about the evaluation of functions having different `PARTITION BY` or `ORDER
BY` specifications. (In such cases a sort step is typically required between
the passes of window function evaluations, and the sort is not guaranteed to
preserve ordering of rows that its `ORDER BY` sees as equivalent.)

Currently, window functions always require presorted data, and so the query
output will be ordered according to one or another of the window functions'
`PARTITION BY`/`ORDER BY` clauses. It is not recommended to rely on this,
however. Use an explicit top-level `ORDER BY` clause if you want to be sure
the results are sorted in a particular way.

* * *

[Prev](queries-overview.html "7.1. Overview")  | [Up](queries.html "Chapter 7. Queries") |  [Next](queries-select-lists.html "7.3. Select Lists")  
---|---|---  
7.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.3. Select Lists  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-table-
expressions.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

