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

Supported Versions: [Current](/docs/current/typeconv.html "PostgreSQL 17 -
Chapter 10. Type Conversion") ([17](/docs/17/typeconv.html "PostgreSQL 17 -
Chapter 10. Type Conversion")) / [16](/docs/16/typeconv.html "PostgreSQL 16 -
Chapter 10. Type Conversion") / [15](/docs/15/typeconv.html "PostgreSQL 15 -
Chapter 10. Type Conversion") / [14](/docs/14/typeconv.html "PostgreSQL 14 -
Chapter 10. Type Conversion") / [13](/docs/13/typeconv.html "PostgreSQL 13 -
Chapter 10. Type Conversion")

Development Versions: [18](/docs/18/typeconv.html "PostgreSQL 18 -
Chapter 10. Type Conversion") / [devel](/docs/devel/typeconv.html "PostgreSQL
devel - Chapter 10. Type Conversion")

Unsupported versions: [12](/docs/12/typeconv.html "PostgreSQL 12 -
Chapter 10. Type Conversion") / [11](/docs/11/typeconv.html "PostgreSQL 11 -
Chapter 10. Type Conversion") / [10](/docs/10/typeconv.html "PostgreSQL 10 -
Chapter 10. Type Conversion") / [9.6](/docs/9.6/typeconv.html "PostgreSQL 9.6
- Chapter 10. Type Conversion") / [9.5](/docs/9.5/typeconv.html "PostgreSQL
9.5 - Chapter 10. Type Conversion") / [9.4](/docs/9.4/typeconv.html
"PostgreSQL 9.4 - Chapter 10. Type Conversion") /
[9.3](/docs/9.3/typeconv.html "PostgreSQL 9.3 - Chapter 10. Type Conversion")
/ [9.2](/docs/9.2/typeconv.html "PostgreSQL 9.2 - Chapter 10. Type
Conversion") / [9.1](/docs/9.1/typeconv.html "PostgreSQL 9.1 -
Chapter 10. Type Conversion") / [9.0](/docs/9.0/typeconv.html "PostgreSQL 9.0
- Chapter 10. Type Conversion") / [8.4](/docs/8.4/typeconv.html "PostgreSQL
8.4 - Chapter 10. Type Conversion") / [8.3](/docs/8.3/typeconv.html
"PostgreSQL 8.3 - Chapter 10. Type Conversion") /
[8.2](/docs/8.2/typeconv.html "PostgreSQL 8.2 - Chapter 10. Type Conversion")
/ [8.1](/docs/8.1/typeconv.html "PostgreSQL 8.1 - Chapter 10. Type
Conversion") / [8.0](/docs/8.0/typeconv.html "PostgreSQL 8.0 -
Chapter 10. Type Conversion") / [7.4](/docs/7.4/typeconv.html "PostgreSQL 7.4
- Chapter 10. Type Conversion") / [7.3](/docs/7.3/typeconv.html "PostgreSQL
7.3 - Chapter 10. Type Conversion") / [7.2](/docs/7.2/typeconv.html
"PostgreSQL 7.2 - Chapter 10. Type Conversion") /
[7.1](/docs/7.1/typeconv.html "PostgreSQL 7.1 - Chapter 10. Type Conversion")

__

Chapter 10. Type Conversion  
---  
[Prev](functions-statistics.html "9.30. Statistics Information Functions")  | [Up](sql.html "Part II. The SQL Language") | Part II. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv-overview.html "10.1. Overview")  
  
* * *

## Chapter 10. Type Conversion

**Table of Contents**

[10.1. Overview](typeconv-overview.html)

[10.2. Operators](typeconv-oper.html)

[10.3. Functions](typeconv-func.html)

[10.4. Value Storage](typeconv-query.html)

[10.5. `UNION`, `CASE`, and Related Constructs](typeconv-union-case.html)

[10.6. `SELECT` Output Columns](typeconv-select.html)

SQL statements can, intentionally or not, require the mixing of different data
types in the same expression. PostgreSQL has extensive facilities for
evaluating mixed-type expressions.

In many cases a user does not need to understand the details of the type
conversion mechanism. However, implicit conversions done by PostgreSQL can
affect the results of a query. When necessary, these results can be tailored
by using _explicit_ type conversion.

This chapter introduces the PostgreSQL type conversion mechanisms and
conventions. Refer to the relevant sections in [Chapter 8](datatype.html
"Chapter 8. Data Types") and [Chapter 9](functions.html "Chapter 9. Functions
and Operators") for more information on specific data types and allowed
functions and operators.

* * *

[Prev](functions-statistics.html "9.30. Statistics Information Functions")  | [Up](sql.html "Part II. The SQL Language") |  [Next](typeconv-overview.html "10.1. Overview")  
---|---|---  
9.30. Statistics Information Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  10.1. Overview  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

