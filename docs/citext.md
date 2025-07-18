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

Supported Versions: [Current](/docs/current/citext.html "PostgreSQL 17 -
F.10. citext — a case-insensitive character string type")
([17](/docs/17/citext.html "PostgreSQL 17 - F.10. citext — a case-insensitive
character string type")) / [16](/docs/16/citext.html "PostgreSQL 16 -
F.10. citext — a case-insensitive character string type") /
[15](/docs/15/citext.html "PostgreSQL 15 - F.10. citext — a case-insensitive
character string type") / [14](/docs/14/citext.html "PostgreSQL 14 -
F.10. citext — a case-insensitive character string type") /
[13](/docs/13/citext.html "PostgreSQL 13 - F.10. citext — a case-insensitive
character string type")

Development Versions: [18](/docs/18/citext.html "PostgreSQL 18 - F.10. citext
— a case-insensitive character string type") / [devel](/docs/devel/citext.html
"PostgreSQL devel - F.10. citext — a case-insensitive character string type")

Unsupported versions: [12](/docs/12/citext.html "PostgreSQL 12 - F.10. citext
— a case-insensitive character string type") / [11](/docs/11/citext.html
"PostgreSQL 11 - F.10. citext — a case-insensitive character string type") /
[10](/docs/10/citext.html "PostgreSQL 10 - F.10. citext — a case-insensitive
character string type") / [9.6](/docs/9.6/citext.html "PostgreSQL 9.6 -
F.10. citext — a case-insensitive character string type") /
[9.5](/docs/9.5/citext.html "PostgreSQL 9.5 - F.10. citext — a case-
insensitive character string type") / [9.4](/docs/9.4/citext.html "PostgreSQL
9.4 - F.10. citext — a case-insensitive character string type") /
[9.3](/docs/9.3/citext.html "PostgreSQL 9.3 - F.10. citext — a case-
insensitive character string type") / [9.2](/docs/9.2/citext.html "PostgreSQL
9.2 - F.10. citext — a case-insensitive character string type") /
[9.1](/docs/9.1/citext.html "PostgreSQL 9.1 - F.10. citext — a case-
insensitive character string type") / [9.0](/docs/9.0/citext.html "PostgreSQL
9.0 - F.10. citext — a case-insensitive character string type") /
[8.4](/docs/8.4/citext.html "PostgreSQL 8.4 - F.10. citext — a case-
insensitive character string type")

__

F.10. citext — a case-insensitive character string type  
---  
[Prev](btree-gist.html "F.9. btree_gist — GiST operator classes with B-tree behavior")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](cube.html "F.11. cube — a multi-dimensional cube data type")  
  
* * *

## F.10. citext — a case-insensitive character string type #

[F.10.1. Rationale](citext.html#CITEXT-RATIONALE)

[F.10.2. How to Use It](citext.html#CITEXT-HOW-TO-USE-IT)

[F.10.3. String Comparison Behavior](citext.html#CITEXT-STRING-COMPARISON-
BEHAVIOR)

[F.10.4. Limitations](citext.html#CITEXT-LIMITATIONS)

[F.10.5. Author](citext.html#CITEXT-AUTHOR)

The `citext` module provides a case-insensitive character string type,
`citext`. Essentially, it internally calls `lower` when comparing values.
Otherwise, it behaves almost exactly like `text`.

### Tip

Consider using _nondeterministic collations_ (see [Section
24.2.2.4](collation.html#COLLATION-NONDETERMINISTIC
"24.2.2.4. Nondeterministic Collations")) instead of this module. They can be
used for case-insensitive comparisons, accent-insensitive comparisons, and
other combinations, and they handle more Unicode special cases correctly.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.10.1. Rationale #

The standard approach to doing case-insensitive matches in PostgreSQL has been
to use the `lower` function when comparing values, for example

    
    
    SELECT * FROM tab WHERE lower(col) = LOWER(?);
    

This works reasonably well, but has a number of drawbacks:

  * It makes your SQL statements verbose, and you always have to remember to use `lower` on both the column and the query value.

  * It won't use an index, unless you create a functional index using `lower`.

  * If you declare a column as `UNIQUE` or `PRIMARY KEY`, the implicitly generated index is case-sensitive. So it's useless for case-insensitive searches, and it won't enforce uniqueness case-insensitively.

The `citext` data type allows you to eliminate calls to `lower` in SQL
queries, and allows a primary key to be case-insensitive. `citext` is locale-
aware, just like `text`, which means that the matching of upper case and lower
case characters is dependent on the rules of the database's `LC_CTYPE`
setting. Again, this behavior is identical to the use of `lower` in queries.
But because it's done transparently by the data type, you don't have to
remember to do anything special in your queries.

### F.10.2. How to Use It #

Here's a simple example of usage:

    
    
    CREATE TABLE users (
        nick CITEXT PRIMARY KEY,
        pass TEXT   NOT NULL
    );
    
    INSERT INTO users VALUES ( 'larry',  sha256(random()::text::bytea) );
    INSERT INTO users VALUES ( 'Tom',    sha256(random()::text::bytea) );
    INSERT INTO users VALUES ( 'Damian', sha256(random()::text::bytea) );
    INSERT INTO users VALUES ( 'NEAL',   sha256(random()::text::bytea) );
    INSERT INTO users VALUES ( 'Bjørn',  sha256(random()::text::bytea) );
    
    SELECT * FROM users WHERE nick = 'Larry';
    

The `SELECT` statement will return one tuple, even though the `nick` column
was set to `larry` and the query was for `Larry`.

### F.10.3. String Comparison Behavior #

`citext` performs comparisons by converting each string to lower case (as
though `lower` were called) and then comparing the results normally. Thus, for
example, two strings are considered equal if `lower` would produce identical
results for them.

In order to emulate a case-insensitive collation as closely as possible, there
are `citext`-specific versions of a number of string-processing operators and
functions. So, for example, the regular expression operators `~` and `~*`
exhibit the same behavior when applied to `citext`: they both match case-
insensitively. The same is true for `!~` and `!~*`, as well as for the `LIKE`
operators `~~` and `~~*`, and `!~~` and `!~~*`. If you'd like to match case-
sensitively, you can cast the operator's arguments to `text`.

Similarly, all of the following functions perform matching case-insensitively
if their arguments are `citext`:

  * `regexp_match()`

  * `regexp_matches()`

  * `regexp_replace()`

  * `regexp_split_to_array()`

  * `regexp_split_to_table()`

  * `replace()`

  * `split_part()`

  * `strpos()`

  * `translate()`

For the regexp functions, if you want to match case-sensitively, you can
specify the “c” flag to force a case-sensitive match. Otherwise, you must cast
to `text` before using one of these functions if you want case-sensitive
behavior.

### F.10.4. Limitations #

  * `citext`'s case-folding behavior depends on the `LC_CTYPE` setting of your database. How it compares values is therefore determined when the database is created. It is not truly case-insensitive in the terms defined by the Unicode standard. Effectively, what this means is that, as long as you're happy with your collation, you should be happy with `citext`'s comparisons. But if you have data in different languages stored in your database, users of one language may find their query results are not as expected if the collation is for another language.

  * As of PostgreSQL 9.1, you can attach a `COLLATE` specification to `citext` columns or data values. Currently, `citext` operators will honor a non-default `COLLATE` specification while comparing case-folded strings, but the initial folding to lower case is always done according to the database's `LC_CTYPE` setting (that is, as though `COLLATE "default"` were given). This may be changed in a future release so that both steps follow the input `COLLATE` specification.

  * `citext` is not as efficient as `text` because the operator functions and the B-tree comparison functions must make copies of the data and convert it to lower case for comparisons. Also, only `text` can support B-Tree deduplication. However, `citext` is slightly more efficient than using `lower` to get case-insensitive matching.

  * `citext` doesn't help much if you need data to compare case-sensitively in some contexts and case-insensitively in other contexts. The standard answer is to use the `text` type and manually use the `lower` function when you need to compare case-insensitively; this works all right if case-insensitive comparison is needed only infrequently. If you need case-insensitive behavior most of the time and case-sensitive infrequently, consider storing the data as `citext` and explicitly casting the column to `text` when you want case-sensitive comparison. In either situation, you will need two indexes if you want both types of searches to be fast.

  * The schema containing the `citext` operators must be in the current `search_path` (typically `public`); if it is not, the normal case-sensitive `text` operators will be invoked instead.

  * The approach of lower-casing strings for comparison does not handle some Unicode special cases correctly, for example when one upper-case letter has two lower-case letter equivalents. Unicode distinguishes between _case mapping_ and _case folding_ for this reason. Use nondeterministic collations instead of `citext` to handle that correctly.

### F.10.5. Author #

David E. Wheeler `<[david@kineticode.com](mailto:david@kineticode.com)>`

Inspired by the original `citext` module by Donald Fraser.

* * *

[Prev](btree-gist.html "F.9. btree_gist — GiST operator classes with B-tree behavior")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](cube.html "F.11. cube — a multi-dimensional cube data type")  
---|---|---  
F.9. btree_gist — GiST operator classes with B-tree behavior  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.11. cube — a multi-dimensional cube data type  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/citext.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

