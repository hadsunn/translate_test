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

Supported Versions: [Current](/docs/current/typeconv-union-case.html
"PostgreSQL 17 - 10.5. UNION, CASE, and Related Constructs")
([17](/docs/17/typeconv-union-case.html "PostgreSQL 17 - 10.5. UNION, CASE,
and Related Constructs")) / [16](/docs/16/typeconv-union-case.html "PostgreSQL
16 - 10.5. UNION, CASE, and Related Constructs") / [15](/docs/15/typeconv-
union-case.html "PostgreSQL 15 - 10.5. UNION, CASE, and Related Constructs") /
[14](/docs/14/typeconv-union-case.html "PostgreSQL 14 - 10.5. UNION, CASE, and
Related Constructs") / [13](/docs/13/typeconv-union-case.html "PostgreSQL 13 -
10.5. UNION, CASE, and Related Constructs")

Development Versions: [18](/docs/18/typeconv-union-case.html "PostgreSQL 18 -
10.5. UNION, CASE, and Related Constructs") / [devel](/docs/devel/typeconv-
union-case.html "PostgreSQL devel - 10.5. UNION, CASE, and Related
Constructs")

Unsupported versions: [12](/docs/12/typeconv-union-case.html "PostgreSQL 12 -
10.5. UNION, CASE, and Related Constructs") / [11](/docs/11/typeconv-union-
case.html "PostgreSQL 11 - 10.5. UNION, CASE, and Related Constructs") /
[10](/docs/10/typeconv-union-case.html "PostgreSQL 10 - 10.5. UNION, CASE, and
Related Constructs") / [9.6](/docs/9.6/typeconv-union-case.html "PostgreSQL
9.6 - 10.5. UNION, CASE, and Related Constructs") / [9.5](/docs/9.5/typeconv-
union-case.html "PostgreSQL 9.5 - 10.5. UNION, CASE, and Related Constructs")
/ [9.4](/docs/9.4/typeconv-union-case.html "PostgreSQL 9.4 - 10.5. UNION,
CASE, and Related Constructs") / [9.3](/docs/9.3/typeconv-union-case.html
"PostgreSQL 9.3 - 10.5. UNION, CASE, and Related Constructs") /
[9.2](/docs/9.2/typeconv-union-case.html "PostgreSQL 9.2 - 10.5. UNION, CASE,
and Related Constructs") / [9.1](/docs/9.1/typeconv-union-case.html
"PostgreSQL 9.1 - 10.5. UNION, CASE, and Related Constructs") /
[9.0](/docs/9.0/typeconv-union-case.html "PostgreSQL 9.0 - 10.5. UNION, CASE,
and Related Constructs") / [8.4](/docs/8.4/typeconv-union-case.html
"PostgreSQL 8.4 - 10.5. UNION, CASE, and Related Constructs") /
[8.3](/docs/8.3/typeconv-union-case.html "PostgreSQL 8.3 - 10.5. UNION, CASE,
and Related Constructs") / [8.2](/docs/8.2/typeconv-union-case.html
"PostgreSQL 8.2 - 10.5. UNION, CASE, and Related Constructs") /
[8.1](/docs/8.1/typeconv-union-case.html "PostgreSQL 8.1 - 10.5. UNION, CASE,
and Related Constructs") / [8.0](/docs/8.0/typeconv-union-case.html
"PostgreSQL 8.0 - 10.5. UNION, CASE, and Related Constructs") /
[7.4](/docs/7.4/typeconv-union-case.html "PostgreSQL 7.4 - 10.5. UNION, CASE,
and Related Constructs") / [7.3](/docs/7.3/typeconv-union-case.html
"PostgreSQL 7.3 - 10.5. UNION, CASE, and Related Constructs") /
[7.2](/docs/7.2/typeconv-union-case.html "PostgreSQL 7.2 - 10.5. UNION, CASE,
and Related Constructs") / [7.1](/docs/7.1/typeconv-union-case.html
"PostgreSQL 7.1 - 10.5. UNION, CASE, and Related Constructs")

__

10.5. `UNION`, `CASE`, and Related Constructs  
---  
[Prev](typeconv-query.html "10.4. Value Storage")  | [Up](typeconv.html "Chapter 10. Type Conversion") | Chapter 10. Type Conversion | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv-select.html "10.6. SELECT Output Columns")  
  
* * *

## 10.5. `UNION`, `CASE`, and Related Constructs #

SQL `UNION` constructs must match up possibly dissimilar types to become a
single result set. The resolution algorithm is applied separately to each
output column of a union query. The `INTERSECT` and `EXCEPT` constructs
resolve dissimilar types in the same way as `UNION`. Some other constructs,
including `CASE`, `ARRAY`, `VALUES`, and the `GREATEST` and `LEAST` functions,
use the identical algorithm to match up their component expressions and select
a result data type.

**Type Resolution for`UNION`, `CASE`, and Related Constructs**

  1. If all inputs are of the same type, and it is not `unknown`, resolve as that type.

  2. If any input is of a domain type, treat it as being of the domain's base type for all subsequent steps. [12]

  3. If all inputs are of type `unknown`, resolve as type `text` (the preferred type of the string category). Otherwise, `unknown` inputs are ignored for the purposes of the remaining rules.

  4. If the non-unknown inputs are not all of the same type category, fail.

  5. Select the first non-unknown input type as the candidate type, then consider each other non-unknown input type, left to right. [13] If the candidate type can be implicitly converted to the other type, but not vice-versa, select the other type as the new candidate type. Then continue considering the remaining inputs. If, at any stage of this process, a preferred type is selected, stop considering additional inputs.

  6. Convert all inputs to the final candidate type. Fail if there is not an implicit conversion from a given input type to the candidate type.

Some examples follow.

**Example  10.10. Type Resolution with Underspecified Types in a Union**

    
    
    SELECT text 'a' AS "text" UNION SELECT 'b';
    
     text
    ------
     a
     b
    (2 rows)
    

Here, the unknown-type literal `'b'` will be resolved to type `text`.

  

**Example  10.11. Type Resolution in a Simple Union**

    
    
    SELECT 1.2 AS "numeric" UNION SELECT 1;
    
     numeric
    ---------
           1
         1.2
    (2 rows)
    

The literal `1.2` is of type `numeric`, and the `integer` value `1` can be
cast implicitly to `numeric`, so that type is used.

  

**Example  10.12. Type Resolution in a Transposed Union**

    
    
    SELECT 1 AS "real" UNION SELECT CAST('2.2' AS REAL);
    
     real
    ------
        1
      2.2
    (2 rows)
    

Here, since type `real` cannot be implicitly cast to `integer`, but `integer`
can be implicitly cast to `real`, the union result type is resolved as `real`.

  

**Example  10.13. Type Resolution in a Nested Union**

    
    
    SELECT NULL UNION SELECT NULL UNION SELECT 1;
    
    ERROR:  UNION types text and integer cannot be matched
    

This failure occurs because PostgreSQL treats multiple `UNION`s as a nest of
pairwise operations; that is, this input is the same as

    
    
    (SELECT NULL UNION SELECT NULL) UNION SELECT 1;
    

The inner `UNION` is resolved as emitting type `text`, according to the rules
given above. Then the outer `UNION` has inputs of types `text` and `integer`,
leading to the observed error. The problem can be fixed by ensuring that the
leftmost `UNION` has at least one input of the desired result type.

`INTERSECT` and `EXCEPT` operations are likewise resolved pairwise. However,
the other constructs described in this section consider all of their inputs in
one resolution step.

  

  

* * *

[12] Somewhat like the treatment of domain inputs for operators and functions,
this behavior allows a domain type to be preserved through a `UNION` or
similar construct, so long as the user is careful to ensure that all inputs
are implicitly or explicitly of that exact type. Otherwise the domain's base
type will be used.

[13] For historical reasons, `CASE` treats its `ELSE` clause (if any) as the
“first” input, with the `THEN` clauses(s) considered after that. In all other
cases, “left to right” means the order in which the expressions appear in the
query text.

* * *

[Prev](typeconv-query.html "10.4. Value Storage")  | [Up](typeconv.html "Chapter 10. Type Conversion") |  [Next](typeconv-select.html "10.6. SELECT Output Columns")  
---|---|---  
10.4. Value Storage  | [Home](index.html "PostgreSQL 16.9 Documentation") |  10.6. `SELECT` Output Columns  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv-union-case.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

