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

Supported Versions: [Current](/docs/current/datatype-bit.html "PostgreSQL 17 -
8.10. Bit String Types") ([17](/docs/17/datatype-bit.html "PostgreSQL 17 -
8.10. Bit String Types")) / [16](/docs/16/datatype-bit.html "PostgreSQL 16 -
8.10. Bit String Types") / [15](/docs/15/datatype-bit.html "PostgreSQL 15 -
8.10. Bit String Types") / [14](/docs/14/datatype-bit.html "PostgreSQL 14 -
8.10. Bit String Types") / [13](/docs/13/datatype-bit.html "PostgreSQL 13 -
8.10. Bit String Types")

Development Versions: [18](/docs/18/datatype-bit.html "PostgreSQL 18 -
8.10. Bit String Types") / [devel](/docs/devel/datatype-bit.html "PostgreSQL
devel - 8.10. Bit String Types")

Unsupported versions: [12](/docs/12/datatype-bit.html "PostgreSQL 12 -
8.10. Bit String Types") / [11](/docs/11/datatype-bit.html "PostgreSQL 11 -
8.10. Bit String Types") / [10](/docs/10/datatype-bit.html "PostgreSQL 10 -
8.10. Bit String Types") / [9.6](/docs/9.6/datatype-bit.html "PostgreSQL 9.6 -
8.10. Bit String Types") / [9.5](/docs/9.5/datatype-bit.html "PostgreSQL 9.5 -
8.10. Bit String Types") / [9.4](/docs/9.4/datatype-bit.html "PostgreSQL 9.4 -
8.10. Bit String Types") / [9.3](/docs/9.3/datatype-bit.html "PostgreSQL 9.3 -
8.10. Bit String Types") / [9.2](/docs/9.2/datatype-bit.html "PostgreSQL 9.2 -
8.10. Bit String Types") / [9.1](/docs/9.1/datatype-bit.html "PostgreSQL 9.1 -
8.10. Bit String Types") / [9.0](/docs/9.0/datatype-bit.html "PostgreSQL 9.0 -
8.10. Bit String Types") / [8.4](/docs/8.4/datatype-bit.html "PostgreSQL 8.4 -
8.10. Bit String Types") / [8.3](/docs/8.3/datatype-bit.html "PostgreSQL 8.3 -
8.10. Bit String Types") / [8.2](/docs/8.2/datatype-bit.html "PostgreSQL 8.2 -
8.10. Bit String Types") / [8.1](/docs/8.1/datatype-bit.html "PostgreSQL 8.1 -
8.10. Bit String Types") / [8.0](/docs/8.0/datatype-bit.html "PostgreSQL 8.0 -
8.10. Bit String Types") / [7.4](/docs/7.4/datatype-bit.html "PostgreSQL 7.4 -
8.10. Bit String Types") / [7.3](/docs/7.3/datatype-bit.html "PostgreSQL 7.3 -
8.10. Bit String Types") / [7.2](/docs/7.2/datatype-bit.html "PostgreSQL 7.2 -
8.10. Bit String Types") / [7.1](/docs/7.1/datatype-bit.html "PostgreSQL 7.1 -
8.10. Bit String Types")

__

8.10. Bit String Types  
---  
[Prev](datatype-net-types.html "8.9. Network Address Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-textsearch.html "8.11. Text Search Types")  
  
* * *

## 8.10. Bit String Types #

Bit strings are strings of 1's and 0's. They can be used to store or visualize
bit masks. There are two SQL bit types: `bit(_`n`_)` and `bit varying(_`n`_)`,
where _`n`_ is a positive integer.

`bit` type data must match the length _`n`_ exactly; it is an error to attempt
to store shorter or longer bit strings. `bit varying` data is of variable
length up to the maximum length _`n`_ ; longer strings will be rejected.
Writing `bit` without a length is equivalent to `bit(1)`, while `bit varying`
without a length specification means unlimited length.

### Note

If one explicitly casts a bit-string value to `bit(_`n`_)`, it will be
truncated or zero-padded on the right to be exactly _`n`_ bits, without
raising an error. Similarly, if one explicitly casts a bit-string value to
`bit varying(_`n`_)`, it will be truncated on the right if it is more than
_`n`_ bits.

Refer to [Section 4.1.2.5](sql-syntax-lexical.html#SQL-SYNTAX-BIT-STRINGS
"4.1.2.5. Bit-String Constants") for information about the syntax of bit
string constants. Bit-logical operators and string manipulation functions are
available; see [Section 9.6](functions-bitstring.html "9.6. Bit String
Functions and Operators").

**Example  8.3. Using the Bit String Types**

    
    
    CREATE TABLE test (a BIT(3), b BIT VARYING(5));
    INSERT INTO test VALUES (B'101', B'00');
    INSERT INTO test VALUES (B'10', B'101');
    
    ERROR:  bit string length 2 does not match type bit(3)
    
    INSERT INTO test VALUES (B'10'::bit(3), B'101');
    SELECT * FROM test;
    
      a  |  b
    -----+-----
     101 | 00
     100 | 101
    
    

  

A bit string value requires 1 byte for each group of 8 bits, plus 5 or 8 bytes
overhead depending on the length of the string (but long values may be
compressed or moved out-of-line, as explained in [Section 8.3](datatype-
character.html "8.3. Character Types") for character strings).

* * *

[Prev](datatype-net-types.html "8.9. Network Address Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-textsearch.html "8.11. Text Search Types")  
---|---|---  
8.9. Network Address Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.11. Text Search Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-bit.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

