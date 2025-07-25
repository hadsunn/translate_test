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

Supported Versions: [Current](/docs/current/fuzzystrmatch.html "PostgreSQL 17
- F.17. fuzzystrmatch — determine string similarities and distance")
([17](/docs/17/fuzzystrmatch.html "PostgreSQL 17 - F.17. fuzzystrmatch —
determine string similarities and distance")) /
[16](/docs/16/fuzzystrmatch.html "PostgreSQL 16 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[15](/docs/15/fuzzystrmatch.html "PostgreSQL 15 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[14](/docs/14/fuzzystrmatch.html "PostgreSQL 14 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[13](/docs/13/fuzzystrmatch.html "PostgreSQL 13 - F.17. fuzzystrmatch —
determine string similarities and distance")

Development Versions: [18](/docs/18/fuzzystrmatch.html "PostgreSQL 18 -
F.17. fuzzystrmatch — determine string similarities and distance") /
[devel](/docs/devel/fuzzystrmatch.html "PostgreSQL devel - F.17. fuzzystrmatch
— determine string similarities and distance")

Unsupported versions: [12](/docs/12/fuzzystrmatch.html "PostgreSQL 12 -
F.17. fuzzystrmatch — determine string similarities and distance") /
[11](/docs/11/fuzzystrmatch.html "PostgreSQL 11 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[10](/docs/10/fuzzystrmatch.html "PostgreSQL 10 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.6](/docs/9.6/fuzzystrmatch.html "PostgreSQL 9.6 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.5](/docs/9.5/fuzzystrmatch.html "PostgreSQL 9.5 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.4](/docs/9.4/fuzzystrmatch.html "PostgreSQL 9.4 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.3](/docs/9.3/fuzzystrmatch.html "PostgreSQL 9.3 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.2](/docs/9.2/fuzzystrmatch.html "PostgreSQL 9.2 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.1](/docs/9.1/fuzzystrmatch.html "PostgreSQL 9.1 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[9.0](/docs/9.0/fuzzystrmatch.html "PostgreSQL 9.0 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[8.4](/docs/8.4/fuzzystrmatch.html "PostgreSQL 8.4 - F.17. fuzzystrmatch —
determine string similarities and distance") /
[8.3](/docs/8.3/fuzzystrmatch.html "PostgreSQL 8.3 - F.17. fuzzystrmatch —
determine string similarities and distance")

__

F.17. fuzzystrmatch — determine string similarities and distance  
---  
[Prev](file-fdw.html "F.16. file_fdw — access data files in the server's file system")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](hstore.html "F.18. hstore — hstore key/value datatype")  
  
* * *

## F.17. fuzzystrmatch — determine string similarities and distance #

[F.17.1. Soundex](fuzzystrmatch.html#FUZZYSTRMATCH-SOUNDEX)

[F.17.2. Daitch-Mokotoff Soundex](fuzzystrmatch.html#FUZZYSTRMATCH-DAITCH-
MOKOTOFF)

[F.17.3. Levenshtein](fuzzystrmatch.html#FUZZYSTRMATCH-LEVENSHTEIN)

[F.17.4. Metaphone](fuzzystrmatch.html#FUZZYSTRMATCH-METAPHONE)

[F.17.5. Double Metaphone](fuzzystrmatch.html#FUZZYSTRMATCH-DOUBLE-METAPHONE)

The `fuzzystrmatch` module provides several functions to determine
similarities and distance between strings.

### Caution

At present, the `soundex`, `metaphone`, `dmetaphone`, and `dmetaphone_alt`
functions do not work well with multibyte encodings (such as UTF-8). Use
`daitch_mokotoff` or `levenshtein` with such data.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.17.1. Soundex #

The Soundex system is a method of matching similar-sounding names by
converting them to the same code. It was initially used by the United States
Census in 1880, 1900, and 1910. Note that Soundex is not very useful for non-
English names.

The `fuzzystrmatch` module provides two functions for working with Soundex
codes:

    
    
    soundex(text) returns text
    difference(text, text) returns int
    

The `soundex` function converts a string to its Soundex code. The `difference`
function converts two strings to their Soundex codes and then reports the
number of matching code positions. Since Soundex codes have four characters,
the result ranges from zero to four, with zero being no match and four being
an exact match. (Thus, the function is misnamed — `similarity` would have been
a better name.)

Here are some usage examples:

    
    
    SELECT soundex('hello world!');
    
    SELECT soundex('Anne'), soundex('Ann'), difference('Anne', 'Ann');
    SELECT soundex('Anne'), soundex('Andrew'), difference('Anne', 'Andrew');
    SELECT soundex('Anne'), soundex('Margaret'), difference('Anne', 'Margaret');
    
    CREATE TABLE s (nm text);
    
    INSERT INTO s VALUES ('john');
    INSERT INTO s VALUES ('joan');
    INSERT INTO s VALUES ('wobbly');
    INSERT INTO s VALUES ('jack');
    
    SELECT * FROM s WHERE soundex(nm) = soundex('john');
    
    SELECT * FROM s WHERE difference(s.nm, 'john') > 2;
    

### F.17.2. Daitch-Mokotoff Soundex #

Like the original Soundex system, Daitch-Mokotoff Soundex matches similar-
sounding names by converting them to the same code. However, Daitch-Mokotoff
Soundex is significantly more useful for non-English names than the original
system. Major improvements over the original system include:

  * The code is based on the first six meaningful letters rather than four.

  * A letter or combination of letters maps into ten possible codes rather than seven.

  * Where two consecutive letters have a single sound, they are coded as a single number.

  * When a letter or combination of letters may have different sounds, multiple codes are emitted to cover all possibilities.

This function generates the Daitch-Mokotoff soundex codes for its input:

    
    
    daitch_mokotoff(_source_ text) returns text[]
    

The result may contain one or more codes depending on how many plausible
pronunciations there are, so it is represented as an array.

Since a Daitch-Mokotoff soundex code consists of only 6 digits, _`source`_
should be preferably a single word or name.

Here are some examples:

    
    
    SELECT daitch_mokotoff('George');
     daitch_mokotoff
    -----------------
     {595000}
    
    SELECT daitch_mokotoff('John');
     daitch_mokotoff
    -----------------
     {160000,460000}
    
    SELECT daitch_mokotoff('Bierschbach');
                          daitch_mokotoff
    -----------------------------------------------------------
     {794575,794574,794750,794740,745750,745740,747500,747400}
    
    SELECT daitch_mokotoff('Schwartzenegger');
     daitch_mokotoff
    -----------------
     {479465}
    

For matching of single names, returned text arrays can be matched directly
using the `&&` operator: any overlap can be considered a match. A GIN index
may be used for efficiency, see [Chapter 70](gin.html "Chapter 70. GIN
Indexes") and this example:

    
    
    CREATE TABLE s (nm text);
    CREATE INDEX ix_s_dm ON s USING gin (daitch_mokotoff(nm)) WITH (fastupdate = off);
    
    INSERT INTO s (nm) VALUES
      ('Schwartzenegger'),
      ('John'),
      ('James'),
      ('Steinman'),
      ('Steinmetz');
    
    SELECT * FROM s WHERE daitch_mokotoff(nm) && daitch_mokotoff('Swartzenegger');
    SELECT * FROM s WHERE daitch_mokotoff(nm) && daitch_mokotoff('Jane');
    SELECT * FROM s WHERE daitch_mokotoff(nm) && daitch_mokotoff('Jens');
    

For indexing and matching of any number of names in any order, Full Text
Search features can be used. See [Chapter 12](textsearch.html
"Chapter 12. Full Text Search") and this example:

    
    
    CREATE FUNCTION soundex_tsvector(v_name text) RETURNS tsvector
    BEGIN ATOMIC
      SELECT to_tsvector('simple',
                         string_agg(array_to_string(daitch_mokotoff(n), ' '), ' '))
      FROM regexp_split_to_table(v_name, '\s+') AS n;
    END;
    
    CREATE FUNCTION soundex_tsquery(v_name text) RETURNS tsquery
    BEGIN ATOMIC
      SELECT string_agg('(' || array_to_string(daitch_mokotoff(n), '|') || ')', '&')::tsquery
      FROM regexp_split_to_table(v_name, '\s+') AS n;
    END;
    
    CREATE TABLE s (nm text);
    CREATE INDEX ix_s_txt ON s USING gin (soundex_tsvector(nm)) WITH (fastupdate = off);
    
    INSERT INTO s (nm) VALUES
      ('John Doe'),
      ('Jane Roe'),
      ('Public John Q.'),
      ('George Best'),
      ('John Yamson');
    
    SELECT * FROM s WHERE soundex_tsvector(nm) @@ soundex_tsquery('john');
    SELECT * FROM s WHERE soundex_tsvector(nm) @@ soundex_tsquery('jane doe');
    SELECT * FROM s WHERE soundex_tsvector(nm) @@ soundex_tsquery('john public');
    SELECT * FROM s WHERE soundex_tsvector(nm) @@ soundex_tsquery('besst, giorgio');
    SELECT * FROM s WHERE soundex_tsvector(nm) @@ soundex_tsquery('Jameson John');
    

If it is desired to avoid recalculation of soundex codes during index
rechecks, an index on a separate column can be used instead of an index on an
expression. A stored generated column can be used for this; see [Section
5.3](ddl-generated-columns.html "5.3. Generated Columns").

### F.17.3. Levenshtein #

This function calculates the Levenshtein distance between two strings:

    
    
    levenshtein(source text, target text, ins_cost int, del_cost int, sub_cost int) returns int
    levenshtein(source text, target text) returns int
    levenshtein_less_equal(source text, target text, ins_cost int, del_cost int, sub_cost int, max_d int) returns int
    levenshtein_less_equal(source text, target text, max_d int) returns int
    

Both `source` and `target` can be any non-null string, with a maximum of 255
characters. The cost parameters specify how much to charge for a character
insertion, deletion, or substitution, respectively. You can omit the cost
parameters, as in the second version of the function; in that case they all
default to 1.

`levenshtein_less_equal` is an accelerated version of the Levenshtein function
for use when only small distances are of interest. If the actual distance is
less than or equal to `max_d`, then `levenshtein_less_equal` returns the
correct distance; otherwise it returns some value greater than `max_d`. If
`max_d` is negative then the behavior is the same as `levenshtein`.

Examples:

    
    
    test=# SELECT levenshtein('GUMBO', 'GAMBOL');
     levenshtein
    -------------
               2
    (1 row)
    
    test=# SELECT levenshtein('GUMBO', 'GAMBOL', 2, 1, 1);
     levenshtein
    -------------
               3
    (1 row)
    
    test=# SELECT levenshtein_less_equal('extensive', 'exhaustive', 2);
     levenshtein_less_equal
    ------------------------
                          3
    (1 row)
    
    test=# SELECT levenshtein_less_equal('extensive', 'exhaustive', 4);
     levenshtein_less_equal
    ------------------------
                          4
    (1 row)
    

### F.17.4. Metaphone #

Metaphone, like Soundex, is based on the idea of constructing a representative
code for an input string. Two strings are then deemed similar if they have the
same codes.

This function calculates the metaphone code of an input string:

    
    
    metaphone(source text, max_output_length int) returns text
    

`source` has to be a non-null string with a maximum of 255 characters.
`max_output_length` sets the maximum length of the output metaphone code; if
longer, the output is truncated to this length.

Example:

    
    
    test=# SELECT metaphone('GUMBO', 4);
     metaphone
    -----------
     KM
    (1 row)
    

### F.17.5. Double Metaphone #

The Double Metaphone system computes two “sounds like” strings for a given
input string — a “primary” and an “alternate”. In most cases they are the
same, but for non-English names especially they can be a bit different,
depending on pronunciation. These functions compute the primary and alternate
codes:

    
    
    dmetaphone(source text) returns text
    dmetaphone_alt(source text) returns text
    

There is no length limit on the input strings.

Example:

    
    
    test=# SELECT dmetaphone('gumbo');
     dmetaphone
    ------------
     KMP
    (1 row)
    

* * *

[Prev](file-fdw.html "F.16. file_fdw — access data files in the server's file system")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](hstore.html "F.18. hstore — hstore key/value datatype")  
---|---|---  
F.16. file_fdw — access data files in the server's file system  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.18. hstore — hstore key/value datatype  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/fuzzystrmatch.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

