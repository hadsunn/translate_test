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

Supported Versions: [Current](/docs/current/functions-sequence.html
"PostgreSQL 17 - 9.17. Sequence Manipulation Functions")
([17](/docs/17/functions-sequence.html "PostgreSQL 17 - 9.17. Sequence
Manipulation Functions")) / [16](/docs/16/functions-sequence.html "PostgreSQL
16 - 9.17. Sequence Manipulation Functions") / [15](/docs/15/functions-
sequence.html "PostgreSQL 15 - 9.17. Sequence Manipulation Functions") /
[14](/docs/14/functions-sequence.html "PostgreSQL 14 - 9.17. Sequence
Manipulation Functions") / [13](/docs/13/functions-sequence.html "PostgreSQL
13 - 9.17. Sequence Manipulation Functions")

Development Versions: [18](/docs/18/functions-sequence.html "PostgreSQL 18 -
9.17. Sequence Manipulation Functions") / [devel](/docs/devel/functions-
sequence.html "PostgreSQL devel - 9.17. Sequence Manipulation Functions")

Unsupported versions: [12](/docs/12/functions-sequence.html "PostgreSQL 12 -
9.17. Sequence Manipulation Functions") / [11](/docs/11/functions-
sequence.html "PostgreSQL 11 - 9.17. Sequence Manipulation Functions") /
[10](/docs/10/functions-sequence.html "PostgreSQL 10 - 9.17. Sequence
Manipulation Functions") / [9.6](/docs/9.6/functions-sequence.html "PostgreSQL
9.6 - 9.17. Sequence Manipulation Functions") / [9.5](/docs/9.5/functions-
sequence.html "PostgreSQL 9.5 - 9.17. Sequence Manipulation Functions") /
[9.4](/docs/9.4/functions-sequence.html "PostgreSQL 9.4 - 9.17. Sequence
Manipulation Functions") / [9.3](/docs/9.3/functions-sequence.html "PostgreSQL
9.3 - 9.17. Sequence Manipulation Functions") / [9.2](/docs/9.2/functions-
sequence.html "PostgreSQL 9.2 - 9.17. Sequence Manipulation Functions") /
[9.1](/docs/9.1/functions-sequence.html "PostgreSQL 9.1 - 9.17. Sequence
Manipulation Functions") / [9.0](/docs/9.0/functions-sequence.html "PostgreSQL
9.0 - 9.17. Sequence Manipulation Functions") / [8.4](/docs/8.4/functions-
sequence.html "PostgreSQL 8.4 - 9.17. Sequence Manipulation Functions") /
[8.3](/docs/8.3/functions-sequence.html "PostgreSQL 8.3 - 9.17. Sequence
Manipulation Functions") / [8.2](/docs/8.2/functions-sequence.html "PostgreSQL
8.2 - 9.17. Sequence Manipulation Functions") / [8.1](/docs/8.1/functions-
sequence.html "PostgreSQL 8.1 - 9.17. Sequence Manipulation Functions") /
[8.0](/docs/8.0/functions-sequence.html "PostgreSQL 8.0 - 9.17. Sequence
Manipulation Functions") / [7.4](/docs/7.4/functions-sequence.html "PostgreSQL
7.4 - 9.17. Sequence Manipulation Functions") / [7.3](/docs/7.3/functions-
sequence.html "PostgreSQL 7.3 - 9.17. Sequence Manipulation Functions") /
[7.2](/docs/7.2/functions-sequence.html "PostgreSQL 7.2 - 9.17. Sequence
Manipulation Functions")

__

9.17. Sequence Manipulation Functions  
---  
[Prev](functions-json.html "9.16. JSON Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-conditional.html "9.18. Conditional Expressions")  
  
* * *

## 9.17. Sequence Manipulation Functions #

This section describes functions for operating on _sequence objects_ , also
called sequence generators or just sequences. Sequence objects are special
single-row tables created with [CREATE SEQUENCE](sql-createsequence.html
"CREATE SEQUENCE"). Sequence objects are commonly used to generate unique
identifiers for rows of a table. The sequence functions, listed in [Table
9.52](functions-sequence.html#FUNCTIONS-SEQUENCE-TABLE "Table 9.52. Sequence
Functions"), provide simple, multiuser-safe methods for obtaining successive
sequence values from sequence objects.

**Table  9.52. Sequence Functions**

Function Description  
---  
`nextval` ( `regclass` ) → `bigint` Advances the sequence object to its next
value and returns that value. This is done atomically: even if multiple
sessions execute `nextval` concurrently, each will safely receive a distinct
sequence value. If the sequence object has been created with default
parameters, successive `nextval` calls will return successive values beginning
with 1. Other behaviors can be obtained by using appropriate parameters in the
[CREATE SEQUENCE](sql-createsequence.html "CREATE SEQUENCE") command. This
function requires `USAGE` or `UPDATE` privilege on the sequence.  
`setval` ( `regclass`, `bigint` [, `boolean` ] ) → `bigint` Sets the sequence
object's current value, and optionally its `is_called` flag. The two-parameter
form sets the sequence's `last_value` field to the specified value and sets
its `is_called` field to `true`, meaning that the next `nextval` will advance
the sequence before returning a value. The value that will be reported by
`currval` is also set to the specified value. In the three-parameter form,
`is_called` can be set to either `true` or `false`. `true` has the same effect
as the two-parameter form. If it is set to `false`, the next `nextval` will
return exactly the specified value, and sequence advancement commences with
the following `nextval`. Furthermore, the value reported by `currval` is not
changed in this case. For example,

    
    
    SELECT setval('myseq', 42);           _Nextnextval will return 43_
    SELECT setval('myseq', 42, true);     _Same as above_
    SELECT setval('myseq', 42, false);    _Nextnextval will return 42_
    

The result returned by `setval` is just the value of its second argument. This
function requires `UPDATE` privilege on the sequence.  
`currval` ( `regclass` ) → `bigint` Returns the value most recently obtained
by `nextval` for this sequence in the current session. (An error is reported
if `nextval` has never been called for this sequence in this session.) Because
this is returning a session-local value, it gives a predictable answer whether
or not other sessions have executed `nextval` since the current session did.
This function requires `USAGE` or `SELECT` privilege on the sequence.  
`lastval` () → `bigint` Returns the value most recently returned by `nextval`
in the current session. This function is identical to `currval`, except that
instead of taking the sequence name as an argument it refers to whichever
sequence `nextval` was most recently applied to in the current session. It is
an error to call `lastval` if `nextval` has not yet been called in the current
session. This function requires `USAGE` or `SELECT` privilege on the last used
sequence.  
  
  

### Caution

To avoid blocking concurrent transactions that obtain numbers from the same
sequence, the value obtained by `nextval` is not reclaimed for re-use if the
calling transaction later aborts. This means that transaction aborts or
database crashes can result in gaps in the sequence of assigned values. That
can happen without a transaction abort, too. For example an `INSERT` with an
`ON CONFLICT` clause will compute the to-be-inserted tuple, including doing
any required `nextval` calls, before detecting any conflict that would cause
it to follow the `ON CONFLICT` rule instead. Thus, PostgreSQL sequence objects
_cannot be used to obtain “gapless” sequences_.

Likewise, sequence state changes made by `setval` are immediately visible to
other transactions, and are not undone if the calling transaction rolls back.

If the database cluster crashes before committing a transaction containing a
`nextval` or `setval` call, the sequence state change might not have made its
way to persistent storage, so that it is uncertain whether the sequence will
have its original or updated state after the cluster restarts. This is
harmless for usage of the sequence within the database, since other effects of
uncommitted transactions will not be visible either. However, if you wish to
use a sequence value for persistent outside-the-database purposes, make sure
that the `nextval` call has been committed before doing so.

The sequence to be operated on by a sequence function is specified by a
`regclass` argument, which is simply the OID of the sequence in the `pg_class`
system catalog. You do not have to look up the OID by hand, however, since the
`regclass` data type's input converter will do the work for you. See [Section
8.19](datatype-oid.html "8.19. Object Identifier Types") for details.

* * *

[Prev](functions-json.html "9.16. JSON Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-conditional.html "9.18. Conditional Expressions")  
---|---|---  
9.16. JSON Functions and Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.18. Conditional Expressions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-sequence.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

