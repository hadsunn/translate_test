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

Supported Versions: [Current](/docs/current/pltcl-functions.html "PostgreSQL
17 - 44.2. PL/Tcl Functions and Arguments") ([17](/docs/17/pltcl-
functions.html "PostgreSQL 17 - 44.2. PL/Tcl Functions and Arguments")) /
[16](/docs/16/pltcl-functions.html "PostgreSQL 16 - 44.2. PL/Tcl Functions and
Arguments") / [15](/docs/15/pltcl-functions.html "PostgreSQL 15 - 44.2. PL/Tcl
Functions and Arguments") / [14](/docs/14/pltcl-functions.html "PostgreSQL 14
- 44.2. PL/Tcl Functions and Arguments") / [13](/docs/13/pltcl-functions.html
"PostgreSQL 13 - 44.2. PL/Tcl Functions and Arguments")

Development Versions: [18](/docs/18/pltcl-functions.html "PostgreSQL 18 -
44.2. PL/Tcl Functions and Arguments") / [devel](/docs/devel/pltcl-
functions.html "PostgreSQL devel - 44.2. PL/Tcl Functions and Arguments")

Unsupported versions: [12](/docs/12/pltcl-functions.html "PostgreSQL 12 -
44.2. PL/Tcl Functions and Arguments") / [11](/docs/11/pltcl-functions.html
"PostgreSQL 11 - 44.2. PL/Tcl Functions and Arguments") / [10](/docs/10/pltcl-
functions.html "PostgreSQL 10 - 44.2. PL/Tcl Functions and Arguments") /
[9.6](/docs/9.6/pltcl-functions.html "PostgreSQL 9.6 - 44.2. PL/Tcl Functions
and Arguments") / [9.5](/docs/9.5/pltcl-functions.html "PostgreSQL 9.5 -
44.2. PL/Tcl Functions and Arguments") / [9.4](/docs/9.4/pltcl-functions.html
"PostgreSQL 9.4 - 44.2. PL/Tcl Functions and Arguments") /
[9.3](/docs/9.3/pltcl-functions.html "PostgreSQL 9.3 - 44.2. PL/Tcl Functions
and Arguments") / [9.2](/docs/9.2/pltcl-functions.html "PostgreSQL 9.2 -
44.2. PL/Tcl Functions and Arguments") / [9.1](/docs/9.1/pltcl-functions.html
"PostgreSQL 9.1 - 44.2. PL/Tcl Functions and Arguments") /
[9.0](/docs/9.0/pltcl-functions.html "PostgreSQL 9.0 - 44.2. PL/Tcl Functions
and Arguments") / [8.4](/docs/8.4/pltcl-functions.html "PostgreSQL 8.4 -
44.2. PL/Tcl Functions and Arguments") / [8.3](/docs/8.3/pltcl-functions.html
"PostgreSQL 8.3 - 44.2. PL/Tcl Functions and Arguments") /
[8.2](/docs/8.2/pltcl-functions.html "PostgreSQL 8.2 - 44.2. PL/Tcl Functions
and Arguments") / [8.1](/docs/8.1/pltcl-functions.html "PostgreSQL 8.1 -
44.2. PL/Tcl Functions and Arguments") / [8.0](/docs/8.0/pltcl-functions.html
"PostgreSQL 8.0 - 44.2. PL/Tcl Functions and Arguments") /
[7.4](/docs/7.4/pltcl-functions.html "PostgreSQL 7.4 - 44.2. PL/Tcl Functions
and Arguments")

__

44.2. PL/Tcl Functions and Arguments  
---  
[Prev](pltcl-overview.html "44.1. Overview")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-data.html "44.3. Data Values in PL/Tcl")  
  
* * *

## 44.2. PL/Tcl Functions and Arguments #

To create a function in the PL/Tcl language, use the standard [CREATE
FUNCTION](sql-createfunction.html "CREATE FUNCTION") syntax:

    
    
    CREATE FUNCTION _funcname_ (_argument-types_) RETURNS _return-type_ AS $$
        # PL/Tcl function body
    $$ LANGUAGE pltcl;
    

PL/TclU is the same, except that the language has to be specified as `pltclu`.

The body of the function is simply a piece of Tcl script. When the function is
called, the argument values are passed to the Tcl script as variables named
`1` ... `_`n`_`. The result is returned from the Tcl code in the usual way,
with a `return` statement. In a procedure, the return value from the Tcl code
is ignored.

For example, a function returning the greater of two integer values could be
defined as:

    
    
    CREATE FUNCTION tcl_max(integer, integer) RETURNS integer AS $$
        if {$1 > $2} {return $1}
        return $2
    $$ LANGUAGE pltcl STRICT;
    

Note the clause `STRICT`, which saves us from having to think about null input
values: if a null value is passed, the function will not be called at all, but
will just return a null result automatically.

In a nonstrict function, if the actual value of an argument is null, the
corresponding `$_`n`_` variable will be set to an empty string. To detect
whether a particular argument is null, use the function `argisnull`. For
example, suppose that we wanted `tcl_max` with one null and one nonnull
argument to return the nonnull argument, rather than null:

    
    
    CREATE FUNCTION tcl_max(integer, integer) RETURNS integer AS $$
        if {[argisnull 1]} {
            if {[argisnull 2]} { return_null }
            return $2
        }
        if {[argisnull 2]} { return $1 }
        if {$1 > $2} {return $1}
        return $2
    $$ LANGUAGE pltcl;
    

As shown above, to return a null value from a PL/Tcl function, execute
`return_null`. This can be done whether the function is strict or not.

Composite-type arguments are passed to the function as Tcl arrays. The element
names of the array are the attribute names of the composite type. If an
attribute in the passed row has the null value, it will not appear in the
array. Here is an example:

    
    
    CREATE TABLE employee (
        name text,
        salary integer,
        age integer
    );
    
    CREATE FUNCTION overpaid(employee) RETURNS boolean AS $$
        if {200000.0 < $1(salary)} {
            return "t"
        }
        if {$1(age) < 30 && 100000.0 < $1(salary)} {
            return "t"
        }
        return "f"
    $$ LANGUAGE pltcl;
    

PL/Tcl functions can return composite-type results, too. To do this, the Tcl
code must return a list of column name/value pairs matching the expected
result type. Any column names omitted from the list are returned as nulls, and
an error is raised if there are unexpected column names. Here is an example:

    
    
    CREATE FUNCTION square_cube(in int, out squared int, out cubed int) AS $$
        return [list squared [expr {$1 * $1}] cubed [expr {$1 * $1 * $1}]]
    $$ LANGUAGE pltcl;
    

Output arguments of procedures are returned in the same way, for example:

    
    
    CREATE PROCEDURE tcl_triple(INOUT a integer, INOUT b integer) AS $$
        return [list a [expr {$1 * 3}] b [expr {$2 * 3}]]
    $$ LANGUAGE pltcl;
    
    CALL tcl_triple(5, 10);
    

### Tip

The result list can be made from an array representation of the desired tuple
with the `array get` Tcl command. For example:

    
    
    CREATE FUNCTION raise_pay(employee, delta int) RETURNS employee AS $$
        set 1(salary) [expr {$1(salary) + $2}]
        return [array get 1]
    $$ LANGUAGE pltcl;
    

PL/Tcl functions can return sets. To do this, the Tcl code should call
`return_next` once per row to be returned, passing either the appropriate
value when returning a scalar type, or a list of column name/value pairs when
returning a composite type. Here is an example returning a scalar type:

    
    
    CREATE FUNCTION sequence(int, int) RETURNS SETOF int AS $$
        for {set i $1} {$i < $2} {incr i} {
            return_next $i
        }
    $$ LANGUAGE pltcl;
    

and here is one returning a composite type:

    
    
    CREATE FUNCTION table_of_squares(int, int) RETURNS TABLE (x int, x2 int) AS $$
        for {set i $1} {$i < $2} {incr i} {
            return_next [list x $i x2 [expr {$i * $i}]]
        }
    $$ LANGUAGE pltcl;
    

* * *

[Prev](pltcl-overview.html "44.1. Overview")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-data.html "44.3. Data Values in PL/Tcl")  
---|---|---  
44.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.3. Data Values in PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-functions.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

