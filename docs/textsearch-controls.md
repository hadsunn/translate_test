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

Supported Versions: [Current](/docs/current/textsearch-controls.html
"PostgreSQL 17 - 12.3. Controlling Text Search") ([17](/docs/17/textsearch-
controls.html "PostgreSQL 17 - 12.3. Controlling Text Search")) /
[16](/docs/16/textsearch-controls.html "PostgreSQL 16 - 12.3. Controlling Text
Search") / [15](/docs/15/textsearch-controls.html "PostgreSQL 15 -
12.3. Controlling Text Search") / [14](/docs/14/textsearch-controls.html
"PostgreSQL 14 - 12.3. Controlling Text Search") / [13](/docs/13/textsearch-
controls.html "PostgreSQL 13 - 12.3. Controlling Text Search")

Development Versions: [18](/docs/18/textsearch-controls.html "PostgreSQL 18 -
12.3. Controlling Text Search") / [devel](/docs/devel/textsearch-controls.html
"PostgreSQL devel - 12.3. Controlling Text Search")

Unsupported versions: [12](/docs/12/textsearch-controls.html "PostgreSQL 12 -
12.3. Controlling Text Search") / [11](/docs/11/textsearch-controls.html
"PostgreSQL 11 - 12.3. Controlling Text Search") / [10](/docs/10/textsearch-
controls.html "PostgreSQL 10 - 12.3. Controlling Text Search") /
[9.6](/docs/9.6/textsearch-controls.html "PostgreSQL 9.6 - 12.3. Controlling
Text Search") / [9.5](/docs/9.5/textsearch-controls.html "PostgreSQL 9.5 -
12.3. Controlling Text Search") / [9.4](/docs/9.4/textsearch-controls.html
"PostgreSQL 9.4 - 12.3. Controlling Text Search") /
[9.3](/docs/9.3/textsearch-controls.html "PostgreSQL 9.3 - 12.3. Controlling
Text Search") / [9.2](/docs/9.2/textsearch-controls.html "PostgreSQL 9.2 -
12.3. Controlling Text Search") / [9.1](/docs/9.1/textsearch-controls.html
"PostgreSQL 9.1 - 12.3. Controlling Text Search") /
[9.0](/docs/9.0/textsearch-controls.html "PostgreSQL 9.0 - 12.3. Controlling
Text Search") / [8.4](/docs/8.4/textsearch-controls.html "PostgreSQL 8.4 -
12.3. Controlling Text Search") / [8.3](/docs/8.3/textsearch-controls.html
"PostgreSQL 8.3 - 12.3. Controlling Text Search")

__

12.3. Controlling Text Search  
---  
[Prev](textsearch-tables.html "12.2. Tables and Indexes")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-features.html "12.4. Additional Features")  
  
* * *

## 12.3. Controlling Text Search #

[12.3.1. Parsing Documents](textsearch-controls.html#TEXTSEARCH-PARSING-
DOCUMENTS)

[12.3.2. Parsing Queries](textsearch-controls.html#TEXTSEARCH-PARSING-QUERIES)

[12.3.3. Ranking Search Results](textsearch-controls.html#TEXTSEARCH-RANKING)

[12.3.4. Highlighting Results](textsearch-controls.html#TEXTSEARCH-HEADLINE)

To implement full text searching there must be a function to create a
`tsvector` from a document and a `tsquery` from a user query. Also, we need to
return results in a useful order, so we need a function that compares
documents with respect to their relevance to the query. It's also important to
be able to display the results nicely. PostgreSQL provides support for all of
these functions.

### 12.3.1. Parsing Documents #

PostgreSQL provides the function `to_tsvector` for converting a document to
the `tsvector` data type.

    
    
    to_tsvector([ _config_ regconfig, ] _document_ text) returns tsvector
    

`to_tsvector` parses a textual document into tokens, reduces the tokens to
lexemes, and returns a `tsvector` which lists the lexemes together with their
positions in the document. The document is processed according to the
specified or default text search configuration. Here is a simple example:

    
    
    SELECT to_tsvector('english', 'a fat  cat sat on a mat - it ate a fat rats');
                      to_tsvector
    -----------------------------------------------------
     'ate':9 'cat':3 'fat':2,11 'mat':7 'rat':12 'sat':4
    

In the example above we see that the resulting `tsvector` does not contain the
words `a`, `on`, or `it`, the word `rats` became `rat`, and the punctuation
sign `-` was ignored.

The `to_tsvector` function internally calls a parser which breaks the document
text into tokens and assigns a type to each token. For each token, a list of
dictionaries ([Section 12.6](textsearch-dictionaries.html
"12.6. Dictionaries")) is consulted, where the list can vary depending on the
token type. The first dictionary that _recognizes_ the token emits one or more
normalized _lexemes_ to represent the token. For example, `rats` became `rat`
because one of the dictionaries recognized that the word `rats` is a plural
form of `rat`. Some words are recognized as _stop words_ ([Section
12.6.1](textsearch-dictionaries.html#TEXTSEARCH-STOPWORDS "12.6.1. Stop
Words")), which causes them to be ignored since they occur too frequently to
be useful in searching. In our example these are `a`, `on`, and `it`. If no
dictionary in the list recognizes the token then it is also ignored. In this
example that happened to the punctuation sign `-` because there are in fact no
dictionaries assigned for its token type (`Space symbols`), meaning space
tokens will never be indexed. The choices of parser, dictionaries and which
types of tokens to index are determined by the selected text search
configuration ([Section 12.7](textsearch-configuration.html
"12.7. Configuration Example")). It is possible to have many different
configurations in the same database, and predefined configurations are
available for various languages. In our example we used the default
configuration `english` for the English language.

The function `setweight` can be used to label the entries of a `tsvector` with
a given _weight_ , where a weight is one of the letters `A`, `B`, `C`, or `D`.
This is typically used to mark entries coming from different parts of a
document, such as title versus body. Later, this information can be used for
ranking of search results.

Because `to_tsvector`(`NULL`) will return `NULL`, it is recommended to use
`coalesce` whenever a field might be null. Here is the recommended method for
creating a `tsvector` from a structured document:

    
    
    UPDATE tt SET ti =
        setweight(to_tsvector(coalesce(title,'')), 'A')    ||
        setweight(to_tsvector(coalesce(keyword,'')), 'B')  ||
        setweight(to_tsvector(coalesce(abstract,'')), 'C') ||
        setweight(to_tsvector(coalesce(body,'')), 'D');
    

Here we have used `setweight` to label the source of each lexeme in the
finished `tsvector`, and then merged the labeled `tsvector` values using the
`tsvector` concatenation operator `||`. ([Section 12.4.1](textsearch-
features.html#TEXTSEARCH-MANIPULATE-TSVECTOR "12.4.1. Manipulating Documents")
gives details about these operations.)

### 12.3.2. Parsing Queries #

PostgreSQL provides the functions `to_tsquery`, `plainto_tsquery`,
`phraseto_tsquery` and `websearch_to_tsquery` for converting a query to the
`tsquery` data type. `to_tsquery` offers access to more features than either
`plainto_tsquery` or `phraseto_tsquery`, but it is less forgiving about its
input. `websearch_to_tsquery` is a simplified version of `to_tsquery` with an
alternative syntax, similar to the one used by web search engines.

    
    
    to_tsquery([ _config_ regconfig, ] _querytext_ text) returns tsquery
    

`to_tsquery` creates a `tsquery` value from _`querytext`_ , which must consist
of single tokens separated by the `tsquery` operators `&` (AND), `|` (OR), `!`
(NOT), and `<->` (FOLLOWED BY), possibly grouped using parentheses. In other
words, the input to `to_tsquery` must already follow the general rules for
`tsquery` input, as described in [Section 8.11.2](datatype-
textsearch.html#DATATYPE-TSQUERY "8.11.2. tsquery"). The difference is that
while basic `tsquery` input takes the tokens at face value, `to_tsquery`
normalizes each token into a lexeme using the specified or default
configuration, and discards any tokens that are stop words according to the
configuration. For example:

    
    
    SELECT to_tsquery('english', 'The & Fat & Rats');
      to_tsquery
    ---------------
     'fat' & 'rat'
    

As in basic `tsquery` input, weight(s) can be attached to each lexeme to
restrict it to match only `tsvector` lexemes of those weight(s). For example:

    
    
    SELECT to_tsquery('english', 'Fat | Rats:AB');
        to_tsquery
    ------------------
     'fat' | 'rat':AB
    

Also, `*` can be attached to a lexeme to specify prefix matching:

    
    
    SELECT to_tsquery('supern:*A & star:A*B');
            to_tsquery
    --------------------------
     'supern':*A & 'star':*AB
    

Such a lexeme will match any word in a `tsvector` that begins with the given
string.

`to_tsquery` can also accept single-quoted phrases. This is primarily useful
when the configuration includes a thesaurus dictionary that may trigger on
such phrases. In the example below, a thesaurus contains the rule `supernovae
stars : sn`:

    
    
    SELECT to_tsquery('''supernovae stars'' & !crab');
      to_tsquery
    ---------------
     'sn' & !'crab'
    

Without quotes, `to_tsquery` will generate a syntax error for tokens that are
not separated by an AND, OR, or FOLLOWED BY operator.

    
    
    plainto_tsquery([ _config_ regconfig, ] _querytext_ text) returns tsquery
    

`plainto_tsquery` transforms the unformatted text _`querytext`_ to a `tsquery`
value. The text is parsed and normalized much as for `to_tsvector`, then the
`&` (AND) `tsquery` operator is inserted between surviving words.

Example:

    
    
    SELECT plainto_tsquery('english', 'The Fat Rats');
     plainto_tsquery
    -----------------
     'fat' & 'rat'
    

Note that `plainto_tsquery` will not recognize `tsquery` operators, weight
labels, or prefix-match labels in its input:

    
    
    SELECT plainto_tsquery('english', 'The Fat & Rats:C');
       plainto_tsquery
    ---------------------
     'fat' & 'rat' & 'c'
    

Here, all the input punctuation was discarded.

    
    
    phraseto_tsquery([ _config_ regconfig, ] _querytext_ text) returns tsquery
    

`phraseto_tsquery` behaves much like `plainto_tsquery`, except that it inserts
the `<->` (FOLLOWED BY) operator between surviving words instead of the `&`
(AND) operator. Also, stop words are not simply discarded, but are accounted
for by inserting `<_`N`_ >` operators rather than `<->` operators. This
function is useful when searching for exact lexeme sequences, since the
FOLLOWED BY operators check lexeme order not just the presence of all the
lexemes.

Example:

    
    
    SELECT phraseto_tsquery('english', 'The Fat Rats');
     phraseto_tsquery
    ------------------
     'fat' <-> 'rat'
    

Like `plainto_tsquery`, the `phraseto_tsquery` function will not recognize
`tsquery` operators, weight labels, or prefix-match labels in its input:

    
    
    SELECT phraseto_tsquery('english', 'The Fat & Rats:C');
          phraseto_tsquery
    -----------------------------
     'fat' <-> 'rat' <-> 'c'
    
    
    
    websearch_to_tsquery([ _config_ regconfig, ] _querytext_ text) returns tsquery
    

`websearch_to_tsquery` creates a `tsquery` value from _`querytext`_ using an
alternative syntax in which simple unformatted text is a valid query. Unlike
`plainto_tsquery` and `phraseto_tsquery`, it also recognizes certain
operators. Moreover, this function will never raise syntax errors, which makes
it possible to use raw user-supplied input for search. The following syntax is
supported:

  * `unquoted text`: text not inside quote marks will be converted to terms separated by `&` operators, as if processed by `plainto_tsquery`.

  * `"quoted text"`: text inside quote marks will be converted to terms separated by `<->` operators, as if processed by `phraseto_tsquery`.

  * `OR`: the word “or” will be converted to the `|` operator.

  * `-`: a dash will be converted to the `!` operator.

Other punctuation is ignored. So like `plainto_tsquery` and
`phraseto_tsquery`, the `websearch_to_tsquery` function will not recognize
`tsquery` operators, weight labels, or prefix-match labels in its input.

Examples:

    
    
    SELECT websearch_to_tsquery('english', 'The fat rats');
     websearch_to_tsquery
    ----------------------
     'fat' & 'rat'
    (1 row)
    
    SELECT websearch_to_tsquery('english', '"supernovae stars" -crab');
           websearch_to_tsquery
    ----------------------------------
     'supernova' <-> 'star' & !'crab'
    (1 row)
    
    SELECT websearch_to_tsquery('english', '"sad cat" or "fat rat"');
           websearch_to_tsquery
    -----------------------------------
     'sad' <-> 'cat' | 'fat' <-> 'rat'
    (1 row)
    
    SELECT websearch_to_tsquery('english', 'signal -"segmentation fault"');
             websearch_to_tsquery
    ---------------------------------------
     'signal' & !( 'segment' <-> 'fault' )
    (1 row)
    
    SELECT websearch_to_tsquery('english', '""" )( dummy \\ query <->');
     websearch_to_tsquery
    ----------------------
     'dummi' & 'queri'
    (1 row)
    

### 12.3.3. Ranking Search Results #

Ranking attempts to measure how relevant documents are to a particular query,
so that when there are many matches the most relevant ones can be shown first.
PostgreSQL provides two predefined ranking functions, which take into account
lexical, proximity, and structural information; that is, they consider how
often the query terms appear in the document, how close together the terms are
in the document, and how important is the part of the document where they
occur. However, the concept of relevancy is vague and very application-
specific. Different applications might require additional information for
ranking, e.g., document modification time. The built-in ranking functions are
only examples. You can write your own ranking functions and/or combine their
results with additional factors to fit your specific needs.

The two ranking functions currently available are:

`ts_rank([ _`weights`_ `float4[]`, ] _`vector`_ `tsvector`, _`query`_
`tsquery` [, _`normalization`_ `integer` ]) returns `float4``

    

Ranks vectors based on the frequency of their matching lexemes.

`ts_rank_cd([ _`weights`_ `float4[]`, ] _`vector`_ `tsvector`, _`query`_
`tsquery` [, _`normalization`_ `integer` ]) returns `float4``

    

This function computes the _cover density_ ranking for the given document
vector and query, as described in Clarke, Cormack, and Tudhope's "Relevance
Ranking for One to Three Term Queries" in the journal "Information Processing
and Management", 1999. Cover density is similar to `ts_rank` ranking except
that the proximity of matching lexemes to each other is taken into
consideration.

This function requires lexeme positional information to perform its
calculation. Therefore, it ignores any “stripped” lexemes in the `tsvector`.
If there are no unstripped lexemes in the input, the result will be zero. (See
[Section 12.4.1](textsearch-features.html#TEXTSEARCH-MANIPULATE-TSVECTOR
"12.4.1. Manipulating Documents") for more information about the `strip`
function and positional information in `tsvector`s.)

For both these functions, the optional _`weights`_ argument offers the ability
to weigh word instances more or less heavily depending on how they are
labeled. The weight arrays specify how heavily to weigh each category of word,
in the order:

    
    
    {D-weight, C-weight, B-weight, A-weight}
    

If no _`weights`_ are provided, then these defaults are used:

    
    
    {0.1, 0.2, 0.4, 1.0}
    

Typically weights are used to mark words from special areas of the document,
like the title or an initial abstract, so they can be treated with more or
less importance than words in the document body.

Since a longer document has a greater chance of containing a query term it is
reasonable to take into account document size, e.g., a hundred-word document
with five instances of a search word is probably more relevant than a
thousand-word document with five instances. Both ranking functions take an
integer _`normalization`_ option that specifies whether and how a document's
length should impact its rank. The integer option controls several behaviors,
so it is a bit mask: you can specify one or more behaviors using `|` (for
example, `2|4`).

  * 0 (the default) ignores the document length

  * 1 divides the rank by 1 + the logarithm of the document length

  * 2 divides the rank by the document length

  * 4 divides the rank by the mean harmonic distance between extents (this is implemented only by `ts_rank_cd`)

  * 8 divides the rank by the number of unique words in document

  * 16 divides the rank by 1 + the logarithm of the number of unique words in document

  * 32 divides the rank by itself + 1

If more than one flag bit is specified, the transformations are applied in the
order listed.

It is important to note that the ranking functions do not use any global
information, so it is impossible to produce a fair normalization to 1% or 100%
as sometimes desired. Normalization option 32 (`rank/(rank+1)`) can be applied
to scale all ranks into the range zero to one, but of course this is just a
cosmetic change; it will not affect the ordering of the search results.

Here is an example that selects only the ten highest-ranked matches:

    
    
    SELECT title, ts_rank_cd(textsearch, query) AS rank
    FROM apod, to_tsquery('neutrino|(dark & matter)') query
    WHERE query @@ textsearch
    ORDER BY rank DESC
    LIMIT 10;
                         title                     |   rank
    -----------------------------------------------+----------
     Neutrinos in the Sun                          |      3.1
     The Sudbury Neutrino Detector                 |      2.4
     A MACHO View of Galactic Dark Matter          |  2.01317
     Hot Gas and Dark Matter                       |  1.91171
     The Virgo Cluster: Hot Plasma and Dark Matter |  1.90953
     Rafting for Solar Neutrinos                   |      1.9
     NGC 4650A: Strange Galaxy and Dark Matter     |  1.85774
     Hot Gas and Dark Matter                       |   1.6123
     Ice Fishing for Cosmic Neutrinos              |      1.6
     Weak Lensing Distorts the Universe            | 0.818218
    

This is the same example using normalized ranking:

    
    
    SELECT title, ts_rank_cd(textsearch, query, 32 /* rank/(rank+1) */ ) AS rank
    FROM apod, to_tsquery('neutrino|(dark & matter)') query
    WHERE  query @@ textsearch
    ORDER BY rank DESC
    LIMIT 10;
                         title                     |        rank
    -----------------------------------------------+-------------------
     Neutrinos in the Sun                          | 0.756097569485493
     The Sudbury Neutrino Detector                 | 0.705882361190954
     A MACHO View of Galactic Dark Matter          | 0.668123210574724
     Hot Gas and Dark Matter                       |  0.65655958650282
     The Virgo Cluster: Hot Plasma and Dark Matter | 0.656301290640973
     Rafting for Solar Neutrinos                   | 0.655172410958162
     NGC 4650A: Strange Galaxy and Dark Matter     | 0.650072921219637
     Hot Gas and Dark Matter                       | 0.617195790024749
     Ice Fishing for Cosmic Neutrinos              | 0.615384618911517
     Weak Lensing Distorts the Universe            | 0.450010798361481
    

Ranking can be expensive since it requires consulting the `tsvector` of each
matching document, which can be I/O bound and therefore slow. Unfortunately,
it is almost impossible to avoid since practical queries often result in large
numbers of matches.

### 12.3.4. Highlighting Results #

To present search results it is ideal to show a part of each document and how
it is related to the query. Usually, search engines show fragments of the
document with marked search terms. PostgreSQL provides a function
`ts_headline` that implements this functionality.

    
    
    ts_headline([ _config_ regconfig, ] _document_ text, _query_ tsquery [, _options_ text ]) returns text
    

`ts_headline` accepts a document along with a query, and returns an excerpt
from the document in which terms from the query are highlighted. Specifically,
the function will use the query to select relevant text fragments, and then
highlight all words that appear in the query, even if those word positions do
not match the query's restrictions. The configuration to be used to parse the
document can be specified by _`config`_ ; if _`config`_ is omitted, the
`default_text_search_config` configuration is used.

If an _`options`_ string is specified it must consist of a comma-separated
list of one or more _`option`_`=`_`value`_ pairs. The available options are:

  * `MaxWords`, `MinWords` (integers): these numbers determine the longest and shortest headlines to output. The default values are 35 and 15.

  * `ShortWord` (integer): words of this length or less will be dropped at the start and end of a headline, unless they are query terms. The default value of three eliminates common English articles.

  * `HighlightAll` (boolean): if `true` the whole document will be used as the headline, ignoring the preceding three parameters. The default is `false`.

  * `MaxFragments` (integer): maximum number of text fragments to display. The default value of zero selects a non-fragment-based headline generation method. A value greater than zero selects fragment-based headline generation (see below).

  * `StartSel`, `StopSel` (strings): the strings with which to delimit query words appearing in the document, to distinguish them from other excerpted words. The default values are “`<b>`” and “`</b>`”, which can be suitable for HTML output (but see the warning below).

  * `FragmentDelimiter` (string): When more than one fragment is displayed, the fragments will be separated by this string. The default is “ `...` ”.

### Warning: Cross-site scripting (XSS) safety

The output from `ts_headline` is not guaranteed to be safe for direct
inclusion in web pages. When `HighlightAll` is `false` (the default), some
simple XML tags are removed from the document, but this is not guaranteed to
remove all HTML markup. Therefore, this does not provide an effective defense
against attacks such as cross-site scripting (XSS) attacks, when working with
untrusted input. To guard against such attacks, all HTML markup should be
removed from the input document, or an HTML sanitizer should be used on the
output.

These option names are recognized case-insensitively. You must double-quote
string values if they contain spaces or commas.

In non-fragment-based headline generation, `ts_headline` locates matches for
the given _`query`_ and chooses a single one to display, preferring matches
that have more query words within the allowed headline length. In fragment-
based headline generation, `ts_headline` locates the query matches and splits
each match into “fragments” of no more than `MaxWords` words each, preferring
fragments with more query words, and when possible “stretching” fragments to
include surrounding words. The fragment-based mode is thus more useful when
the query matches span large sections of the document, or when it's desirable
to display multiple matches. In either mode, if no query matches can be
identified, then a single fragment of the first `MinWords` words in the
document will be displayed.

For example:

    
    
    SELECT ts_headline('english',
      'The most common type of search
    is to find all documents containing given query terms
    and return them in order of their similarity to the
    query.',
      to_tsquery('english', 'query & similarity'));
                            ts_headline
    ------------------------------------------------------------
     containing given <b>query</b> terms                       +
     and return them in order of their <b>similarity</b> to the+
     <b>query</b>.
    
    SELECT ts_headline('english',
      'Search terms may occur
    many times in a document,
    requiring ranking of the search matches to decide which
    occurrences to display in the result.',
      to_tsquery('english', 'search & term'),
      'MaxFragments=10, MaxWords=7, MinWords=3, StartSel=<<, StopSel=>>');
                            ts_headline
    ------------------------------------------------------------
     <<Search>> <<terms>> may occur                            +
     many times ... ranking of the <<search>> matches to decide
    

`ts_headline` uses the original document, not a `tsvector` summary, so it can
be slow and should be used with care.

* * *

[Prev](textsearch-tables.html "12.2. Tables and Indexes")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-features.html "12.4. Additional Features")  
---|---|---  
12.2. Tables and Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.4. Additional Features  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-controls.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

