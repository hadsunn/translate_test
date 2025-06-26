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

Supported Versions: [16](/docs/16/spgist-implementation.html "PostgreSQL 16 -
69.4. Implementation") / [15](/docs/15/spgist-implementation.html "PostgreSQL
15 - 69.4. Implementation") / [14](/docs/14/spgist-implementation.html
"PostgreSQL 14 - 69.4. Implementation") / [13](/docs/13/spgist-
implementation.html "PostgreSQL 13 - 69.4. Implementation")

Unsupported versions: [12](/docs/12/spgist-implementation.html "PostgreSQL 12
- 69.4. Implementation") / [11](/docs/11/spgist-implementation.html
"PostgreSQL 11 - 69.4. Implementation") / [10](/docs/10/spgist-
implementation.html "PostgreSQL 10 - 69.4. Implementation") /
[9.6](/docs/9.6/spgist-implementation.html "PostgreSQL 9.6 -
69.4. Implementation") / [9.5](/docs/9.5/spgist-implementation.html
"PostgreSQL 9.5 - 69.4. Implementation") / [9.4](/docs/9.4/spgist-
implementation.html "PostgreSQL 9.4 - 69.4. Implementation") /
[9.3](/docs/9.3/spgist-implementation.html "PostgreSQL 9.3 -
69.4. Implementation") / [9.2](/docs/9.2/spgist-implementation.html
"PostgreSQL 9.2 - 69.4. Implementation")

__

69.4. Implementation  
---  
[Prev](spgist-extensibility.html "69.3. Extensibility")  | [Up](spgist.html "Chapter 69. SP-GiST Indexes") | Chapter 69. SP-GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spgist-examples.html "69.5. Examples")  
  
* * *

## 69.4. Implementation #

[69.4.1. SP-GiST Limits](spgist-implementation.html#SPGIST-LIMITS)

[69.4.2. SP-GiST Without Node Labels](spgist-implementation.html#SPGIST-NULL-
LABELS)

[69.4.3. “All-the-Same” Inner Tuples](spgist-implementation.html#SPGIST-ALL-
THE-SAME)

This section covers implementation details and other tricks that are useful
for implementers of SP-GiST operator classes to know.

### 69.4.1. SP-GiST Limits #

Individual leaf tuples and inner tuples must fit on a single index page (8kB
by default). Therefore, when indexing values of variable-length data types,
long values can only be supported by methods such as radix trees, in which
each level of the tree includes a prefix that is short enough to fit on a
page, and the final leaf level includes a suffix also short enough to fit on a
page. The operator class should set `longValuesOK` to true only if it is
prepared to arrange for this to happen. Otherwise, the SP-GiST core will
reject any request to index a value that is too large to fit on an index page.

Likewise, it is the operator class's responsibility that inner tuples do not
grow too large to fit on an index page; this limits the number of child nodes
that can be used in one inner tuple, as well as the maximum size of a prefix
value.

Another limitation is that when an inner tuple's node points to a set of leaf
tuples, those tuples must all be in the same index page. (This is a design
decision to reduce seeking and save space in the links that chain such tuples
together.) If the set of leaf tuples grows too large for a page, a split is
performed and an intermediate inner tuple is inserted. For this to fix the
problem, the new inner tuple _must_ divide the set of leaf values into more
than one node group. If the operator class's `picksplit` function fails to do
that, the SP-GiST core resorts to extraordinary measures described in [Section
69.4.3](spgist-implementation.html#SPGIST-ALL-THE-SAME "69.4.3. “All-the-Same”
Inner Tuples").

When `longValuesOK` is true, it is expected that successive levels of the SP-
GiST tree will absorb more and more information into the prefixes and node
labels of the inner tuples, making the required leaf datum smaller and
smaller, so that eventually it will fit on a page. To prevent bugs in operator
classes from causing infinite insertion loops, the SP-GiST core will raise an
error if the leaf datum does not become any smaller within ten cycles of
`choose` method calls.

### 69.4.2. SP-GiST Without Node Labels #

Some tree algorithms use a fixed set of nodes for each inner tuple; for
example, in a quad-tree there are always exactly four nodes corresponding to
the four quadrants around the inner tuple's centroid point. In such a case the
code typically works with the nodes by number, and there is no need for
explicit node labels. To suppress node labels (and thereby save some space),
the `picksplit` function can return NULL for the `nodeLabels` array, and
likewise the `choose` function can return NULL for the `prefixNodeLabels`
array during a `spgSplitTuple` action. This will in turn result in
`nodeLabels` being NULL during subsequent calls to `choose` and
`inner_consistent`. In principle, node labels could be used for some inner
tuples and omitted for others in the same index.

When working with an inner tuple having unlabeled nodes, it is an error for
`choose` to return `spgAddNode`, since the set of nodes is supposed to be
fixed in such cases.

### 69.4.3. “All-the-Same” Inner Tuples #

The SP-GiST core can override the results of the operator class's `picksplit`
function when `picksplit` fails to divide the supplied leaf values into at
least two node categories. When this happens, the new inner tuple is created
with multiple nodes that each have the same label (if any) that `picksplit`
gave to the one node it did use, and the leaf values are divided at random
among these equivalent nodes. The `allTheSame` flag is set on the inner tuple
to warn the `choose` and `inner_consistent` functions that the tuple does not
have the node set that they might otherwise expect.

When dealing with an `allTheSame` tuple, a `choose` result of `spgMatchNode`
is interpreted to mean that the new value can be assigned to any of the
equivalent nodes; the core code will ignore the supplied `nodeN` value and
descend into one of the nodes at random (so as to keep the tree balanced). It
is an error for `choose` to return `spgAddNode`, since that would make the
nodes not all equivalent; the `spgSplitTuple` action must be used if the value
to be inserted doesn't match the existing nodes.

When dealing with an `allTheSame` tuple, the `inner_consistent` function
should return either all or none of the nodes as targets for continuing the
index search, since they are all equivalent. This may or may not require any
special-case code, depending on how much the `inner_consistent` function
normally assumes about the meaning of the nodes.

* * *

[Prev](spgist-extensibility.html "69.3. Extensibility")  | [Up](spgist.html "Chapter 69. SP-GiST Indexes") |  [Next](spgist-examples.html "69.5. Examples")  
---|---|---  
69.3. Extensibility  | [Home](index.html "PostgreSQL 16.9 Documentation") |  69.5. Examples  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spgist-implementation.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

