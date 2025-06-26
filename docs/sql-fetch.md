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

Supported Versions: [Current](/docs/current/sql-fetch.html "PostgreSQL 17 -
FETCH") ([17](/docs/17/sql-fetch.html "PostgreSQL 17 - FETCH")) /
[16](/docs/16/sql-fetch.html "PostgreSQL 16 - FETCH") / [15](/docs/15/sql-
fetch.html "PostgreSQL 15 - FETCH") / [14](/docs/14/sql-fetch.html "PostgreSQL
14 - FETCH") / [13](/docs/13/sql-fetch.html "PostgreSQL 13 - FETCH")

Development Versions: [18](/docs/18/sql-fetch.html "PostgreSQL 18 - FETCH") /
[devel](/docs/devel/sql-fetch.html "PostgreSQL devel - FETCH")

Unsupported versions: [12](/docs/12/sql-fetch.html "PostgreSQL 12 - FETCH") /
[11](/docs/11/sql-fetch.html "PostgreSQL 11 - FETCH") / [10](/docs/10/sql-
fetch.html "PostgreSQL 10 - FETCH") / [9.6](/docs/9.6/sql-fetch.html
"PostgreSQL 9.6 - FETCH") / [9.5](/docs/9.5/sql-fetch.html "PostgreSQL 9.5 -
FETCH") / [9.4](/docs/9.4/sql-fetch.html "PostgreSQL 9.4 - FETCH") /
[9.3](/docs/9.3/sql-fetch.html "PostgreSQL 9.3 - FETCH") /
[9.2](/docs/9.2/sql-fetch.html "PostgreSQL 9.2 - FETCH") /
[9.1](/docs/9.1/sql-fetch.html "PostgreSQL 9.1 - FETCH") /
[9.0](/docs/9.0/sql-fetch.html "PostgreSQL 9.0 - FETCH") /
[8.4](/docs/8.4/sql-fetch.html "PostgreSQL 8.4 - FETCH") /
[8.3](/docs/8.3/sql-fetch.html "PostgreSQL 8.3 - FETCH") /
[8.2](/docs/8.2/sql-fetch.html "PostgreSQL 8.2 - FETCH") /
[8.1](/docs/8.1/sql-fetch.html "PostgreSQL 8.1 - FETCH") /
[8.0](/docs/8.0/sql-fetch.html "PostgreSQL 8.0 - FETCH") /
[7.4](/docs/7.4/sql-fetch.html "PostgreSQL 7.4 - FETCH") /
[7.3](/docs/7.3/sql-fetch.html "PostgreSQL 7.3 - FETCH") /
[7.2](/docs/7.2/sql-fetch.html "PostgreSQL 7.2 - FETCH") /
[7.1](/docs/7.1/sql-fetch.html "PostgreSQL 7.1 - FETCH")

__

FETCH  
---  
[Prev](sql-explain.html "EXPLAIN")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-grant.html "GRANT")  
  
* * *

## FETCH

FETCH — retrieve rows from a query using a cursor

## Synopsis

    
    
    FETCH [ _direction_ ] [ FROM | IN ] _cursor_name_
    
    where _direction_ can be one of:
    
        NEXT
        PRIOR
        FIRST
        LAST
        ABSOLUTE _count_
        RELATIVE _count_
        _count_
        ALL
        FORWARD
        FORWARD _count_
        FORWARD ALL
        BACKWARD
        BACKWARD _count_
        BACKWARD ALL
    

## Description

`FETCH` retrieves rows using a previously-created cursor.

A cursor has an associated position, which is used by `FETCH`. The cursor
position can be before the first row of the query result, on any particular
row of the result, or after the last row of the result. When created, a cursor
is positioned before the first row. After fetching some rows, the cursor is
positioned on the row most recently retrieved. If `FETCH` runs off the end of
the available rows then the cursor is left positioned after the last row, or
before the first row if fetching backward. `FETCH ALL` or `FETCH BACKWARD ALL`
will always leave the cursor positioned after the last row or before the first
row.

The forms `NEXT`, `PRIOR`, `FIRST`, `LAST`, `ABSOLUTE`, `RELATIVE` fetch a
single row after moving the cursor appropriately. If there is no such row, an
empty result is returned, and the cursor is left positioned before the first
row or after the last row as appropriate.

The forms using `FORWARD` and `BACKWARD` retrieve the indicated number of rows
moving in the forward or backward direction, leaving the cursor positioned on
the last-returned row (or after/before all rows, if the _`count`_ exceeds the
number of rows available).

`RELATIVE 0`, `FORWARD 0`, and `BACKWARD 0` all request fetching the current
row without moving the cursor, that is, re-fetching the most recently fetched
row. This will succeed unless the cursor is positioned before the first row or
after the last row; in which case, no row is returned.

### Note

This page describes usage of cursors at the SQL command level. If you are
trying to use cursors inside a PL/pgSQL function, the rules are different —
see [Section 43.7.3](plpgsql-cursors.html#PLPGSQL-CURSOR-USING "43.7.3. Using
Cursors").

## Parameters

_`direction`_

    

_`direction`_ defines the fetch direction and number of rows to fetch. It can
be one of the following:

`NEXT`

    

Fetch the next row. This is the default if _`direction`_ is omitted.

`PRIOR`

    

Fetch the prior row.

`FIRST`

    

Fetch the first row of the query (same as `ABSOLUTE 1`).

`LAST`

    

Fetch the last row of the query (same as `ABSOLUTE -1`).

`ABSOLUTE _`count`_`

    

Fetch the _`count`_ 'th row of the query, or the `abs(_`count`_)`'th row from
the end if _`count`_ is negative. Position before first row or after last row
if _`count`_ is out of range; in particular, `ABSOLUTE 0` positions before the
first row.

`RELATIVE _`count`_`

    

Fetch the _`count`_ 'th succeeding row, or the `abs(_`count`_)`'th prior row
if _`count`_ is negative. `RELATIVE 0` re-fetches the current row, if any.

_`count`_

    

Fetch the next _`count`_ rows (same as `FORWARD _`count`_`).

`ALL`

    

Fetch all remaining rows (same as `FORWARD ALL`).

`FORWARD`

    

Fetch the next row (same as `NEXT`).

`FORWARD _`count`_`

    

Fetch the next _`count`_ rows. `FORWARD 0` re-fetches the current row.

`FORWARD ALL`

    

Fetch all remaining rows.

`BACKWARD`

    

Fetch the prior row (same as `PRIOR`).

`BACKWARD _`count`_`

    

Fetch the prior _`count`_ rows (scanning backwards). `BACKWARD 0` re-fetches
the current row.

`BACKWARD ALL`

    

Fetch all prior rows (scanning backwards).

_`count`_

    

_`count`_ is a possibly-signed integer constant, determining the location or
number of rows to fetch. For `FORWARD` and `BACKWARD` cases, specifying a
negative _`count`_ is equivalent to changing the sense of `FORWARD` and
`BACKWARD`.

_`cursor_name`_

    

An open cursor's name.

## Outputs

On successful completion, a `FETCH` command returns a command tag of the form

    
    
    FETCH _count_
    

The _`count`_ is the number of rows fetched (possibly zero). Note that in
psql, the command tag will not actually be displayed, since psql displays the
fetched rows instead.

## Notes

The cursor should be declared with the `SCROLL` option if one intends to use
any variants of `FETCH` other than `FETCH NEXT` or `FETCH FORWARD` with a
positive count. For simple queries PostgreSQL will allow backwards fetch from
cursors not declared with `SCROLL`, but this behavior is best not relied on.
If the cursor is declared with `NO SCROLL`, no backward fetches are allowed.

`ABSOLUTE` fetches are not any faster than navigating to the desired row with
a relative move: the underlying implementation must traverse all the
intermediate rows anyway. Negative absolute fetches are even worse: the query
must be read to the end to find the last row, and then traversed backward from
there. However, rewinding to the start of the query (as with `FETCH ABSOLUTE
0`) is fast.

[`DECLARE`](sql-declare.html "DECLARE") is used to define a cursor. Use
[`MOVE`](sql-move.html "MOVE") to change cursor position without retrieving
data.

## Examples

The following example traverses a table using a cursor:

    
    
    BEGIN WORK;
    
    -- Set up a cursor:
    DECLARE liahona SCROLL CURSOR FOR SELECT * FROM films;
    
    -- Fetch the first 5 rows in the cursor liahona:
    FETCH FORWARD 5 FROM liahona;
    
     code  |          title          | did | date_prod  |   kind   |  len
    -------+-------------------------+-----+------------+----------+-------
     BL101 | The Third Man           | 101 | 1949-12-23 | Drama    | 01:44
     BL102 | The African Queen       | 101 | 1951-08-11 | Romantic | 01:43
     JL201 | Une Femme est une Femme | 102 | 1961-03-12 | Romantic | 01:25
     P_301 | Vertigo                 | 103 | 1958-11-14 | Action   | 02:08
     P_302 | Becket                  | 103 | 1964-02-03 | Drama    | 02:28
    
    -- Fetch the previous row:
    FETCH PRIOR FROM liahona;
    
     code  |  title  | did | date_prod  |  kind  |  len
    -------+---------+-----+------------+--------+-------
     P_301 | Vertigo | 103 | 1958-11-14 | Action | 02:08
    
    -- Close the cursor and end the transaction:
    CLOSE liahona;
    COMMIT WORK;
    

## Compatibility

The SQL standard defines `FETCH` for use in embedded SQL only. The variant of
`FETCH` described here returns the data as if it were a `SELECT` result rather
than placing it in host variables. Other than this point, `FETCH` is fully
upward-compatible with the SQL standard.

The `FETCH` forms involving `FORWARD` and `BACKWARD`, as well as the forms
`FETCH _`count`_` and `FETCH ALL`, in which `FORWARD` is implicit, are
PostgreSQL extensions.

The SQL standard allows only `FROM` preceding the cursor name; the option to
use `IN`, or to leave them out altogether, is an extension.

## See Also

[CLOSE](sql-close.html "CLOSE"), [DECLARE](sql-declare.html "DECLARE"),
[MOVE](sql-move.html "MOVE")

* * *

[Prev](sql-explain.html "EXPLAIN")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-grant.html "GRANT")  
---|---|---  
EXPLAIN  | [Home](index.html "PostgreSQL 16.9 Documentation") |  GRANT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-fetch.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

