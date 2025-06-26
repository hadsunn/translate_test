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

Supported Versions: [Current](/docs/current/unaccent.html "PostgreSQL 17 -
F.48. unaccent — a text search dictionary which removes diacritics")
([17](/docs/17/unaccent.html "PostgreSQL 17 - F.48. unaccent — a text search
dictionary which removes diacritics")) / [16](/docs/16/unaccent.html
"PostgreSQL 16 - F.48. unaccent — a text search dictionary which removes
diacritics") / [15](/docs/15/unaccent.html "PostgreSQL 15 - F.48. unaccent — a
text search dictionary which removes diacritics") /
[14](/docs/14/unaccent.html "PostgreSQL 14 - F.48. unaccent — a text search
dictionary which removes diacritics") / [13](/docs/13/unaccent.html
"PostgreSQL 13 - F.48. unaccent — a text search dictionary which removes
diacritics")

Development Versions: [18](/docs/18/unaccent.html "PostgreSQL 18 -
F.48. unaccent — a text search dictionary which removes diacritics") /
[devel](/docs/devel/unaccent.html "PostgreSQL devel - F.48. unaccent — a text
search dictionary which removes diacritics")

Unsupported versions: [12](/docs/12/unaccent.html "PostgreSQL 12 -
F.48. unaccent — a text search dictionary which removes diacritics") /
[11](/docs/11/unaccent.html "PostgreSQL 11 - F.48. unaccent — a text search
dictionary which removes diacritics") / [10](/docs/10/unaccent.html
"PostgreSQL 10 - F.48. unaccent — a text search dictionary which removes
diacritics") / [9.6](/docs/9.6/unaccent.html "PostgreSQL 9.6 - F.48. unaccent
— a text search dictionary which removes diacritics") /
[9.5](/docs/9.5/unaccent.html "PostgreSQL 9.5 - F.48. unaccent — a text search
dictionary which removes diacritics") / [9.4](/docs/9.4/unaccent.html
"PostgreSQL 9.4 - F.48. unaccent — a text search dictionary which removes
diacritics") / [9.3](/docs/9.3/unaccent.html "PostgreSQL 9.3 - F.48. unaccent
— a text search dictionary which removes diacritics") /
[9.2](/docs/9.2/unaccent.html "PostgreSQL 9.2 - F.48. unaccent — a text search
dictionary which removes diacritics") / [9.1](/docs/9.1/unaccent.html
"PostgreSQL 9.1 - F.48. unaccent — a text search dictionary which removes
diacritics") / [9.0](/docs/9.0/unaccent.html "PostgreSQL 9.0 - F.48. unaccent
— a text search dictionary which removes diacritics")

__

F.48. unaccent — a text search dictionary which removes diacritics  
---  
[Prev](tsm-system-time.html "F.47. tsm_system_time —  the SYSTEM_TIME sampling method for TABLESAMPLE")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](uuid-ossp.html "F.49. uuid-ossp — a UUID generator")  
  
* * *

## F.48. unaccent — a text search dictionary which removes diacritics #

[F.48.1. Configuration](unaccent.html#UNACCENT-CONFIGURATION)

[F.48.2. Usage](unaccent.html#UNACCENT-USAGE)

[F.48.3. Functions](unaccent.html#UNACCENT-FUNCTIONS)

`unaccent` is a text search dictionary that removes accents (diacritic signs)
from lexemes. It's a filtering dictionary, which means its output is always
passed to the next dictionary (if any), unlike the normal behavior of
dictionaries. This allows accent-insensitive processing for full text search.

The current implementation of `unaccent` cannot be used as a normalizing
dictionary for the `thesaurus` dictionary.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.48.1. Configuration #

An `unaccent` dictionary accepts the following options:

  * `RULES` is the base name of the file containing the list of translation rules. This file must be stored in `$SHAREDIR/tsearch_data/` (where `$SHAREDIR` means the PostgreSQL installation's shared-data directory). Its name must end in `.rules` (which is not to be included in the `RULES` parameter).

The rules file has the following format:

  * Each line represents one translation rule, consisting of a character with accent followed by a character without accent. The first is translated into the second. For example,
        
        À        A
        Á        A
        Â        A
        Ã        A
        Ä        A
        Å        A
        Æ        AE
        

The two characters must be separated by whitespace, and any leading or
trailing whitespace on a line is ignored.

  * Alternatively, if only one character is given on a line, instances of that character are deleted; this is useful in languages where accents are represented by separate characters.

  * Actually, each “character” can be any string not containing whitespace, so `unaccent` dictionaries could be used for other sorts of substring substitutions besides diacritic removal.

  * As with other PostgreSQL text search configuration files, the rules file must be stored in UTF-8 encoding. The data is automatically translated into the current database's encoding when loaded. Any lines containing untranslatable characters are silently ignored, so that rules files can contain rules that are not applicable in the current encoding.

A more complete example, which is directly useful for most European languages,
can be found in `unaccent.rules`, which is installed in
`$SHAREDIR/tsearch_data/` when the `unaccent` module is installed. This rules
file translates characters with accents to the same characters without
accents, and it also expands ligatures into the equivalent series of simple
characters (for example, Æ to AE).

### F.48.2. Usage #

Installing the `unaccent` extension creates a text search template `unaccent`
and a dictionary `unaccent` based on it. The `unaccent` dictionary has the
default parameter setting `RULES='unaccent'`, which makes it immediately
usable with the standard `unaccent.rules` file. If you wish, you can alter the
parameter, for example

    
    
    mydb=# ALTER TEXT SEARCH DICTIONARY unaccent (RULES='my_rules');
    

or create new dictionaries based on the template.

To test the dictionary, you can try:

    
    
    mydb=# select ts_lexize('unaccent','Hôtel');
     ts_lexize
    -----------
     {Hotel}
    (1 row)
    

Here is an example showing how to insert the `unaccent` dictionary into a text
search configuration:

    
    
    mydb=# CREATE TEXT SEARCH CONFIGURATION fr ( COPY = french );
    mydb=# ALTER TEXT SEARCH CONFIGURATION fr
            ALTER MAPPING FOR hword, hword_part, word
            WITH unaccent, french_stem;
    mydb=# select to_tsvector('fr','Hôtels de la Mer');
        to_tsvector
    -------------------
     'hotel':1 'mer':4
    (1 row)
    
    mydb=# select to_tsvector('fr','Hôtel de la Mer') @@ to_tsquery('fr','Hotels');
     ?column?
    ----------
     t
    (1 row)
    
    mydb=# select ts_headline('fr','Hôtel de la Mer',to_tsquery('fr','Hotels'));
          ts_headline
    ------------------------
     <b>Hôtel</b> de la Mer
    (1 row)
    

### F.48.3. Functions #

The `unaccent()` function removes accents (diacritic signs) from a given
string. Basically, it's a wrapper around `unaccent`-type dictionaries, but it
can be used outside normal text search contexts.

    
    
    unaccent([_dictionary_ regdictionary, ] _string_ text) returns text
    

If the _`dictionary`_ argument is omitted, the text search dictionary named
`unaccent` and appearing in the same schema as the `unaccent()` function
itself is used.

For example:

    
    
    SELECT unaccent('unaccent', 'Hôtel');
    SELECT unaccent('Hôtel');
    

* * *

[Prev](tsm-system-time.html "F.47. tsm_system_time —  the SYSTEM_TIME sampling method for TABLESAMPLE")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](uuid-ossp.html "F.49. uuid-ossp — a UUID generator")  
---|---|---  
F.47. tsm_system_time — the `SYSTEM_TIME` sampling method for `TABLESAMPLE`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.49. uuid-ossp — a UUID generator  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/unaccent.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

