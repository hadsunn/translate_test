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

Supported Versions: [Current](/docs/current/datatype-binary.html "PostgreSQL
17 - 8.4. Binary Data Types") ([17](/docs/17/datatype-binary.html "PostgreSQL
17 - 8.4. Binary Data Types")) / [16](/docs/16/datatype-binary.html
"PostgreSQL 16 - 8.4. Binary Data Types") / [15](/docs/15/datatype-binary.html
"PostgreSQL 15 - 8.4. Binary Data Types") / [14](/docs/14/datatype-binary.html
"PostgreSQL 14 - 8.4. Binary Data Types") / [13](/docs/13/datatype-binary.html
"PostgreSQL 13 - 8.4. Binary Data Types")

Development Versions: [18](/docs/18/datatype-binary.html "PostgreSQL 18 -
8.4. Binary Data Types") / [devel](/docs/devel/datatype-binary.html
"PostgreSQL devel - 8.4. Binary Data Types")

Unsupported versions: [12](/docs/12/datatype-binary.html "PostgreSQL 12 -
8.4. Binary Data Types") / [11](/docs/11/datatype-binary.html "PostgreSQL 11 -
8.4. Binary Data Types") / [10](/docs/10/datatype-binary.html "PostgreSQL 10 -
8.4. Binary Data Types") / [9.6](/docs/9.6/datatype-binary.html "PostgreSQL
9.6 - 8.4. Binary Data Types") / [9.5](/docs/9.5/datatype-binary.html
"PostgreSQL 9.5 - 8.4. Binary Data Types") / [9.4](/docs/9.4/datatype-
binary.html "PostgreSQL 9.4 - 8.4. Binary Data Types") /
[9.3](/docs/9.3/datatype-binary.html "PostgreSQL 9.3 - 8.4. Binary Data
Types") / [9.2](/docs/9.2/datatype-binary.html "PostgreSQL 9.2 - 8.4. Binary
Data Types") / [9.1](/docs/9.1/datatype-binary.html "PostgreSQL 9.1 -
8.4. Binary Data Types") / [9.0](/docs/9.0/datatype-binary.html "PostgreSQL
9.0 - 8.4. Binary Data Types") / [8.4](/docs/8.4/datatype-binary.html
"PostgreSQL 8.4 - 8.4. Binary Data Types") / [8.3](/docs/8.3/datatype-
binary.html "PostgreSQL 8.3 - 8.4. Binary Data Types") /
[8.2](/docs/8.2/datatype-binary.html "PostgreSQL 8.2 - 8.4. Binary Data
Types") / [8.1](/docs/8.1/datatype-binary.html "PostgreSQL 8.1 - 8.4. Binary
Data Types") / [8.0](/docs/8.0/datatype-binary.html "PostgreSQL 8.0 -
8.4. Binary Data Types") / [7.4](/docs/7.4/datatype-binary.html "PostgreSQL
7.4 - 8.4. Binary Data Types") / [7.3](/docs/7.3/datatype-binary.html
"PostgreSQL 7.3 - 8.4. Binary Data Types") / [7.2](/docs/7.2/datatype-
binary.html "PostgreSQL 7.2 - 8.4. Binary Data Types")

__

8.4. Binary Data Types  
---  
[Prev](datatype-character.html "8.3. Character Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-datetime.html "8.5. Date/Time Types")  
  
* * *

## 8.4. Binary Data Types #

[8.4.1. `bytea` Hex Format](datatype-binary.html#DATATYPE-BINARY-BYTEA-HEX-
FORMAT)

[8.4.2. `bytea` Escape Format](datatype-binary.html#DATATYPE-BINARY-BYTEA-
ESCAPE-FORMAT)

The `bytea` data type allows storage of binary strings; see [Table
8.6](datatype-binary.html#DATATYPE-BINARY-TABLE "Table 8.6. Binary Data
Types").

**Table  8.6. Binary Data Types**

Name | Storage Size | Description  
---|---|---  
`bytea` | 1 or 4 bytes plus the actual binary string | variable-length binary string  
  
  

A binary string is a sequence of octets (or bytes). Binary strings are
distinguished from character strings in two ways. First, binary strings
specifically allow storing octets of value zero and other “non-printable”
octets (usually, octets outside the decimal range 32 to 126). Character
strings disallow zero octets, and also disallow any other octet values and
sequences of octet values that are invalid according to the database's
selected character set encoding. Second, operations on binary strings process
the actual bytes, whereas the processing of character strings depends on
locale settings. In short, binary strings are appropriate for storing data
that the programmer thinks of as “raw bytes”, whereas character strings are
appropriate for storing text.

The `bytea` type supports two formats for input and output: “hex” format and
PostgreSQL's historical “escape” format. Both of these are always accepted on
input. The output format depends on the configuration parameter
[bytea_output](runtime-config-client.html#GUC-BYTEA-OUTPUT); the default is
hex. (Note that the hex format was introduced in PostgreSQL 9.0; earlier
versions and some tools don't understand it.)

The SQL standard defines a different binary string type, called `BLOB` or
`BINARY LARGE OBJECT`. The input format is different from `bytea`, but the
provided functions and operators are mostly the same.

### 8.4.1. `bytea` Hex Format #

The “hex” format encodes binary data as 2 hexadecimal digits per byte, most
significant nibble first. The entire string is preceded by the sequence `\x`
(to distinguish it from the escape format). In some contexts, the initial
backslash may need to be escaped by doubling it (see [Section 4.1.2.1](sql-
syntax-lexical.html#SQL-SYNTAX-STRINGS "4.1.2.1. String Constants")). For
input, the hexadecimal digits can be either upper or lower case, and
whitespace is permitted between digit pairs (but not within a digit pair nor
in the starting `\x` sequence). The hex format is compatible with a wide range
of external applications and protocols, and it tends to be faster to convert
than the escape format, so its use is preferred.

Example:

    
    
    SET bytea_output = 'hex';
    
    SELECT '\xDEADBEEF'::bytea;
       bytea
    ------------
     \xdeadbeef
    

### 8.4.2. `bytea` Escape Format #

The “escape” format is the traditional PostgreSQL format for the `bytea` type.
It takes the approach of representing a binary string as a sequence of ASCII
characters, while converting those bytes that cannot be represented as an
ASCII character into special escape sequences. If, from the point of view of
the application, representing bytes as characters makes sense, then this
representation can be convenient. But in practice it is usually confusing
because it fuzzes up the distinction between binary strings and character
strings, and also the particular escape mechanism that was chosen is somewhat
unwieldy. Therefore, this format should probably be avoided for most new
applications.

When entering `bytea` values in escape format, octets of certain values _must_
be escaped, while all octet values _can_ be escaped. In general, to escape an
octet, convert it into its three-digit octal value and precede it by a
backslash. Backslash itself (octet decimal value 92) can alternatively be
represented by double backslashes. [Table 8.7](datatype-binary.html#DATATYPE-
BINARY-SQLESC "Table 8.7. bytea Literal Escaped Octets") shows the characters
that must be escaped, and gives the alternative escape sequences where
applicable.

**Table  8.7. `bytea` Literal Escaped Octets**

Decimal Octet Value | Description | Escaped Input Representation | Example | Hex Representation  
---|---|---|---|---  
0 | zero octet | `'\000'` | `'\000'::bytea` | `\x00`  
39 | single quote | `''''` or `'\047'` | `''''::bytea` | `\x27`  
92 | backslash | `'\\'` or `'\134'` | `'\\'::bytea` | `\x5c`  
0 to 31 and 127 to 255 | “non-printable” octets | `'\_`xxx'`_` (octal value) | `'\001'::bytea` | `\x01`  
  
  

The requirement to escape _non-printable_ octets varies depending on locale
settings. In some instances you can get away with leaving them unescaped.

The reason that single quotes must be doubled, as shown in [Table
8.7](datatype-binary.html#DATATYPE-BINARY-SQLESC "Table 8.7. bytea Literal
Escaped Octets"), is that this is true for any string literal in an SQL
command. The generic string-literal parser consumes the outermost single
quotes and reduces any pair of single quotes to one data character. What the
`bytea` input function sees is just one single quote, which it treats as a
plain data character. However, the `bytea` input function treats backslashes
as special, and the other behaviors shown in [Table 8.7](datatype-
binary.html#DATATYPE-BINARY-SQLESC "Table 8.7. bytea Literal Escaped Octets")
are implemented by that function.

In some contexts, backslashes must be doubled compared to what is shown above,
because the generic string-literal parser will also reduce pairs of
backslashes to one data character; see [Section 4.1.2.1](sql-syntax-
lexical.html#SQL-SYNTAX-STRINGS "4.1.2.1. String Constants").

`Bytea` octets are output in `hex` format by default. If you change
[bytea_output](runtime-config-client.html#GUC-BYTEA-OUTPUT) to `escape`, “non-
printable” octets are converted to their equivalent three-digit octal value
and preceded by one backslash. Most “printable” octets are output by their
standard representation in the client character set, e.g.:

    
    
    SET bytea_output = 'escape';
    
    SELECT 'abc \153\154\155 \052\251\124'::bytea;
         bytea
    ----------------
     abc klm *\251T
    

The octet with decimal value 92 (backslash) is doubled in the output. Details
are in [Table 8.8](datatype-binary.html#DATATYPE-BINARY-RESESC
"Table 8.8. bytea Output Escaped Octets").

**Table  8.8. `bytea` Output Escaped Octets**

Decimal Octet Value | Description | Escaped Output Representation | Example | Output Result  
---|---|---|---|---  
92 | backslash | `\\` | `'\134'::bytea` | `\\`  
0 to 31 and 127 to 255 | “non-printable” octets | `\_`xxx`_` (octal value) | `'\001'::bytea` | `\001`  
32 to 126 | “printable” octets | client character set representation | `'\176'::bytea` | `~`  
  
  

Depending on the front end to PostgreSQL you use, you might have additional
work to do in terms of escaping and unescaping `bytea` strings. For example,
you might also have to escape line feeds and carriage returns if your
interface automatically translates these.

* * *

[Prev](datatype-character.html "8.3. Character Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-datetime.html "8.5. Date/Time Types")  
---|---|---  
8.3. Character Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.5. Date/Time Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-binary.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

