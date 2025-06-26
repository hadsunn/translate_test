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

Supported Versions: [Current](/docs/current/datatype-textsearch.html
"PostgreSQL 17 - 8.11. Text Search Types") ([17](/docs/17/datatype-
textsearch.html "PostgreSQL 17 - 8.11. Text Search Types")) /
[16](/docs/16/datatype-textsearch.html "PostgreSQL 16 - 8.11. Text Search
Types") / [15](/docs/15/datatype-textsearch.html "PostgreSQL 15 - 8.11. Text
Search Types") / [14](/docs/14/datatype-textsearch.html "PostgreSQL 14 -
8.11. Text Search Types") / [13](/docs/13/datatype-textsearch.html "PostgreSQL
13 - 8.11. Text Search Types")

Development Versions: [18](/docs/18/datatype-textsearch.html "PostgreSQL 18 -
8.11. Text Search Types") / [devel](/docs/devel/datatype-textsearch.html
"PostgreSQL devel - 8.11. Text Search Types")

Unsupported versions: [12](/docs/12/datatype-textsearch.html "PostgreSQL 12 -
8.11. Text Search Types") / [11](/docs/11/datatype-textsearch.html "PostgreSQL
11 - 8.11. Text Search Types") / [10](/docs/10/datatype-textsearch.html
"PostgreSQL 10 - 8.11. Text Search Types") / [9.6](/docs/9.6/datatype-
textsearch.html "PostgreSQL 9.6 - 8.11. Text Search Types") /
[9.5](/docs/9.5/datatype-textsearch.html "PostgreSQL 9.5 - 8.11. Text Search
Types") / [9.4](/docs/9.4/datatype-textsearch.html "PostgreSQL 9.4 -
8.11. Text Search Types") / [9.3](/docs/9.3/datatype-textsearch.html
"PostgreSQL 9.3 - 8.11. Text Search Types") / [9.2](/docs/9.2/datatype-
textsearch.html "PostgreSQL 9.2 - 8.11. Text Search Types") /
[9.1](/docs/9.1/datatype-textsearch.html "PostgreSQL 9.1 - 8.11. Text Search
Types") / [9.0](/docs/9.0/datatype-textsearch.html "PostgreSQL 9.0 -
8.11. Text Search Types") / [8.4](/docs/8.4/datatype-textsearch.html
"PostgreSQL 8.4 - 8.11. Text Search Types") / [8.3](/docs/8.3/datatype-
textsearch.html "PostgreSQL 8.3 - 8.11. Text Search Types")

__

8.11. Text Search Types  
---  
[Prev](datatype-bit.html "8.10. Bit String Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-uuid.html "8.12. UUID Type")  
  
* * *

## 8.11. Text Search Types #

[8.11.1. `tsvector`](datatype-textsearch.html#DATATYPE-TSVECTOR)

[8.11.2. `tsquery`](datatype-textsearch.html#DATATYPE-TSQUERY)

PostgreSQL provides two data types that are designed to support full text
search, which is the activity of searching through a collection of natural-
language _documents_ to locate those that best match a _query_. The `tsvector`
type represents a document in a form optimized for text search; the `tsquery`
type similarly represents a text query. [Chapter 12](textsearch.html
"Chapter 12. Full Text Search") provides a detailed explanation of this
facility, and [Section 9.13](functions-textsearch.html "9.13. Text Search
Functions and Operators") summarizes the related functions and operators.

### 8.11.1. `tsvector` #

A `tsvector` value is a sorted list of distinct _lexemes_ , which are words
that have been _normalized_ to merge different variants of the same word (see
[Chapter 12](textsearch.html "Chapter 12. Full Text Search") for details).
Sorting and duplicate-elimination are done automatically during input, as
shown in this example:

    
    
    SELECT 'a fat cat sat on a mat and ate a fat rat'::tsvector;
                          tsvector
    ----------------------------------------------------
     'a' 'and' 'ate' 'cat' 'fat' 'mat' 'on' 'rat' 'sat'
    

To represent lexemes containing whitespace or punctuation, surround them with
quotes:

    
    
    SELECT $$the lexeme '    ' contains spaces$$::tsvector;
                     tsvector
    -------------------------------------------
     '    ' 'contains' 'lexeme' 'spaces' 'the'
    

(We use dollar-quoted string literals in this example and the next one to
avoid the confusion of having to double quote marks within the literals.)
Embedded quotes and backslashes must be doubled:

    
    
    SELECT $$the lexeme 'Joe''s' contains a quote$$::tsvector;
                        tsvector
    ------------------------------------------------
     'Joe''s' 'a' 'contains' 'lexeme' 'quote' 'the'
    

Optionally, integer _positions_ can be attached to lexemes:

    
    
    SELECT 'a:1 fat:2 cat:3 sat:4 on:5 a:6 mat:7 and:8 ate:9 a:10 fat:11 rat:12'::tsvector;
                                      tsvector
    -------------------------------------------------------------------​------------
     'a':1,6,10 'and':8 'ate':9 'cat':3 'fat':2,11 'mat':7 'on':5 'rat':12 'sat':4
    

A position normally indicates the source word's location in the document.
Positional information can be used for _proximity ranking_. Position values
can range from 1 to 16383; larger numbers are silently set to 16383. Duplicate
positions for the same lexeme are discarded.

Lexemes that have positions can further be labeled with a _weight_ , which can
be `A`, `B`, `C`, or `D`. `D` is the default and hence is not shown on output:

    
    
    SELECT 'a:1A fat:2B,4C cat:5D'::tsvector;
              tsvector
    ----------------------------
     'a':1A 'cat':5 'fat':2B,4C
    

Weights are typically used to reflect document structure, for example by
marking title words differently from body words. Text search ranking functions
can assign different priorities to the different weight markers.

It is important to understand that the `tsvector` type itself does not perform
any word normalization; it assumes the words it is given are normalized
appropriately for the application. For example,

    
    
    SELECT 'The Fat Rats'::tsvector;
          tsvector
    --------------------
     'Fat' 'Rats' 'The'
    

For most English-text-searching applications the above words would be
considered non-normalized, but `tsvector` doesn't care. Raw document text
should usually be passed through `to_tsvector` to normalize the words
appropriately for searching:

    
    
    SELECT to_tsvector('english', 'The Fat Rats');
       to_tsvector
    -----------------
     'fat':2 'rat':3
    

Again, see [Chapter 12](textsearch.html "Chapter 12. Full Text Search") for
more detail.

### 8.11.2. `tsquery` #

A `tsquery` value stores lexemes that are to be searched for, and can combine
them using the Boolean operators `&` (AND), `|` (OR), and `!` (NOT), as well
as the phrase search operator `<->` (FOLLOWED BY). There is also a variant
`<_`N`_ >` of the FOLLOWED BY operator, where _`N`_ is an integer constant
that specifies the distance between the two lexemes being searched for. `<->`
is equivalent to `<1>`.

Parentheses can be used to enforce grouping of these operators. In the absence
of parentheses, `!` (NOT) binds most tightly, `<->` (FOLLOWED BY) next most
tightly, then `&` (AND), with `|` (OR) binding the least tightly.

Here are some examples:

    
    
    SELECT 'fat & rat'::tsquery;
        tsquery
    ---------------
     'fat' & 'rat'
    
    SELECT 'fat & (rat | cat)'::tsquery;
              tsquery
    ---------------------------
     'fat' & ( 'rat' | 'cat' )
    
    SELECT 'fat & rat & ! cat'::tsquery;
            tsquery
    ------------------------
     'fat' & 'rat' & !'cat'
    

Optionally, lexemes in a `tsquery` can be labeled with one or more weight
letters, which restricts them to match only `tsvector` lexemes with one of
those weights:

    
    
    SELECT 'fat:ab & cat'::tsquery;
        tsquery
    ------------------
     'fat':AB & 'cat'
    

Also, lexemes in a `tsquery` can be labeled with `*` to specify prefix
matching:

    
    
    SELECT 'super:*'::tsquery;
      tsquery
    -----------
     'super':*
    

This query will match any word in a `tsvector` that begins with “super”.

Quoting rules for lexemes are the same as described previously for lexemes in
`tsvector`; and, as with `tsvector`, any required normalization of words must
be done before converting to the `tsquery` type. The `to_tsquery` function is
convenient for performing such normalization:

    
    
    SELECT to_tsquery('Fat:ab & Cats');
        to_tsquery
    ------------------
     'fat':AB & 'cat'
    

Note that `to_tsquery` will process prefixes in the same way as other words,
which means this comparison returns true:

    
    
    SELECT to_tsvector( 'postgraduate' ) @@ to_tsquery( 'postgres:*' );
     ?column?
    ----------
     t
    

because `postgres` gets stemmed to `postgr`:

    
    
    SELECT to_tsvector( 'postgraduate' ), to_tsquery( 'postgres:*' );
      to_tsvector  | to_tsquery
    ---------------+------------
     'postgradu':1 | 'postgr':*
    

which will match the stemmed form of `postgraduate`.

* * *

[Prev](datatype-bit.html "8.10. Bit String Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-uuid.html "8.12. UUID Type")  
---|---|---  
8.10. Bit String Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.12. UUID Type  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-textsearch.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

