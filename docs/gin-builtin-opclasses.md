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

Supported Versions: [16](/docs/16/gin-builtin-opclasses.html "PostgreSQL 16 -
70.2. Built-in Operator Classes") / [15](/docs/15/gin-builtin-opclasses.html
"PostgreSQL 15 - 70.2. Built-in Operator Classes") / [14](/docs/14/gin-
builtin-opclasses.html "PostgreSQL 14 - 70.2. Built-in Operator Classes") /
[13](/docs/13/gin-builtin-opclasses.html "PostgreSQL 13 - 70.2. Built-in
Operator Classes")

Unsupported versions: [12](/docs/12/gin-builtin-opclasses.html "PostgreSQL 12
- 70.2. Built-in Operator Classes") / [11](/docs/11/gin-builtin-opclasses.html
"PostgreSQL 11 - 70.2. Built-in Operator Classes") / [10](/docs/10/gin-
builtin-opclasses.html "PostgreSQL 10 - 70.2. Built-in Operator Classes") /
[9.6](/docs/9.6/gin-builtin-opclasses.html "PostgreSQL 9.6 - 70.2. Built-in
Operator Classes") / [9.5](/docs/9.5/gin-builtin-opclasses.html "PostgreSQL
9.5 - 70.2. Built-in Operator Classes") / [9.4](/docs/9.4/gin-builtin-
opclasses.html "PostgreSQL 9.4 - 70.2. Built-in Operator Classes")

__

70.2. Built-in Operator Classes  
---  
[Prev](gin-intro.html "70.1. Introduction")  | [Up](gin.html "Chapter 70. GIN Indexes") | Chapter 70. GIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gin-extensibility.html "70.3. Extensibility")  
  
* * *

## 70.2. Built-in Operator Classes #

The core PostgreSQL distribution includes the GIN operator classes shown in
[Table 70.1](gin-builtin-opclasses.html#GIN-BUILTIN-OPCLASSES-TABLE
"Table 70.1. Built-in GIN Operator Classes"). (Some of the optional modules
described in [Appendix F](contrib.html "Appendix F. Additional Supplied
Modules and Extensions") provide additional GIN operator classes.)

**Table  70.1. Built-in GIN Operator Classes**

Name | Indexable Operators  
---|---  
`array_ops` | `&& (anyarray,anyarray)`  
`@> (anyarray,anyarray)`  
`<@ (anyarray,anyarray)`  
`= (anyarray,anyarray)`  
`jsonb_ops` | `@> (jsonb,jsonb)`  
`@? (jsonb,jsonpath)`  
`@@ (jsonb,jsonpath)`  
`? (jsonb,text)`  
`?| (jsonb,text[])`  
`?& (jsonb,text[])`  
`jsonb_path_ops` | `@> (jsonb,jsonb)`  
`@? (jsonb,jsonpath)`  
`@@ (jsonb,jsonpath)`  
`tsvector_ops` | `@@ (tsvector,tsquery)`  
`@@@ (tsvector,tsquery)`  
  
  

Of the two operator classes for type `jsonb`, `jsonb_ops` is the default.
`jsonb_path_ops` supports fewer operators but offers better performance for
those operators. See [Section 8.14.4](datatype-json.html#JSON-INDEXING
"8.14.4. jsonb Indexing") for details.

* * *

[Prev](gin-intro.html "70.1. Introduction")  | [Up](gin.html "Chapter 70. GIN Indexes") |  [Next](gin-extensibility.html "70.3. Extensibility")  
---|---|---  
70.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  70.3. Extensibility  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gin-builtin-opclasses.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

