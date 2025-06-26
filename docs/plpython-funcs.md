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

Supported Versions: [Current](/docs/current/plpython-funcs.html "PostgreSQL 17
- 46.1. PL/Python Functions") ([17](/docs/17/plpython-funcs.html "PostgreSQL
17 - 46.1. PL/Python Functions")) / [16](/docs/16/plpython-funcs.html
"PostgreSQL 16 - 46.1. PL/Python Functions") / [15](/docs/15/plpython-
funcs.html "PostgreSQL 15 - 46.1. PL/Python Functions") /
[14](/docs/14/plpython-funcs.html "PostgreSQL 14 - 46.1. PL/Python Functions")
/ [13](/docs/13/plpython-funcs.html "PostgreSQL 13 - 46.1. PL/Python
Functions")

Development Versions: [18](/docs/18/plpython-funcs.html "PostgreSQL 18 -
46.1. PL/Python Functions") / [devel](/docs/devel/plpython-funcs.html
"PostgreSQL devel - 46.1. PL/Python Functions")

Unsupported versions: [12](/docs/12/plpython-funcs.html "PostgreSQL 12 -
46.1. PL/Python Functions") / [11](/docs/11/plpython-funcs.html "PostgreSQL 11
- 46.1. PL/Python Functions") / [10](/docs/10/plpython-funcs.html "PostgreSQL
10 - 46.1. PL/Python Functions") / [9.6](/docs/9.6/plpython-funcs.html
"PostgreSQL 9.6 - 46.1. PL/Python Functions") / [9.5](/docs/9.5/plpython-
funcs.html "PostgreSQL 9.5 - 46.1. PL/Python Functions") /
[9.4](/docs/9.4/plpython-funcs.html "PostgreSQL 9.4 - 46.1. PL/Python
Functions") / [9.3](/docs/9.3/plpython-funcs.html "PostgreSQL 9.3 -
46.1. PL/Python Functions") / [9.2](/docs/9.2/plpython-funcs.html "PostgreSQL
9.2 - 46.1. PL/Python Functions") / [9.1](/docs/9.1/plpython-funcs.html
"PostgreSQL 9.1 - 46.1. PL/Python Functions") / [9.0](/docs/9.0/plpython-
funcs.html "PostgreSQL 9.0 - 46.1. PL/Python Functions") /
[8.4](/docs/8.4/plpython-funcs.html "PostgreSQL 8.4 - 46.1. PL/Python
Functions") / [8.3](/docs/8.3/plpython-funcs.html "PostgreSQL 8.3 -
46.1. PL/Python Functions") / [8.2](/docs/8.2/plpython-funcs.html "PostgreSQL
8.2 - 46.1. PL/Python Functions")

__

46.1. PL/Python Functions  
---  
[Prev](plpython.html "Chapter 46. PL/Python — Python Procedural Language")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-data.html "46.2. Data Values")  
  
* * *

## 46.1. PL/Python Functions #

Functions in PL/Python are declared via the standard [CREATE FUNCTION](sql-
createfunction.html "CREATE FUNCTION") syntax:

    
    
    CREATE FUNCTION _funcname_ (_argument-list_)
      RETURNS _return-type_
    AS $$
      # PL/Python function body
    $$ LANGUAGE plpython3u;
    

The body of a function is simply a Python script. When the function is called,
its arguments are passed as elements of the list `args`; named arguments are
also passed as ordinary variables to the Python script. Use of named arguments
is usually more readable. The result is returned from the Python code in the
usual way, with `return` or `yield` (in case of a result-set statement). If
you do not provide a return value, Python returns the default `None`.
PL/Python translates Python's `None` into the SQL null value. In a procedure,
the result from the Python code must be `None` (typically achieved by ending
the procedure without a `return` statement or by using a `return` statement
without argument); otherwise, an error will be raised.

For example, a function to return the greater of two integers can be defined
as:

    
    
    CREATE FUNCTION pymax (a integer, b integer)
      RETURNS integer
    AS $$
      if a > b:
        return a
      return b
    $$ LANGUAGE plpython3u;
    

The Python code that is given as the body of the function definition is
transformed into a Python function. For example, the above results in:

    
    
    def __plpython_procedure_pymax_23456():
      if a > b:
        return a
      return b
    

assuming that 23456 is the OID assigned to the function by PostgreSQL.

The arguments are set as global variables. Because of the scoping rules of
Python, this has the subtle consequence that an argument variable cannot be
reassigned inside the function to the value of an expression that involves the
variable name itself, unless the variable is redeclared as global in the
block. For example, the following won't work:

    
    
    CREATE FUNCTION pystrip(x text)
      RETURNS text
    AS $$
      x = x.strip()  # error
      return x
    $$ LANGUAGE plpython3u;
    

because assigning to `x` makes `x` a local variable for the entire block, and
so the `x` on the right-hand side of the assignment refers to a not-yet-
assigned local variable `x`, not the PL/Python function parameter. Using the
`global` statement, this can be made to work:

    
    
    CREATE FUNCTION pystrip(x text)
      RETURNS text
    AS $$
      global x
      x = x.strip()  # ok now
      return x
    $$ LANGUAGE plpython3u;
    

But it is advisable not to rely on this implementation detail of PL/Python. It
is better to treat the function parameters as read-only.

* * *

[Prev](plpython.html "Chapter 46. PL/Python — Python Procedural Language")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-data.html "46.2. Data Values")  
---|---|---  
Chapter 46. PL/Python — Python Procedural Language  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.2. Data Values  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-funcs.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

