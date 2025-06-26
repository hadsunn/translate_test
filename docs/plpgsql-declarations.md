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

Supported Versions: [Current](/docs/current/plpgsql-declarations.html
"PostgreSQL 17 - 43.3. Declarations") ([17](/docs/17/plpgsql-declarations.html
"PostgreSQL 17 - 43.3. Declarations")) / [16](/docs/16/plpgsql-
declarations.html "PostgreSQL 16 - 43.3. Declarations") /
[15](/docs/15/plpgsql-declarations.html "PostgreSQL 15 - 43.3. Declarations")
/ [14](/docs/14/plpgsql-declarations.html "PostgreSQL 14 -
43.3. Declarations") / [13](/docs/13/plpgsql-declarations.html "PostgreSQL 13
- 43.3. Declarations")

Development Versions: [18](/docs/18/plpgsql-declarations.html "PostgreSQL 18 -
43.3. Declarations") / [devel](/docs/devel/plpgsql-declarations.html
"PostgreSQL devel - 43.3. Declarations")

Unsupported versions: [12](/docs/12/plpgsql-declarations.html "PostgreSQL 12 -
43.3. Declarations") / [11](/docs/11/plpgsql-declarations.html "PostgreSQL 11
- 43.3. Declarations") / [10](/docs/10/plpgsql-declarations.html "PostgreSQL
10 - 43.3. Declarations") / [9.6](/docs/9.6/plpgsql-declarations.html
"PostgreSQL 9.6 - 43.3. Declarations") / [9.5](/docs/9.5/plpgsql-
declarations.html "PostgreSQL 9.5 - 43.3. Declarations") /
[9.4](/docs/9.4/plpgsql-declarations.html "PostgreSQL 9.4 -
43.3. Declarations") / [9.3](/docs/9.3/plpgsql-declarations.html "PostgreSQL
9.3 - 43.3. Declarations") / [9.2](/docs/9.2/plpgsql-declarations.html
"PostgreSQL 9.2 - 43.3. Declarations") / [9.1](/docs/9.1/plpgsql-
declarations.html "PostgreSQL 9.1 - 43.3. Declarations") /
[9.0](/docs/9.0/plpgsql-declarations.html "PostgreSQL 9.0 -
43.3. Declarations") / [8.4](/docs/8.4/plpgsql-declarations.html "PostgreSQL
8.4 - 43.3. Declarations") / [8.3](/docs/8.3/plpgsql-declarations.html
"PostgreSQL 8.3 - 43.3. Declarations") / [8.2](/docs/8.2/plpgsql-
declarations.html "PostgreSQL 8.2 - 43.3. Declarations") /
[8.1](/docs/8.1/plpgsql-declarations.html "PostgreSQL 8.1 -
43.3. Declarations") / [8.0](/docs/8.0/plpgsql-declarations.html "PostgreSQL
8.0 - 43.3. Declarations") / [7.4](/docs/7.4/plpgsql-declarations.html
"PostgreSQL 7.4 - 43.3. Declarations") / [7.3](/docs/7.3/plpgsql-
declarations.html "PostgreSQL 7.3 - 43.3. Declarations") /
[7.2](/docs/7.2/plpgsql-declarations.html "PostgreSQL 7.2 -
43.3. Declarations")

__

43.3. Declarations  
---  
[Prev](plpgsql-structure.html "43.2. Structure of PL/pgSQL")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-expressions.html "43.4. Expressions")  
  
* * *

## 43.3. Declarations #

[43.3.1. Declaring Function Parameters](plpgsql-declarations.html#PLPGSQL-
DECLARATION-PARAMETERS)

[43.3.2. `ALIAS`](plpgsql-declarations.html#PLPGSQL-DECLARATION-ALIAS)

[43.3.3. Copying Types](plpgsql-declarations.html#PLPGSQL-DECLARATION-TYPE)

[43.3.4. Row Types](plpgsql-declarations.html#PLPGSQL-DECLARATION-ROWTYPES)

[43.3.5. Record Types](plpgsql-declarations.html#PLPGSQL-DECLARATION-RECORDS)

[43.3.6. Collation of PL/pgSQL Variables](plpgsql-declarations.html#PLPGSQL-
DECLARATION-COLLATION)

All variables used in a block must be declared in the declarations section of
the block. (The only exceptions are that the loop variable of a `FOR` loop
iterating over a range of integer values is automatically declared as an
integer variable, and likewise the loop variable of a `FOR` loop iterating
over a cursor's result is automatically declared as a record variable.)

PL/pgSQL variables can have any SQL data type, such as `integer`, `varchar`,
and `char`.

Here are some examples of variable declarations:

    
    
    user_id integer;
    quantity numeric(5);
    url varchar;
    myrow tablename%ROWTYPE;
    myfield tablename.columnname%TYPE;
    arow RECORD;
    

The general syntax of a variable declaration is:

    
    
    _name_ [ CONSTANT ] _type_ [ COLLATE _collation_name_ ] [ NOT NULL ] [ { DEFAULT | := | = } _expression_ ];
    

The `DEFAULT` clause, if given, specifies the initial value assigned to the
variable when the block is entered. If the `DEFAULT` clause is not given then
the variable is initialized to the SQL null value. The `CONSTANT` option
prevents the variable from being assigned to after initialization, so that its
value will remain constant for the duration of the block. The `COLLATE` option
specifies a collation to use for the variable (see [Section 43.3.6](plpgsql-
declarations.html#PLPGSQL-DECLARATION-COLLATION "43.3.6. Collation of PL/pgSQL
Variables")). If `NOT NULL` is specified, an assignment of a null value
results in a run-time error. All variables declared as `NOT NULL` must have a
nonnull default value specified. Equal (`=`) can be used instead of PL/SQL-
compliant `:=`.

A variable's default value is evaluated and assigned to the variable each time
the block is entered (not just once per function call). So, for example,
assigning `now()` to a variable of type `timestamp` causes the variable to
have the time of the current function call, not the time when the function was
precompiled.

Examples:

    
    
    quantity integer DEFAULT 32;
    url varchar := 'http://mysite.com';
    transaction_time CONSTANT timestamp with time zone := now();
    

Once declared, a variable's value can be used in later initialization
expressions in the same block, for example:

    
    
    DECLARE
      x integer := 1;
      y integer := x + 1;
    

### 43.3.1. Declaring Function Parameters #

Parameters passed to functions are named with the identifiers `$1`, `$2`, etc.
Optionally, aliases can be declared for `$_`n`_` parameter names for increased
readability. Either the alias or the numeric identifier can then be used to
refer to the parameter value.

There are two ways to create an alias. The preferred way is to give a name to
the parameter in the `CREATE FUNCTION` command, for example:

    
    
    CREATE FUNCTION sales_tax(subtotal real) RETURNS real AS $$
    BEGIN
        RETURN subtotal * 0.06;
    END;
    $$ LANGUAGE plpgsql;
    

The other way is to explicitly declare an alias, using the declaration syntax

    
    
    _name_ ALIAS FOR $_n_ ;
    

The same example in this style looks like:

    
    
    CREATE FUNCTION sales_tax(real) RETURNS real AS $$
    DECLARE
        subtotal ALIAS FOR $1;
    BEGIN
        RETURN subtotal * 0.06;
    END;
    $$ LANGUAGE plpgsql;
    

### Note

These two examples are not perfectly equivalent. In the first case, `subtotal`
could be referenced as `sales_tax.subtotal`, but in the second case it could
not. (Had we attached a label to the inner block, `subtotal` could be
qualified with that label, instead.)

Some more examples:

    
    
    CREATE FUNCTION instr(varchar, integer) RETURNS integer AS $$
    DECLARE
        v_string ALIAS FOR $1;
        index ALIAS FOR $2;
    BEGIN
        -- some computations using v_string and index here
    END;
    $$ LANGUAGE plpgsql;
    
    
    CREATE FUNCTION concat_selected_fields(in_t sometablename) RETURNS text AS $$
    BEGIN
        RETURN in_t.f1 || in_t.f3 || in_t.f5 || in_t.f7;
    END;
    $$ LANGUAGE plpgsql;
    

When a PL/pgSQL function is declared with output parameters, the output
parameters are given `$_`n`_` names and optional aliases in just the same way
as the normal input parameters. An output parameter is effectively a variable
that starts out NULL; it should be assigned to during the execution of the
function. The final value of the parameter is what is returned. For instance,
the sales-tax example could also be done this way:

    
    
    CREATE FUNCTION sales_tax(subtotal real, OUT tax real) AS $$
    BEGIN
        tax := subtotal * 0.06;
    END;
    $$ LANGUAGE plpgsql;
    

Notice that we omitted `RETURNS real` — we could have included it, but it
would be redundant.

To call a function with `OUT` parameters, omit the output parameter(s) in the
function call:

    
    
    SELECT sales_tax(100.00);
    

Output parameters are most useful when returning multiple values. A trivial
example is:

    
    
    CREATE FUNCTION sum_n_product(x int, y int, OUT sum int, OUT prod int) AS $$
    BEGIN
        sum := x + y;
        prod := x * y;
    END;
    $$ LANGUAGE plpgsql;
    
    SELECT * FROM sum_n_product(2, 4);
     sum | prod
    -----+------
       6 |    8
    

As discussed in [Section 38.5.4](xfunc-sql.html#XFUNC-OUTPUT-PARAMETERS
"38.5.4. SQL Functions with Output Parameters"), this effectively creates an
anonymous record type for the function's results. If a `RETURNS` clause is
given, it must say `RETURNS record`.

This also works with procedures, for example:

    
    
    CREATE PROCEDURE sum_n_product(x int, y int, OUT sum int, OUT prod int) AS $$
    BEGIN
        sum := x + y;
        prod := x * y;
    END;
    $$ LANGUAGE plpgsql;
    

In a call to a procedure, all the parameters must be specified. For output
parameters, `NULL` may be specified when calling the procedure from plain SQL:

    
    
    CALL sum_n_product(2, 4, NULL, NULL);
     sum | prod
    -----+------
       6 |    8
    

However, when calling a procedure from PL/pgSQL, you should instead write a
variable for any output parameter; the variable will receive the result of the
call. See [Section 43.6.3](plpgsql-control-structures.html#PLPGSQL-STATEMENTS-
CALLING-PROCEDURE "43.6.3. Calling a Procedure") for details.

Another way to declare a PL/pgSQL function is with `RETURNS TABLE`, for
example:

    
    
    CREATE FUNCTION extended_sales(p_itemno int)
    RETURNS TABLE(quantity int, total numeric) AS $$
    BEGIN
        RETURN QUERY SELECT s.quantity, s.quantity * s.price FROM sales AS s
                     WHERE s.itemno = p_itemno;
    END;
    $$ LANGUAGE plpgsql;
    

This is exactly equivalent to declaring one or more `OUT` parameters and
specifying `RETURNS SETOF _`sometype`_`.

When the return type of a PL/pgSQL function is declared as a polymorphic type
(see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC
"38.2.5. Polymorphic Types")), a special parameter `$0` is created. Its data
type is the actual return type of the function, as deduced from the actual
input types. This allows the function to access its actual return type as
shown in [Section 43.3.3](plpgsql-declarations.html#PLPGSQL-DECLARATION-TYPE
"43.3.3. Copying Types"). `$0` is initialized to null and can be modified by
the function, so it can be used to hold the return value if desired, though
that is not required. `$0` can also be given an alias. For example, this
function works on any data type that has a `+` operator:

    
    
    CREATE FUNCTION add_three_values(v1 anyelement, v2 anyelement, v3 anyelement)
    RETURNS anyelement AS $$
    DECLARE
        result ALIAS FOR $0;
    BEGIN
        result := v1 + v2 + v3;
        RETURN result;
    END;
    $$ LANGUAGE plpgsql;
    

The same effect can be obtained by declaring one or more output parameters as
polymorphic types. In this case the special `$0` parameter is not used; the
output parameters themselves serve the same purpose. For example:

    
    
    CREATE FUNCTION add_three_values(v1 anyelement, v2 anyelement, v3 anyelement,
                                     OUT sum anyelement)
    AS $$
    BEGIN
        sum := v1 + v2 + v3;
    END;
    $$ LANGUAGE plpgsql;
    

In practice it might be more useful to declare a polymorphic function using
the `anycompatible` family of types, so that automatic promotion of the input
arguments to a common type will occur. For example:

    
    
    CREATE FUNCTION add_three_values(v1 anycompatible, v2 anycompatible, v3 anycompatible)
    RETURNS anycompatible AS $$
    BEGIN
        RETURN v1 + v2 + v3;
    END;
    $$ LANGUAGE plpgsql;
    

With this example, a call such as

    
    
    SELECT add_three_values(1, 2, 4.7);
    

will work, automatically promoting the integer inputs to numeric. The function
using `anyelement` would require you to cast the three inputs to the same type
manually.

### 43.3.2. `ALIAS` #

    
    
    _newname_ ALIAS FOR _oldname_ ;
    

The `ALIAS` syntax is more general than is suggested in the previous section:
you can declare an alias for any variable, not just function parameters. The
main practical use for this is to assign a different name for variables with
predetermined names, such as `NEW` or `OLD` within a trigger function.

Examples:

    
    
    DECLARE
      prior ALIAS FOR old;
      updated ALIAS FOR new;
    

Since `ALIAS` creates two different ways to name the same object, unrestricted
use can be confusing. It's best to use it only for the purpose of overriding
predetermined names.

### 43.3.3. Copying Types #

    
    
    _variable_ %TYPE
    

`%TYPE` provides the data type of a variable or table column. You can use this
to declare variables that will hold database values. For example, let's say
you have a column named `user_id` in your `users` table. To declare a variable
with the same data type as `users.user_id` you write:

    
    
    user_id users.user_id%TYPE;
    

By using `%TYPE` you don't need to know the data type of the structure you are
referencing, and most importantly, if the data type of the referenced item
changes in the future (for instance: you change the type of `user_id` from
`integer` to `real`), you might not need to change your function definition.

`%TYPE` is particularly valuable in polymorphic functions, since the data
types needed for internal variables can change from one call to the next.
Appropriate variables can be created by applying `%TYPE` to the function's
arguments or result placeholders.

### 43.3.4. Row Types #

    
    
    _name_ _table_name_%ROWTYPE;
    _name_ _composite_type_name_ ;
    

A variable of a composite type is called a _row_ variable (or _row-type_
variable). Such a variable can hold a whole row of a `SELECT` or `FOR` query
result, so long as that query's column set matches the declared type of the
variable. The individual fields of the row value are accessed using the usual
dot notation, for example `rowvar.field`.

A row variable can be declared to have the same type as the rows of an
existing table or view, by using the _`table_name`_`%ROWTYPE` notation; or it
can be declared by giving a composite type's name. (Since every table has an
associated composite type of the same name, it actually does not matter in
PostgreSQL whether you write `%ROWTYPE` or not. But the form with `%ROWTYPE`
is more portable.)

Parameters to a function can be composite types (complete table rows). In that
case, the corresponding identifier `$_`n`_` will be a row variable, and fields
can be selected from it, for example `$1.user_id`.

Here is an example of using composite types. `table1` and `table2` are
existing tables having at least the mentioned fields:

    
    
    CREATE FUNCTION merge_fields(t_row table1) RETURNS text AS $$
    DECLARE
        t2_row table2%ROWTYPE;
    BEGIN
        SELECT * INTO t2_row FROM table2 WHERE ... ;
        RETURN t_row.f1 || t2_row.f3 || t_row.f5 || t2_row.f7;
    END;
    $$ LANGUAGE plpgsql;
    
    SELECT merge_fields(t.*) FROM table1 t WHERE ... ;
    

### 43.3.5. Record Types #

    
    
    _name_ RECORD;
    

Record variables are similar to row-type variables, but they have no
predefined structure. They take on the actual row structure of the row they
are assigned during a `SELECT` or `FOR` command. The substructure of a record
variable can change each time it is assigned to. A consequence of this is that
until a record variable is first assigned to, it has no substructure, and any
attempt to access a field in it will draw a run-time error.

Note that `RECORD` is not a true data type, only a placeholder. One should
also realize that when a PL/pgSQL function is declared to return type
`record`, this is not quite the same concept as a record variable, even though
such a function might use a record variable to hold its result. In both cases
the actual row structure is unknown when the function is written, but for a
function returning `record` the actual structure is determined when the
calling query is parsed, whereas a record variable can change its row
structure on-the-fly.

### 43.3.6. Collation of PL/pgSQL Variables #

When a PL/pgSQL function has one or more parameters of collatable data types,
a collation is identified for each function call depending on the collations
assigned to the actual arguments, as described in [Section
24.2](collation.html "24.2. Collation Support"). If a collation is
successfully identified (i.e., there are no conflicts of implicit collations
among the arguments) then all the collatable parameters are treated as having
that collation implicitly. This will affect the behavior of collation-
sensitive operations within the function. For example, consider

    
    
    CREATE FUNCTION less_than(a text, b text) RETURNS boolean AS $$
    BEGIN
        RETURN a < b;
    END;
    $$ LANGUAGE plpgsql;
    
    SELECT less_than(text_field_1, text_field_2) FROM table1;
    SELECT less_than(text_field_1, text_field_2 COLLATE "C") FROM table1;
    

The first use of `less_than` will use the common collation of `text_field_1`
and `text_field_2` for the comparison, while the second use will use `C`
collation.

Furthermore, the identified collation is also assumed as the collation of any
local variables that are of collatable types. Thus this function would not
work any differently if it were written as

    
    
    CREATE FUNCTION less_than(a text, b text) RETURNS boolean AS $$
    DECLARE
        local_a text := a;
        local_b text := b;
    BEGIN
        RETURN local_a < local_b;
    END;
    $$ LANGUAGE plpgsql;
    

If there are no parameters of collatable data types, or no common collation
can be identified for them, then parameters and local variables use the
default collation of their data type (which is usually the database's default
collation, but could be different for variables of domain types).

A local variable of a collatable data type can have a different collation
associated with it by including the `COLLATE` option in its declaration, for
example

    
    
    DECLARE
        local_a text COLLATE "en_US";
    

This option overrides the collation that would otherwise be given to the
variable according to the rules above.

Also, of course explicit `COLLATE` clauses can be written inside a function if
it is desired to force a particular collation to be used in a particular
operation. For example,

    
    
    CREATE FUNCTION less_than_c(a text, b text) RETURNS boolean AS $$
    BEGIN
        RETURN a < b COLLATE "C";
    END;
    $$ LANGUAGE plpgsql;
    

This overrides the collations associated with the table columns, parameters,
or local variables used in the expression, just as would happen in a plain SQL
command.

* * *

[Prev](plpgsql-structure.html "43.2. Structure of PL/pgSQL")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-expressions.html "43.4. Expressions")  
---|---|---  
43.2. Structure of PL/pgSQL  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.4. Expressions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-declarations.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

