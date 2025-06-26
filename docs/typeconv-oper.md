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

Supported Versions: [Current](/docs/current/typeconv-oper.html "PostgreSQL 17
- 10.2. Operators") ([17](/docs/17/typeconv-oper.html "PostgreSQL 17 -
10.2. Operators")) / [16](/docs/16/typeconv-oper.html "PostgreSQL 16 -
10.2. Operators") / [15](/docs/15/typeconv-oper.html "PostgreSQL 15 -
10.2. Operators") / [14](/docs/14/typeconv-oper.html "PostgreSQL 14 -
10.2. Operators") / [13](/docs/13/typeconv-oper.html "PostgreSQL 13 -
10.2. Operators")

Development Versions: [18](/docs/18/typeconv-oper.html "PostgreSQL 18 -
10.2. Operators") / [devel](/docs/devel/typeconv-oper.html "PostgreSQL devel -
10.2. Operators")

Unsupported versions: [12](/docs/12/typeconv-oper.html "PostgreSQL 12 -
10.2. Operators") / [11](/docs/11/typeconv-oper.html "PostgreSQL 11 -
10.2. Operators") / [10](/docs/10/typeconv-oper.html "PostgreSQL 10 -
10.2. Operators") / [9.6](/docs/9.6/typeconv-oper.html "PostgreSQL 9.6 -
10.2. Operators") / [9.5](/docs/9.5/typeconv-oper.html "PostgreSQL 9.5 -
10.2. Operators") / [9.4](/docs/9.4/typeconv-oper.html "PostgreSQL 9.4 -
10.2. Operators") / [9.3](/docs/9.3/typeconv-oper.html "PostgreSQL 9.3 -
10.2. Operators") / [9.2](/docs/9.2/typeconv-oper.html "PostgreSQL 9.2 -
10.2. Operators") / [9.1](/docs/9.1/typeconv-oper.html "PostgreSQL 9.1 -
10.2. Operators") / [9.0](/docs/9.0/typeconv-oper.html "PostgreSQL 9.0 -
10.2. Operators") / [8.4](/docs/8.4/typeconv-oper.html "PostgreSQL 8.4 -
10.2. Operators") / [8.3](/docs/8.3/typeconv-oper.html "PostgreSQL 8.3 -
10.2. Operators") / [8.2](/docs/8.2/typeconv-oper.html "PostgreSQL 8.2 -
10.2. Operators") / [8.1](/docs/8.1/typeconv-oper.html "PostgreSQL 8.1 -
10.2. Operators") / [8.0](/docs/8.0/typeconv-oper.html "PostgreSQL 8.0 -
10.2. Operators") / [7.4](/docs/7.4/typeconv-oper.html "PostgreSQL 7.4 -
10.2. Operators") / [7.3](/docs/7.3/typeconv-oper.html "PostgreSQL 7.3 -
10.2. Operators") / [7.2](/docs/7.2/typeconv-oper.html "PostgreSQL 7.2 -
10.2. Operators") / [7.1](/docs/7.1/typeconv-oper.html "PostgreSQL 7.1 -
10.2. Operators")

__

10.2. Operators  
---  
[Prev](typeconv-overview.html "10.1. Overview")  | [Up](typeconv.html "Chapter 10. Type Conversion") | Chapter 10. Type Conversion | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv-func.html "10.3. Functions")  
  
* * *

## 10.2. Operators #

The specific operator that is referenced by an operator expression is
determined using the following procedure. Note that this procedure is
indirectly affected by the precedence of the operators involved, since that
will determine which sub-expressions are taken to be the inputs of which
operators. See [Section 4.1.6](sql-syntax-lexical.html#SQL-PRECEDENCE
"4.1.6. Operator Precedence") for more information.

**Operator Type Resolution**

  1. Select the operators to be considered from the `pg_operator` system catalog. If a non-schema-qualified operator name was used (the usual case), the operators considered are those with the matching name and argument count that are visible in the current search path (see [Section 5.9.3](ddl-schemas.html#DDL-SCHEMAS-PATH "5.9.3. The Schema Search Path")). If a qualified operator name was given, only operators in the specified schema are considered.

     1. If the search path finds multiple operators with identical argument types, only the one appearing earliest in the path is considered. Operators with different argument types are considered on an equal footing regardless of search path position.

  2. Check for an operator accepting exactly the input argument types. If one exists (there can be only one exact match in the set of operators considered), use it. Lack of an exact match creates a security hazard when calling, via qualified name [9] (not typical), any operator found in a schema that permits untrusted users to create objects. In such situations, cast arguments to force an exact match.

     1. If one argument of a binary operator invocation is of the `unknown` type, then assume it is the same type as the other argument for this check. Invocations involving two `unknown` inputs, or a prefix operator with an `unknown` input, will never find a match at this step.

     2. If one argument of a binary operator invocation is of the `unknown` type and the other is of a domain type, next check to see if there is an operator accepting exactly the domain's base type on both sides; if so, use it.

  3. Look for the best match.

     1. Discard candidate operators for which the input types do not match and cannot be converted (using an implicit conversion) to match. `unknown` literals are assumed to be convertible to anything for this purpose. If only one candidate remains, use it; else continue to the next step.

     2. If any input argument is of a domain type, treat it as being of the domain's base type for all subsequent steps. This ensures that domains act like their base types for purposes of ambiguous-operator resolution.

     3. Run through all candidates and keep those with the most exact matches on input types. Keep all candidates if none have exact matches. If only one candidate remains, use it; else continue to the next step.

     4. Run through all candidates and keep those that accept preferred types (of the input data type's type category) at the most positions where type conversion will be required. Keep all candidates if none accept preferred types. If only one candidate remains, use it; else continue to the next step.

     5. If any input arguments are `unknown`, check the type categories accepted at those argument positions by the remaining candidates. At each position, select the `string` category if any candidate accepts that category. (This bias towards string is appropriate since an unknown-type literal looks like a string.) Otherwise, if all the remaining candidates accept the same type category, select that category; otherwise fail because the correct choice cannot be deduced without more clues. Now discard candidates that do not accept the selected type category. Furthermore, if any candidate accepts a preferred type in that category, discard candidates that accept non-preferred types for that argument. Keep all candidates if none survive these tests. If only one candidate remains, use it; else continue to the next step.

     6. If there are both `unknown` and known-type arguments, and all the known-type arguments have the same type, assume that the `unknown` arguments are also of that type, and check which candidates can accept that type at the `unknown`-argument positions. If exactly one candidate passes this test, use it. Otherwise, fail.

Some examples follow.

**Example  10.1. Square Root Operator Type Resolution**

There is only one square root operator (prefix `|/`) defined in the standard
catalog, and it takes an argument of type `double precision`. The scanner
assigns an initial type of `integer` to the argument in this query expression:

    
    
    SELECT |/ 40 AS "square root of 40";
     square root of 40
    -------------------
     6.324555320336759
    (1 row)
    

So the parser does a type conversion on the operand and the query is
equivalent to:

    
    
    SELECT |/ CAST(40 AS double precision) AS "square root of 40";
    

  

**Example  10.2. String Concatenation Operator Type Resolution**

A string-like syntax is used for working with string types and for working
with complex extension types. Strings with unspecified type are matched with
likely operator candidates.

An example with one unspecified argument:

    
    
    SELECT text 'abc' || 'def' AS "text and unknown";
    
     text and unknown
    ------------------
     abcdef
    (1 row)
    

In this case the parser looks to see if there is an operator taking `text` for
both arguments. Since there is, it assumes that the second argument should be
interpreted as type `text`.

Here is a concatenation of two values of unspecified types:

    
    
    SELECT 'abc' || 'def' AS "unspecified";
    
     unspecified
    -------------
     abcdef
    (1 row)
    

In this case there is no initial hint for which type to use, since no types
are specified in the query. So, the parser looks for all candidate operators
and finds that there are candidates accepting both string-category and bit-
string-category inputs. Since string category is preferred when available,
that category is selected, and then the preferred type for strings, `text`, is
used as the specific type to resolve the unknown-type literals as.

  

**Example  10.3. Absolute-Value and Negation Operator Type Resolution**

The PostgreSQL operator catalog has several entries for the prefix operator
`@`, all of which implement absolute-value operations for various numeric data
types. One of these entries is for type `float8`, which is the preferred type
in the numeric category. Therefore, PostgreSQL will use that entry when faced
with an `unknown` input:

    
    
    SELECT @ '-4.5' AS "abs";
     abs
    -----
     4.5
    (1 row)
    

Here the system has implicitly resolved the unknown-type literal as type
`float8` before applying the chosen operator. We can verify that `float8` and
not some other type was used:

    
    
    SELECT @ '-4.5e500' AS "abs";
    
    ERROR:  "-4.5e500" is out of range for type double precision
    

On the other hand, the prefix operator `~` (bitwise negation) is defined only
for integer data types, not for `float8`. So, if we try a similar case with
`~`, we get:

    
    
    SELECT ~ '20' AS "negation";
    
    ERROR:  operator is not unique: ~ "unknown"
    HINT:  Could not choose a best candidate operator. You might need to add
    explicit type casts.
    

This happens because the system cannot decide which of the several possible
`~` operators should be preferred. We can help it out with an explicit cast:

    
    
    SELECT ~ CAST('20' AS int8) AS "negation";
    
     negation
    ----------
          -21
    (1 row)
    

  

**Example  10.4. Array Inclusion Operator Type Resolution**

Here is another example of resolving an operator with one known and one
unknown input:

    
    
    SELECT array[1,2] <@ '{1,2,3}' as "is subset";
    
     is subset
    -----------
     t
    (1 row)
    

The PostgreSQL operator catalog has several entries for the infix operator
`<@`, but the only two that could possibly accept an integer array on the
left-hand side are array inclusion (`anyarray` `<@` `anyarray`) and range
inclusion (`anyelement` `<@` `anyrange`). Since none of these polymorphic
pseudo-types (see [Section 8.21](datatype-pseudo.html "8.21. Pseudo-Types"))
are considered preferred, the parser cannot resolve the ambiguity on that
basis. However, [Step 3.f](typeconv-oper.html#OP-RESOL-LAST-UNKNOWN "Step
3.f") tells it to assume that the unknown-type literal is of the same type as
the other input, that is, integer array. Now only one of the two operators can
match, so array inclusion is selected. (Had range inclusion been selected, we
would have gotten an error, because the string does not have the right format
to be a range literal.)

  

**Example  10.5. Custom Operator on a Domain Type**

Users sometimes try to declare operators applying just to a domain type. This
is possible but is not nearly as useful as it might seem, because the operator
resolution rules are designed to select operators applying to the domain's
base type. As an example consider

    
    
    CREATE DOMAIN mytext AS text CHECK(...);
    CREATE FUNCTION mytext_eq_text (mytext, text) RETURNS boolean AS ...;
    CREATE OPERATOR = (procedure=mytext_eq_text, leftarg=mytext, rightarg=text);
    CREATE TABLE mytable (val mytext);
    
    SELECT * FROM mytable WHERE val = 'foo';
    

This query will not use the custom operator. The parser will first see if
there is a `mytext` `=` `mytext` operator ([Step 2.a](typeconv-oper.html#OP-
RESOL-EXACT-UNKNOWN "Step 2.a")), which there is not; then it will consider
the domain's base type `text`, and see if there is a `text` `=` `text`
operator ([Step 2.b](typeconv-oper.html#OP-RESOL-EXACT-DOMAIN "Step 2.b")),
which there is; so it resolves the `unknown`-type literal as `text` and uses
the `text` `=` `text` operator. The only way to get the custom operator to be
used is to explicitly cast the literal:

    
    
    SELECT * FROM mytable WHERE val = text 'foo';
    

so that the `mytext` `=` `text` operator is found immediately according to the
exact-match rule. If the best-match rules are reached, they actively
discriminate against operators on domain types. If they did not, such an
operator would create too many ambiguous-operator failures, because the
casting rules always consider a domain as castable to or from its base type,
and so the domain operator would be considered usable in all the same cases as
a similarly-named operator on the base type.

  

  

* * *

[9] The hazard does not arise with a non-schema-qualified name, because a
search path containing schemas that permit untrusted users to create objects
is not a [secure schema usage pattern](ddl-schemas.html#DDL-SCHEMAS-PATTERNS
"5.9.6. Usage Patterns").

* * *

[Prev](typeconv-overview.html "10.1. Overview")  | [Up](typeconv.html "Chapter 10. Type Conversion") |  [Next](typeconv-func.html "10.3. Functions")  
---|---|---  
10.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  10.3. Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv-oper.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

