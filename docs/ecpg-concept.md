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

Supported Versions: [Current](/docs/current/ecpg-concept.html "PostgreSQL 17 -
36.1. The Concept") ([17](/docs/17/ecpg-concept.html "PostgreSQL 17 -
36.1. The Concept")) / [16](/docs/16/ecpg-concept.html "PostgreSQL 16 -
36.1. The Concept") / [15](/docs/15/ecpg-concept.html "PostgreSQL 15 -
36.1. The Concept") / [14](/docs/14/ecpg-concept.html "PostgreSQL 14 -
36.1. The Concept") / [13](/docs/13/ecpg-concept.html "PostgreSQL 13 -
36.1. The Concept")

Development Versions: [18](/docs/18/ecpg-concept.html "PostgreSQL 18 -
36.1. The Concept") / [devel](/docs/devel/ecpg-concept.html "PostgreSQL devel
- 36.1. The Concept")

Unsupported versions: [12](/docs/12/ecpg-concept.html "PostgreSQL 12 -
36.1. The Concept") / [11](/docs/11/ecpg-concept.html "PostgreSQL 11 -
36.1. The Concept") / [10](/docs/10/ecpg-concept.html "PostgreSQL 10 -
36.1. The Concept") / [9.6](/docs/9.6/ecpg-concept.html "PostgreSQL 9.6 -
36.1. The Concept") / [9.5](/docs/9.5/ecpg-concept.html "PostgreSQL 9.5 -
36.1. The Concept") / [9.4](/docs/9.4/ecpg-concept.html "PostgreSQL 9.4 -
36.1. The Concept") / [9.3](/docs/9.3/ecpg-concept.html "PostgreSQL 9.3 -
36.1. The Concept") / [9.2](/docs/9.2/ecpg-concept.html "PostgreSQL 9.2 -
36.1. The Concept") / [9.1](/docs/9.1/ecpg-concept.html "PostgreSQL 9.1 -
36.1. The Concept") / [9.0](/docs/9.0/ecpg-concept.html "PostgreSQL 9.0 -
36.1. The Concept") / [8.4](/docs/8.4/ecpg-concept.html "PostgreSQL 8.4 -
36.1. The Concept") / [8.3](/docs/8.3/ecpg-concept.html "PostgreSQL 8.3 -
36.1. The Concept") / [8.2](/docs/8.2/ecpg-concept.html "PostgreSQL 8.2 -
36.1. The Concept") / [7.2](/docs/7.2/ecpg-concept.html "PostgreSQL 7.2 -
36.1. The Concept") / [7.1](/docs/7.1/ecpg-concept.html "PostgreSQL 7.1 -
36.1. The Concept")

__

36.1. The Concept  
---  
[Prev](ecpg.html "Chapter 36. ECPG — Embedded SQL in C")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-connect.html "36.2. Managing Database Connections")  
  
* * *

## 36.1. The Concept #

An embedded SQL program consists of code written in an ordinary programming
language, in this case C, mixed with SQL commands in specially marked
sections. To build the program, the source code (`*.pgc`) is first passed
through the embedded SQL preprocessor, which converts it to an ordinary C
program (`*.c`), and afterwards it can be processed by a C compiler. (For
details about the compiling and linking see [Section 36.10](ecpg-process.html
"36.10. Processing Embedded SQL Programs").) Converted ECPG applications call
functions in the libpq library through the embedded SQL library (ecpglib), and
communicate with the PostgreSQL server using the normal frontend-backend
protocol.

Embedded SQL has advantages over other methods for handling SQL commands from
C code. First, it takes care of the tedious passing of information to and from
variables in your C program. Second, the SQL code in the program is checked at
build time for syntactical correctness. Third, embedded SQL in C is specified
in the SQL standard and supported by many other SQL database systems. The
PostgreSQL implementation is designed to match this standard as much as
possible, and it is usually possible to port embedded SQL programs written for
other SQL databases to PostgreSQL with relative ease.

As already stated, programs written for the embedded SQL interface are normal
C programs with special code inserted to perform database-related actions.
This special code always has the form:

    
    
    EXEC SQL ...;
    

These statements syntactically take the place of a C statement. Depending on
the particular statement, they can appear at the global level or within a
function.

Embedded SQL statements follow the case-sensitivity rules of normal SQL code,
and not those of C. Also they allow nested C-style comments as per the SQL
standard. The C part of the program, however, follows the C standard of not
accepting nested comments. Embedded SQL statements likewise use SQL rules, not
C rules, for parsing quoted strings and identifiers. (See [Section
4.1.2.1](sql-syntax-lexical.html#SQL-SYNTAX-STRINGS "4.1.2.1. String
Constants") and [Section 4.1.1](sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS
"4.1.1. Identifiers and Key Words") respectively. Note that ECPG assumes that
`standard_conforming_strings` is `on`.) Of course, the C part of the program
follows C quoting rules.

The following sections explain all the embedded SQL statements.

* * *

[Prev](ecpg.html "Chapter 36. ECPG — Embedded SQL in C")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-connect.html "36.2. Managing Database Connections")  
---|---|---  
Chapter 36. ECPG — Embedded SQL in C  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.2. Managing Database Connections  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-concept.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

