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

Supported Versions: [Current](/docs/current/typeconv-select.html "PostgreSQL
17 - 10.6. SELECT Output Columns") ([17](/docs/17/typeconv-select.html
"PostgreSQL 17 - 10.6. SELECT Output Columns")) / [16](/docs/16/typeconv-
select.html "PostgreSQL 16 - 10.6. SELECT Output Columns") /
[15](/docs/15/typeconv-select.html "PostgreSQL 15 - 10.6. SELECT Output
Columns") / [14](/docs/14/typeconv-select.html "PostgreSQL 14 - 10.6. SELECT
Output Columns") / [13](/docs/13/typeconv-select.html "PostgreSQL 13 -
10.6. SELECT Output Columns")

Development Versions: [18](/docs/18/typeconv-select.html "PostgreSQL 18 -
10.6. SELECT Output Columns") / [devel](/docs/devel/typeconv-select.html
"PostgreSQL devel - 10.6. SELECT Output Columns")

Unsupported versions: [12](/docs/12/typeconv-select.html "PostgreSQL 12 -
10.6. SELECT Output Columns") / [11](/docs/11/typeconv-select.html "PostgreSQL
11 - 10.6. SELECT Output Columns") / [10](/docs/10/typeconv-select.html
"PostgreSQL 10 - 10.6. SELECT Output Columns")

__

10.6. `SELECT` Output Columns  
---  
[Prev](typeconv-union-case.html "10.5. UNION, CASE, and Related Constructs")  | [Up](typeconv.html "Chapter 10. Type Conversion") | Chapter 10. Type Conversion | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes.html "Chapter 11. Indexes")  
  
* * *

## 10.6. `SELECT` Output Columns #

The rules given in the preceding sections will result in assignment of
non-`unknown` data types to all expressions in an SQL query, except for
unspecified-type literals that appear as simple output columns of a `SELECT`
command. For example, in

    
    
    SELECT 'Hello World';
    

there is nothing to identify what type the string literal should be taken as.
In this situation PostgreSQL will fall back to resolving the literal's type as
`text`.

When the `SELECT` is one arm of a `UNION` (or `INTERSECT` or `EXCEPT`)
construct, or when it appears within `INSERT ... SELECT`, this rule is not
applied since rules given in preceding sections take precedence. The type of
an unspecified-type literal can be taken from the other `UNION` arm in the
first case, or from the destination column in the second case.

`RETURNING` lists are treated the same as `SELECT` output lists for this
purpose.

### Note

Prior to PostgreSQL 10, this rule did not exist, and unspecified-type literals
in a `SELECT` output list were left as type `unknown`. That had assorted bad
consequences, so it's been changed.

* * *

[Prev](typeconv-union-case.html "10.5. UNION, CASE, and Related Constructs")  | [Up](typeconv.html "Chapter 10. Type Conversion") |  [Next](indexes.html "Chapter 11. Indexes")  
---|---|---  
10.5. `UNION`, `CASE`, and Related Constructs  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 11. Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv-select.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

