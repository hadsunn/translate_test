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

Supported Versions: [Current](/docs/current/datatype-pseudo.html "PostgreSQL
17 - 8.21. Pseudo-Types") ([17](/docs/17/datatype-pseudo.html "PostgreSQL 17 -
8.21. Pseudo-Types")) / [16](/docs/16/datatype-pseudo.html "PostgreSQL 16 -
8.21. Pseudo-Types") / [15](/docs/15/datatype-pseudo.html "PostgreSQL 15 -
8.21. Pseudo-Types") / [14](/docs/14/datatype-pseudo.html "PostgreSQL 14 -
8.21. Pseudo-Types") / [13](/docs/13/datatype-pseudo.html "PostgreSQL 13 -
8.21. Pseudo-Types")

Development Versions: [18](/docs/18/datatype-pseudo.html "PostgreSQL 18 -
8.21. Pseudo-Types") / [devel](/docs/devel/datatype-pseudo.html "PostgreSQL
devel - 8.21. Pseudo-Types")

Unsupported versions: [12](/docs/12/datatype-pseudo.html "PostgreSQL 12 -
8.21. Pseudo-Types") / [11](/docs/11/datatype-pseudo.html "PostgreSQL 11 -
8.21. Pseudo-Types") / [10](/docs/10/datatype-pseudo.html "PostgreSQL 10 -
8.21. Pseudo-Types") / [9.6](/docs/9.6/datatype-pseudo.html "PostgreSQL 9.6 -
8.21. Pseudo-Types") / [9.5](/docs/9.5/datatype-pseudo.html "PostgreSQL 9.5 -
8.21. Pseudo-Types") / [9.4](/docs/9.4/datatype-pseudo.html "PostgreSQL 9.4 -
8.21. Pseudo-Types") / [9.3](/docs/9.3/datatype-pseudo.html "PostgreSQL 9.3 -
8.21. Pseudo-Types") / [9.2](/docs/9.2/datatype-pseudo.html "PostgreSQL 9.2 -
8.21. Pseudo-Types") / [9.1](/docs/9.1/datatype-pseudo.html "PostgreSQL 9.1 -
8.21. Pseudo-Types") / [9.0](/docs/9.0/datatype-pseudo.html "PostgreSQL 9.0 -
8.21. Pseudo-Types") / [8.4](/docs/8.4/datatype-pseudo.html "PostgreSQL 8.4 -
8.21. Pseudo-Types") / [8.3](/docs/8.3/datatype-pseudo.html "PostgreSQL 8.3 -
8.21. Pseudo-Types") / [8.2](/docs/8.2/datatype-pseudo.html "PostgreSQL 8.2 -
8.21. Pseudo-Types") / [8.1](/docs/8.1/datatype-pseudo.html "PostgreSQL 8.1 -
8.21. Pseudo-Types") / [8.0](/docs/8.0/datatype-pseudo.html "PostgreSQL 8.0 -
8.21. Pseudo-Types") / [7.4](/docs/7.4/datatype-pseudo.html "PostgreSQL 7.4 -
8.21. Pseudo-Types") / [7.3](/docs/7.3/datatype-pseudo.html "PostgreSQL 7.3 -
8.21. Pseudo-Types")

__

8.21. Pseudo-Types  
---  
[Prev](datatype-pg-lsn.html "8.20. pg_lsn Type")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions.html "Chapter 9. Functions and Operators")  
  
* * *

## 8.21. Pseudo-Types #

The PostgreSQL type system contains a number of special-purpose entries that
are collectively called _pseudo-types_. A pseudo-type cannot be used as a
column data type, but it can be used to declare a function's argument or
result type. Each of the available pseudo-types is useful in situations where
a function's behavior does not correspond to simply taking or returning a
value of a specific SQL data type. [Table 8.27](datatype-pseudo.html#DATATYPE-
PSEUDOTYPES-TABLE "Table 8.27. Pseudo-Types") lists the existing pseudo-types.

**Table  8.27. Pseudo-Types**

Name | Description  
---|---  
`any` | Indicates that a function accepts any input data type.  
`anyelement` | Indicates that a function accepts any data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types")).  
`anyarray` | Indicates that a function accepts any array data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types")).  
`anynonarray` | Indicates that a function accepts any non-array data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types")).  
`anyenum` | Indicates that a function accepts any enum data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types") and [Section 8.7](datatype-enum.html "8.7. Enumerated Types")).  
`anyrange` | Indicates that a function accepts any range data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types") and [Section 8.17](rangetypes.html "8.17. Range Types")).  
`anymultirange` | Indicates that a function accepts any multirange data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types") and [Section 8.17](rangetypes.html "8.17. Range Types")).  
`anycompatible` | Indicates that a function accepts any data type, with automatic promotion of multiple arguments to a common data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types")).  
`anycompatiblearray` | Indicates that a function accepts any array data type, with automatic promotion of multiple arguments to a common data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types")).  
`anycompatiblenonarray` | Indicates that a function accepts any non-array data type, with automatic promotion of multiple arguments to a common data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types")).  
`anycompatiblerange` | Indicates that a function accepts any range data type, with automatic promotion of multiple arguments to a common data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types") and [Section 8.17](rangetypes.html "8.17. Range Types")).  
`anycompatiblemultirange` | Indicates that a function accepts any multirange data type, with automatic promotion of multiple arguments to a common data type (see [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC "38.2.5. Polymorphic Types") and [Section 8.17](rangetypes.html "8.17. Range Types")).  
`cstring` | Indicates that a function accepts or returns a null-terminated C string.  
`internal` | Indicates that a function accepts or returns a server-internal data type.  
`language_handler` | A procedural language call handler is declared to return `language_handler`.  
`fdw_handler` | A foreign-data wrapper handler is declared to return `fdw_handler`.  
`table_am_handler` | A table access method handler is declared to return `table_am_handler`.  
`index_am_handler` | An index access method handler is declared to return `index_am_handler`.  
`tsm_handler` | A tablesample method handler is declared to return `tsm_handler`.  
`record` | Identifies a function taking or returning an unspecified row type.  
`trigger` | A trigger function is declared to return `trigger.`  
`event_trigger` | An event trigger function is declared to return `event_trigger.`  
`pg_ddl_command` | Identifies a representation of DDL commands that is available to event triggers.  
`void` | Indicates that a function returns no value.  
`unknown` | Identifies a not-yet-resolved type, e.g., of an undecorated string literal.  
  
  

Functions coded in C (whether built-in or dynamically loaded) can be declared
to accept or return any of these pseudo-types. It is up to the function author
to ensure that the function will behave safely when a pseudo-type is used as
an argument type.

Functions coded in procedural languages can use pseudo-types only as allowed
by their implementation languages. At present most procedural languages forbid
use of a pseudo-type as an argument type, and allow only `void` and `record`
as a result type (plus `trigger` or `event_trigger` when the function is used
as a trigger or event trigger). Some also support polymorphic functions using
the polymorphic pseudo-types, which are shown above and discussed in detail in
[Section 38.2.5](extend-type-system.html#EXTEND-TYPES-POLYMORPHIC
"38.2.5. Polymorphic Types").

The `internal` pseudo-type is used to declare functions that are meant only to
be called internally by the database system, and not by direct invocation in
an SQL query. If a function has at least one `internal`-type argument then it
cannot be called from SQL. To preserve the type safety of this restriction it
is important to follow this coding rule: do not create any function that is
declared to return `internal` unless it has at least one `internal` argument.

* * *

[Prev](datatype-pg-lsn.html "8.20. pg_lsn Type")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](functions.html "Chapter 9. Functions and Operators")  
---|---|---  
8.20. `pg_lsn` Type  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 9. Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-pseudo.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

