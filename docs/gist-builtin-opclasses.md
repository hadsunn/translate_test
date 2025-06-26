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

Supported Versions: [16](/docs/16/gist-builtin-opclasses.html "PostgreSQL 16 -
68.2. Built-in Operator Classes") / [15](/docs/15/gist-builtin-opclasses.html
"PostgreSQL 15 - 68.2. Built-in Operator Classes") / [14](/docs/14/gist-
builtin-opclasses.html "PostgreSQL 14 - 68.2. Built-in Operator Classes") /
[13](/docs/13/gist-builtin-opclasses.html "PostgreSQL 13 - 68.2. Built-in
Operator Classes")

Unsupported versions: [12](/docs/12/gist-builtin-opclasses.html "PostgreSQL 12
- 68.2. Built-in Operator Classes") / [11](/docs/11/gist-builtin-
opclasses.html "PostgreSQL 11 - 68.2. Built-in Operator Classes") /
[10](/docs/10/gist-builtin-opclasses.html "PostgreSQL 10 - 68.2. Built-in
Operator Classes") / [9.6](/docs/9.6/gist-builtin-opclasses.html "PostgreSQL
9.6 - 68.2. Built-in Operator Classes") / [9.5](/docs/9.5/gist-builtin-
opclasses.html "PostgreSQL 9.5 - 68.2. Built-in Operator Classes") /
[9.4](/docs/9.4/gist-builtin-opclasses.html "PostgreSQL 9.4 - 68.2. Built-in
Operator Classes")

__

68.2. Built-in Operator Classes  
---  
[Prev](gist-intro.html "68.1. Introduction")  | [Up](gist.html "Chapter 68. GiST Indexes") | Chapter 68. GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gist-extensibility.html "68.3. Extensibility")  
  
* * *

## 68.2. Built-in Operator Classes #

The core PostgreSQL distribution includes the GiST operator classes shown in
[Table 68.1](gist-builtin-opclasses.html#GIST-BUILTIN-OPCLASSES-TABLE
"Table 68.1. Built-in GiST Operator Classes"). (Some of the optional modules
described in [Appendix F](contrib.html "Appendix F. Additional Supplied
Modules and Extensions") provide additional GiST operator classes.)

**Table  68.1. Built-in GiST Operator Classes**

Name | Indexable Operators | Ordering Operators  
---|---|---  
`box_ops` | `<< (box, box)` | `<-> (box, point)`  
`&< (box, box)`  
`&& (box, box)`  
`&> (box, box)`  
`>> (box, box)`  
`~= (box, box)`  
`@> (box, box)`  
`<@ (box, box)`  
`&<| (box, box)`  
`<<| (box, box)`  
`|>> (box, box)`  
`|&> (box, box)`  
`circle_ops` | `<< (circle, circle)` | `<-> (circle, point)`  
`&< (circle, circle)`  
`&> (circle, circle)`  
`>> (circle, circle)`  
`<@ (circle, circle)`  
`@> (circle, circle)`  
`~= (circle, circle)`  
`&& (circle, circle)`  
`|>> (circle, circle)`  
`<<| (circle, circle)`  
`&<| (circle, circle)`  
`|&> (circle, circle)`  
`inet_ops` | `<< (inet, inet)` |    
`<<= (inet, inet)`  
`>> (inet, inet)`  
`>>= (inet, inet)`  
`= (inet, inet)`  
`<> (inet, inet)`  
`< (inet, inet)`  
`<= (inet, inet)`  
`> (inet, inet)`  
`>= (inet, inet)`  
`&& (inet, inet)`  
`multirange_ops` | `= (anymultirange, anymultirange)` |    
`&& (anymultirange, anymultirange)`  
`&& (anymultirange, anyrange)`  
`@> (anymultirange, anyelement)`  
`@> (anymultirange, anymultirange)`  
`@> (anymultirange, anyrange)`  
`<@ (anymultirange, anymultirange)`  
`<@ (anymultirange, anyrange)`  
`<< (anymultirange, anymultirange)`  
`<< (anymultirange, anyrange)`  
`>> (anymultirange, anymultirange)`  
`>> (anymultirange, anyrange)`  
`&< (anymultirange, anymultirange)`  
`&< (anymultirange, anyrange)`  
`&> (anymultirange, anymultirange)`  
`&> (anymultirange, anyrange)`  
`-|- (anymultirange, anymultirange)`  
`-|- (anymultirange, anyrange)`  
`point_ops` | `|>> (point, point)` | `<-> (point, point)`  
`<< (point, point)`  
`>> (point, point)`  
`<<| (point, point)`  
`~= (point, point)`  
`<@ (point, box)`  
`<@ (point, polygon)`  
`<@ (point, circle)`  
`poly_ops` | `<< (polygon, polygon)` | `<-> (polygon, point)`  
`&< (polygon, polygon)`  
`&> (polygon, polygon)`  
`>> (polygon, polygon)`  
`<@ (polygon, polygon)`  
`@> (polygon, polygon)`  
`~= (polygon, polygon)`  
`&& (polygon, polygon)`  
`<<| (polygon, polygon)`  
`&<| (polygon, polygon)`  
`|&> (polygon, polygon)`  
`|>> (polygon, polygon)`  
`range_ops` | `= (anyrange, anyrange)` |    
`&& (anyrange, anyrange)`  
`&& (anyrange, anymultirange)`  
`@> (anyrange, anyelement)`  
`@> (anyrange, anyrange)`  
`@> (anyrange, anymultirange)`  
`<@ (anyrange, anyrange)`  
`<@ (anyrange, anymultirange)`  
`<< (anyrange, anyrange)`  
`<< (anyrange, anymultirange)`  
`>> (anyrange, anyrange)`  
`>> (anyrange, anymultirange)`  
`&< (anyrange, anyrange)`  
`&< (anyrange, anymultirange)`  
`&> (anyrange, anyrange)`  
`&> (anyrange, anymultirange)`  
`-|- (anyrange, anyrange)`  
`-|- (anyrange, anymultirange)`  
`tsquery_ops` | `<@ (tsquery, tsquery)` |    
`@> (tsquery, tsquery)`  
`tsvector_ops` | `@@ (tsvector, tsquery)` |    
  
  

For historical reasons, the `inet_ops` operator class is not the default class
for types `inet` and `cidr`. To use it, mention the class name in `CREATE
INDEX`, for example

    
    
    CREATE INDEX ON my_table USING GIST (my_inet_column inet_ops);
    

* * *

[Prev](gist-intro.html "68.1. Introduction")  | [Up](gist.html "Chapter 68. GiST Indexes") |  [Next](gist-extensibility.html "68.3. Extensibility")  
---|---|---  
68.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  68.3. Extensibility  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gist-builtin-opclasses.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

