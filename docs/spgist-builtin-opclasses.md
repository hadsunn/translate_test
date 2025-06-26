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

Supported Versions: [16](/docs/16/spgist-builtin-opclasses.html "PostgreSQL 16
- 69.2. Built-in Operator Classes") / [15](/docs/15/spgist-builtin-
opclasses.html "PostgreSQL 15 - 69.2. Built-in Operator Classes") /
[14](/docs/14/spgist-builtin-opclasses.html "PostgreSQL 14 - 69.2. Built-in
Operator Classes") / [13](/docs/13/spgist-builtin-opclasses.html "PostgreSQL
13 - 69.2. Built-in Operator Classes")

Unsupported versions: [12](/docs/12/spgist-builtin-opclasses.html "PostgreSQL
12 - 69.2. Built-in Operator Classes") / [11](/docs/11/spgist-builtin-
opclasses.html "PostgreSQL 11 - 69.2. Built-in Operator Classes") /
[10](/docs/10/spgist-builtin-opclasses.html "PostgreSQL 10 - 69.2. Built-in
Operator Classes") / [9.6](/docs/9.6/spgist-builtin-opclasses.html "PostgreSQL
9.6 - 69.2. Built-in Operator Classes") / [9.5](/docs/9.5/spgist-builtin-
opclasses.html "PostgreSQL 9.5 - 69.2. Built-in Operator Classes") /
[9.4](/docs/9.4/spgist-builtin-opclasses.html "PostgreSQL 9.4 - 69.2. Built-in
Operator Classes")

__

69.2. Built-in Operator Classes  
---  
[Prev](spgist-intro.html "69.1. Introduction")  | [Up](spgist.html "Chapter 69. SP-GiST Indexes") | Chapter 69. SP-GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spgist-extensibility.html "69.3. Extensibility")  
  
* * *

## 69.2. Built-in Operator Classes #

The core PostgreSQL distribution includes the SP-GiST operator classes shown
in [Table 69.1](spgist-builtin-opclasses.html#SPGIST-BUILTIN-OPCLASSES-TABLE
"Table 69.1. Built-in SP-GiST Operator Classes").

**Table  69.1. Built-in SP-GiST Operator Classes**

Name | Indexable Operators | Ordering Operators  
---|---|---  
`box_ops` | `<< (box,box)` | `<-> (box,point)`  
`&< (box,box)`  
`&> (box,box)`  
`>> (box,box)`  
`<@ (box,box)`  
`@> (box,box)`  
`~= (box,box)`  
`&& (box,box)`  
`<<| (box,box)`  
`&<| (box,box)`  
`|&> (box,box)`  
`|>> (box,box)`  
`inet_ops` | `<< (inet,inet)` |    
`<<= (inet,inet)`  
`>> (inet,inet)`  
`>>= (inet,inet)`  
`= (inet,inet)`  
`<> (inet,inet)`  
`< (inet,inet)`  
`<= (inet,inet)`  
`> (inet,inet)`  
`>= (inet,inet)`  
`&& (inet,inet)`  
`kd_point_ops` | `|>> (point,point)` | `<-> (point,point)`  
`<< (point,point)`  
`>> (point,point)`  
`<<| (point,point)`  
`~= (point,point)`  
`<@ (point,box)`  
`poly_ops` | `<< (polygon,polygon)` | `<-> (polygon,point)`  
`&< (polygon,polygon)`  
`&> (polygon,polygon)`  
`>> (polygon,polygon)`  
`<@ (polygon,polygon)`  
`@> (polygon,polygon)`  
`~= (polygon,polygon)`  
`&& (polygon,polygon)`  
`<<| (polygon,polygon)`  
`&<| (polygon,polygon)`  
`|>> (polygon,polygon)`  
`|&> (polygon,polygon)`  
`quad_point_ops` | `|>> (point,point)` | `<-> (point,point)`  
`<< (point,point)`  
`>> (point,point)`  
`<<| (point,point)`  
`~= (point,point)`  
`<@ (point,box)`  
`range_ops` | `= (anyrange,anyrange)` |    
`&& (anyrange,anyrange)`  
`@> (anyrange,anyelement)`  
`@> (anyrange,anyrange)`  
`<@ (anyrange,anyrange)`  
`<< (anyrange,anyrange)`  
`>> (anyrange,anyrange)`  
`&< (anyrange,anyrange)`  
`&> (anyrange,anyrange)`  
`-|- (anyrange,anyrange)`  
`text_ops` | `= (text,text)` |    
`< (text,text)`  
`<= (text,text)`  
`> (text,text)`  
`>= (text,text)`  
`~<~ (text,text)`  
`~<=~ (text,text)`  
`~>=~ (text,text)`  
`~>~ (text,text)`  
`^@ (text,text)`  
  
  

Of the two operator classes for type `point`, `quad_point_ops` is the default.
`kd_point_ops` supports the same operators but uses a different index data
structure that may offer better performance in some applications.

The `quad_point_ops`, `kd_point_ops` and `poly_ops` operator classes support
the `<->` ordering operator, which enables the k-nearest neighbor (`k-NN`)
search over indexed point or polygon data sets.

* * *

[Prev](spgist-intro.html "69.1. Introduction")  | [Up](spgist.html "Chapter 69. SP-GiST Indexes") |  [Next](spgist-extensibility.html "69.3. Extensibility")  
---|---|---  
69.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  69.3. Extensibility  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spgist-builtin-
opclasses.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

