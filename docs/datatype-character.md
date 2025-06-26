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

Supported Versions: [Current](/docs/current/datatype-character.html
"PostgreSQL 17 - 8.3. Character Types") ([17](/docs/17/datatype-character.html
"PostgreSQL 17 - 8.3. Character Types")) / [16](/docs/16/datatype-
character.html "PostgreSQL 16 - 8.3. Character Types") /
[15](/docs/15/datatype-character.html "PostgreSQL 15 - 8.3. Character Types")
/ [14](/docs/14/datatype-character.html "PostgreSQL 14 - 8.3. Character
Types") / [13](/docs/13/datatype-character.html "PostgreSQL 13 -
8.3. Character Types")

Development Versions: [18](/docs/18/datatype-character.html "PostgreSQL 18 -
8.3. Character Types") / [devel](/docs/devel/datatype-character.html
"PostgreSQL devel - 8.3. Character Types")

Unsupported versions: [12](/docs/12/datatype-character.html "PostgreSQL 12 -
8.3. Character Types") / [11](/docs/11/datatype-character.html "PostgreSQL 11
- 8.3. Character Types") / [10](/docs/10/datatype-character.html "PostgreSQL
10 - 8.3. Character Types") / [9.6](/docs/9.6/datatype-character.html
"PostgreSQL 9.6 - 8.3. Character Types") / [9.5](/docs/9.5/datatype-
character.html "PostgreSQL 9.5 - 8.3. Character Types") /
[9.4](/docs/9.4/datatype-character.html "PostgreSQL 9.4 - 8.3. Character
Types") / [9.3](/docs/9.3/datatype-character.html "PostgreSQL 9.3 -
8.3. Character Types") / [9.2](/docs/9.2/datatype-character.html "PostgreSQL
9.2 - 8.3. Character Types") / [9.1](/docs/9.1/datatype-character.html
"PostgreSQL 9.1 - 8.3. Character Types") / [9.0](/docs/9.0/datatype-
character.html "PostgreSQL 9.0 - 8.3. Character Types") /
[8.4](/docs/8.4/datatype-character.html "PostgreSQL 8.4 - 8.3. Character
Types") / [8.3](/docs/8.3/datatype-character.html "PostgreSQL 8.3 -
8.3. Character Types") / [8.2](/docs/8.2/datatype-character.html "PostgreSQL
8.2 - 8.3. Character Types") / [8.1](/docs/8.1/datatype-character.html
"PostgreSQL 8.1 - 8.3. Character Types") / [8.0](/docs/8.0/datatype-
character.html "PostgreSQL 8.0 - 8.3. Character Types") /
[7.4](/docs/7.4/datatype-character.html "PostgreSQL 7.4 - 8.3. Character
Types") / [7.3](/docs/7.3/datatype-character.html "PostgreSQL 7.3 -
8.3. Character Types") / [7.2](/docs/7.2/datatype-character.html "PostgreSQL
7.2 - 8.3. Character Types") / [7.1](/docs/7.1/datatype-character.html
"PostgreSQL 7.1 - 8.3. Character Types")

__

8.3. Character Types  
---  
[Prev](datatype-money.html "8.2. Monetary Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-binary.html "8.4. Binary Data Types")  
  
* * *

## 8.3. Character Types #

**Table  8.4. Character Types**

Name | Description  
---|---  
`character varying(_`n`_)`, `varchar(_`n`_)` | variable-length with limit  
`character(_`n`_)`, `char(_`n`_)`, `bpchar(_`n`_)` | fixed-length, blank-padded  
`bpchar` | variable unlimited length, blank-trimmed  
`text` | variable unlimited length  
  
  

[Table 8.4](datatype-character.html#DATATYPE-CHARACTER-TABLE
"Table 8.4. Character Types") shows the general-purpose character types
available in PostgreSQL.

SQL defines two primary character types: `character varying(_`n`_)` and
`character(_`n`_)`, where _`n`_ is a positive integer. Both of these types can
store strings up to _`n`_ characters (not bytes) in length. An attempt to
store a longer string into a column of these types will result in an error,
unless the excess characters are all spaces, in which case the string will be
truncated to the maximum length. (This somewhat bizarre exception is required
by the SQL standard.) However, if one explicitly casts a value to `character
varying(_`n`_)` or `character(_`n`_)`, then an over-length value will be
truncated to _`n`_ characters without raising an error. (This too is required
by the SQL standard.) If the string to be stored is shorter than the declared
length, values of type `character` will be space-padded; values of type
`character varying` will simply store the shorter string.

In addition, PostgreSQL provides the `text` type, which stores strings of any
length. Although the `text` type is not in the SQL standard, several other SQL
database management systems have it as well. `text` is PostgreSQL's native
string data type, in that most built-in functions operating on strings are
declared to take or return `text` not `character varying`. For many purposes,
`character varying` acts as though it were a [domain](domains.html
"8.18. Domain Types") over `text`.

The type name `varchar` is an alias for `character varying`, while `bpchar`
(with length specifier) and `char` are aliases for `character`. The `varchar`
and `char` aliases are defined in the SQL standard; `bpchar` is a PostgreSQL
extension.

If specified, the length _`n`_ must be greater than zero and cannot exceed
10,485,760. If `character varying` (or `varchar`) is used without length
specifier, the type accepts strings of any length. If `bpchar` lacks a length
specifier, it also accepts strings of any length, but trailing spaces are
semantically insignificant. If `character` (or `char`) lacks a specifier, it
is equivalent to `character(1)`.

Values of type `character` are physically padded with spaces to the specified
width _`n`_ , and are stored and displayed that way. However, trailing spaces
are treated as semantically insignificant and disregarded when comparing two
values of type `character`. In collations where whitespace is significant,
this behavior can produce unexpected results; for example `SELECT 'a
'::CHAR(2) collate "C" < E'a\n'::CHAR(2)` returns true, even though `C` locale
would consider a space to be greater than a newline. Trailing spaces are
removed when converting a `character` value to one of the other string types.
Note that trailing spaces _are_ semantically significant in `character
varying` and `text` values, and when using pattern matching, that is `LIKE`
and regular expressions.

The characters that can be stored in any of these data types are determined by
the database character set, which is selected when the database is created.
Regardless of the specific character set, the character with code zero
(sometimes called NUL) cannot be stored. For more information refer to
[Section 24.3](multibyte.html "24.3. Character Set Support").

The storage requirement for a short string (up to 126 bytes) is 1 byte plus
the actual string, which includes the space padding in the case of
`character`. Longer strings have 4 bytes of overhead instead of 1. Long
strings are compressed by the system automatically, so the physical
requirement on disk might be less. Very long values are also stored in
background tables so that they do not interfere with rapid access to shorter
column values. In any case, the longest possible character string that can be
stored is about 1 GB. (The maximum value that will be allowed for _`n`_ in the
data type declaration is less than that. It wouldn't be useful to change this
because with multibyte character encodings the number of characters and bytes
can be quite different. If you desire to store long strings with no specific
upper limit, use `text` or `character varying` without a length specifier,
rather than making up an arbitrary length limit.)

### Tip

There is no performance difference among these three types, apart from
increased storage space when using the blank-padded type, and a few extra CPU
cycles to check the length when storing into a length-constrained column.
While `character(_`n`_)` has performance advantages in some other database
systems, there is no such advantage in PostgreSQL; in fact `character(_`n`_)`
is usually the slowest of the three because of its additional storage costs.
In most situations `text` or `character varying` should be used instead.

Refer to [Section 4.1.2.1](sql-syntax-lexical.html#SQL-SYNTAX-STRINGS
"4.1.2.1. String Constants") for information about the syntax of string
literals, and to [Chapter 9](functions.html "Chapter 9. Functions and
Operators") for information about available operators and functions.

**Example  8.1. Using the Character Types**

    
    
    CREATE TABLE test1 (a character(4));
    INSERT INTO test1 VALUES ('ok');
    SELECT a, char_length(a) FROM test1; -- (1)
    
      a   | char_length
    ------+-------------
     ok   |           2
    
    
    CREATE TABLE test2 (b varchar(5));
    INSERT INTO test2 VALUES ('ok');
    INSERT INTO test2 VALUES ('good      ');
    INSERT INTO test2 VALUES ('too long');
    ERROR:  value too long for type character varying(5)
    INSERT INTO test2 VALUES ('too long'::varchar(5)); -- explicit truncation
    SELECT b, char_length(b) FROM test2;
    
       b   | char_length
    -------+-------------
     ok    |           2
     good  |           5
     too l |           5
    
    

(1) |  The `char_length` function is discussed in [Section 9.4](functions-string.html "9.4. String Functions and Operators").  
---|---  
  
  

There are two other fixed-length character types in PostgreSQL, shown in
[Table 8.5](datatype-character.html#DATATYPE-CHARACTER-SPECIAL-TABLE
"Table 8.5. Special Character Types"). These are not intended for general-
purpose use, only for use in the internal system catalogs. The `name` type is
used to store identifiers. Its length is currently defined as 64 bytes (63
usable characters plus terminator) but should be referenced using the constant
`NAMEDATALEN` in `C` source code. The length is set at compile time (and is
therefore adjustable for special uses); the default maximum length might
change in a future release. The type `"char"` (note the quotes) is different
from `char(1)` in that it only uses one byte of storage, and therefore can
store only a single ASCII character. It is used in the system catalogs as a
simplistic enumeration type.

**Table  8.5. Special Character Types**

Name | Storage Size | Description  
---|---|---  
`"char"` | 1 byte | single-byte internal type  
`name` | 64 bytes | internal type for object names  
  
  

* * *

[Prev](datatype-money.html "8.2. Monetary Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-binary.html "8.4. Binary Data Types")  
---|---|---  
8.2. Monetary Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.4. Binary Data Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-character.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

