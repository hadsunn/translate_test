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

Supported Versions: [Current](/docs/current/datatype-money.html "PostgreSQL 17
- 8.2. Monetary Types") ([17](/docs/17/datatype-money.html "PostgreSQL 17 -
8.2. Monetary Types")) / [16](/docs/16/datatype-money.html "PostgreSQL 16 -
8.2. Monetary Types") / [15](/docs/15/datatype-money.html "PostgreSQL 15 -
8.2. Monetary Types") / [14](/docs/14/datatype-money.html "PostgreSQL 14 -
8.2. Monetary Types") / [13](/docs/13/datatype-money.html "PostgreSQL 13 -
8.2. Monetary Types")

Development Versions: [18](/docs/18/datatype-money.html "PostgreSQL 18 -
8.2. Monetary Types") / [devel](/docs/devel/datatype-money.html "PostgreSQL
devel - 8.2. Monetary Types")

Unsupported versions: [12](/docs/12/datatype-money.html "PostgreSQL 12 -
8.2. Monetary Types") / [11](/docs/11/datatype-money.html "PostgreSQL 11 -
8.2. Monetary Types") / [10](/docs/10/datatype-money.html "PostgreSQL 10 -
8.2. Monetary Types") / [9.6](/docs/9.6/datatype-money.html "PostgreSQL 9.6 -
8.2. Monetary Types") / [9.5](/docs/9.5/datatype-money.html "PostgreSQL 9.5 -
8.2. Monetary Types") / [9.4](/docs/9.4/datatype-money.html "PostgreSQL 9.4 -
8.2. Monetary Types") / [9.3](/docs/9.3/datatype-money.html "PostgreSQL 9.3 -
8.2. Monetary Types") / [9.2](/docs/9.2/datatype-money.html "PostgreSQL 9.2 -
8.2. Monetary Types") / [9.1](/docs/9.1/datatype-money.html "PostgreSQL 9.1 -
8.2. Monetary Types") / [9.0](/docs/9.0/datatype-money.html "PostgreSQL 9.0 -
8.2. Monetary Types") / [8.4](/docs/8.4/datatype-money.html "PostgreSQL 8.4 -
8.2. Monetary Types") / [8.3](/docs/8.3/datatype-money.html "PostgreSQL 8.3 -
8.2. Monetary Types") / [8.2](/docs/8.2/datatype-money.html "PostgreSQL 8.2 -
8.2. Monetary Types") / [8.1](/docs/8.1/datatype-money.html "PostgreSQL 8.1 -
8.2. Monetary Types") / [8.0](/docs/8.0/datatype-money.html "PostgreSQL 8.0 -
8.2. Monetary Types") / [7.4](/docs/7.4/datatype-money.html "PostgreSQL 7.4 -
8.2. Monetary Types") / [7.3](/docs/7.3/datatype-money.html "PostgreSQL 7.3 -
8.2. Monetary Types") / [7.2](/docs/7.2/datatype-money.html "PostgreSQL 7.2 -
8.2. Monetary Types") / [7.1](/docs/7.1/datatype-money.html "PostgreSQL 7.1 -
8.2. Monetary Types")

__

8.2. Monetary Types  
---  
[Prev](datatype-numeric.html "8.1. Numeric Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-character.html "8.3. Character Types")  
  
* * *

## 8.2. Monetary Types #

The `money` type stores a currency amount with a fixed fractional precision;
see [Table 8.3](datatype-money.html#DATATYPE-MONEY-TABLE "Table 8.3. Monetary
Types"). The fractional precision is determined by the database's
[lc_monetary](runtime-config-client.html#GUC-LC-MONETARY) setting. The range
shown in the table assumes there are two fractional digits. Input is accepted
in a variety of formats, including integer and floating-point literals, as
well as typical currency formatting, such as `'$1,000.00'`. Output is
generally in the latter form but depends on the locale.

**Table  8.3. Monetary Types**

Name | Storage Size | Description | Range  
---|---|---|---  
`money` | 8 bytes | currency amount | -92233720368547758.08 to +92233720368547758.07  
  
  

Since the output of this data type is locale-sensitive, it might not work to
load `money` data into a database that has a different setting of
`lc_monetary`. To avoid problems, before restoring a dump into a new database
make sure `lc_monetary` has the same or equivalent value as in the database
that was dumped.

Values of the `numeric`, `int`, and `bigint` data types can be cast to
`money`. Conversion from the `real` and `double precision` data types can be
done by casting to `numeric` first, for example:

    
    
    SELECT '12.34'::float8::numeric::money;
    

However, this is not recommended. Floating point numbers should not be used to
handle money due to the potential for rounding errors.

A `money` value can be cast to `numeric` without loss of precision. Conversion
to other types could potentially lose precision, and must also be done in two
stages:

    
    
    SELECT '52093.89'::money::numeric::float8;
    

Division of a `money` value by an integer value is performed with truncation
of the fractional part towards zero. To get a rounded result, divide by a
floating-point value, or cast the `money` value to `numeric` before dividing
and back to `money` afterwards. (The latter is preferable to avoid risking
precision loss.) When a `money` value is divided by another `money` value, the
result is `double precision` (i.e., a pure number, not money); the currency
units cancel each other out in the division.

* * *

[Prev](datatype-numeric.html "8.1. Numeric Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-character.html "8.3. Character Types")  
---|---|---  
8.1. Numeric Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.3. Character Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-money.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

