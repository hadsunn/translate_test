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

Supported Versions: [Current](/docs/current/typeconv-func.html "PostgreSQL 17
- 10.3. Functions") ([17](/docs/17/typeconv-func.html "PostgreSQL 17 -
10.3. Functions")) / [16](/docs/16/typeconv-func.html "PostgreSQL 16 -
10.3. Functions") / [15](/docs/15/typeconv-func.html "PostgreSQL 15 -
10.3. Functions") / [14](/docs/14/typeconv-func.html "PostgreSQL 14 -
10.3. Functions") / [13](/docs/13/typeconv-func.html "PostgreSQL 13 -
10.3. Functions")

Development Versions: [18](/docs/18/typeconv-func.html "PostgreSQL 18 -
10.3. Functions") / [devel](/docs/devel/typeconv-func.html "PostgreSQL devel -
10.3. Functions")

Unsupported versions: [12](/docs/12/typeconv-func.html "PostgreSQL 12 -
10.3. Functions") / [11](/docs/11/typeconv-func.html "PostgreSQL 11 -
10.3. Functions") / [10](/docs/10/typeconv-func.html "PostgreSQL 10 -
10.3. Functions") / [9.6](/docs/9.6/typeconv-func.html "PostgreSQL 9.6 -
10.3. Functions") / [9.5](/docs/9.5/typeconv-func.html "PostgreSQL 9.5 -
10.3. Functions") / [9.4](/docs/9.4/typeconv-func.html "PostgreSQL 9.4 -
10.3. Functions") / [9.3](/docs/9.3/typeconv-func.html "PostgreSQL 9.3 -
10.3. Functions") / [9.2](/docs/9.2/typeconv-func.html "PostgreSQL 9.2 -
10.3. Functions") / [9.1](/docs/9.1/typeconv-func.html "PostgreSQL 9.1 -
10.3. Functions") / [9.0](/docs/9.0/typeconv-func.html "PostgreSQL 9.0 -
10.3. Functions") / [8.4](/docs/8.4/typeconv-func.html "PostgreSQL 8.4 -
10.3. Functions") / [8.3](/docs/8.3/typeconv-func.html "PostgreSQL 8.3 -
10.3. Functions") / [8.2](/docs/8.2/typeconv-func.html "PostgreSQL 8.2 -
10.3. Functions") / [8.1](/docs/8.1/typeconv-func.html "PostgreSQL 8.1 -
10.3. Functions") / [8.0](/docs/8.0/typeconv-func.html "PostgreSQL 8.0 -
10.3. Functions") / [7.4](/docs/7.4/typeconv-func.html "PostgreSQL 7.4 -
10.3. Functions") / [7.3](/docs/7.3/typeconv-func.html "PostgreSQL 7.3 -
10.3. Functions") / [7.2](/docs/7.2/typeconv-func.html "PostgreSQL 7.2 -
10.3. Functions") / [7.1](/docs/7.1/typeconv-func.html "PostgreSQL 7.1 -
10.3. Functions")

__

10.3. Functions  
---  
[Prev](typeconv-oper.html "10.2. Operators")  | [Up](typeconv.html "Chapter 10. Type Conversion") | Chapter 10. Type Conversion | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv-query.html "10.4. Value Storage")  
  
* * *

## 10.3. Functions #

The specific function that is referenced by a function call is determined
using the following procedure.

**Function Type Resolution**

  1. Select the functions to be considered from the `pg_proc` system catalog. If a non-schema-qualified function name was used, the functions considered are those with the matching name and argument count that are visible in the current search path (see [Section 5.9.3](ddl-schemas.html#DDL-SCHEMAS-PATH "5.9.3. The Schema Search Path")). If a qualified function name was given, only functions in the specified schema are considered.

     1. If the search path finds multiple functions of identical argument types, only the one appearing earliest in the path is considered. Functions of different argument types are considered on an equal footing regardless of search path position.

     2. If a function is declared with a `VARIADIC` array parameter, and the call does not use the `VARIADIC` keyword, then the function is treated as if the array parameter were replaced by one or more occurrences of its element type, as needed to match the call. After such expansion the function might have effective argument types identical to some non-variadic function. In that case the function appearing earlier in the search path is used, or if the two functions are in the same schema, the non-variadic one is preferred.

This creates a security hazard when calling, via qualified name [10], a
variadic function found in a schema that permits untrusted users to create
objects. A malicious user can take control and execute arbitrary SQL functions
as though you executed them. Substitute a call bearing the `VARIADIC` keyword,
which bypasses this hazard. Calls populating `VARIADIC "any"` parameters often
have no equivalent formulation containing the `VARIADIC` keyword. To issue
those calls safely, the function's schema must permit only trusted users to
create objects.

     3. Functions that have default values for parameters are considered to match any call that omits zero or more of the defaultable parameter positions. If more than one such function matches a call, the one appearing earliest in the search path is used. If there are two or more such functions in the same schema with identical parameter types in the non-defaulted positions (which is possible if they have different sets of defaultable parameters), the system will not be able to determine which to prefer, and so an “ambiguous function call” error will result if no better match to the call can be found.

This creates an availability hazard when calling, via qualified
name[[10]](typeconv-func.html#ftn.FUNC-QUALIFIED-SECURITY), any function found
in a schema that permits untrusted users to create objects. A malicious user
can create a function with the name of an existing function, replicating that
function's parameters and appending novel parameters having default values.
This precludes new calls to the original function. To forestall this hazard,
place functions in schemas that permit only trusted users to create objects.

  2. Check for a function accepting exactly the input argument types. If one exists (there can be only one exact match in the set of functions considered), use it. Lack of an exact match creates a security hazard when calling, via qualified name[[10]](typeconv-func.html#ftn.FUNC-QUALIFIED-SECURITY), a function found in a schema that permits untrusted users to create objects. In such situations, cast arguments to force an exact match. (Cases involving `unknown` will never find a match at this step.)

  3. If no exact match is found, see if the function call appears to be a special type conversion request. This happens if the function call has just one argument and the function name is the same as the (internal) name of some data type. Furthermore, the function argument must be either an unknown-type literal, or a type that is binary-coercible to the named data type, or a type that could be converted to the named data type by applying that type's I/O functions (that is, the conversion is either to or from one of the standard string types). When these conditions are met, the function call is treated as a form of `CAST` specification. [11]

  4. Look for the best match.

     1. Discard candidate functions for which the input types do not match and cannot be converted (using an implicit conversion) to match. `unknown` literals are assumed to be convertible to anything for this purpose. If only one candidate remains, use it; else continue to the next step.

     2. If any input argument is of a domain type, treat it as being of the domain's base type for all subsequent steps. This ensures that domains act like their base types for purposes of ambiguous-function resolution.

     3. Run through all candidates and keep those with the most exact matches on input types. Keep all candidates if none have exact matches. If only one candidate remains, use it; else continue to the next step.

     4. Run through all candidates and keep those that accept preferred types (of the input data type's type category) at the most positions where type conversion will be required. Keep all candidates if none accept preferred types. If only one candidate remains, use it; else continue to the next step.

     5. If any input arguments are `unknown`, check the type categories accepted at those argument positions by the remaining candidates. At each position, select the `string` category if any candidate accepts that category. (This bias towards string is appropriate since an unknown-type literal looks like a string.) Otherwise, if all the remaining candidates accept the same type category, select that category; otherwise fail because the correct choice cannot be deduced without more clues. Now discard candidates that do not accept the selected type category. Furthermore, if any candidate accepts a preferred type in that category, discard candidates that accept non-preferred types for that argument. Keep all candidates if none survive these tests. If only one candidate remains, use it; else continue to the next step.

     6. If there are both `unknown` and known-type arguments, and all the known-type arguments have the same type, assume that the `unknown` arguments are also of that type, and check which candidates can accept that type at the `unknown`-argument positions. If exactly one candidate passes this test, use it. Otherwise, fail.

Note that the “best match” rules are identical for operator and function type
resolution. Some examples follow.

**Example  10.6. Rounding Function Argument Type Resolution**

There is only one `round` function that takes two arguments; it takes a first
argument of type `numeric` and a second argument of type `integer`. So the
following query automatically converts the first argument of type `integer` to
`numeric`:

    
    
    SELECT round(4, 4);
    
     round
    --------
     4.0000
    (1 row)
    

That query is actually transformed by the parser to:

    
    
    SELECT round(CAST (4 AS numeric), 4);
    

Since numeric constants with decimal points are initially assigned the type
`numeric`, the following query will require no type conversion and therefore
might be slightly more efficient:

    
    
    SELECT round(4.0, 4);
    

  

**Example  10.7. Variadic Function Resolution**

    
    
    CREATE FUNCTION public.variadic_example(VARIADIC numeric[]) RETURNS int
      LANGUAGE sql AS 'SELECT 1';
    CREATE FUNCTION
    

This function accepts, but does not require, the VARIADIC keyword. It
tolerates both integer and numeric arguments:

    
    
    SELECT public.variadic_example(0),
           public.variadic_example(0.0),
           public.variadic_example(VARIADIC array[0.0]);
     variadic_example | variadic_example | variadic_example
    ------------------+------------------+------------------
                    1 |                1 |                1
    (1 row)
    

However, the first and second calls will prefer more-specific functions, if
available:

    
    
    CREATE FUNCTION public.variadic_example(numeric) RETURNS int
      LANGUAGE sql AS 'SELECT 2';
    CREATE FUNCTION
    
    CREATE FUNCTION public.variadic_example(int) RETURNS int
      LANGUAGE sql AS 'SELECT 3';
    CREATE FUNCTION
    
    SELECT public.variadic_example(0),
           public.variadic_example(0.0),
           public.variadic_example(VARIADIC array[0.0]);
     variadic_example | variadic_example | variadic_example
    ------------------+------------------+------------------
                    3 |                2 |                1
    (1 row)
    

Given the default configuration and only the first function existing, the
first and second calls are insecure. Any user could intercept them by creating
the second or third function. By matching the argument type exactly and using
the `VARIADIC` keyword, the third call is secure.

  

**Example  10.8. Substring Function Type Resolution**

There are several `substr` functions, one of which takes types `text` and
`integer`. If called with a string constant of unspecified type, the system
chooses the candidate function that accepts an argument of the preferred
category `string` (namely of type `text`).

    
    
    SELECT substr('1234', 3);
    
     substr
    --------
         34
    (1 row)
    

If the string is declared to be of type `varchar`, as might be the case if it
comes from a table, then the parser will try to convert it to become `text`:

    
    
    SELECT substr(varchar '1234', 3);
    
     substr
    --------
         34
    (1 row)
    

This is transformed by the parser to effectively become:

    
    
    SELECT substr(CAST (varchar '1234' AS text), 3);
    

### Note

The parser learns from the `pg_cast` catalog that `text` and `varchar` are
binary-compatible, meaning that one can be passed to a function that accepts
the other without doing any physical conversion. Therefore, no type conversion
call is really inserted in this case.

And, if the function is called with an argument of type `integer`, the parser
will try to convert that to `text`:

    
    
    SELECT substr(1234, 3);
    ERROR:  function substr(integer, integer) does not exist
    HINT:  No function matches the given name and argument types. You might need
    to add explicit type casts.
    

This does not work because `integer` does not have an implicit cast to `text`.
An explicit cast will work, however:

    
    
    SELECT substr(CAST (1234 AS text), 3);
    
     substr
    --------
         34
    (1 row)
    

  

  

* * *

[10] The hazard does not arise with a non-schema-qualified name, because a
search path containing schemas that permit untrusted users to create objects
is not a [secure schema usage pattern](ddl-schemas.html#DDL-SCHEMAS-PATTERNS
"5.9.6. Usage Patterns").

[11] The reason for this step is to support function-style cast specifications
in cases where there is not an actual cast function. If there is a cast
function, it is conventionally named after its output type, and so there is no
need to have a special case. See [CREATE CAST](sql-createcast.html "CREATE
CAST") for additional commentary.

* * *

[Prev](typeconv-oper.html "10.2. Operators")  | [Up](typeconv.html "Chapter 10. Type Conversion") |  [Next](typeconv-query.html "10.4. Value Storage")  
---|---|---  
10.2. Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  10.4. Value Storage  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv-func.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

