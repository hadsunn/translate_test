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

Supported Versions: [Current](/docs/current/textsearch-dictionaries.html
"PostgreSQL 17 - 12.6. Dictionaries") ([17](/docs/17/textsearch-
dictionaries.html "PostgreSQL 17 - 12.6. Dictionaries")) /
[16](/docs/16/textsearch-dictionaries.html "PostgreSQL 16 -
12.6. Dictionaries") / [15](/docs/15/textsearch-dictionaries.html "PostgreSQL
15 - 12.6. Dictionaries") / [14](/docs/14/textsearch-dictionaries.html
"PostgreSQL 14 - 12.6. Dictionaries") / [13](/docs/13/textsearch-
dictionaries.html "PostgreSQL 13 - 12.6. Dictionaries")

Development Versions: [18](/docs/18/textsearch-dictionaries.html "PostgreSQL
18 - 12.6. Dictionaries") / [devel](/docs/devel/textsearch-dictionaries.html
"PostgreSQL devel - 12.6. Dictionaries")

Unsupported versions: [12](/docs/12/textsearch-dictionaries.html "PostgreSQL
12 - 12.6. Dictionaries") / [11](/docs/11/textsearch-dictionaries.html
"PostgreSQL 11 - 12.6. Dictionaries") / [10](/docs/10/textsearch-
dictionaries.html "PostgreSQL 10 - 12.6. Dictionaries") /
[9.6](/docs/9.6/textsearch-dictionaries.html "PostgreSQL 9.6 -
12.6. Dictionaries") / [9.5](/docs/9.5/textsearch-dictionaries.html
"PostgreSQL 9.5 - 12.6. Dictionaries") / [9.4](/docs/9.4/textsearch-
dictionaries.html "PostgreSQL 9.4 - 12.6. Dictionaries") /
[9.3](/docs/9.3/textsearch-dictionaries.html "PostgreSQL 9.3 -
12.6. Dictionaries") / [9.2](/docs/9.2/textsearch-dictionaries.html
"PostgreSQL 9.2 - 12.6. Dictionaries") / [9.1](/docs/9.1/textsearch-
dictionaries.html "PostgreSQL 9.1 - 12.6. Dictionaries") /
[9.0](/docs/9.0/textsearch-dictionaries.html "PostgreSQL 9.0 -
12.6. Dictionaries") / [8.4](/docs/8.4/textsearch-dictionaries.html
"PostgreSQL 8.4 - 12.6. Dictionaries") / [8.3](/docs/8.3/textsearch-
dictionaries.html "PostgreSQL 8.3 - 12.6. Dictionaries")

__

12.6. Dictionaries  
---  
[Prev](textsearch-parsers.html "12.5. Parsers")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-configuration.html "12.7. Configuration Example")  
  
* * *

## 12.6. Dictionaries #

[12.6.1. Stop Words](textsearch-dictionaries.html#TEXTSEARCH-STOPWORDS)

[12.6.2. Simple Dictionary](textsearch-dictionaries.html#TEXTSEARCH-SIMPLE-
DICTIONARY)

[12.6.3. Synonym Dictionary](textsearch-dictionaries.html#TEXTSEARCH-SYNONYM-
DICTIONARY)

[12.6.4. Thesaurus Dictionary](textsearch-dictionaries.html#TEXTSEARCH-
THESAURUS)

[12.6.5. Ispell Dictionary](textsearch-dictionaries.html#TEXTSEARCH-ISPELL-
DICTIONARY)

[12.6.6. Snowball Dictionary](textsearch-dictionaries.html#TEXTSEARCH-
SNOWBALL-DICTIONARY)

Dictionaries are used to eliminate words that should not be considered in a
search (_stop words_), and to _normalize_ words so that different derived
forms of the same word will match. A successfully normalized word is called a
_lexeme_. Aside from improving search quality, normalization and removal of
stop words reduce the size of the `tsvector` representation of a document,
thereby improving performance. Normalization does not always have linguistic
meaning and usually depends on application semantics.

Some examples of normalization:

  * Linguistic — Ispell dictionaries try to reduce input words to a normalized form; stemmer dictionaries remove word endings

  * URL locations can be canonicalized to make equivalent URLs match:

    * http://www.pgsql.ru/db/mw/index.html

    * http://www.pgsql.ru/db/mw/

    * http://www.pgsql.ru/db/../db/mw/index.html

  * Color names can be replaced by their hexadecimal values, e.g., `red, green, blue, magenta -> FF0000, 00FF00, 0000FF, FF00FF`

  * If indexing numbers, we can remove some fractional digits to reduce the range of possible numbers, so for example _3.14_ 159265359, _3.14_ 15926, _3.14_ will be the same after normalization if only two digits are kept after the decimal point.

A dictionary is a program that accepts a token as input and returns:

  * an array of lexemes if the input token is known to the dictionary (notice that one token can produce more than one lexeme)

  * a single lexeme with the `TSL_FILTER` flag set, to replace the original token with a new token to be passed to subsequent dictionaries (a dictionary that does this is called a _filtering dictionary_)

  * an empty array if the dictionary knows the token, but it is a stop word

  * `NULL` if the dictionary does not recognize the input token

PostgreSQL provides predefined dictionaries for many languages. There are also
several predefined templates that can be used to create new dictionaries with
custom parameters. Each predefined dictionary template is described below. If
no existing template is suitable, it is possible to create new ones; see the
`contrib/` area of the PostgreSQL distribution for examples.

A text search configuration binds a parser together with a set of dictionaries
to process the parser's output tokens. For each token type that the parser can
return, a separate list of dictionaries is specified by the configuration.
When a token of that type is found by the parser, each dictionary in the list
is consulted in turn, until some dictionary recognizes it as a known word. If
it is identified as a stop word, or if no dictionary recognizes the token, it
will be discarded and not indexed or searched for. Normally, the first
dictionary that returns a non-`NULL` output determines the result, and any
remaining dictionaries are not consulted; but a filtering dictionary can
replace the given word with a modified word, which is then passed to
subsequent dictionaries.

The general rule for configuring a list of dictionaries is to place first the
most narrow, most specific dictionary, then the more general dictionaries,
finishing with a very general dictionary, like a Snowball stemmer or `simple`,
which recognizes everything. For example, for an astronomy-specific search
(`astro_en` configuration) one could bind token type `asciiword` (ASCII word)
to a synonym dictionary of astronomical terms, a general English dictionary
and a Snowball English stemmer:

    
    
    ALTER TEXT SEARCH CONFIGURATION astro_en
        ADD MAPPING FOR asciiword WITH astrosyn, english_ispell, english_stem;
    

A filtering dictionary can be placed anywhere in the list, except at the end
where it'd be useless. Filtering dictionaries are useful to partially
normalize words to simplify the task of later dictionaries. For example, a
filtering dictionary could be used to remove accents from accented letters, as
is done by the [unaccent](unaccent.html "F.48. unaccent — a text search
dictionary which removes diacritics") module.

### 12.6.1. Stop Words #

Stop words are words that are very common, appear in almost every document,
and have no discrimination value. Therefore, they can be ignored in the
context of full text searching. For example, every English text contains words
like `a` and `the`, so it is useless to store them in an index. However, stop
words do affect the positions in `tsvector`, which in turn affect ranking:

    
    
    SELECT to_tsvector('english', 'in the list of stop words');
            to_tsvector
    ----------------------------
     'list':3 'stop':5 'word':6
    

The missing positions 1,2,4 are because of stop words. Ranks calculated for
documents with and without stop words are quite different:

    
    
    SELECT ts_rank_cd (to_tsvector('english', 'in the list of stop words'), to_tsquery('list & stop'));
     ts_rank_cd
    ------------
           0.05
    
    SELECT ts_rank_cd (to_tsvector('english', 'list stop words'), to_tsquery('list & stop'));
     ts_rank_cd
    ------------
            0.1
    

It is up to the specific dictionary how it treats stop words. For example,
`ispell` dictionaries first normalize words and then look at the list of stop
words, while `Snowball` stemmers first check the list of stop words. The
reason for the different behavior is an attempt to decrease noise.

### 12.6.2. Simple Dictionary #

The `simple` dictionary template operates by converting the input token to
lower case and checking it against a file of stop words. If it is found in the
file then an empty array is returned, causing the token to be discarded. If
not, the lower-cased form of the word is returned as the normalized lexeme.
Alternatively, the dictionary can be configured to report non-stop-words as
unrecognized, allowing them to be passed on to the next dictionary in the
list.

Here is an example of a dictionary definition using the `simple` template:

    
    
    CREATE TEXT SEARCH DICTIONARY public.simple_dict (
        TEMPLATE = pg_catalog.simple,
        STOPWORDS = english
    );
    

Here, `english` is the base name of a file of stop words. The file's full name
will be `$SHAREDIR/tsearch_data/english.stop`, where `$SHAREDIR` means the
PostgreSQL installation's shared-data directory, often
`/usr/local/share/postgresql` (use `pg_config --sharedir` to determine it if
you're not sure). The file format is simply a list of words, one per line.
Blank lines and trailing spaces are ignored, and upper case is folded to lower
case, but no other processing is done on the file contents.

Now we can test our dictionary:

    
    
    SELECT ts_lexize('public.simple_dict', 'YeS');
     ts_lexize
    -----------
     {yes}
    
    SELECT ts_lexize('public.simple_dict', 'The');
     ts_lexize
    -----------
     {}
    

We can also choose to return `NULL`, instead of the lower-cased word, if it is
not found in the stop words file. This behavior is selected by setting the
dictionary's `Accept` parameter to `false`. Continuing the example:

    
    
    ALTER TEXT SEARCH DICTIONARY public.simple_dict ( Accept = false );
    
    SELECT ts_lexize('public.simple_dict', 'YeS');
     ts_lexize
    -----------
    
    
    SELECT ts_lexize('public.simple_dict', 'The');
     ts_lexize
    -----------
     {}
    

With the default setting of `Accept` = `true`, it is only useful to place a
`simple` dictionary at the end of a list of dictionaries, since it will never
pass on any token to a following dictionary. Conversely, `Accept` = `false` is
only useful when there is at least one following dictionary.

### Caution

Most types of dictionaries rely on configuration files, such as files of stop
words. These files _must_ be stored in UTF-8 encoding. They will be translated
to the actual database encoding, if that is different, when they are read into
the server.

### Caution

Normally, a database session will read a dictionary configuration file only
once, when it is first used within the session. If you modify a configuration
file and want to force existing sessions to pick up the new contents, issue an
`ALTER TEXT SEARCH DICTIONARY` command on the dictionary. This can be a
“dummy” update that doesn't actually change any parameter values.

### 12.6.3. Synonym Dictionary #

This dictionary template is used to create dictionaries that replace a word
with a synonym. Phrases are not supported (use the thesaurus template
([Section 12.6.4](textsearch-dictionaries.html#TEXTSEARCH-THESAURUS
"12.6.4. Thesaurus Dictionary")) for that). A synonym dictionary can be used
to overcome linguistic problems, for example, to prevent an English stemmer
dictionary from reducing the word “Paris” to “pari”. It is enough to have a
`Paris paris` line in the synonym dictionary and put it before the
`english_stem` dictionary. For example:

    
    
    SELECT * FROM ts_debug('english', 'Paris');
       alias   |   description   | token |  dictionaries  |  dictionary  | lexemes
    -----------+-----------------+-------+----------------+--------------+---------
     asciiword | Word, all ASCII | Paris | {english_stem} | english_stem | {pari}
    
    CREATE TEXT SEARCH DICTIONARY my_synonym (
        TEMPLATE = synonym,
        SYNONYMS = my_synonyms
    );
    
    ALTER TEXT SEARCH CONFIGURATION english
        ALTER MAPPING FOR asciiword
        WITH my_synonym, english_stem;
    
    SELECT * FROM ts_debug('english', 'Paris');
       alias   |   description   | token |       dictionaries        | dictionary | lexemes
    -----------+-----------------+-------+---------------------------+------------+---------
     asciiword | Word, all ASCII | Paris | {my_synonym,english_stem} | my_synonym | {paris}
    

The only parameter required by the `synonym` template is `SYNONYMS`, which is
the base name of its configuration file — `my_synonyms` in the above example.
The file's full name will be `$SHAREDIR/tsearch_data/my_synonyms.syn` (where
`$SHAREDIR` means the PostgreSQL installation's shared-data directory). The
file format is just one line per word to be substituted, with the word
followed by its synonym, separated by white space. Blank lines and trailing
spaces are ignored.

The `synonym` template also has an optional parameter `CaseSensitive`, which
defaults to `false`. When `CaseSensitive` is `false`, words in the synonym
file are folded to lower case, as are input tokens. When it is `true`, words
and tokens are not folded to lower case, but are compared as-is.

An asterisk (`*`) can be placed at the end of a synonym in the configuration
file. This indicates that the synonym is a prefix. The asterisk is ignored
when the entry is used in `to_tsvector()`, but when it is used in
`to_tsquery()`, the result will be a query item with the prefix match marker
(see [Section 12.3.2](textsearch-controls.html#TEXTSEARCH-PARSING-QUERIES
"12.3.2. Parsing Queries")). For example, suppose we have these entries in
`$SHAREDIR/tsearch_data/synonym_sample.syn`:

    
    
    postgres        pgsql
    postgresql      pgsql
    postgre pgsql
    gogle   googl
    indices index*
    

Then we will get these results:

    
    
    mydb=# CREATE TEXT SEARCH DICTIONARY syn (template=synonym, synonyms='synonym_sample');
    mydb=# SELECT ts_lexize('syn', 'indices');
     ts_lexize
    -----------
     {index}
    (1 row)
    
    mydb=# CREATE TEXT SEARCH CONFIGURATION tst (copy=simple);
    mydb=# ALTER TEXT SEARCH CONFIGURATION tst ALTER MAPPING FOR asciiword WITH syn;
    mydb=# SELECT to_tsvector('tst', 'indices');
     to_tsvector
    -------------
     'index':1
    (1 row)
    
    mydb=# SELECT to_tsquery('tst', 'indices');
     to_tsquery
    ------------
     'index':*
    (1 row)
    
    mydb=# SELECT 'indexes are very useful'::tsvector;
                tsvector
    ---------------------------------
     'are' 'indexes' 'useful' 'very'
    (1 row)
    
    mydb=# SELECT 'indexes are very useful'::tsvector @@ to_tsquery('tst', 'indices');
     ?column?
    ----------
     t
    (1 row)
    

### 12.6.4. Thesaurus Dictionary #

A thesaurus dictionary (sometimes abbreviated as TZ) is a collection of words
that includes information about the relationships of words and phrases, i.e.,
broader terms (BT), narrower terms (NT), preferred terms, non-preferred terms,
related terms, etc.

Basically a thesaurus dictionary replaces all non-preferred terms by one
preferred term and, optionally, preserves the original terms for indexing as
well. PostgreSQL's current implementation of the thesaurus dictionary is an
extension of the synonym dictionary with added _phrase_ support. A thesaurus
dictionary requires a configuration file of the following format:

    
    
    # this is a comment
    sample word(s) : indexed word(s)
    more sample word(s) : more indexed word(s)
    ...
    

where the colon (`:`) symbol acts as a delimiter between a phrase and its
replacement.

A thesaurus dictionary uses a _subdictionary_ (which is specified in the
dictionary's configuration) to normalize the input text before checking for
phrase matches. It is only possible to select one subdictionary. An error is
reported if the subdictionary fails to recognize a word. In that case, you
should remove the use of the word or teach the subdictionary about it. You can
place an asterisk (`*`) at the beginning of an indexed word to skip applying
the subdictionary to it, but all sample words _must_ be known to the
subdictionary.

The thesaurus dictionary chooses the longest match if there are multiple
phrases matching the input, and ties are broken by using the last definition.

Specific stop words recognized by the subdictionary cannot be specified;
instead use `?` to mark the location where any stop word can appear. For
example, assuming that `a` and `the` are stop words according to the
subdictionary:

    
    
    ? one ? two : swsw
    

matches `a one the two` and `the one a two`; both would be replaced by `swsw`.

Since a thesaurus dictionary has the capability to recognize phrases it must
remember its state and interact with the parser. A thesaurus dictionary uses
these assignments to check if it should handle the next word or stop
accumulation. The thesaurus dictionary must be configured carefully. For
example, if the thesaurus dictionary is assigned to handle only the
`asciiword` token, then a thesaurus dictionary definition like `one 7` will
not work since token type `uint` is not assigned to the thesaurus dictionary.

### Caution

Thesauruses are used during indexing so any change in the thesaurus
dictionary's parameters _requires_ reindexing. For most other dictionary
types, small changes such as adding or removing stopwords does not force
reindexing.

#### 12.6.4.1. Thesaurus Configuration #

To define a new thesaurus dictionary, use the `thesaurus` template. For
example:

    
    
    CREATE TEXT SEARCH DICTIONARY thesaurus_simple (
        TEMPLATE = thesaurus,
        DictFile = mythesaurus,
        Dictionary = pg_catalog.english_stem
    );
    

Here:

  * `thesaurus_simple` is the new dictionary's name

  * `mythesaurus` is the base name of the thesaurus configuration file. (Its full name will be `$SHAREDIR/tsearch_data/mythesaurus.ths`, where `$SHAREDIR` means the installation shared-data directory.)

  * `pg_catalog.english_stem` is the subdictionary (here, a Snowball English stemmer) to use for thesaurus normalization. Notice that the subdictionary will have its own configuration (for example, stop words), which is not shown here.

Now it is possible to bind the thesaurus dictionary `thesaurus_simple` to the
desired token types in a configuration, for example:

    
    
    ALTER TEXT SEARCH CONFIGURATION russian
        ALTER MAPPING FOR asciiword, asciihword, hword_asciipart
        WITH thesaurus_simple;
    

#### 12.6.4.2. Thesaurus Example #

Consider a simple astronomical thesaurus `thesaurus_astro`, which contains
some astronomical word combinations:

    
    
    supernovae stars : sn
    crab nebulae : crab
    

Below we create a dictionary and bind some token types to an astronomical
thesaurus and English stemmer:

    
    
    CREATE TEXT SEARCH DICTIONARY thesaurus_astro (
        TEMPLATE = thesaurus,
        DictFile = thesaurus_astro,
        Dictionary = english_stem
    );
    
    ALTER TEXT SEARCH CONFIGURATION russian
        ALTER MAPPING FOR asciiword, asciihword, hword_asciipart
        WITH thesaurus_astro, english_stem;
    

Now we can see how it works. `ts_lexize` is not very useful for testing a
thesaurus, because it treats its input as a single token. Instead we can use
`plainto_tsquery` and `to_tsvector` which will break their input strings into
multiple tokens:

    
    
    SELECT plainto_tsquery('supernova star');
     plainto_tsquery
    -----------------
     'sn'
    
    SELECT to_tsvector('supernova star');
     to_tsvector
    -------------
     'sn':1
    

In principle, one can use `to_tsquery` if you quote the argument:

    
    
    SELECT to_tsquery('''supernova star''');
     to_tsquery
    ------------
     'sn'
    

Notice that `supernova star` matches `supernovae stars` in `thesaurus_astro`
because we specified the `english_stem` stemmer in the thesaurus definition.
The stemmer removed the `e` and `s`.

To index the original phrase as well as the substitute, just include it in the
right-hand part of the definition:

    
    
    supernovae stars : sn supernovae stars
    
    SELECT plainto_tsquery('supernova star');
           plainto_tsquery
    -----------------------------
     'sn' & 'supernova' & 'star'
    

### 12.6.5. Ispell Dictionary #

The Ispell dictionary template supports _morphological dictionaries_ , which
can normalize many different linguistic forms of a word into the same lexeme.
For example, an English Ispell dictionary can match all declensions and
conjugations of the search term `bank`, e.g., `banking`, `banked`, `banks`,
`banks'`, and `bank's`.

The standard PostgreSQL distribution does not include any Ispell configuration
files. Dictionaries for a large number of languages are available from
[Ispell](https://www.cs.hmc.edu/~geoff/ispell.html). Also, some more modern
dictionary file formats are supported —
[MySpell](https://en.wikipedia.org/wiki/MySpell) (OO < 2.0.1) and
[Hunspell](https://hunspell.github.io/) (OO >= 2.0.2). A large list of
dictionaries is available on the [OpenOffice
Wiki](https://wiki.openoffice.org/wiki/Dictionaries).

To create an Ispell dictionary perform these steps:

  * download dictionary configuration files. OpenOffice extension files have the `.oxt` extension. It is necessary to extract `.aff` and `.dic` files, change extensions to `.affix` and `.dict`. For some dictionary files it is also needed to convert characters to the UTF-8 encoding with commands (for example, for a Norwegian language dictionary):
        
        iconv -f ISO_8859-1 -t UTF-8 -o nn_no.affix nn_NO.aff
        iconv -f ISO_8859-1 -t UTF-8 -o nn_no.dict nn_NO.dic
        

  * copy files to the `$SHAREDIR/tsearch_data` directory

  * load files into PostgreSQL with the following command:
        
        CREATE TEXT SEARCH DICTIONARY english_hunspell (
            TEMPLATE = ispell,
            DictFile = en_us,
            AffFile = en_us,
            Stopwords = english);
        

Here, `DictFile`, `AffFile`, and `StopWords` specify the base names of the
dictionary, affixes, and stop-words files. The stop-words file has the same
format explained above for the `simple` dictionary type. The format of the
other files is not specified here but is available from the above-mentioned
web sites.

Ispell dictionaries usually recognize a limited set of words, so they should
be followed by another broader dictionary; for example, a Snowball dictionary,
which recognizes everything.

The `.affix` file of Ispell has the following structure:

    
    
    prefixes
    flag *A:
        .           >   RE      # As in enter > reenter
    suffixes
    flag T:
        E           >   ST      # As in late > latest
        [^AEIOU]Y   >   -Y,IEST # As in dirty > dirtiest
        [AEIOU]Y    >   EST     # As in gray > grayest
        [^EY]       >   EST     # As in small > smallest
    

And the `.dict` file has the following structure:

    
    
    lapse/ADGRS
    lard/DGRS
    large/PRTY
    lark/MRS
    

Format of the `.dict` file is:

    
    
    basic_form/affix_class_name
    

In the `.affix` file every affix flag is described in the following format:

    
    
    condition > [-stripping_letters,] adding_affix
    

Here, condition has a format similar to the format of regular expressions. It
can use groupings `[...]` and `[^...]`. For example, `[AEIOU]Y` means that the
last letter of the word is `"y"` and the penultimate letter is `"a"`, `"e"`,
`"i"`, `"o"` or `"u"`. `[^EY]` means that the last letter is neither `"e"` nor
`"y"`.

Ispell dictionaries support splitting compound words; a useful feature. Notice
that the affix file should specify a special flag using the `compoundwords
controlled` statement that marks dictionary words that can participate in
compound formation:

    
    
    compoundwords  controlled z
    

Here are some examples for the Norwegian language:

    
    
    SELECT ts_lexize('norwegian_ispell', 'overbuljongterningpakkmesterassistent');
       {over,buljong,terning,pakk,mester,assistent}
    SELECT ts_lexize('norwegian_ispell', 'sjokoladefabrikk');
       {sjokoladefabrikk,sjokolade,fabrikk}
    

MySpell format is a subset of Hunspell. The `.affix` file of Hunspell has the
following structure:

    
    
    PFX A Y 1
    PFX A   0     re         .
    SFX T N 4
    SFX T   0     st         e
    SFX T   y     iest       [^aeiou]y
    SFX T   0     est        [aeiou]y
    SFX T   0     est        [^ey]
    

The first line of an affix class is the header. Fields of an affix rules are
listed after the header:

  * parameter name (PFX or SFX)

  * flag (name of the affix class)

  * stripping characters from beginning (at prefix) or end (at suffix) of the word

  * adding affix

  * condition that has a format similar to the format of regular expressions.

The `.dict` file looks like the `.dict` file of Ispell:

    
    
    larder/M
    lardy/RT
    large/RSPMYT
    largehearted
    

### Note

MySpell does not support compound words. Hunspell has sophisticated support
for compound words. At present, PostgreSQL implements only the basic compound
word operations of Hunspell.

### 12.6.6. Snowball Dictionary #

The Snowball dictionary template is based on a project by Martin Porter,
inventor of the popular Porter's stemming algorithm for the English language.
Snowball now provides stemming algorithms for many languages (see the
[Snowball site](https://snowballstem.org/) for more information). Each
algorithm understands how to reduce common variant forms of words to a base,
or stem, spelling within its language. A Snowball dictionary requires a
`language` parameter to identify which stemmer to use, and optionally can
specify a `stopword` file name that gives a list of words to eliminate.
(PostgreSQL's standard stopword lists are also provided by the Snowball
project.) For example, there is a built-in definition equivalent to

    
    
    CREATE TEXT SEARCH DICTIONARY english_stem (
        TEMPLATE = snowball,
        Language = english,
        StopWords = english
    );
    

The stopword file format is the same as already explained.

A Snowball dictionary recognizes everything, whether or not it is able to
simplify the word, so it should be placed at the end of the dictionary list.
It is useless to have it before any other dictionary because a token will
never pass through it to the next dictionary.

* * *

[Prev](textsearch-parsers.html "12.5. Parsers")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-configuration.html "12.7. Configuration Example")  
---|---|---  
12.5. Parsers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.7. Configuration Example  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-dictionaries.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

