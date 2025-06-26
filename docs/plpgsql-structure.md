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

Supported Versions: [Current](/docs/current/plpgsql-structure.html "PostgreSQL
17 - 43.2. Structure of PL/pgSQL") ([17](/docs/17/plpgsql-structure.html
"PostgreSQL 17 - 43.2. Structure of PL/pgSQL")) / [16](/docs/16/plpgsql-
structure.html "PostgreSQL 16 - 43.2. Structure of PL/pgSQL") /
[15](/docs/15/plpgsql-structure.html "PostgreSQL 15 - 43.2. Structure of
PL/pgSQL") / [14](/docs/14/plpgsql-structure.html "PostgreSQL 14 -
43.2. Structure of PL/pgSQL") / [13](/docs/13/plpgsql-structure.html
"PostgreSQL 13 - 43.2. Structure of PL/pgSQL")

Development Versions: [18](/docs/18/plpgsql-structure.html "PostgreSQL 18 -
43.2. Structure of PL/pgSQL") / [devel](/docs/devel/plpgsql-structure.html
"PostgreSQL devel - 43.2. Structure of PL/pgSQL")

Unsupported versions: [12](/docs/12/plpgsql-structure.html "PostgreSQL 12 -
43.2. Structure of PL/pgSQL") / [11](/docs/11/plpgsql-structure.html
"PostgreSQL 11 - 43.2. Structure of PL/pgSQL") / [10](/docs/10/plpgsql-
structure.html "PostgreSQL 10 - 43.2. Structure of PL/pgSQL") /
[9.6](/docs/9.6/plpgsql-structure.html "PostgreSQL 9.6 - 43.2. Structure of
PL/pgSQL") / [9.5](/docs/9.5/plpgsql-structure.html "PostgreSQL 9.5 -
43.2. Structure of PL/pgSQL") / [9.4](/docs/9.4/plpgsql-structure.html
"PostgreSQL 9.4 - 43.2. Structure of PL/pgSQL") / [9.3](/docs/9.3/plpgsql-
structure.html "PostgreSQL 9.3 - 43.2. Structure of PL/pgSQL") /
[9.2](/docs/9.2/plpgsql-structure.html "PostgreSQL 9.2 - 43.2. Structure of
PL/pgSQL") / [9.1](/docs/9.1/plpgsql-structure.html "PostgreSQL 9.1 -
43.2. Structure of PL/pgSQL") / [9.0](/docs/9.0/plpgsql-structure.html
"PostgreSQL 9.0 - 43.2. Structure of PL/pgSQL") / [8.4](/docs/8.4/plpgsql-
structure.html "PostgreSQL 8.4 - 43.2. Structure of PL/pgSQL") /
[8.3](/docs/8.3/plpgsql-structure.html "PostgreSQL 8.3 - 43.2. Structure of
PL/pgSQL") / [8.2](/docs/8.2/plpgsql-structure.html "PostgreSQL 8.2 -
43.2. Structure of PL/pgSQL") / [8.1](/docs/8.1/plpgsql-structure.html
"PostgreSQL 8.1 - 43.2. Structure of PL/pgSQL") / [8.0](/docs/8.0/plpgsql-
structure.html "PostgreSQL 8.0 - 43.2. Structure of PL/pgSQL") /
[7.4](/docs/7.4/plpgsql-structure.html "PostgreSQL 7.4 - 43.2. Structure of
PL/pgSQL") / [7.3](/docs/7.3/plpgsql-structure.html "PostgreSQL 7.3 -
43.2. Structure of PL/pgSQL") / [7.2](/docs/7.2/plpgsql-structure.html
"PostgreSQL 7.2 - 43.2. Structure of PL/pgSQL")

__

43.2. Structure of PL/pgSQL  
---  
[Prev](plpgsql-overview.html "43.1. Overview")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-declarations.html "43.3. Declarations")  
  
* * *

## 43.2. Structure of PL/pgSQL #

Functions written in PL/pgSQL are defined to the server by executing [CREATE
FUNCTION](sql-createfunction.html "CREATE FUNCTION") commands. Such a command
would normally look like, say,

    
    
    CREATE FUNCTION somefunc(integer, text) RETURNS integer
    AS '_function body text_ '
    LANGUAGE plpgsql;
    

The function body is simply a string literal so far as `CREATE FUNCTION` is
concerned. It is often helpful to use dollar quoting (see [Section
4.1.2.4](sql-syntax-lexical.html#SQL-SYNTAX-DOLLAR-QUOTING "4.1.2.4. Dollar-
Quoted String Constants")) to write the function body, rather than the normal
single quote syntax. Without dollar quoting, any single quotes or backslashes
in the function body must be escaped by doubling them. Almost all the examples
in this chapter use dollar-quoted literals for their function bodies.

PL/pgSQL is a block-structured language. The complete text of a function body
must be a _block_. A block is defined as:

    
    
    [ <<_label_ >> ]
    [ DECLARE
        _declarations_ ]
    BEGIN
        _statements_
    END [ _label_ ];
    

Each declaration and each statement within a block is terminated by a
semicolon. A block that appears within another block must have a semicolon
after `END`, as shown above; however the final `END` that concludes a function
body does not require a semicolon.

### Tip

A common mistake is to write a semicolon immediately after `BEGIN`. This is
incorrect and will result in a syntax error.

A _`label`_ is only needed if you want to identify the block for use in an
`EXIT` statement, or to qualify the names of the variables declared in the
block. If a label is given after `END`, it must match the label at the block's
beginning.

All key words are case-insensitive. Identifiers are implicitly converted to
lower case unless double-quoted, just as they are in ordinary SQL commands.

Comments work the same way in PL/pgSQL code as in ordinary SQL. A double dash
(`--`) starts a comment that extends to the end of the line. A `/*` starts a
block comment that extends to the matching occurrence of `*/`. Block comments
nest.

Any statement in the statement section of a block can be a _subblock_.
Subblocks can be used for logical grouping or to localize variables to a small
group of statements. Variables declared in a subblock mask any similarly-named
variables of outer blocks for the duration of the subblock; but you can access
the outer variables anyway if you qualify their names with their block's
label. For example:

    
    
    CREATE FUNCTION somefunc() RETURNS integer AS $$
    << outerblock >>
    DECLARE
        quantity integer := 30;
    BEGIN
        RAISE NOTICE 'Quantity here is %', quantity;  -- Prints 30
        quantity := 50;
        --
        -- Create a subblock
        --
        DECLARE
            quantity integer := 80;
        BEGIN
            RAISE NOTICE 'Quantity here is %', quantity;  -- Prints 80
            RAISE NOTICE 'Outer quantity here is %', outerblock.quantity;  -- Prints 50
        END;
    
        RAISE NOTICE 'Quantity here is %', quantity;  -- Prints 50
    
        RETURN quantity;
    END;
    $$ LANGUAGE plpgsql;
    

### Note

There is actually a hidden “outer block” surrounding the body of any PL/pgSQL
function. This block provides the declarations of the function's parameters
(if any), as well as some special variables such as `FOUND` (see [Section
43.5.5](plpgsql-statements.html#PLPGSQL-STATEMENTS-DIAGNOSTICS
"43.5.5. Obtaining the Result Status")). The outer block is labeled with the
function's name, meaning that parameters and special variables can be
qualified with the function's name.

It is important not to confuse the use of `BEGIN`/`END` for grouping
statements in PL/pgSQL with the similarly-named SQL commands for transaction
control. PL/pgSQL's `BEGIN`/`END` are only for grouping; they do not start or
end a transaction. See [Section 43.8](plpgsql-transactions.html
"43.8. Transaction Management") for information on managing transactions in
PL/pgSQL. Also, a block containing an `EXCEPTION` clause effectively forms a
subtransaction that can be rolled back without affecting the outer
transaction. For more about that see [Section 43.6.8](plpgsql-control-
structures.html#PLPGSQL-ERROR-TRAPPING "43.6.8. Trapping Errors").

* * *

[Prev](plpgsql-overview.html "43.1. Overview")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-declarations.html "43.3. Declarations")  
---|---|---  
43.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.3. Declarations  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-structure.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

