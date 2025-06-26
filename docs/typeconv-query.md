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

Supported Versions: [Current](/docs/current/typeconv-query.html "PostgreSQL 17
- 10.4. Value Storage") ([17](/docs/17/typeconv-query.html "PostgreSQL 17 -
10.4. Value Storage")) / [16](/docs/16/typeconv-query.html "PostgreSQL 16 -
10.4. Value Storage") / [15](/docs/15/typeconv-query.html "PostgreSQL 15 -
10.4. Value Storage") / [14](/docs/14/typeconv-query.html "PostgreSQL 14 -
10.4. Value Storage") / [13](/docs/13/typeconv-query.html "PostgreSQL 13 -
10.4. Value Storage")

Development Versions: [18](/docs/18/typeconv-query.html "PostgreSQL 18 -
10.4. Value Storage") / [devel](/docs/devel/typeconv-query.html "PostgreSQL
devel - 10.4. Value Storage")

Unsupported versions: [12](/docs/12/typeconv-query.html "PostgreSQL 12 -
10.4. Value Storage") / [11](/docs/11/typeconv-query.html "PostgreSQL 11 -
10.4. Value Storage") / [10](/docs/10/typeconv-query.html "PostgreSQL 10 -
10.4. Value Storage") / [9.6](/docs/9.6/typeconv-query.html "PostgreSQL 9.6 -
10.4. Value Storage") / [9.5](/docs/9.5/typeconv-query.html "PostgreSQL 9.5 -
10.4. Value Storage") / [9.4](/docs/9.4/typeconv-query.html "PostgreSQL 9.4 -
10.4. Value Storage") / [9.3](/docs/9.3/typeconv-query.html "PostgreSQL 9.3 -
10.4. Value Storage") / [9.2](/docs/9.2/typeconv-query.html "PostgreSQL 9.2 -
10.4. Value Storage") / [9.1](/docs/9.1/typeconv-query.html "PostgreSQL 9.1 -
10.4. Value Storage") / [9.0](/docs/9.0/typeconv-query.html "PostgreSQL 9.0 -
10.4. Value Storage") / [8.4](/docs/8.4/typeconv-query.html "PostgreSQL 8.4 -
10.4. Value Storage") / [8.3](/docs/8.3/typeconv-query.html "PostgreSQL 8.3 -
10.4. Value Storage") / [8.2](/docs/8.2/typeconv-query.html "PostgreSQL 8.2 -
10.4. Value Storage") / [8.1](/docs/8.1/typeconv-query.html "PostgreSQL 8.1 -
10.4. Value Storage") / [8.0](/docs/8.0/typeconv-query.html "PostgreSQL 8.0 -
10.4. Value Storage") / [7.4](/docs/7.4/typeconv-query.html "PostgreSQL 7.4 -
10.4. Value Storage") / [7.3](/docs/7.3/typeconv-query.html "PostgreSQL 7.3 -
10.4. Value Storage") / [7.2](/docs/7.2/typeconv-query.html "PostgreSQL 7.2 -
10.4. Value Storage") / [7.1](/docs/7.1/typeconv-query.html "PostgreSQL 7.1 -
10.4. Value Storage")

__

10.4. Value Storage  
---  
[Prev](typeconv-func.html "10.3. Functions")  | [Up](typeconv.html "Chapter 10. Type Conversion") | Chapter 10. Type Conversion | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv-union-case.html "10.5. UNION, CASE, and Related Constructs")  
  
* * *

## 10.4. Value Storage #

Values to be inserted into a table are converted to the destination column's
data type according to the following steps.

**Value Storage Type Conversion**

  1. Check for an exact match with the target.

  2. Otherwise, try to convert the expression to the target type. This is possible if an _assignment cast_ between the two types is registered in the `pg_cast` catalog (see [CREATE CAST](sql-createcast.html "CREATE CAST")). Alternatively, if the expression is an unknown-type literal, the contents of the literal string will be fed to the input conversion routine for the target type.

  3. Check to see if there is a sizing cast for the target type. A sizing cast is a cast from that type to itself. If one is found in the `pg_cast` catalog, apply it to the expression before storing into the destination column. The implementation function for such a cast always takes an extra parameter of type `integer`, which receives the destination column's `atttypmod` value (typically its declared length, although the interpretation of `atttypmod` varies for different data types), and it may take a third `boolean` parameter that says whether the cast is explicit or implicit. The cast function is responsible for applying any length-dependent semantics such as size checking or truncation.

**Example  10.9. `character` Storage Type Conversion**

For a target column declared as `character(20)` the following statement shows
that the stored value is sized correctly:

    
    
    CREATE TABLE vv (v character(20));
    INSERT INTO vv SELECT 'abc' || 'def';
    SELECT v, octet_length(v) FROM vv;
    
              v           | octet_length
    ----------------------+--------------
     abcdef               |           20
    (1 row)
    

What has really happened here is that the two unknown literals are resolved to
`text` by default, allowing the `||` operator to be resolved as `text`
concatenation. Then the `text` result of the operator is converted to `bpchar`
(“blank-padded char”, the internal name of the `character` data type) to match
the target column type. (Since the conversion from `text` to `bpchar` is
binary-coercible, this conversion does not insert any real function call.)
Finally, the sizing function `bpchar(bpchar, integer, boolean)` is found in
the system catalog and applied to the operator's result and the stored column
length. This type-specific function performs the required length check and
addition of padding spaces.

  

* * *

[Prev](typeconv-func.html "10.3. Functions")  | [Up](typeconv.html "Chapter 10. Type Conversion") |  [Next](typeconv-union-case.html "10.5. UNION, CASE, and Related Constructs")  
---|---|---  
10.3. Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  10.5. `UNION`, `CASE`, and Related Constructs  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv-query.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

