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

Supported Versions: [Current](/docs/current/sql-values.html "PostgreSQL 17 -
VALUES") ([17](/docs/17/sql-values.html "PostgreSQL 17 - VALUES")) /
[16](/docs/16/sql-values.html "PostgreSQL 16 - VALUES") / [15](/docs/15/sql-
values.html "PostgreSQL 15 - VALUES") / [14](/docs/14/sql-values.html
"PostgreSQL 14 - VALUES") / [13](/docs/13/sql-values.html "PostgreSQL 13 -
VALUES")

Development Versions: [18](/docs/18/sql-values.html "PostgreSQL 18 - VALUES")
/ [devel](/docs/devel/sql-values.html "PostgreSQL devel - VALUES")

Unsupported versions: [12](/docs/12/sql-values.html "PostgreSQL 12 - VALUES")
/ [11](/docs/11/sql-values.html "PostgreSQL 11 - VALUES") / [10](/docs/10/sql-
values.html "PostgreSQL 10 - VALUES") / [9.6](/docs/9.6/sql-values.html
"PostgreSQL 9.6 - VALUES") / [9.5](/docs/9.5/sql-values.html "PostgreSQL 9.5 -
VALUES") / [9.4](/docs/9.4/sql-values.html "PostgreSQL 9.4 - VALUES") /
[9.3](/docs/9.3/sql-values.html "PostgreSQL 9.3 - VALUES") /
[9.2](/docs/9.2/sql-values.html "PostgreSQL 9.2 - VALUES") /
[9.1](/docs/9.1/sql-values.html "PostgreSQL 9.1 - VALUES") /
[9.0](/docs/9.0/sql-values.html "PostgreSQL 9.0 - VALUES") /
[8.4](/docs/8.4/sql-values.html "PostgreSQL 8.4 - VALUES") /
[8.3](/docs/8.3/sql-values.html "PostgreSQL 8.3 - VALUES") /
[8.2](/docs/8.2/sql-values.html "PostgreSQL 8.2 - VALUES")

__

VALUES  
---  
[Prev](sql-vacuum.html "VACUUM")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](reference-client.html "PostgreSQL Client Applications")  
  
* * *

## VALUES

VALUES — compute a set of rows

## Synopsis

    
    
    VALUES ( _expression_ [, ...] ) [, ...]
        [ ORDER BY _sort_expression_ [ ASC | DESC | USING _operator_ ] [, ...] ]
        [ LIMIT { _count_ | ALL } ]
        [ OFFSET _start_ [ ROW | ROWS ] ]
        [ FETCH { FIRST | NEXT } [ _count_ ] { ROW | ROWS } ONLY ]
    

## Description

`VALUES` computes a row value or set of row values specified by value
expressions. It is most commonly used to generate a “constant table” within a
larger command, but it can be used on its own.

When more than one row is specified, all the rows must have the same number of
elements. The data types of the resulting table's columns are determined by
combining the explicit or inferred types of the expressions appearing in that
column, using the same rules as for `UNION` (see [Section 10.5](typeconv-
union-case.html "10.5. UNION, CASE, and Related Constructs")).

Within larger commands, `VALUES` is syntactically allowed anywhere that
`SELECT` is. Because it is treated like a `SELECT` by the grammar, it is
possible to use the `ORDER BY`, `LIMIT` (or equivalently `FETCH FIRST`), and
`OFFSET` clauses with a `VALUES` command.

## Parameters

_`expression`_

    

A constant or expression to compute and insert at the indicated place in the
resulting table (set of rows). In a `VALUES` list appearing at the top level
of an `INSERT`, an _`expression`_ can be replaced by `DEFAULT` to indicate
that the destination column's default value should be inserted. `DEFAULT`
cannot be used when `VALUES` appears in other contexts.

_`sort_expression`_

    

An expression or integer constant indicating how to sort the result rows. This
expression can refer to the columns of the `VALUES` result as `column1`,
`column2`, etc. For more details see [ORDER BY Clause](sql-select.html#SQL-
ORDERBY "ORDER BY Clause") in the [SELECT](sql-select.html "SELECT")
documentation.

_`operator`_

    

A sorting operator. For details see [ORDER BY Clause](sql-select.html#SQL-
ORDERBY "ORDER BY Clause") in the [SELECT](sql-select.html "SELECT")
documentation.

_`count`_

    

The maximum number of rows to return. For details see [LIMIT Clause](sql-
select.html#SQL-LIMIT "LIMIT Clause") in the [SELECT](sql-select.html
"SELECT") documentation.

_`start`_

    

The number of rows to skip before starting to return rows. For details see
[LIMIT Clause](sql-select.html#SQL-LIMIT "LIMIT Clause") in the [SELECT](sql-
select.html "SELECT") documentation.

## Notes

`VALUES` lists with very large numbers of rows should be avoided, as you might
encounter out-of-memory failures or poor performance. `VALUES` appearing
within `INSERT` is a special case (because the desired column types are known
from the `INSERT`'s target table, and need not be inferred by scanning the
`VALUES` list), so it can handle larger lists than are practical in other
contexts.

## Examples

A bare `VALUES` command:

    
    
    VALUES (1, 'one'), (2, 'two'), (3, 'three');
    

This will return a table of two columns and three rows. It's effectively
equivalent to:

    
    
    SELECT 1 AS column1, 'one' AS column2
    UNION ALL
    SELECT 2, 'two'
    UNION ALL
    SELECT 3, 'three';
    

More usually, `VALUES` is used within a larger SQL command. The most common
use is in `INSERT`:

    
    
    INSERT INTO films (code, title, did, date_prod, kind)
        VALUES ('T_601', 'Yojimbo', 106, '1961-06-16', 'Drama');
    

In the context of `INSERT`, entries of a `VALUES` list can be `DEFAULT` to
indicate that the column default should be used here instead of specifying a
value:

    
    
    INSERT INTO films VALUES
        ('UA502', 'Bananas', 105, DEFAULT, 'Comedy', '82 minutes'),
        ('T_601', 'Yojimbo', 106, DEFAULT, 'Drama', DEFAULT);
    

`VALUES` can also be used where a sub-`SELECT` might be written, for example
in a `FROM` clause:

    
    
    SELECT f.*
      FROM films f, (VALUES('MGM', 'Horror'), ('UA', 'Sci-Fi')) AS t (studio, kind)
      WHERE f.studio = t.studio AND f.kind = t.kind;
    
    UPDATE employees SET salary = salary * v.increase
      FROM (VALUES(1, 200000, 1.2), (2, 400000, 1.4)) AS v (depno, target, increase)
      WHERE employees.depno = v.depno AND employees.sales >= v.target;
    

Note that an `AS` clause is required when `VALUES` is used in a `FROM` clause,
just as is true for `SELECT`. It is not required that the `AS` clause specify
names for all the columns, but it's good practice to do so. (The default
column names for `VALUES` are `column1`, `column2`, etc. in PostgreSQL, but
these names might be different in other database systems.)

When `VALUES` is used in `INSERT`, the values are all automatically coerced to
the data type of the corresponding destination column. When it's used in other
contexts, it might be necessary to specify the correct data type. If the
entries are all quoted literal constants, coercing the first is sufficient to
determine the assumed type for all:

    
    
    SELECT * FROM machines
    WHERE ip_address IN (VALUES('192.168.0.1'::inet), ('192.168.0.10'), ('192.168.1.43'));
    

### Tip

For simple `IN` tests, it's better to rely on the [list-of-scalars](functions-
comparisons.html#FUNCTIONS-COMPARISONS-IN-SCALAR "9.24.1. IN") form of `IN`
than to write a `VALUES` query as shown above. The list of scalars method
requires less writing and is often more efficient.

## Compatibility

`VALUES` conforms to the SQL standard. `LIMIT` and `OFFSET` are PostgreSQL
extensions; see also under [SELECT](sql-select.html "SELECT").

## See Also

[INSERT](sql-insert.html "INSERT"), [SELECT](sql-select.html "SELECT")

* * *

[Prev](sql-vacuum.html "VACUUM")  | [Up](sql-commands.html "SQL Commands") |  [Next](reference-client.html "PostgreSQL Client Applications")  
---|---|---  
VACUUM  | [Home](index.html "PostgreSQL 16.9 Documentation") |  PostgreSQL Client Applications  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-values.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

