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

Supported Versions: [Current](/docs/current/dict-xsyn.html "PostgreSQL 17 -
F.14. dict_xsyn — example synonym full-text search dictionary")
([17](/docs/17/dict-xsyn.html "PostgreSQL 17 - F.14. dict_xsyn — example
synonym full-text search dictionary")) / [16](/docs/16/dict-xsyn.html
"PostgreSQL 16 - F.14. dict_xsyn — example synonym full-text search
dictionary") / [15](/docs/15/dict-xsyn.html "PostgreSQL 15 - F.14. dict_xsyn —
example synonym full-text search dictionary") / [14](/docs/14/dict-xsyn.html
"PostgreSQL 14 - F.14. dict_xsyn — example synonym full-text search
dictionary") / [13](/docs/13/dict-xsyn.html "PostgreSQL 13 - F.14. dict_xsyn —
example synonym full-text search dictionary")

Development Versions: [18](/docs/18/dict-xsyn.html "PostgreSQL 18 -
F.14. dict_xsyn — example synonym full-text search dictionary") /
[devel](/docs/devel/dict-xsyn.html "PostgreSQL devel - F.14. dict_xsyn —
example synonym full-text search dictionary")

Unsupported versions: [12](/docs/12/dict-xsyn.html "PostgreSQL 12 -
F.14. dict_xsyn — example synonym full-text search dictionary") /
[11](/docs/11/dict-xsyn.html "PostgreSQL 11 - F.14. dict_xsyn — example
synonym full-text search dictionary") / [10](/docs/10/dict-xsyn.html
"PostgreSQL 10 - F.14. dict_xsyn — example synonym full-text search
dictionary") / [9.6](/docs/9.6/dict-xsyn.html "PostgreSQL 9.6 -
F.14. dict_xsyn — example synonym full-text search dictionary") /
[9.5](/docs/9.5/dict-xsyn.html "PostgreSQL 9.5 - F.14. dict_xsyn — example
synonym full-text search dictionary") / [9.4](/docs/9.4/dict-xsyn.html
"PostgreSQL 9.4 - F.14. dict_xsyn — example synonym full-text search
dictionary") / [9.3](/docs/9.3/dict-xsyn.html "PostgreSQL 9.3 -
F.14. dict_xsyn — example synonym full-text search dictionary") /
[9.2](/docs/9.2/dict-xsyn.html "PostgreSQL 9.2 - F.14. dict_xsyn — example
synonym full-text search dictionary") / [9.1](/docs/9.1/dict-xsyn.html
"PostgreSQL 9.1 - F.14. dict_xsyn — example synonym full-text search
dictionary") / [9.0](/docs/9.0/dict-xsyn.html "PostgreSQL 9.0 -
F.14. dict_xsyn — example synonym full-text search dictionary") /
[8.4](/docs/8.4/dict-xsyn.html "PostgreSQL 8.4 - F.14. dict_xsyn — example
synonym full-text search dictionary") / [8.3](/docs/8.3/dict-xsyn.html
"PostgreSQL 8.3 - F.14. dict_xsyn — example synonym full-text search
dictionary")

__

F.14. dict_xsyn — example synonym full-text search dictionary  
---  
[Prev](dict-int.html "F.13. dict_int —  example full-text search dictionary for integers")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](earthdistance.html "F.15. earthdistance — calculate great-circle distances")  
  
* * *

## F.14. dict_xsyn — example synonym full-text search dictionary #

[F.14.1. Configuration](dict-xsyn.html#DICT-XSYN-CONFIG)

[F.14.2. Usage](dict-xsyn.html#DICT-XSYN-USAGE)

`dict_xsyn` (Extended Synonym Dictionary) is an example of an add-on
dictionary template for full-text search. This dictionary type replaces words
with groups of their synonyms, and so makes it possible to search for a word
using any of its synonyms.

### F.14.1. Configuration #

A `dict_xsyn` dictionary accepts the following options:

  * `matchorig` controls whether the original word is accepted by the dictionary. Default is `true`.

  * `matchsynonyms` controls whether the synonyms are accepted by the dictionary. Default is `false`.

  * `keeporig` controls whether the original word is included in the dictionary's output. Default is `true`.

  * `keepsynonyms` controls whether the synonyms are included in the dictionary's output. Default is `true`.

  * `rules` is the base name of the file containing the list of synonyms. This file must be stored in `$SHAREDIR/tsearch_data/` (where `$SHAREDIR` means the PostgreSQL installation's shared-data directory). Its name must end in `.rules` (which is not to be included in the `rules` parameter).

The rules file has the following format:

  * Each line represents a group of synonyms for a single word, which is given first on the line. Synonyms are separated by whitespace, thus:
        
        word syn1 syn2 syn3
        

  * The sharp (`#`) sign is a comment delimiter. It may appear at any position in a line. The rest of the line will be skipped.

Look at `xsyn_sample.rules`, which is installed in `$SHAREDIR/tsearch_data/`,
for an example.

### F.14.2. Usage #

Installing the `dict_xsyn` extension creates a text search template
`xsyn_template` and a dictionary `xsyn` based on it, with default parameters.
You can alter the parameters, for example

    
    
    mydb# ALTER TEXT SEARCH DICTIONARY xsyn (RULES='my_rules', KEEPORIG=false);
    ALTER TEXT SEARCH DICTIONARY
    

or create new dictionaries based on the template.

To test the dictionary, you can try

    
    
    mydb=# SELECT ts_lexize('xsyn', 'word');
          ts_lexize
    -----------------------
     {syn1,syn2,syn3}
    
    mydb# ALTER TEXT SEARCH DICTIONARY xsyn (RULES='my_rules', KEEPORIG=true);
    ALTER TEXT SEARCH DICTIONARY
    
    mydb=# SELECT ts_lexize('xsyn', 'word');
          ts_lexize
    -----------------------
     {word,syn1,syn2,syn3}
    
    mydb# ALTER TEXT SEARCH DICTIONARY xsyn (RULES='my_rules', KEEPORIG=false, MATCHSYNONYMS=true);
    ALTER TEXT SEARCH DICTIONARY
    
    mydb=# SELECT ts_lexize('xsyn', 'syn1');
          ts_lexize
    -----------------------
     {syn1,syn2,syn3}
    
    mydb# ALTER TEXT SEARCH DICTIONARY xsyn (RULES='my_rules', KEEPORIG=true, MATCHORIG=false, KEEPSYNONYMS=false);
    ALTER TEXT SEARCH DICTIONARY
    
    mydb=# SELECT ts_lexize('xsyn', 'syn1');
          ts_lexize
    -----------------------
     {word}
    

Real-world usage will involve including it in a text search configuration as
described in [Chapter 12](textsearch.html "Chapter 12. Full Text Search").
That might look like this:

    
    
    ALTER TEXT SEARCH CONFIGURATION english
        ALTER MAPPING FOR word, asciiword WITH xsyn, english_stem;
    

* * *

[Prev](dict-int.html "F.13. dict_int —  example full-text search dictionary for integers")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](earthdistance.html "F.15. earthdistance — calculate great-circle distances")  
---|---|---  
F.13. dict_int — example full-text search dictionary for integers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.15. earthdistance — calculate great-circle distances  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dict-xsyn.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

