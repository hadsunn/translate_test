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

Supported Versions: [Current](/docs/current/parser-stage.html "PostgreSQL 17 -
52.3. The Parser Stage") ([17](/docs/17/parser-stage.html "PostgreSQL 17 -
52.3. The Parser Stage")) / [16](/docs/16/parser-stage.html "PostgreSQL 16 -
52.3. The Parser Stage") / [15](/docs/15/parser-stage.html "PostgreSQL 15 -
52.3. The Parser Stage") / [14](/docs/14/parser-stage.html "PostgreSQL 14 -
52.3. The Parser Stage") / [13](/docs/13/parser-stage.html "PostgreSQL 13 -
52.3. The Parser Stage")

Development Versions: [18](/docs/18/parser-stage.html "PostgreSQL 18 -
52.3. The Parser Stage") / [devel](/docs/devel/parser-stage.html "PostgreSQL
devel - 52.3. The Parser Stage")

Unsupported versions: [12](/docs/12/parser-stage.html "PostgreSQL 12 -
52.3. The Parser Stage") / [11](/docs/11/parser-stage.html "PostgreSQL 11 -
52.3. The Parser Stage") / [10](/docs/10/parser-stage.html "PostgreSQL 10 -
52.3. The Parser Stage") / [9.6](/docs/9.6/parser-stage.html "PostgreSQL 9.6 -
52.3. The Parser Stage") / [9.5](/docs/9.5/parser-stage.html "PostgreSQL 9.5 -
52.3. The Parser Stage") / [9.4](/docs/9.4/parser-stage.html "PostgreSQL 9.4 -
52.3. The Parser Stage") / [9.3](/docs/9.3/parser-stage.html "PostgreSQL 9.3 -
52.3. The Parser Stage") / [9.2](/docs/9.2/parser-stage.html "PostgreSQL 9.2 -
52.3. The Parser Stage") / [9.1](/docs/9.1/parser-stage.html "PostgreSQL 9.1 -
52.3. The Parser Stage") / [9.0](/docs/9.0/parser-stage.html "PostgreSQL 9.0 -
52.3. The Parser Stage") / [8.4](/docs/8.4/parser-stage.html "PostgreSQL 8.4 -
52.3. The Parser Stage") / [8.3](/docs/8.3/parser-stage.html "PostgreSQL 8.3 -
52.3. The Parser Stage") / [8.2](/docs/8.2/parser-stage.html "PostgreSQL 8.2 -
52.3. The Parser Stage") / [8.1](/docs/8.1/parser-stage.html "PostgreSQL 8.1 -
52.3. The Parser Stage") / [8.0](/docs/8.0/parser-stage.html "PostgreSQL 8.0 -
52.3. The Parser Stage") / [7.4](/docs/7.4/parser-stage.html "PostgreSQL 7.4 -
52.3. The Parser Stage") / [7.3](/docs/7.3/parser-stage.html "PostgreSQL 7.3 -
52.3. The Parser Stage") / [7.2](/docs/7.2/parser-stage.html "PostgreSQL 7.2 -
52.3. The Parser Stage") / [7.1](/docs/7.1/parser-stage.html "PostgreSQL 7.1 -
52.3. The Parser Stage")

__

52.3. The Parser Stage  
---  
[Prev](connect-estab.html "52.2. How Connections Are Established")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") | Chapter 52. Overview of PostgreSQL Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](rule-system.html "52.4. The PostgreSQL Rule System")  
  
* * *

## 52.3. The Parser Stage #

[52.3.1. Parser](parser-stage.html#PARSER-STAGE-PARSER)

[52.3.2. Transformation Process](parser-stage.html#PARSER-STAGE-
TRANSFORMATION-PROCESS)

The _parser stage_ consists of two parts:

  * The _parser_ defined in `gram.y` and `scan.l` is built using the Unix tools bison and flex.

  * The _transformation process_ does modifications and augmentations to the data structures returned by the parser.

### 52.3.1. Parser #

The parser has to check the query string (which arrives as plain text) for
valid syntax. If the syntax is correct a _parse tree_ is built up and handed
back; otherwise an error is returned. The parser and lexer are implemented
using the well-known Unix tools bison and flex.

The _lexer_ is defined in the file `scan.l` and is responsible for recognizing
_identifiers_ , the _SQL key words_ etc. For every key word or identifier that
is found, a _token_ is generated and handed to the parser.

The parser is defined in the file `gram.y` and consists of a set of _grammar
rules_ and _actions_ that are executed whenever a rule is fired. The code of
the actions (which is actually C code) is used to build up the parse tree.

The file `scan.l` is transformed to the C source file `scan.c` using the
program flex and `gram.y` is transformed to `gram.c` using bison. After these
transformations have taken place a normal C compiler can be used to create the
parser. Never make any changes to the generated C files as they will be
overwritten the next time flex or bison is called.

### Note

The mentioned transformations and compilations are normally done automatically
using the _makefiles_ shipped with the PostgreSQL source distribution.

A detailed description of bison or the grammar rules given in `gram.y` would
be beyond the scope of this manual. There are many books and documents dealing
with flex and bison. You should be familiar with bison before you start to
study the grammar given in `gram.y` otherwise you won't understand what
happens there.

### 52.3.2. Transformation Process #

The parser stage creates a parse tree using only fixed rules about the
syntactic structure of SQL. It does not make any lookups in the system
catalogs, so there is no possibility to understand the detailed semantics of
the requested operations. After the parser completes, the _transformation
process_ takes the tree handed back by the parser as input and does the
semantic interpretation needed to understand which tables, functions, and
operators are referenced by the query. The data structure that is built to
represent this information is called the _query tree_.

The reason for separating raw parsing from semantic analysis is that system
catalog lookups can only be done within a transaction, and we do not wish to
start a transaction immediately upon receiving a query string. The raw parsing
stage is sufficient to identify the transaction control commands (`BEGIN`,
`ROLLBACK`, etc.), and these can then be correctly executed without any
further analysis. Once we know that we are dealing with an actual query (such
as `SELECT` or `UPDATE`), it is okay to start a transaction if we're not
already in one. Only then can the transformation process be invoked.

The query tree created by the transformation process is structurally similar
to the raw parse tree in most places, but it has many differences in detail.
For example, a `FuncCall` node in the parse tree represents something that
looks syntactically like a function call. This might be transformed to either
a `FuncExpr` or `Aggref` node depending on whether the referenced name turns
out to be an ordinary function or an aggregate function. Also, information
about the actual data types of columns and expression results is added to the
query tree.

* * *

[Prev](connect-estab.html "52.2. How Connections Are Established")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") |  [Next](rule-system.html "52.4. The PostgreSQL Rule System")  
---|---|---  
52.2. How Connections Are Established  | [Home](index.html "PostgreSQL 16.9 Documentation") |  52.4. The PostgreSQL Rule System  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/parser-stage.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

