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

Supported Versions: [Current](/docs/current/datatype-boolean.html "PostgreSQL
17 - 8.6. Boolean Type") ([17](/docs/17/datatype-boolean.html "PostgreSQL 17 -
8.6. Boolean Type")) / [16](/docs/16/datatype-boolean.html "PostgreSQL 16 -
8.6. Boolean Type") / [15](/docs/15/datatype-boolean.html "PostgreSQL 15 -
8.6. Boolean Type") / [14](/docs/14/datatype-boolean.html "PostgreSQL 14 -
8.6. Boolean Type") / [13](/docs/13/datatype-boolean.html "PostgreSQL 13 -
8.6. Boolean Type")

Development Versions: [18](/docs/18/datatype-boolean.html "PostgreSQL 18 -
8.6. Boolean Type") / [devel](/docs/devel/datatype-boolean.html "PostgreSQL
devel - 8.6. Boolean Type")

Unsupported versions: [12](/docs/12/datatype-boolean.html "PostgreSQL 12 -
8.6. Boolean Type") / [11](/docs/11/datatype-boolean.html "PostgreSQL 11 -
8.6. Boolean Type") / [10](/docs/10/datatype-boolean.html "PostgreSQL 10 -
8.6. Boolean Type") / [9.6](/docs/9.6/datatype-boolean.html "PostgreSQL 9.6 -
8.6. Boolean Type") / [9.5](/docs/9.5/datatype-boolean.html "PostgreSQL 9.5 -
8.6. Boolean Type") / [9.4](/docs/9.4/datatype-boolean.html "PostgreSQL 9.4 -
8.6. Boolean Type") / [9.3](/docs/9.3/datatype-boolean.html "PostgreSQL 9.3 -
8.6. Boolean Type") / [9.2](/docs/9.2/datatype-boolean.html "PostgreSQL 9.2 -
8.6. Boolean Type") / [9.1](/docs/9.1/datatype-boolean.html "PostgreSQL 9.1 -
8.6. Boolean Type") / [9.0](/docs/9.0/datatype-boolean.html "PostgreSQL 9.0 -
8.6. Boolean Type") / [8.4](/docs/8.4/datatype-boolean.html "PostgreSQL 8.4 -
8.6. Boolean Type") / [8.3](/docs/8.3/datatype-boolean.html "PostgreSQL 8.3 -
8.6. Boolean Type") / [8.2](/docs/8.2/datatype-boolean.html "PostgreSQL 8.2 -
8.6. Boolean Type") / [8.1](/docs/8.1/datatype-boolean.html "PostgreSQL 8.1 -
8.6. Boolean Type") / [8.0](/docs/8.0/datatype-boolean.html "PostgreSQL 8.0 -
8.6. Boolean Type") / [7.4](/docs/7.4/datatype-boolean.html "PostgreSQL 7.4 -
8.6. Boolean Type") / [7.3](/docs/7.3/datatype-boolean.html "PostgreSQL 7.3 -
8.6. Boolean Type") / [7.2](/docs/7.2/datatype-boolean.html "PostgreSQL 7.2 -
8.6. Boolean Type") / [7.1](/docs/7.1/datatype-boolean.html "PostgreSQL 7.1 -
8.6. Boolean Type")

__

8.6. Boolean Type  
---  
[Prev](datatype-datetime.html "8.5. Date/Time Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-enum.html "8.7. Enumerated Types")  
  
* * *

## 8.6. Boolean Type #

PostgreSQL provides the standard SQL type `boolean`; see [Table
8.19](datatype-boolean.html#DATATYPE-BOOLEAN-TABLE "Table 8.19. Boolean Data
Type"). The `boolean` type can have several states: “true”, “false”, and a
third state, “unknown”, which is represented by the SQL null value.

**Table  8.19. Boolean Data Type**

Name | Storage Size | Description  
---|---|---  
`boolean` | 1 byte | state of true or false  
  
  

Boolean constants can be represented in SQL queries by the SQL key words
`TRUE`, `FALSE`, and `NULL`.

The datatype input function for type `boolean` accepts these string
representations for the “true” state:

`true`  
---  
`yes`  
`on`  
`1`  
  
and these representations for the “false” state:

`false`  
---  
`no`  
`off`  
`0`  
  
Unique prefixes of these strings are also accepted, for example `t` or `n`.
Leading or trailing whitespace is ignored, and case does not matter.

The datatype output function for type `boolean` always emits either `t` or
`f`, as shown in [Example 8.2](datatype-boolean.html#DATATYPE-BOOLEAN-EXAMPLE
"Example 8.2. Using the boolean Type").

**Example  8.2. Using the `boolean` Type**

    
    
    CREATE TABLE test1 (a boolean, b text);
    INSERT INTO test1 VALUES (TRUE, 'sic est');
    INSERT INTO test1 VALUES (FALSE, 'non est');
    SELECT * FROM test1;
     a |    b
    ---+---------
     t | sic est
     f | non est
    
    SELECT * FROM test1 WHERE a;
     a |    b
    ---+---------
     t | sic est
    

  

The key words `TRUE` and `FALSE` are the preferred (SQL-compliant) method for
writing Boolean constants in SQL queries. But you can also use the string
representations by following the generic string-literal constant syntax
described in [Section 4.1.2.7](sql-syntax-lexical.html#SQL-SYNTAX-CONSTANTS-
GENERIC "4.1.2.7. Constants of Other Types"), for example `'yes'::boolean`.

Note that the parser automatically understands that `TRUE` and `FALSE` are of
type `boolean`, but this is not so for `NULL` because that can have any type.
So in some contexts you might have to cast `NULL` to `boolean` explicitly, for
example `NULL::boolean`. Conversely, the cast can be omitted from a string-
literal Boolean value in contexts where the parser can deduce that the literal
must be of type `boolean`.

* * *

[Prev](datatype-datetime.html "8.5. Date/Time Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-enum.html "8.7. Enumerated Types")  
---|---|---  
8.5. Date/Time Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.7. Enumerated Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-boolean.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

