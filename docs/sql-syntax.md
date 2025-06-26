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

Supported Versions: [Current](/docs/current/sql-syntax.html "PostgreSQL 17 -
Chapter 4. SQL Syntax") ([17](/docs/17/sql-syntax.html "PostgreSQL 17 -
Chapter 4. SQL Syntax")) / [16](/docs/16/sql-syntax.html "PostgreSQL 16 -
Chapter 4. SQL Syntax") / [15](/docs/15/sql-syntax.html "PostgreSQL 15 -
Chapter 4. SQL Syntax") / [14](/docs/14/sql-syntax.html "PostgreSQL 14 -
Chapter 4. SQL Syntax") / [13](/docs/13/sql-syntax.html "PostgreSQL 13 -
Chapter 4. SQL Syntax")

Development Versions: [18](/docs/18/sql-syntax.html "PostgreSQL 18 -
Chapter 4. SQL Syntax") / [devel](/docs/devel/sql-syntax.html "PostgreSQL
devel - Chapter 4. SQL Syntax")

Unsupported versions: [12](/docs/12/sql-syntax.html "PostgreSQL 12 -
Chapter 4. SQL Syntax") / [11](/docs/11/sql-syntax.html "PostgreSQL 11 -
Chapter 4. SQL Syntax") / [10](/docs/10/sql-syntax.html "PostgreSQL 10 -
Chapter 4. SQL Syntax") / [9.6](/docs/9.6/sql-syntax.html "PostgreSQL 9.6 -
Chapter 4. SQL Syntax") / [9.5](/docs/9.5/sql-syntax.html "PostgreSQL 9.5 -
Chapter 4. SQL Syntax") / [9.4](/docs/9.4/sql-syntax.html "PostgreSQL 9.4 -
Chapter 4. SQL Syntax") / [9.3](/docs/9.3/sql-syntax.html "PostgreSQL 9.3 -
Chapter 4. SQL Syntax") / [9.2](/docs/9.2/sql-syntax.html "PostgreSQL 9.2 -
Chapter 4. SQL Syntax") / [9.1](/docs/9.1/sql-syntax.html "PostgreSQL 9.1 -
Chapter 4. SQL Syntax") / [9.0](/docs/9.0/sql-syntax.html "PostgreSQL 9.0 -
Chapter 4. SQL Syntax") / [8.4](/docs/8.4/sql-syntax.html "PostgreSQL 8.4 -
Chapter 4. SQL Syntax") / [8.3](/docs/8.3/sql-syntax.html "PostgreSQL 8.3 -
Chapter 4. SQL Syntax") / [8.2](/docs/8.2/sql-syntax.html "PostgreSQL 8.2 -
Chapter 4. SQL Syntax") / [8.1](/docs/8.1/sql-syntax.html "PostgreSQL 8.1 -
Chapter 4. SQL Syntax") / [8.0](/docs/8.0/sql-syntax.html "PostgreSQL 8.0 -
Chapter 4. SQL Syntax") / [7.4](/docs/7.4/sql-syntax.html "PostgreSQL 7.4 -
Chapter 4. SQL Syntax") / [7.3](/docs/7.3/sql-syntax.html "PostgreSQL 7.3 -
Chapter 4. SQL Syntax") / [7.2](/docs/7.2/sql-syntax.html "PostgreSQL 7.2 -
Chapter 4. SQL Syntax") / [7.1](/docs/7.1/sql-syntax.html "PostgreSQL 7.1 -
Chapter 4. SQL Syntax")

__

Chapter 4. SQL Syntax  
---  
[Prev](sql.html "Part II. The SQL Language")  | [Up](sql.html "Part II. The SQL Language") | Part II. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-syntax-lexical.html "4.1. Lexical Structure")  
  
* * *

## Chapter 4. SQL Syntax

**Table of Contents**

[4.1. Lexical Structure](sql-syntax-lexical.html)

    

[4.1.1. Identifiers and Key Words](sql-syntax-lexical.html#SQL-SYNTAX-
IDENTIFIERS)

[4.1.2. Constants](sql-syntax-lexical.html#SQL-SYNTAX-CONSTANTS)

[4.1.3. Operators](sql-syntax-lexical.html#SQL-SYNTAX-OPERATORS)

[4.1.4. Special Characters](sql-syntax-lexical.html#SQL-SYNTAX-SPECIAL-CHARS)

[4.1.5. Comments](sql-syntax-lexical.html#SQL-SYNTAX-COMMENTS)

[4.1.6. Operator Precedence](sql-syntax-lexical.html#SQL-PRECEDENCE)

[4.2. Value Expressions](sql-expressions.html)

    

[4.2.1. Column References](sql-expressions.html#SQL-EXPRESSIONS-COLUMN-REFS)

[4.2.2. Positional Parameters](sql-expressions.html#SQL-EXPRESSIONS-
PARAMETERS-POSITIONAL)

[4.2.3. Subscripts](sql-expressions.html#SQL-EXPRESSIONS-SUBSCRIPTS)

[4.2.4. Field Selection](sql-expressions.html#FIELD-SELECTION)

[4.2.5. Operator Invocations](sql-expressions.html#SQL-EXPRESSIONS-OPERATOR-
CALLS)

[4.2.6. Function Calls](sql-expressions.html#SQL-EXPRESSIONS-FUNCTION-CALLS)

[4.2.7. Aggregate Expressions](sql-expressions.html#SYNTAX-AGGREGATES)

[4.2.8. Window Function Calls](sql-expressions.html#SYNTAX-WINDOW-FUNCTIONS)

[4.2.9. Type Casts](sql-expressions.html#SQL-SYNTAX-TYPE-CASTS)

[4.2.10. Collation Expressions](sql-expressions.html#SQL-SYNTAX-COLLATE-EXPRS)

[4.2.11. Scalar Subqueries](sql-expressions.html#SQL-SYNTAX-SCALAR-SUBQUERIES)

[4.2.12. Array Constructors](sql-expressions.html#SQL-SYNTAX-ARRAY-
CONSTRUCTORS)

[4.2.13. Row Constructors](sql-expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS)

[4.2.14. Expression Evaluation Rules](sql-expressions.html#SYNTAX-EXPRESS-
EVAL)

[4.3. Calling Functions](sql-syntax-calling-funcs.html)

    

[4.3.1. Using Positional Notation](sql-syntax-calling-funcs.html#SQL-SYNTAX-
CALLING-FUNCS-POSITIONAL)

[4.3.2. Using Named Notation](sql-syntax-calling-funcs.html#SQL-SYNTAX-
CALLING-FUNCS-NAMED)

[4.3.3. Using Mixed Notation](sql-syntax-calling-funcs.html#SQL-SYNTAX-
CALLING-FUNCS-MIXED)

This chapter describes the syntax of SQL. It forms the foundation for
understanding the following chapters which will go into detail about how SQL
commands are applied to define and modify data.

We also advise users who are already familiar with SQL to read this chapter
carefully because it contains several rules and concepts that are implemented
inconsistently among SQL databases or that are specific to PostgreSQL.

* * *

[Prev](sql.html "Part II. The SQL Language")  | [Up](sql.html "Part II. The SQL Language") |  [Next](sql-syntax-lexical.html "4.1. Lexical Structure")  
---|---|---  
Part II. The SQL Language  | [Home](index.html "PostgreSQL 16.9 Documentation") |  4.1. Lexical Structure  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-syntax.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

