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

Supported Versions: [Current](/docs/current/queries-with.html "PostgreSQL 17 -
7.8. WITH Queries \(Common Table Expressions\)") ([17](/docs/17/queries-
with.html "PostgreSQL 17 - 7.8. WITH Queries \(Common Table Expressions\)")) /
[16](/docs/16/queries-with.html "PostgreSQL 16 - 7.8. WITH Queries \(Common
Table Expressions\)") / [15](/docs/15/queries-with.html "PostgreSQL 15 -
7.8. WITH Queries \(Common Table Expressions\)") / [14](/docs/14/queries-
with.html "PostgreSQL 14 - 7.8. WITH Queries \(Common Table Expressions\)") /
[13](/docs/13/queries-with.html "PostgreSQL 13 - 7.8. WITH Queries \(Common
Table Expressions\)")

Development Versions: [18](/docs/18/queries-with.html "PostgreSQL 18 -
7.8. WITH Queries \(Common Table Expressions\)") /
[devel](/docs/devel/queries-with.html "PostgreSQL devel - 7.8. WITH Queries
\(Common Table Expressions\)")

Unsupported versions: [12](/docs/12/queries-with.html "PostgreSQL 12 -
7.8. WITH Queries \(Common Table Expressions\)") / [11](/docs/11/queries-
with.html "PostgreSQL 11 - 7.8. WITH Queries \(Common Table Expressions\)") /
[10](/docs/10/queries-with.html "PostgreSQL 10 - 7.8. WITH Queries \(Common
Table Expressions\)") / [9.6](/docs/9.6/queries-with.html "PostgreSQL 9.6 -
7.8. WITH Queries \(Common Table Expressions\)") / [9.5](/docs/9.5/queries-
with.html "PostgreSQL 9.5 - 7.8. WITH Queries \(Common Table Expressions\)") /
[9.4](/docs/9.4/queries-with.html "PostgreSQL 9.4 - 7.8. WITH Queries \(Common
Table Expressions\)") / [9.3](/docs/9.3/queries-with.html "PostgreSQL 9.3 -
7.8. WITH Queries \(Common Table Expressions\)") / [9.2](/docs/9.2/queries-
with.html "PostgreSQL 9.2 - 7.8. WITH Queries \(Common Table Expressions\)") /
[9.1](/docs/9.1/queries-with.html "PostgreSQL 9.1 - 7.8. WITH Queries \(Common
Table Expressions\)") / [9.0](/docs/9.0/queries-with.html "PostgreSQL 9.0 -
7.8. WITH Queries \(Common Table Expressions\)") / [8.4](/docs/8.4/queries-
with.html "PostgreSQL 8.4 - 7.8. WITH Queries \(Common Table Expressions\)")

__

7.8. `WITH` Queries (Common Table Expressions)  
---  
[Prev](queries-values.html "7.7. VALUES Lists")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype.html "Chapter 8. Data Types")  
  
* * *

## 7.8. `WITH` Queries (Common Table Expressions) #

[7.8.1. `SELECT` in `WITH`](queries-with.html#QUERIES-WITH-SELECT)

[7.8.2. Recursive Queries](queries-with.html#QUERIES-WITH-RECURSIVE)

[7.8.3. Common Table Expression Materialization](queries-with.html#QUERIES-
WITH-CTE-MATERIALIZATION)

[7.8.4. Data-Modifying Statements in `WITH`](queries-with.html#QUERIES-WITH-
MODIFYING)

`WITH` provides a way to write auxiliary statements for use in a larger query.
These statements, which are often referred to as Common Table Expressions or
CTEs, can be thought of as defining temporary tables that exist just for one
query. Each auxiliary statement in a `WITH` clause can be a `SELECT`,
`INSERT`, `UPDATE`, or `DELETE`; and the `WITH` clause itself is attached to a
primary statement that can be a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or
`MERGE`.

### 7.8.1. `SELECT` in `WITH` #

The basic value of `SELECT` in `WITH` is to break down complicated queries
into simpler parts. An example is:

    
    
    WITH regional_sales AS (
        SELECT region, SUM(amount) AS total_sales
        FROM orders
        GROUP BY region
    ), top_regions AS (
        SELECT region
        FROM regional_sales
        WHERE total_sales > (SELECT SUM(total_sales)/10 FROM regional_sales)
    )
    SELECT region,
           product,
           SUM(quantity) AS product_units,
           SUM(amount) AS product_sales
    FROM orders
    WHERE region IN (SELECT region FROM top_regions)
    GROUP BY region, product;
    

which displays per-product sales totals in only the top sales regions. The
`WITH` clause defines two auxiliary statements named `regional_sales` and
`top_regions`, where the output of `regional_sales` is used in `top_regions`
and the output of `top_regions` is used in the primary `SELECT` query. This
example could have been written without `WITH`, but we'd have needed two
levels of nested sub-`SELECT`s. It's a bit easier to follow this way.

### 7.8.2. Recursive Queries #

The optional `RECURSIVE` modifier changes `WITH` from a mere syntactic
convenience into a feature that accomplishes things not otherwise possible in
standard SQL. Using `RECURSIVE`, a `WITH` query can refer to its own output. A
very simple example is this query to sum the integers from 1 through 100:

    
    
    WITH RECURSIVE t(n) AS (
        VALUES (1)
      UNION ALL
        SELECT n+1 FROM t WHERE n < 100
    )
    SELECT sum(n) FROM t;
    

The general form of a recursive `WITH` query is always a _non-recursive term_
, then `UNION` (or `UNION ALL`), then a _recursive term_ , where only the
recursive term can contain a reference to the query's own output. Such a query
is executed as follows:

**Recursive Query Evaluation**

  1. Evaluate the non-recursive term. For `UNION` (but not `UNION ALL`), discard duplicate rows. Include all remaining rows in the result of the recursive query, and also place them in a temporary _working table_.

  2. So long as the working table is not empty, repeat these steps:

     1. Evaluate the recursive term, substituting the current contents of the working table for the recursive self-reference. For `UNION` (but not `UNION ALL`), discard duplicate rows and rows that duplicate any previous result row. Include all remaining rows in the result of the recursive query, and also place them in a temporary _intermediate table_.

     2. Replace the contents of the working table with the contents of the intermediate table, then empty the intermediate table.

### Note

While `RECURSIVE` allows queries to be specified recursively, internally such
queries are evaluated iteratively.

In the example above, the working table has just a single row in each step,
and it takes on the values from 1 through 100 in successive steps. In the
100th step, there is no output because of the `WHERE` clause, and so the query
terminates.

Recursive queries are typically used to deal with hierarchical or tree-
structured data. A useful example is this query to find all the direct and
indirect sub-parts of a product, given only a table that shows immediate
inclusions:

    
    
    WITH RECURSIVE included_parts(sub_part, part, quantity) AS (
        SELECT sub_part, part, quantity FROM parts WHERE part = 'our_product'
      UNION ALL
        SELECT p.sub_part, p.part, p.quantity * pr.quantity
        FROM included_parts pr, parts p
        WHERE p.part = pr.sub_part
    )
    SELECT sub_part, SUM(quantity) as total_quantity
    FROM included_parts
    GROUP BY sub_part
    

#### 7.8.2.1. Search Order #

When computing a tree traversal using a recursive query, you might want to
order the results in either depth-first or breadth-first order. This can be
done by computing an ordering column alongside the other data columns and
using that to sort the results at the end. Note that this does not actually
control in which order the query evaluation visits the rows; that is as always
in SQL implementation-dependent. This approach merely provides a convenient
way to order the results afterwards.

To create a depth-first order, we compute for each result row an array of rows
that we have visited so far. For example, consider the following query that
searches a table `tree` using a `link` field:

    
    
    WITH RECURSIVE search_tree(id, link, data) AS (
        SELECT t.id, t.link, t.data
        FROM tree t
      UNION ALL
        SELECT t.id, t.link, t.data
        FROM tree t, search_tree st
        WHERE t.id = st.link
    )
    SELECT * FROM search_tree;
    

To add depth-first ordering information, you can write this:

    
    
    WITH RECURSIVE search_tree(id, link, data, **path**) AS (
        SELECT t.id, t.link, t.data, **ARRAY[t.id]**
        FROM tree t
      UNION ALL
        SELECT t.id, t.link, t.data, **path || t.id**
        FROM tree t, search_tree st
        WHERE t.id = st.link
    )
    SELECT * FROM search_tree **ORDER BY path** ;
    

In the general case where more than one field needs to be used to identify a
row, use an array of rows. For example, if we needed to track fields `f1` and
`f2`:

    
    
    WITH RECURSIVE search_tree(id, link, data, **path**) AS (
        SELECT t.id, t.link, t.data, **ARRAY[ROW(t.f1, t.f2)]**
        FROM tree t
      UNION ALL
        SELECT t.id, t.link, t.data, **path || ROW(t.f1, t.f2)**
        FROM tree t, search_tree st
        WHERE t.id = st.link
    )
    SELECT * FROM search_tree **ORDER BY path** ;
    

### Tip

Omit the `ROW()` syntax in the common case where only one field needs to be
tracked. This allows a simple array rather than a composite-type array to be
used, gaining efficiency.

To create a breadth-first order, you can add a column that tracks the depth of
the search, for example:

    
    
    WITH RECURSIVE search_tree(id, link, data, **depth**) AS (
        SELECT t.id, t.link, t.data, **0**
        FROM tree t
      UNION ALL
        SELECT t.id, t.link, t.data, **depth + 1**
        FROM tree t, search_tree st
        WHERE t.id = st.link
    )
    SELECT * FROM search_tree **ORDER BY depth** ;
    

To get a stable sort, add data columns as secondary sorting columns.

### Tip

The recursive query evaluation algorithm produces its output in breadth-first
search order. However, this is an implementation detail and it is perhaps
unsound to rely on it. The order of the rows within each level is certainly
undefined, so some explicit ordering might be desired in any case.

There is built-in syntax to compute a depth- or breadth-first sort column. For
example:

    
    
    WITH RECURSIVE search_tree(id, link, data) AS (
        SELECT t.id, t.link, t.data
        FROM tree t
      UNION ALL
        SELECT t.id, t.link, t.data
        FROM tree t, search_tree st
        WHERE t.id = st.link
    ) **SEARCH DEPTH FIRST BY id SET ordercol**
    SELECT * FROM search_tree ORDER BY ordercol;
    
    WITH RECURSIVE search_tree(id, link, data) AS (
        SELECT t.id, t.link, t.data
        FROM tree t
      UNION ALL
        SELECT t.id, t.link, t.data
        FROM tree t, search_tree st
        WHERE t.id = st.link
    ) **SEARCH BREADTH FIRST BY id SET ordercol**
    SELECT * FROM search_tree ORDER BY ordercol;
    

This syntax is internally expanded to something similar to the above hand-
written forms. The `SEARCH` clause specifies whether depth- or breadth first
search is wanted, the list of columns to track for sorting, and a column name
that will contain the result data that can be used for sorting. That column
will implicitly be added to the output rows of the CTE.

#### 7.8.2.2. Cycle Detection #

When working with recursive queries it is important to be sure that the
recursive part of the query will eventually return no tuples, or else the
query will loop indefinitely. Sometimes, using `UNION` instead of `UNION ALL`
can accomplish this by discarding rows that duplicate previous output rows.
However, often a cycle does not involve output rows that are completely
duplicate: it may be necessary to check just one or a few fields to see if the
same point has been reached before. The standard method for handling such
situations is to compute an array of the already-visited values. For example,
consider again the following query that searches a table `graph` using a
`link` field:

    
    
    WITH RECURSIVE search_graph(id, link, data, depth) AS (
        SELECT g.id, g.link, g.data, 0
        FROM graph g
      UNION ALL
        SELECT g.id, g.link, g.data, sg.depth + 1
        FROM graph g, search_graph sg
        WHERE g.id = sg.link
    )
    SELECT * FROM search_graph;
    

This query will loop if the `link` relationships contain cycles. Because we
require a “depth” output, just changing `UNION ALL` to `UNION` would not
eliminate the looping. Instead we need to recognize whether we have reached
the same row again while following a particular path of links. We add two
columns `is_cycle` and `path` to the loop-prone query:

    
    
    WITH RECURSIVE search_graph(id, link, data, depth, **is_cycle, path**) AS (
        SELECT g.id, g.link, g.data, 0,
          **false,
          ARRAY[g.id]**
        FROM graph g
      UNION ALL
        SELECT g.id, g.link, g.data, sg.depth + 1,
          **g.id = ANY(path),
          path || g.id**
        FROM graph g, search_graph sg
        WHERE g.id = sg.link **AND NOT is_cycle**
    )
    SELECT * FROM search_graph;
    

Aside from preventing cycles, the array value is often useful in its own right
as representing the “path” taken to reach any particular row.

In the general case where more than one field needs to be checked to recognize
a cycle, use an array of rows. For example, if we needed to compare fields
`f1` and `f2`:

    
    
    WITH RECURSIVE search_graph(id, link, data, depth, **is_cycle, path**) AS (
        SELECT g.id, g.link, g.data, 0,
          **false,
          ARRAY[ROW(g.f1, g.f2)]**
        FROM graph g
      UNION ALL
        SELECT g.id, g.link, g.data, sg.depth + 1,
          **ROW(g.f1, g.f2) = ANY(path),
          path || ROW(g.f1, g.f2)**
        FROM graph g, search_graph sg
        WHERE g.id = sg.link **AND NOT is_cycle**
    )
    SELECT * FROM search_graph;
    

### Tip

Omit the `ROW()` syntax in the common case where only one field needs to be
checked to recognize a cycle. This allows a simple array rather than a
composite-type array to be used, gaining efficiency.

There is built-in syntax to simplify cycle detection. The above query can also
be written like this:

    
    
    WITH RECURSIVE search_graph(id, link, data, depth) AS (
        SELECT g.id, g.link, g.data, 1
        FROM graph g
      UNION ALL
        SELECT g.id, g.link, g.data, sg.depth + 1
        FROM graph g, search_graph sg
        WHERE g.id = sg.link
    ) **CYCLE id SET is_cycle USING path**
    SELECT * FROM search_graph;
    

and it will be internally rewritten to the above form. The `CYCLE` clause
specifies first the list of columns to track for cycle detection, then a
column name that will show whether a cycle has been detected, and finally the
name of another column that will track the path. The cycle and path columns
will implicitly be added to the output rows of the CTE.

### Tip

The cycle path column is computed in the same way as the depth-first ordering
column show in the previous section. A query can have both a `SEARCH` and a
`CYCLE` clause, but a depth-first search specification and a cycle detection
specification would create redundant computations, so it's more efficient to
just use the `CYCLE` clause and order by the path column. If breadth-first
ordering is wanted, then specifying both `SEARCH` and `CYCLE` can be useful.

A helpful trick for testing queries when you are not certain if they might
loop is to place a `LIMIT` in the parent query. For example, this query would
loop forever without the `LIMIT`:

    
    
    WITH RECURSIVE t(n) AS (
        SELECT 1
      UNION ALL
        SELECT n+1 FROM t
    )
    SELECT n FROM t **LIMIT 100** ;
    

This works because PostgreSQL's implementation evaluates only as many rows of
a `WITH` query as are actually fetched by the parent query. Using this trick
in production is not recommended, because other systems might work
differently. Also, it usually won't work if you make the outer query sort the
recursive query's results or join them to some other table, because in such
cases the outer query will usually try to fetch all of the `WITH` query's
output anyway.

### 7.8.3. Common Table Expression Materialization #

A useful property of `WITH` queries is that they are normally evaluated only
once per execution of the parent query, even if they are referred to more than
once by the parent query or sibling `WITH` queries. Thus, expensive
calculations that are needed in multiple places can be placed within a `WITH`
query to avoid redundant work. Another possible application is to prevent
unwanted multiple evaluations of functions with side-effects. However, the
other side of this coin is that the optimizer is not able to push restrictions
from the parent query down into a multiply-referenced `WITH` query, since that
might affect all uses of the `WITH` query's output when it should affect only
one. The multiply-referenced `WITH` query will be evaluated as written,
without suppression of rows that the parent query might discard afterwards.
(But, as mentioned above, evaluation might stop early if the reference(s) to
the query demand only a limited number of rows.)

However, if a `WITH` query is non-recursive and side-effect-free (that is, it
is a `SELECT` containing no volatile functions) then it can be folded into the
parent query, allowing joint optimization of the two query levels. By default,
this happens if the parent query references the `WITH` query just once, but
not if it references the `WITH` query more than once. You can override that
decision by specifying `MATERIALIZED` to force separate calculation of the
`WITH` query, or by specifying `NOT MATERIALIZED` to force it to be merged
into the parent query. The latter choice risks duplicate computation of the
`WITH` query, but it can still give a net savings if each usage of the `WITH`
query needs only a small part of the `WITH` query's full output.

A simple example of these rules is

    
    
    WITH w AS (
        SELECT * FROM big_table
    )
    SELECT * FROM w WHERE key = 123;
    

This `WITH` query will be folded, producing the same execution plan as

    
    
    SELECT * FROM big_table WHERE key = 123;
    

In particular, if there's an index on `key`, it will probably be used to fetch
just the rows having `key = 123`. On the other hand, in

    
    
    WITH w AS (
        SELECT * FROM big_table
    )
    SELECT * FROM w AS w1 JOIN w AS w2 ON w1.key = w2.ref
    WHERE w2.key = 123;
    

the `WITH` query will be materialized, producing a temporary copy of
`big_table` that is then joined with itself — without benefit of any index.
This query will be executed much more efficiently if written as

    
    
    WITH w AS NOT MATERIALIZED (
        SELECT * FROM big_table
    )
    SELECT * FROM w AS w1 JOIN w AS w2 ON w1.key = w2.ref
    WHERE w2.key = 123;
    

so that the parent query's restrictions can be applied directly to scans of
`big_table`.

An example where `NOT MATERIALIZED` could be undesirable is

    
    
    WITH w AS (
        SELECT key, very_expensive_function(val) as f FROM some_table
    )
    SELECT * FROM w AS w1 JOIN w AS w2 ON w1.f = w2.f;
    

Here, materialization of the `WITH` query ensures that
`very_expensive_function` is evaluated only once per table row, not twice.

The examples above only show `WITH` being used with `SELECT`, but it can be
attached in the same way to `INSERT`, `UPDATE`, `DELETE`, or `MERGE`. In each
case it effectively provides temporary table(s) that can be referred to in the
main command.

### 7.8.4. Data-Modifying Statements in `WITH` #

You can use most data-modifying statements (`INSERT`, `UPDATE`, or `DELETE`,
but not `MERGE`) in `WITH`. This allows you to perform several different
operations in the same query. An example is:

    
    
    WITH moved_rows AS (
        DELETE FROM products
        WHERE
            "date" >= '2010-10-01' AND
            "date" < '2010-11-01'
        RETURNING *
    )
    INSERT INTO products_log
    SELECT * FROM moved_rows;
    

This query effectively moves rows from `products` to `products_log`. The
`DELETE` in `WITH` deletes the specified rows from `products`, returning their
contents by means of its `RETURNING` clause; and then the primary query reads
that output and inserts it into `products_log`.

A fine point of the above example is that the `WITH` clause is attached to the
`INSERT`, not the sub-`SELECT` within the `INSERT`. This is necessary because
data-modifying statements are only allowed in `WITH` clauses that are attached
to the top-level statement. However, normal `WITH` visibility rules apply, so
it is possible to refer to the `WITH` statement's output from the
sub-`SELECT`.

Data-modifying statements in `WITH` usually have `RETURNING` clauses (see
[Section 6.4](dml-returning.html "6.4. Returning Data from Modified Rows")),
as shown in the example above. It is the output of the `RETURNING` clause,
_not_ the target table of the data-modifying statement, that forms the
temporary table that can be referred to by the rest of the query. If a data-
modifying statement in `WITH` lacks a `RETURNING` clause, then it forms no
temporary table and cannot be referred to in the rest of the query. Such a
statement will be executed nonetheless. A not-particularly-useful example is:

    
    
    WITH t AS (
        DELETE FROM foo
    )
    DELETE FROM bar;
    

This example would remove all rows from tables `foo` and `bar`. The number of
affected rows reported to the client would only include rows removed from
`bar`.

Recursive self-references in data-modifying statements are not allowed. In
some cases it is possible to work around this limitation by referring to the
output of a recursive `WITH`, for example:

    
    
    WITH RECURSIVE included_parts(sub_part, part) AS (
        SELECT sub_part, part FROM parts WHERE part = 'our_product'
      UNION ALL
        SELECT p.sub_part, p.part
        FROM included_parts pr, parts p
        WHERE p.part = pr.sub_part
    )
    DELETE FROM parts
      WHERE part IN (SELECT part FROM included_parts);
    

This query would remove all direct and indirect subparts of a product.

Data-modifying statements in `WITH` are executed exactly once, and always to
completion, independently of whether the primary query reads all (or indeed
any) of their output. Notice that this is different from the rule for `SELECT`
in `WITH`: as stated in the previous section, execution of a `SELECT` is
carried only as far as the primary query demands its output.

The sub-statements in `WITH` are executed concurrently with each other and
with the main query. Therefore, when using data-modifying statements in
`WITH`, the order in which the specified updates actually happen is
unpredictable. All the statements are executed with the same _snapshot_ (see
[Chapter 13](mvcc.html "Chapter 13. Concurrency Control")), so they cannot
“see” one another's effects on the target tables. This alleviates the effects
of the unpredictability of the actual order of row updates, and means that
`RETURNING` data is the only way to communicate changes between different
`WITH` sub-statements and the main query. An example of this is that in

    
    
    WITH t AS (
        UPDATE products SET price = price * 1.05
        RETURNING *
    )
    SELECT * FROM products;
    

the outer `SELECT` would return the original prices before the action of the
`UPDATE`, while in

    
    
    WITH t AS (
        UPDATE products SET price = price * 1.05
        RETURNING *
    )
    SELECT * FROM t;
    

the outer `SELECT` would return the updated data.

Trying to update the same row twice in a single statement is not supported.
Only one of the modifications takes place, but it is not easy (and sometimes
not possible) to reliably predict which one. This also applies to deleting a
row that was already updated in the same statement: only the update is
performed. Therefore you should generally avoid trying to modify a single row
twice in a single statement. In particular avoid writing `WITH` sub-statements
that could affect the same rows changed by the main statement or a sibling
sub-statement. The effects of such a statement will not be predictable.

At present, any table used as the target of a data-modifying statement in
`WITH` must not have a conditional rule, nor an `ALSO` rule, nor an `INSTEAD`
rule that expands to multiple statements.

* * *

[Prev](queries-values.html "7.7. VALUES Lists")  | [Up](queries.html "Chapter 7. Queries") |  [Next](datatype.html "Chapter 8. Data Types")  
---|---|---  
7.7. `VALUES` Lists  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 8. Data Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-with.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

