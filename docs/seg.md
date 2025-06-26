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

Supported Versions: [Current](/docs/current/seg.html "PostgreSQL 17 -
F.39. seg — a datatype for line segments or floating point intervals")
([17](/docs/17/seg.html "PostgreSQL 17 - F.39. seg — a datatype for line
segments or floating point intervals")) / [16](/docs/16/seg.html "PostgreSQL
16 - F.39. seg — a datatype for line segments or floating point intervals") /
[15](/docs/15/seg.html "PostgreSQL 15 - F.39. seg — a datatype for line
segments or floating point intervals") / [14](/docs/14/seg.html "PostgreSQL 14
- F.39. seg — a datatype for line segments or floating point intervals") /
[13](/docs/13/seg.html "PostgreSQL 13 - F.39. seg — a datatype for line
segments or floating point intervals")

Development Versions: [18](/docs/18/seg.html "PostgreSQL 18 - F.39. seg — a
datatype for line segments or floating point intervals") /
[devel](/docs/devel/seg.html "PostgreSQL devel - F.39. seg — a datatype for
line segments or floating point intervals")

Unsupported versions: [12](/docs/12/seg.html "PostgreSQL 12 - F.39. seg — a
datatype for line segments or floating point intervals") /
[11](/docs/11/seg.html "PostgreSQL 11 - F.39. seg — a datatype for line
segments or floating point intervals") / [10](/docs/10/seg.html "PostgreSQL 10
- F.39. seg — a datatype for line segments or floating point intervals") /
[9.6](/docs/9.6/seg.html "PostgreSQL 9.6 - F.39. seg — a datatype for line
segments or floating point intervals") / [9.5](/docs/9.5/seg.html "PostgreSQL
9.5 - F.39. seg — a datatype for line segments or floating point intervals") /
[9.4](/docs/9.4/seg.html "PostgreSQL 9.4 - F.39. seg — a datatype for line
segments or floating point intervals") / [9.3](/docs/9.3/seg.html "PostgreSQL
9.3 - F.39. seg — a datatype for line segments or floating point intervals") /
[9.2](/docs/9.2/seg.html "PostgreSQL 9.2 - F.39. seg — a datatype for line
segments or floating point intervals") / [9.1](/docs/9.1/seg.html "PostgreSQL
9.1 - F.39. seg — a datatype for line segments or floating point intervals") /
[9.0](/docs/9.0/seg.html "PostgreSQL 9.0 - F.39. seg — a datatype for line
segments or floating point intervals") / [8.4](/docs/8.4/seg.html "PostgreSQL
8.4 - F.39. seg — a datatype for line segments or floating point intervals") /
[8.3](/docs/8.3/seg.html "PostgreSQL 8.3 - F.39. seg — a datatype for line
segments or floating point intervals")

__

F.39. seg — a datatype for line segments or floating point intervals  
---  
[Prev](postgres-fdw.html "F.38. postgres_fdw —  access data stored in external PostgreSQL  servers")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sepgsql.html "F.40. sepgsql —  SELinux-, label-based mandatory access control \(MAC\) security module")  
  
* * *

## F.39. seg — a datatype for line segments or floating point intervals #

[F.39.1. Rationale](seg.html#SEG-RATIONALE)

[F.39.2. Syntax](seg.html#SEG-SYNTAX)

[F.39.3. Precision](seg.html#SEG-PRECISION)

[F.39.4. Usage](seg.html#SEG-USAGE)

[F.39.5. Notes](seg.html#SEG-NOTES)

[F.39.6. Credits](seg.html#SEG-CREDITS)

This module implements a data type `seg` for representing line segments, or
floating point intervals. `seg` can represent uncertainty in the interval
endpoints, making it especially useful for representing laboratory
measurements.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.39.1. Rationale #

The geometry of measurements is usually more complex than that of a point in a
numeric continuum. A measurement is usually a segment of that continuum with
somewhat fuzzy limits. The measurements come out as intervals because of
uncertainty and randomness, as well as because the value being measured may
naturally be an interval indicating some condition, such as the temperature
range of stability of a protein.

Using just common sense, it appears more convenient to store such data as
intervals, rather than pairs of numbers. In practice, it even turns out more
efficient in most applications.

Further along the line of common sense, the fuzziness of the limits suggests
that the use of traditional numeric data types leads to a certain loss of
information. Consider this: your instrument reads 6.50, and you input this
reading into the database. What do you get when you fetch it? Watch:

    
    
    test=> select 6.50 :: float8 as "pH";
     pH
    ---
    6.5
    (1 row)
    

In the world of measurements, 6.50 is not the same as 6.5. It may sometimes be
critically different. The experimenters usually write down (and publish) the
digits they trust. 6.50 is actually a fuzzy interval contained within a bigger
and even fuzzier interval, 6.5, with their center points being (probably) the
only common feature they share. We definitely do not want such different data
items to appear the same.

Conclusion? It is nice to have a special data type that can record the limits
of an interval with arbitrarily variable precision. Variable in the sense that
each data element records its own precision.

Check this out:

    
    
    test=> select '6.25 .. 6.50'::seg as "pH";
              pH
    ------------
    6.25 .. 6.50
    (1 row)
    

### F.39.2. Syntax #

The external representation of an interval is formed using one or two
floating-point numbers joined by the range operator (`..` or `...`).
Alternatively, it can be specified as a center point plus or minus a
deviation. Optional certainty indicators (`<`, `>` or `~`) can be stored as
well. (Certainty indicators are ignored by all the built-in operators,
however.) [Table F.28](seg.html#SEG-REPR-TABLE "Table F.28. seg External
Representations") gives an overview of allowed representations; [Table
F.29](seg.html#SEG-INPUT-EXAMPLES "Table F.29. Examples of Valid seg Input")
shows some examples.

In [Table F.28](seg.html#SEG-REPR-TABLE "Table F.28. seg External
Representations"), _`x`_ , _`y`_ , and _`delta`_ denote floating-point
numbers. _`x`_ and _`y`_ , but not _`delta`_ , can be preceded by a certainty
indicator.

**Table  F.28. `seg` External Representations**

`_`x`_` | Single value (zero-length interval)  
---|---  
`_`x`_ .. _`y`_` | Interval from _`x`_ to _`y`_  
`_`x`_ (+-) _`delta`_` | Interval from _`x`_ \- _`delta`_ to _`x`_ \+ _`delta`_  
`_`x`_ ..` | Open interval with lower bound _`x`_  
`.. _`x`_` | Open interval with upper bound _`x`_  
  
  

**Table  F.29. Examples of Valid `seg` Input**

`5.0` | Creates a zero-length segment (a point, if you will)  
---|---  
`~5.0` | Creates a zero-length segment and records `~` in the data. `~` is ignored by `seg` operations, but is preserved as a comment.  
`<5.0` | Creates a point at 5.0. `<` is ignored but is preserved as a comment.  
`>5.0` | Creates a point at 5.0. `>` is ignored but is preserved as a comment.  
`5(+-)0.3` | Creates an interval `4.7 .. 5.3`. Note that the `(+-)` notation isn't preserved.  
`50 ..` | Everything that is greater than or equal to 50  
`.. 0` | Everything that is less than or equal to 0  
`1.5e-2 .. 2E-2` | Creates an interval `0.015 .. 0.02`  
`1 ... 2` | The same as `1...2`, or `1 .. 2`, or `1..2` (spaces around the range operator are ignored)  
  
  

Because the `...` operator is widely used in data sources, it is allowed as an
alternative spelling of the `..` operator. Unfortunately, this creates a
parsing ambiguity: it is not clear whether the upper bound in `0...23` is
meant to be `23` or `0.23`. This is resolved by requiring at least one digit
before the decimal point in all numbers in `seg` input.

As a sanity check, `seg` rejects intervals with the lower bound greater than
the upper, for example `5 .. 2`.

### F.39.3. Precision #

`seg` values are stored internally as pairs of 32-bit floating point numbers.
This means that numbers with more than 7 significant digits will be truncated.

Numbers with 7 or fewer significant digits retain their original precision.
That is, if your query returns 0.00, you will be sure that the trailing zeroes
are not the artifacts of formatting: they reflect the precision of the
original data. The number of leading zeroes does not affect precision: the
value 0.0067 is considered to have just 2 significant digits.

### F.39.4. Usage #

The `seg` module includes a GiST index operator class for `seg` values. The
operators supported by the GiST operator class are shown in [Table
F.30](seg.html#SEG-GIST-OPERATORS "Table F.30. Seg GiST Operators").

**Table  F.30. Seg GiST Operators**

Operator Description  
---  
`seg` `<<` `seg` → `boolean` Is the first `seg` entirely to the left of the
second? [a, b] << [c, d] is true if b < c.  
`seg` `>>` `seg` → `boolean` Is the first `seg` entirely to the right of the
second? [a, b] >> [c, d] is true if a > d.  
`seg` `&<` `seg` → `boolean` Does the first `seg` not extend to the right of
the second? [a, b] &< [c, d] is true if b <= d.  
`seg` `&>` `seg` → `boolean` Does the first `seg` not extend to the left of
the second? [a, b] &> [c, d] is true if a >= c.  
`seg` `=` `seg` → `boolean` Are the two `seg`s equal?  
`seg` `&&` `seg` → `boolean` Do the two `seg`s overlap?  
`seg` `@>` `seg` → `boolean` Does the first `seg` contain the second?  
`seg` `<@` `seg` → `boolean` Is the first `seg` contained in the second?  
  
  

In addition to the above operators, the usual comparison operators shown in
[Table 9.1](functions-comparison.html#FUNCTIONS-COMPARISON-OP-TABLE
"Table 9.1. Comparison Operators") are available for type `seg`. These
operators first compare (a) to (c), and if these are equal, compare (b) to
(d). That results in reasonably good sorting in most cases, which is useful if
you want to use ORDER BY with this type.

### F.39.5. Notes #

For examples of usage, see the regression test `sql/seg.sql`.

The mechanism that converts `(+-)` to regular ranges isn't completely accurate
in determining the number of significant digits for the boundaries. For
example, it adds an extra digit to the lower boundary if the resulting
interval includes a power of ten:

    
    
    postgres=> select '10(+-)1'::seg as seg;
          seg
    ---------
    9.0 .. 11             -- should be: 9 .. 11
    

The performance of an R-tree index can largely depend on the initial order of
input values. It may be very helpful to sort the input table on the `seg`
column; see the script `sort-segments.pl` for an example.

### F.39.6. Credits #

Original author: Gene Selkov, Jr.
`<[selkovjr@mcs.anl.gov](mailto:selkovjr@mcs.anl.gov)>`, Mathematics and
Computer Science Division, Argonne National Laboratory.

My thanks are primarily to Prof. Joe Hellerstein
(<https://dsf.berkeley.edu/jmh/>) for elucidating the gist of the GiST
(<http://gist.cs.berkeley.edu/>). I am also grateful to all Postgres
developers, present and past, for enabling myself to create my own world and
live undisturbed in it. And I would like to acknowledge my gratitude to
Argonne Lab and to the U.S. Department of Energy for the years of faithful
support of my database research.

* * *

[Prev](postgres-fdw.html "F.38. postgres_fdw —  access data stored in external PostgreSQL  servers")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](sepgsql.html "F.40. sepgsql —  SELinux-, label-based mandatory access control \(MAC\) security module")  
---|---|---  
F.38. postgres_fdw — access data stored in external PostgreSQL servers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.40. sepgsql — SELinux-, label-based mandatory access control (MAC) security module  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/seg.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

