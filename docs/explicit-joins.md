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

Supported Versions: [Current](/docs/current/explicit-joins.html "PostgreSQL 17
- 14.3. Controlling the Planner with Explicit JOIN Clauses")
([17](/docs/17/explicit-joins.html "PostgreSQL 17 - 14.3. Controlling the
Planner with Explicit JOIN Clauses")) / [16](/docs/16/explicit-joins.html
"PostgreSQL 16 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[15](/docs/15/explicit-joins.html "PostgreSQL 15 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [14](/docs/14/explicit-joins.html
"PostgreSQL 14 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[13](/docs/13/explicit-joins.html "PostgreSQL 13 - 14.3. Controlling the
Planner with Explicit JOIN Clauses")

Development Versions: [18](/docs/18/explicit-joins.html "PostgreSQL 18 -
14.3. Controlling the Planner with Explicit JOIN Clauses") /
[devel](/docs/devel/explicit-joins.html "PostgreSQL devel - 14.3. Controlling
the Planner with Explicit JOIN Clauses")

Unsupported versions: [12](/docs/12/explicit-joins.html "PostgreSQL 12 -
14.3. Controlling the Planner with Explicit JOIN Clauses") /
[11](/docs/11/explicit-joins.html "PostgreSQL 11 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [10](/docs/10/explicit-joins.html
"PostgreSQL 10 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[9.6](/docs/9.6/explicit-joins.html "PostgreSQL 9.6 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [9.5](/docs/9.5/explicit-joins.html
"PostgreSQL 9.5 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[9.4](/docs/9.4/explicit-joins.html "PostgreSQL 9.4 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [9.3](/docs/9.3/explicit-joins.html
"PostgreSQL 9.3 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[9.2](/docs/9.2/explicit-joins.html "PostgreSQL 9.2 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [9.1](/docs/9.1/explicit-joins.html
"PostgreSQL 9.1 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[9.0](/docs/9.0/explicit-joins.html "PostgreSQL 9.0 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [8.4](/docs/8.4/explicit-joins.html
"PostgreSQL 8.4 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[8.3](/docs/8.3/explicit-joins.html "PostgreSQL 8.3 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [8.2](/docs/8.2/explicit-joins.html
"PostgreSQL 8.2 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[8.1](/docs/8.1/explicit-joins.html "PostgreSQL 8.1 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [8.0](/docs/8.0/explicit-joins.html
"PostgreSQL 8.0 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[7.4](/docs/7.4/explicit-joins.html "PostgreSQL 7.4 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [7.3](/docs/7.3/explicit-joins.html
"PostgreSQL 7.3 - 14.3. Controlling the Planner with Explicit JOIN Clauses") /
[7.2](/docs/7.2/explicit-joins.html "PostgreSQL 7.2 - 14.3. Controlling the
Planner with Explicit JOIN Clauses") / [7.1](/docs/7.1/explicit-joins.html
"PostgreSQL 7.1 - 14.3. Controlling the Planner with Explicit JOIN Clauses")

__

14.3. Controlling the Planner with Explicit `JOIN` Clauses  
---  
[Prev](planner-stats.html "14.2. Statistics Used by the Planner")  | [Up](performance-tips.html "Chapter 14. Performance Tips") | Chapter 14. Performance Tips | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](populate.html "14.4. Populating a Database")  
  
* * *

## 14.3. Controlling the Planner with Explicit `JOIN` Clauses #

It is possible to control the query planner to some extent by using the
explicit `JOIN` syntax. To see why this matters, we first need some
background.

In a simple join query, such as:

    
    
    SELECT * FROM a, b, c WHERE a.id = b.id AND b.ref = c.id;
    

the planner is free to join the given tables in any order. For example, it
could generate a query plan that joins A to B, using the `WHERE` condition
`a.id = b.id`, and then joins C to this joined table, using the other `WHERE`
condition. Or it could join B to C and then join A to that result. Or it could
join A to C and then join them with B — but that would be inefficient, since
the full Cartesian product of A and C would have to be formed, there being no
applicable condition in the `WHERE` clause to allow optimization of the join.
(All joins in the PostgreSQL executor happen between two input tables, so it's
necessary to build up the result in one or another of these fashions.) The
important point is that these different join possibilities give semantically
equivalent results but might have hugely different execution costs. Therefore,
the planner will explore all of them to try to find the most efficient query
plan.

When a query only involves two or three tables, there aren't many join orders
to worry about. But the number of possible join orders grows exponentially as
the number of tables expands. Beyond ten or so input tables it's no longer
practical to do an exhaustive search of all the possibilities, and even for
six or seven tables planning might take an annoyingly long time. When there
are too many input tables, the PostgreSQL planner will switch from exhaustive
search to a _genetic_ probabilistic search through a limited number of
possibilities. (The switch-over threshold is set by the
[geqo_threshold](runtime-config-query.html#GUC-GEQO-THRESHOLD) run-time
parameter.) The genetic search takes less time, but it won't necessarily find
the best possible plan.

When the query involves outer joins, the planner has less freedom than it does
for plain (inner) joins. For example, consider:

    
    
    SELECT * FROM a LEFT JOIN (b JOIN c ON (b.ref = c.id)) ON (a.id = b.id);
    

Although this query's restrictions are superficially similar to the previous
example, the semantics are different because a row must be emitted for each
row of A that has no matching row in the join of B and C. Therefore the
planner has no choice of join order here: it must join B to C and then join A
to that result. Accordingly, this query takes less time to plan than the
previous query. In other cases, the planner might be able to determine that
more than one join order is safe. For example, given:

    
    
    SELECT * FROM a LEFT JOIN b ON (a.bid = b.id) LEFT JOIN c ON (a.cid = c.id);
    

it is valid to join A to either B or C first. Currently, only `FULL JOIN`
completely constrains the join order. Most practical cases involving `LEFT
JOIN` or `RIGHT JOIN` can be rearranged to some extent.

Explicit inner join syntax (`INNER JOIN`, `CROSS JOIN`, or unadorned `JOIN`)
is semantically the same as listing the input relations in `FROM`, so it does
not constrain the join order.

Even though most kinds of `JOIN` don't completely constrain the join order, it
is possible to instruct the PostgreSQL query planner to treat all `JOIN`
clauses as constraining the join order anyway. For example, these three
queries are logically equivalent:

    
    
    SELECT * FROM a, b, c WHERE a.id = b.id AND b.ref = c.id;
    SELECT * FROM a CROSS JOIN b CROSS JOIN c WHERE a.id = b.id AND b.ref = c.id;
    SELECT * FROM a JOIN (b JOIN c ON (b.ref = c.id)) ON (a.id = b.id);
    

But if we tell the planner to honor the `JOIN` order, the second and third
take less time to plan than the first. This effect is not worth worrying about
for only three tables, but it can be a lifesaver with many tables.

To force the planner to follow the join order laid out by explicit `JOIN`s,
set the [join_collapse_limit](runtime-config-query.html#GUC-JOIN-COLLAPSE-
LIMIT) run-time parameter to 1. (Other possible values are discussed below.)

You do not need to constrain the join order completely in order to cut search
time, because it's OK to use `JOIN` operators within items of a plain `FROM`
list. For example, consider:

    
    
    SELECT * FROM a CROSS JOIN b, c, d, e WHERE ...;
    

With `join_collapse_limit` = 1, this forces the planner to join A to B before
joining them to other tables, but doesn't constrain its choices otherwise. In
this example, the number of possible join orders is reduced by a factor of 5.

Constraining the planner's search in this way is a useful technique both for
reducing planning time and for directing the planner to a good query plan. If
the planner chooses a bad join order by default, you can force it to choose a
better order via `JOIN` syntax — assuming that you know of a better order,
that is. Experimentation is recommended.

A closely related issue that affects planning time is collapsing of subqueries
into their parent query. For example, consider:

    
    
    SELECT *
    FROM x, y,
        (SELECT * FROM a, b, c WHERE something) AS ss
    WHERE somethingelse;
    

This situation might arise from use of a view that contains a join; the view's
`SELECT` rule will be inserted in place of the view reference, yielding a
query much like the above. Normally, the planner will try to collapse the
subquery into the parent, yielding:

    
    
    SELECT * FROM x, y, a, b, c WHERE something AND somethingelse;
    

This usually results in a better plan than planning the subquery separately.
(For example, the outer `WHERE` conditions might be such that joining X to A
first eliminates many rows of A, thus avoiding the need to form the full
logical output of the subquery.) But at the same time, we have increased the
planning time; here, we have a five-way join problem replacing two separate
three-way join problems. Because of the exponential growth of the number of
possibilities, this makes a big difference. The planner tries to avoid getting
stuck in huge join search problems by not collapsing a subquery if more than
`from_collapse_limit` `FROM` items would result in the parent query. You can
trade off planning time against quality of plan by adjusting this run-time
parameter up or down.

[from_collapse_limit](runtime-config-query.html#GUC-FROM-COLLAPSE-LIMIT) and
[join_collapse_limit](runtime-config-query.html#GUC-JOIN-COLLAPSE-LIMIT) are
similarly named because they do almost the same thing: one controls when the
planner will “flatten out” subqueries, and the other controls when it will
flatten out explicit joins. Typically you would either set
`join_collapse_limit` equal to `from_collapse_limit` (so that explicit joins
and subqueries act similarly) or set `join_collapse_limit` to 1 (if you want
to control join order with explicit joins). But you might set them differently
if you are trying to fine-tune the trade-off between planning time and run
time.

* * *

[Prev](planner-stats.html "14.2. Statistics Used by the Planner")  | [Up](performance-tips.html "Chapter 14. Performance Tips") |  [Next](populate.html "14.4. Populating a Database")  
---|---|---  
14.2. Statistics Used by the Planner  | [Home](index.html "PostgreSQL 16.9 Documentation") |  14.4. Populating a Database  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/explicit-joins.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

