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

Supported Versions: [16](/docs/16/btree-behavior.html "PostgreSQL 16 -
67.2. Behavior of B-Tree Operator Classes") / [15](/docs/15/btree-
behavior.html "PostgreSQL 15 - 67.2. Behavior of B-Tree Operator Classes") /
[14](/docs/14/btree-behavior.html "PostgreSQL 14 - 67.2. Behavior of B-Tree
Operator Classes") / [13](/docs/13/btree-behavior.html "PostgreSQL 13 -
67.2. Behavior of B-Tree Operator Classes")

Unsupported versions: [12](/docs/12/btree-behavior.html "PostgreSQL 12 -
67.2. Behavior of B-Tree Operator Classes") / [11](/docs/11/btree-
behavior.html "PostgreSQL 11 - 67.2. Behavior of B-Tree Operator Classes")

__

67.2. Behavior of B-Tree Operator Classes  
---  
[Prev](btree-intro.html "67.1. Introduction")  | [Up](btree.html "Chapter 67. B-Tree Indexes") | Chapter 67. B-Tree Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](btree-support-funcs.html "67.3. B-Tree Support Functions")  
  
* * *

## 67.2. Behavior of B-Tree Operator Classes #

As shown in [Table 38.3](xindex.html#XINDEX-BTREE-STRAT-TABLE
"Table 38.3. B-Tree Strategies"), a btree operator class must provide five
comparison operators, `<`, `<=`, `=`, `>=` and `>`. One might expect that `<>`
should also be part of the operator class, but it is not, because it would
almost never be useful to use a `<>` WHERE clause in an index search. (For
some purposes, the planner treats `<>` as associated with a btree operator
class; but it finds that operator via the `=` operator's negator link, rather
than from `pg_amop`.)

When several data types share near-identical sorting semantics, their operator
classes can be grouped into an operator family. Doing so is advantageous
because it allows the planner to make deductions about cross-type comparisons.
Each operator class within the family should contain the single-type operators
(and associated support functions) for its input data type, while cross-type
comparison operators and support functions are “loose” in the family. It is
recommendable that a complete set of cross-type operators be included in the
family, thus ensuring that the planner can represent any comparison conditions
that it deduces from transitivity.

There are some basic assumptions that a btree operator family must satisfy:

  * An `=` operator must be an equivalence relation; that is, for all non-null values _`A`_ , _`B`_ , _`C`_ of the data type:

    * _`A`_ `=` _`A`_ is true (_reflexive law_)

    * if _`A`_ `=` _`B`_ , then _`B`_ `=` _`A`_ (_symmetric law_)

    * if _`A`_ `=` _`B`_ and _`B`_ `=` _`C`_ , then _`A`_ `=` _`C`_ (_transitive law_)

  * A `<` operator must be a strong ordering relation; that is, for all non-null values _`A`_ , _`B`_ , _`C`_ :

    * _`A`_ `<` _`A`_ is false (_irreflexive law_)

    * if _`A`_ `<` _`B`_ and _`B`_ `<` _`C`_ , then _`A`_ `<` _`C`_ (_transitive law_)

  * Furthermore, the ordering is total; that is, for all non-null values _`A`_ , _`B`_ :

    * exactly one of _`A`_ `<` _`B`_ , _`A`_ `=` _`B`_ , and _`B`_ `<` _`A`_ is true (_trichotomy law_)

(The trichotomy law justifies the definition of the comparison support
function, of course.)

The other three operators are defined in terms of `=` and `<` in the obvious
way, and must act consistently with them.

For an operator family supporting multiple data types, the above laws must
hold when _`A`_ , _`B`_ , _`C`_ are taken from any data types in the family.
The transitive laws are the trickiest to ensure, as in cross-type situations
they represent statements that the behaviors of two or three different
operators are consistent. As an example, it would not work to put `float8` and
`numeric` into the same operator family, at least not with the current
semantics that `numeric` values are converted to `float8` for comparison to a
`float8`. Because of the limited accuracy of `float8`, this means there are
distinct `numeric` values that will compare equal to the same `float8` value,
and thus the transitive law would fail.

Another requirement for a multiple-data-type family is that any implicit or
binary-coercion casts that are defined between data types included in the
operator family must not change the associated sort ordering.

It should be fairly clear why a btree index requires these laws to hold within
a single data type: without them there is no ordering to arrange the keys
with. Also, index searches using a comparison key of a different data type
require comparisons to behave sanely across two data types. The extensions to
three or more data types within a family are not strictly required by the
btree index mechanism itself, but the planner relies on them for optimization
purposes.

* * *

[Prev](btree-intro.html "67.1. Introduction")  | [Up](btree.html "Chapter 67. B-Tree Indexes") |  [Next](btree-support-funcs.html "67.3. B-Tree Support Functions")  
---|---|---  
67.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  67.3. B-Tree Support Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/btree-behavior.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

