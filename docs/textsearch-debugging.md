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

Supported Versions: [Current](/docs/current/textsearch-debugging.html
"PostgreSQL 17 - 12.8. Testing and Debugging Text Search")
([17](/docs/17/textsearch-debugging.html "PostgreSQL 17 - 12.8. Testing and
Debugging Text Search")) / [16](/docs/16/textsearch-debugging.html "PostgreSQL
16 - 12.8. Testing and Debugging Text Search") / [15](/docs/15/textsearch-
debugging.html "PostgreSQL 15 - 12.8. Testing and Debugging Text Search") /
[14](/docs/14/textsearch-debugging.html "PostgreSQL 14 - 12.8. Testing and
Debugging Text Search") / [13](/docs/13/textsearch-debugging.html "PostgreSQL
13 - 12.8. Testing and Debugging Text Search")

Development Versions: [18](/docs/18/textsearch-debugging.html "PostgreSQL 18 -
12.8. Testing and Debugging Text Search") / [devel](/docs/devel/textsearch-
debugging.html "PostgreSQL devel - 12.8. Testing and Debugging Text Search")

Unsupported versions: [12](/docs/12/textsearch-debugging.html "PostgreSQL 12 -
12.8. Testing and Debugging Text Search") / [11](/docs/11/textsearch-
debugging.html "PostgreSQL 11 - 12.8. Testing and Debugging Text Search") /
[10](/docs/10/textsearch-debugging.html "PostgreSQL 10 - 12.8. Testing and
Debugging Text Search") / [9.6](/docs/9.6/textsearch-debugging.html
"PostgreSQL 9.6 - 12.8. Testing and Debugging Text Search") /
[9.5](/docs/9.5/textsearch-debugging.html "PostgreSQL 9.5 - 12.8. Testing and
Debugging Text Search") / [9.4](/docs/9.4/textsearch-debugging.html
"PostgreSQL 9.4 - 12.8. Testing and Debugging Text Search") /
[9.3](/docs/9.3/textsearch-debugging.html "PostgreSQL 9.3 - 12.8. Testing and
Debugging Text Search") / [9.2](/docs/9.2/textsearch-debugging.html
"PostgreSQL 9.2 - 12.8. Testing and Debugging Text Search") /
[9.1](/docs/9.1/textsearch-debugging.html "PostgreSQL 9.1 - 12.8. Testing and
Debugging Text Search") / [9.0](/docs/9.0/textsearch-debugging.html
"PostgreSQL 9.0 - 12.8. Testing and Debugging Text Search") /
[8.4](/docs/8.4/textsearch-debugging.html "PostgreSQL 8.4 - 12.8. Testing and
Debugging Text Search") / [8.3](/docs/8.3/textsearch-debugging.html
"PostgreSQL 8.3 - 12.8. Testing and Debugging Text Search")

__

12.8. Testing and Debugging Text Search  
---  
[Prev](textsearch-configuration.html "12.7. Configuration Example")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-indexes.html "12.9. Preferred Index Types for Text Search")  
  
* * *

## 12.8. Testing and Debugging Text Search #

[12.8.1. Configuration Testing](textsearch-debugging.html#TEXTSEARCH-
CONFIGURATION-TESTING)

[12.8.2. Parser Testing](textsearch-debugging.html#TEXTSEARCH-PARSER-TESTING)

[12.8.3. Dictionary Testing](textsearch-debugging.html#TEXTSEARCH-DICTIONARY-
TESTING)

The behavior of a custom text search configuration can easily become
confusing. The functions described in this section are useful for testing text
search objects. You can test a complete configuration, or test parsers and
dictionaries separately.

### 12.8.1. Configuration Testing #

The function `ts_debug` allows easy testing of a text search configuration.

    
    
    ts_debug([ _config_ regconfig, ] _document_ text,
             OUT _alias_ text,
             OUT _description_ text,
             OUT _token_ text,
             OUT _dictionaries_ regdictionary[],
             OUT _dictionary_ regdictionary,
             OUT _lexemes_ text[])
             returns setof record
    

`ts_debug` displays information about every token of _`document`_ as produced
by the parser and processed by the configured dictionaries. It uses the
configuration specified by _`config`_ , or `default_text_search_config` if
that argument is omitted.

`ts_debug` returns one row for each token identified in the text by the
parser. The columns returned are

  * _`alias`_ `text` — short name of the token type

  * _`description`_ `text` — description of the token type

  * _`token`_ `text` — text of the token

  * _`dictionaries`_ `regdictionary[]` — the dictionaries selected by the configuration for this token type

  * _`dictionary`_ `regdictionary` — the dictionary that recognized the token, or `NULL` if none did

  * _`lexemes`_ `text[]` — the lexeme(s) produced by the dictionary that recognized the token, or `NULL` if none did; an empty array (`{}`) means it was recognized as a stop word

Here is a simple example:

    
    
    SELECT * FROM ts_debug('english', 'a fat  cat sat on a mat - it ate a fat rats');
       alias   |   description   | token |  dictionaries  |  dictionary  | lexemes
    -----------+-----------------+-------+----------------+--------------+---------
     asciiword | Word, all ASCII | a     | {english_stem} | english_stem | {}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | fat   | {english_stem} | english_stem | {fat}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | cat   | {english_stem} | english_stem | {cat}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | sat   | {english_stem} | english_stem | {sat}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | on    | {english_stem} | english_stem | {}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | a     | {english_stem} | english_stem | {}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | mat   | {english_stem} | english_stem | {mat}
     blank     | Space symbols   |       | {}             |              |
     blank     | Space symbols   | -     | {}             |              |
     asciiword | Word, all ASCII | it    | {english_stem} | english_stem | {}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | ate   | {english_stem} | english_stem | {ate}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | a     | {english_stem} | english_stem | {}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | fat   | {english_stem} | english_stem | {fat}
     blank     | Space symbols   |       | {}             |              |
     asciiword | Word, all ASCII | rats  | {english_stem} | english_stem | {rat}
    

For a more extensive demonstration, we first create a `public.english`
configuration and Ispell dictionary for the English language:

    
    
    CREATE TEXT SEARCH CONFIGURATION public.english ( COPY = pg_catalog.english );
    
    CREATE TEXT SEARCH DICTIONARY english_ispell (
        TEMPLATE = ispell,
        DictFile = english,
        AffFile = english,
        StopWords = english
    );
    
    ALTER TEXT SEARCH CONFIGURATION public.english
       ALTER MAPPING FOR asciiword WITH english_ispell, english_stem;
    
    
    
    SELECT * FROM ts_debug('public.english', 'The Brightest supernovaes');
       alias   |   description   |    token    |         dictionaries          |   dictionary   |   lexemes
    -----------+-----------------+-------------+-------------------------------+----------------+-------------
     asciiword | Word, all ASCII | The         | {english_ispell,english_stem} | english_ispell | {}
     blank     | Space symbols   |             | {}                            |                |
     asciiword | Word, all ASCII | Brightest   | {english_ispell,english_stem} | english_ispell | {bright}
     blank     | Space symbols   |             | {}                            |                |
     asciiword | Word, all ASCII | supernovaes | {english_ispell,english_stem} | english_stem   | {supernova}
    

In this example, the word `Brightest` was recognized by the parser as an
`ASCII word` (alias `asciiword`). For this token type the dictionary list is
`english_ispell` and `english_stem`. The word was recognized by
`english_ispell`, which reduced it to the noun `bright`. The word
`supernovaes` is unknown to the `english_ispell` dictionary so it was passed
to the next dictionary, and, fortunately, was recognized (in fact,
`english_stem` is a Snowball dictionary which recognizes everything; that is
why it was placed at the end of the dictionary list).

The word `The` was recognized by the `english_ispell` dictionary as a stop
word ([Section 12.6.1](textsearch-dictionaries.html#TEXTSEARCH-STOPWORDS
"12.6.1. Stop Words")) and will not be indexed. The spaces are discarded too,
since the configuration provides no dictionaries at all for them.

You can reduce the width of the output by explicitly specifying which columns
you want to see:

    
    
    SELECT alias, token, dictionary, lexemes
    FROM ts_debug('public.english', 'The Brightest supernovaes');
       alias   |    token    |   dictionary   |   lexemes
    -----------+-------------+----------------+-------------
     asciiword | The         | english_ispell | {}
     blank     |             |                |
     asciiword | Brightest   | english_ispell | {bright}
     blank     |             |                |
     asciiword | supernovaes | english_stem   | {supernova}
    

### 12.8.2. Parser Testing #

The following functions allow direct testing of a text search parser.

    
    
    ts_parse(_parser_name_ text, _document_ text,
             OUT _tokid_ integer, OUT _token_ text) returns setof record
    ts_parse(_parser_oid_ oid, _document_ text,
             OUT _tokid_ integer, OUT _token_ text) returns setof record
    

`ts_parse` parses the given _`document`_ and returns a series of records, one
for each token produced by parsing. Each record includes a `tokid` showing the
assigned token type and a `token` which is the text of the token. For example:

    
    
    SELECT * FROM ts_parse('default', '123 - a number');
     tokid | token
    -------+--------
        22 | 123
        12 |
        12 | -
         1 | a
        12 |
         1 | number
    
    
    
    ts_token_type(_parser_name_ text, OUT _tokid_ integer,
                  OUT _alias_ text, OUT _description_ text) returns setof record
    ts_token_type(_parser_oid_ oid, OUT _tokid_ integer,
                  OUT _alias_ text, OUT _description_ text) returns setof record
    

`ts_token_type` returns a table which describes each type of token the
specified parser can recognize. For each token type, the table gives the
integer `tokid` that the parser uses to label a token of that type, the
`alias` that names the token type in configuration commands, and a short
`description`. For example:

    
    
    SELECT * FROM ts_token_type('default');
     tokid |      alias      |               description
    -------+-----------------+------------------------------------------
         1 | asciiword       | Word, all ASCII
         2 | word            | Word, all letters
         3 | numword         | Word, letters and digits
         4 | email           | Email address
         5 | url             | URL
         6 | host            | Host
         7 | sfloat          | Scientific notation
         8 | version         | Version number
         9 | hword_numpart   | Hyphenated word part, letters and digits
        10 | hword_part      | Hyphenated word part, all letters
        11 | hword_asciipart | Hyphenated word part, all ASCII
        12 | blank           | Space symbols
        13 | tag             | XML tag
        14 | protocol        | Protocol head
        15 | numhword        | Hyphenated word, letters and digits
        16 | asciihword      | Hyphenated word, all ASCII
        17 | hword           | Hyphenated word, all letters
        18 | url_path        | URL path
        19 | file            | File or path name
        20 | float           | Decimal notation
        21 | int             | Signed integer
        22 | uint            | Unsigned integer
        23 | entity          | XML entity
    

### 12.8.3. Dictionary Testing #

The `ts_lexize` function facilitates dictionary testing.

    
    
    ts_lexize(_dict_ regdictionary, _token_ text) returns text[]
    

`ts_lexize` returns an array of lexemes if the input _`token`_ is known to the
dictionary, or an empty array if the token is known to the dictionary but it
is a stop word, or `NULL` if it is an unknown word.

Examples:

    
    
    SELECT ts_lexize('english_stem', 'stars');
     ts_lexize
    -----------
     {star}
    
    SELECT ts_lexize('english_stem', 'a');
     ts_lexize
    -----------
     {}
    

### Note

The `ts_lexize` function expects a single _token_ , not text. Here is a case
where this can be confusing:

    
    
    SELECT ts_lexize('thesaurus_astro', 'supernovae stars') is null;
     ?column?
    ----------
     t
    

The thesaurus dictionary `thesaurus_astro` does know the phrase `supernovae
stars`, but `ts_lexize` fails since it does not parse the input text but
treats it as a single token. Use `plainto_tsquery` or `to_tsvector` to test
thesaurus dictionaries, for example:

    
    
    SELECT plainto_tsquery('supernovae stars');
     plainto_tsquery
    -----------------
     'sn'
    

* * *

[Prev](textsearch-configuration.html "12.7. Configuration Example")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-indexes.html "12.9. Preferred Index Types for Text Search")  
---|---|---  
12.7. Configuration Example  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.9. Preferred Index Types for Text Search  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-debugging.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

