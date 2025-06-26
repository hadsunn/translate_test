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

Supported Versions: [Current](/docs/current/sql-syntax-calling-funcs.html
"PostgreSQL 17 - 4.3. Calling Functions") ([17](/docs/17/sql-syntax-calling-
funcs.html "PostgreSQL 17 - 4.3. Calling Functions")) / [16](/docs/16/sql-
syntax-calling-funcs.html "PostgreSQL 16 - 4.3. Calling Functions") /
[15](/docs/15/sql-syntax-calling-funcs.html "PostgreSQL 15 - 4.3. Calling
Functions") / [14](/docs/14/sql-syntax-calling-funcs.html "PostgreSQL 14 -
4.3. Calling Functions") / [13](/docs/13/sql-syntax-calling-funcs.html
"PostgreSQL 13 - 4.3. Calling Functions")

Development Versions: [18](/docs/18/sql-syntax-calling-funcs.html "PostgreSQL
18 - 4.3. Calling Functions") / [devel](/docs/devel/sql-syntax-calling-
funcs.html "PostgreSQL devel - 4.3. Calling Functions")

Unsupported versions: [12](/docs/12/sql-syntax-calling-funcs.html "PostgreSQL
12 - 4.3. Calling Functions") / [11](/docs/11/sql-syntax-calling-funcs.html
"PostgreSQL 11 - 4.3. Calling Functions") / [10](/docs/10/sql-syntax-calling-
funcs.html "PostgreSQL 10 - 4.3. Calling Functions") / [9.6](/docs/9.6/sql-
syntax-calling-funcs.html "PostgreSQL 9.6 - 4.3. Calling Functions") /
[9.5](/docs/9.5/sql-syntax-calling-funcs.html "PostgreSQL 9.5 - 4.3. Calling
Functions") / [9.4](/docs/9.4/sql-syntax-calling-funcs.html "PostgreSQL 9.4 -
4.3. Calling Functions") / [9.3](/docs/9.3/sql-syntax-calling-funcs.html
"PostgreSQL 9.3 - 4.3. Calling Functions") / [9.2](/docs/9.2/sql-syntax-
calling-funcs.html "PostgreSQL 9.2 - 4.3. Calling Functions") /
[9.1](/docs/9.1/sql-syntax-calling-funcs.html "PostgreSQL 9.1 - 4.3. Calling
Functions") / [9.0](/docs/9.0/sql-syntax-calling-funcs.html "PostgreSQL 9.0 -
4.3. Calling Functions")

__

4.3. Calling Functions  
---  
[Prev](sql-expressions.html "4.2. Value Expressions")  | [Up](sql-syntax.html "Chapter 4. SQL Syntax") | Chapter 4. SQL Syntax | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl.html "Chapter 5. Data Definition")  
  
* * *

## 4.3. Calling Functions #

[4.3.1. Using Positional Notation](sql-syntax-calling-funcs.html#SQL-SYNTAX-
CALLING-FUNCS-POSITIONAL)

[4.3.2. Using Named Notation](sql-syntax-calling-funcs.html#SQL-SYNTAX-
CALLING-FUNCS-NAMED)

[4.3.3. Using Mixed Notation](sql-syntax-calling-funcs.html#SQL-SYNTAX-
CALLING-FUNCS-MIXED)

PostgreSQL allows functions that have named parameters to be called using
either _positional_ or _named_ notation. Named notation is especially useful
for functions that have a large number of parameters, since it makes the
associations between parameters and actual arguments more explicit and
reliable. In positional notation, a function call is written with its argument
values in the same order as they are defined in the function declaration. In
named notation, the arguments are matched to the function parameters by name
and can be written in any order. For each notation, also consider the effect
of function argument types, documented in [Section 10.3](typeconv-func.html
"10.3. Functions").

In either notation, parameters that have default values given in the function
declaration need not be written in the call at all. But this is particularly
useful in named notation, since any combination of parameters can be omitted;
while in positional notation parameters can only be omitted from right to
left.

PostgreSQL also supports _mixed_ notation, which combines positional and named
notation. In this case, positional parameters are written first and named
parameters appear after them.

The following examples will illustrate the usage of all three notations, using
the following function definition:

    
    
    CREATE FUNCTION concat_lower_or_upper(a text, b text, uppercase boolean DEFAULT false)
    RETURNS text
    AS
    $$
     SELECT CASE
            WHEN $3 THEN UPPER($1 || ' ' || $2)
            ELSE LOWER($1 || ' ' || $2)
            END;
    $$
    LANGUAGE SQL IMMUTABLE STRICT;
    

Function `concat_lower_or_upper` has two mandatory parameters, `a` and `b`.
Additionally there is one optional parameter `uppercase` which defaults to
`false`. The `a` and `b` inputs will be concatenated, and forced to either
upper or lower case depending on the `uppercase` parameter. The remaining
details of this function definition are not important here (see [Chapter
38](extend.html "Chapter 38. Extending SQL") for more information).

### 4.3.1. Using Positional Notation #

Positional notation is the traditional mechanism for passing arguments to
functions in PostgreSQL. An example is:

    
    
    SELECT concat_lower_or_upper('Hello', 'World', true);
     concat_lower_or_upper
    -----------------------
     HELLO WORLD
    (1 row)
    

All arguments are specified in order. The result is upper case since
`uppercase` is specified as `true`. Another example is:

    
    
    SELECT concat_lower_or_upper('Hello', 'World');
     concat_lower_or_upper
    -----------------------
     hello world
    (1 row)
    

Here, the `uppercase` parameter is omitted, so it receives its default value
of `false`, resulting in lower case output. In positional notation, arguments
can be omitted from right to left so long as they have defaults.

### 4.3.2. Using Named Notation #

In named notation, each argument's name is specified using `=>` to separate it
from the argument expression. For example:

    
    
    SELECT concat_lower_or_upper(a => 'Hello', b => 'World');
     concat_lower_or_upper
    -----------------------
     hello world
    (1 row)
    

Again, the argument `uppercase` was omitted so it is set to `false`
implicitly. One advantage of using named notation is that the arguments may be
specified in any order, for example:

    
    
    SELECT concat_lower_or_upper(a => 'Hello', b => 'World', uppercase => true);
     concat_lower_or_upper
    -----------------------
     HELLO WORLD
    (1 row)
    
    SELECT concat_lower_or_upper(a => 'Hello', uppercase => true, b => 'World');
     concat_lower_or_upper
    -----------------------
     HELLO WORLD
    (1 row)
    

An older syntax based on ":=" is supported for backward compatibility:

    
    
    SELECT concat_lower_or_upper(a := 'Hello', uppercase := true, b := 'World');
     concat_lower_or_upper
    -----------------------
     HELLO WORLD
    (1 row)
    

### 4.3.3. Using Mixed Notation #

The mixed notation combines positional and named notation. However, as already
mentioned, named arguments cannot precede positional arguments. For example:

    
    
    SELECT concat_lower_or_upper('Hello', 'World', uppercase => true);
     concat_lower_or_upper
    -----------------------
     HELLO WORLD
    (1 row)
    

In the above query, the arguments `a` and `b` are specified positionally,
while `uppercase` is specified by name. In this example, that adds little
except documentation. With a more complex function having numerous parameters
that have default values, named or mixed notation can save a great deal of
writing and reduce chances for error.

### Note

Named and mixed call notations currently cannot be used when calling an
aggregate function (but they do work when an aggregate function is used as a
window function).

* * *

[Prev](sql-expressions.html "4.2. Value Expressions")  | [Up](sql-syntax.html "Chapter 4. SQL Syntax") |  [Next](ddl.html "Chapter 5. Data Definition")  
---|---|---  
4.2. Value Expressions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 5. Data Definition  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-syntax-calling-
funcs.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

