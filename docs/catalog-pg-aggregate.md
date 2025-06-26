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

Supported Versions: [Current](/docs/current/catalog-pg-aggregate.html
"PostgreSQL 17 - 53.2. pg_aggregate") ([17](/docs/17/catalog-pg-aggregate.html
"PostgreSQL 17 - 53.2. pg_aggregate")) / [16](/docs/16/catalog-pg-
aggregate.html "PostgreSQL 16 - 53.2. pg_aggregate") / [15](/docs/15/catalog-
pg-aggregate.html "PostgreSQL 15 - 53.2. pg_aggregate") /
[14](/docs/14/catalog-pg-aggregate.html "PostgreSQL 14 - 53.2. pg_aggregate")
/ [13](/docs/13/catalog-pg-aggregate.html "PostgreSQL 13 -
53.2. pg_aggregate")

Development Versions: [18](/docs/18/catalog-pg-aggregate.html "PostgreSQL 18 -
53.2. pg_aggregate") / [devel](/docs/devel/catalog-pg-aggregate.html
"PostgreSQL devel - 53.2. pg_aggregate")

Unsupported versions: [12](/docs/12/catalog-pg-aggregate.html "PostgreSQL 12 -
53.2. pg_aggregate") / [11](/docs/11/catalog-pg-aggregate.html "PostgreSQL 11
- 53.2. pg_aggregate") / [10](/docs/10/catalog-pg-aggregate.html "PostgreSQL
10 - 53.2. pg_aggregate") / [9.6](/docs/9.6/catalog-pg-aggregate.html
"PostgreSQL 9.6 - 53.2. pg_aggregate") / [9.5](/docs/9.5/catalog-pg-
aggregate.html "PostgreSQL 9.5 - 53.2. pg_aggregate") /
[9.4](/docs/9.4/catalog-pg-aggregate.html "PostgreSQL 9.4 -
53.2. pg_aggregate") / [9.3](/docs/9.3/catalog-pg-aggregate.html "PostgreSQL
9.3 - 53.2. pg_aggregate") / [9.2](/docs/9.2/catalog-pg-aggregate.html
"PostgreSQL 9.2 - 53.2. pg_aggregate") / [9.1](/docs/9.1/catalog-pg-
aggregate.html "PostgreSQL 9.1 - 53.2. pg_aggregate") /
[9.0](/docs/9.0/catalog-pg-aggregate.html "PostgreSQL 9.0 -
53.2. pg_aggregate") / [8.4](/docs/8.4/catalog-pg-aggregate.html "PostgreSQL
8.4 - 53.2. pg_aggregate") / [8.3](/docs/8.3/catalog-pg-aggregate.html
"PostgreSQL 8.3 - 53.2. pg_aggregate") / [8.2](/docs/8.2/catalog-pg-
aggregate.html "PostgreSQL 8.2 - 53.2. pg_aggregate") /
[8.1](/docs/8.1/catalog-pg-aggregate.html "PostgreSQL 8.1 -
53.2. pg_aggregate") / [8.0](/docs/8.0/catalog-pg-aggregate.html "PostgreSQL
8.0 - 53.2. pg_aggregate") / [7.4](/docs/7.4/catalog-pg-aggregate.html
"PostgreSQL 7.4 - 53.2. pg_aggregate") / [7.3](/docs/7.3/catalog-pg-
aggregate.html "PostgreSQL 7.3 - 53.2. pg_aggregate") /
[7.2](/docs/7.2/catalog-pg-aggregate.html "PostgreSQL 7.2 -
53.2. pg_aggregate") / [7.1](/docs/7.1/catalog-pg-aggregate.html "PostgreSQL
7.1 - 53.2. pg_aggregate")

__

53.2. `pg_aggregate`  
---  
[Prev](catalogs-overview.html "53.1. Overview")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-am.html "53.3. pg_am")  
  
* * *

## 53.2. `pg_aggregate` #

The catalog `pg_aggregate` stores information about aggregate functions. An
aggregate function is a function that operates on a set of values (typically
one column from each row that matches a query condition) and returns a single
value computed from all these values. Typical aggregate functions are `sum`,
`count`, and `max`. Each entry in `pg_aggregate` is an extension of an entry
in [`pg_proc`](catalog-pg-proc.html "53.39. pg_proc"). The `pg_proc` entry
carries the aggregate's name, input and output data types, and other
information that is similar to ordinary functions.

**Table  53.2. `pg_aggregate` Columns**

Column Type Description  
---  
`aggfnoid` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) `pg_proc` OID of the aggregate function  
`aggkind` `char` Aggregate kind: `n` for “normal” aggregates, `o` for
“ordered-set” aggregates, or `h` for “hypothetical-set” aggregates  
`aggnumdirectargs` `int2` Number of direct (non-aggregated) arguments of an
ordered-set or hypothetical-set aggregate, counting a variadic array as one
argument. If equal to `pronargs`, the aggregate must be variadic and the
variadic array describes the aggregated arguments as well as the final direct
arguments. Always zero for normal aggregates.  
`aggtransfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Transition function  
`aggfinalfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Final function (zero if none)  
`aggcombinefn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Combine function (zero if none)  
`aggserialfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Serialization function (zero if none)  
`aggdeserialfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Deserialization function (zero if none)  
`aggmtransfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Forward transition function for moving-aggregate mode
(zero if none)  
`aggminvtransfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Inverse transition function for moving-aggregate mode
(zero if none)  
`aggmfinalfn` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Final function for moving-aggregate mode (zero if
none)  
`aggfinalextra` `bool` True to pass extra dummy arguments to `aggfinalfn`  
`aggmfinalextra` `bool` True to pass extra dummy arguments to `aggmfinalfn`  
`aggfinalmodify` `char` Whether `aggfinalfn` modifies the transition state
value: `r` if it is read-only, `s` if the `aggtransfn` cannot be applied after
the `aggfinalfn`, or `w` if it writes on the value  
`aggmfinalmodify` `char` Like `aggfinalmodify`, but for the `aggmfinalfn`  
`aggsortop` `oid` (references [`pg_operator`](catalog-pg-operator.html
"53.34. pg_operator").`oid`) Associated sort operator (zero if none)  
`aggtranstype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type of the aggregate function's internal
transition (state) data  
`aggtransspace` `int4` Approximate average size (in bytes) of the transition
state data, or zero to use a default estimate  
`aggmtranstype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type of the aggregate function's internal
transition (state) data for moving-aggregate mode (zero if none)  
`aggmtransspace` `int4` Approximate average size (in bytes) of the transition
state data for moving-aggregate mode, or zero to use a default estimate  
`agginitval` `text` The initial value of the transition state. This is a text
field containing the initial value in its external string representation. If
this field is null, the transition state value starts out null.  
`aggminitval` `text` The initial value of the transition state for moving-
aggregate mode. This is a text field containing the initial value in its
external string representation. If this field is null, the transition state
value starts out null.  
  
  

New aggregate functions are registered with the [`CREATE AGGREGATE`](sql-
createaggregate.html "CREATE AGGREGATE") command. See [Section
38.12](xaggr.html "38.12. User-Defined Aggregates") for more information about
writing aggregate functions and the meaning of the transition functions, etc.

* * *

[Prev](catalogs-overview.html "53.1. Overview")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-am.html "53.3. pg_am")  
---|---|---  
53.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.3. `pg_am`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-aggregate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

