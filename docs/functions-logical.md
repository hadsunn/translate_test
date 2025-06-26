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

Supported Versions: [Current](/docs/current/functions-logical.html "PostgreSQL
17 - 9.1. Logical Operators") ([17](/docs/17/functions-logical.html
"PostgreSQL 17 - 9.1. Logical Operators")) / [16](/docs/16/functions-
logical.html "PostgreSQL 16 - 9.1. Logical Operators") /
[15](/docs/15/functions-logical.html "PostgreSQL 15 - 9.1. Logical Operators")
/ [14](/docs/14/functions-logical.html "PostgreSQL 14 - 9.1. Logical
Operators") / [13](/docs/13/functions-logical.html "PostgreSQL 13 -
9.1. Logical Operators")

Development Versions: [18](/docs/18/functions-logical.html "PostgreSQL 18 -
9.1. Logical Operators") / [devel](/docs/devel/functions-logical.html
"PostgreSQL devel - 9.1. Logical Operators")

Unsupported versions: [12](/docs/12/functions-logical.html "PostgreSQL 12 -
9.1. Logical Operators") / [11](/docs/11/functions-logical.html "PostgreSQL 11
- 9.1. Logical Operators") / [10](/docs/10/functions-logical.html "PostgreSQL
10 - 9.1. Logical Operators") / [9.6](/docs/9.6/functions-logical.html
"PostgreSQL 9.6 - 9.1. Logical Operators") / [9.5](/docs/9.5/functions-
logical.html "PostgreSQL 9.5 - 9.1. Logical Operators") /
[9.4](/docs/9.4/functions-logical.html "PostgreSQL 9.4 - 9.1. Logical
Operators") / [9.3](/docs/9.3/functions-logical.html "PostgreSQL 9.3 -
9.1. Logical Operators") / [9.2](/docs/9.2/functions-logical.html "PostgreSQL
9.2 - 9.1. Logical Operators") / [9.1](/docs/9.1/functions-logical.html
"PostgreSQL 9.1 - 9.1. Logical Operators") / [9.0](/docs/9.0/functions-
logical.html "PostgreSQL 9.0 - 9.1. Logical Operators") /
[8.4](/docs/8.4/functions-logical.html "PostgreSQL 8.4 - 9.1. Logical
Operators") / [8.3](/docs/8.3/functions-logical.html "PostgreSQL 8.3 -
9.1. Logical Operators") / [8.2](/docs/8.2/functions-logical.html "PostgreSQL
8.2 - 9.1. Logical Operators")

__

9.1. Logical Operators  
---  
[Prev](functions.html "Chapter 9. Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-comparison.html "9.2. Comparison Functions and Operators")  
  
* * *

## 9.1. Logical Operators #

The usual logical operators are available:

    
    
    boolean AND boolean → boolean
    boolean OR boolean → boolean
    NOT boolean → boolean
    

SQL uses a three-valued logic system with true, false, and `null`, which
represents “unknown”. Observe the following truth tables:

_`a`_ | _`b`_ | _`a`_ AND _`b`_ | _`a`_ OR _`b`_  
---|---|---|---  
TRUE | TRUE | TRUE | TRUE  
TRUE | FALSE | FALSE | TRUE  
TRUE | NULL | NULL | TRUE  
FALSE | FALSE | FALSE | FALSE  
FALSE | NULL | FALSE | NULL  
NULL | NULL | NULL | NULL  
  
_`a`_ | NOT _`a`_  
---|---  
TRUE | FALSE  
FALSE | TRUE  
NULL | NULL  
  
The operators `AND` and `OR` are commutative, that is, you can switch the left
and right operands without affecting the result. (However, it is not
guaranteed that the left operand is evaluated before the right operand. See
[Section 4.2.14](sql-expressions.html#SYNTAX-EXPRESS-EVAL "4.2.14. Expression
Evaluation Rules") for more information about the order of evaluation of
subexpressions.)

* * *

[Prev](functions.html "Chapter 9. Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-comparison.html "9.2. Comparison Functions and Operators")  
---|---|---  
Chapter 9. Functions and Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.2. Comparison Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-logical.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

