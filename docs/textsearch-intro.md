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

Supported Versions: [Current](/docs/current/textsearch-intro.html "PostgreSQL
17 - 12.1. Introduction") ([17](/docs/17/textsearch-intro.html "PostgreSQL 17
- 12.1. Introduction")) / [16](/docs/16/textsearch-intro.html "PostgreSQL 16 -
12.1. Introduction") / [15](/docs/15/textsearch-intro.html "PostgreSQL 15 -
12.1. Introduction") / [14](/docs/14/textsearch-intro.html "PostgreSQL 14 -
12.1. Introduction") / [13](/docs/13/textsearch-intro.html "PostgreSQL 13 -
12.1. Introduction")

Development Versions: [18](/docs/18/textsearch-intro.html "PostgreSQL 18 -
12.1. Introduction") / [devel](/docs/devel/textsearch-intro.html "PostgreSQL
devel - 12.1. Introduction")

Unsupported versions: [12](/docs/12/textsearch-intro.html "PostgreSQL 12 -
12.1. Introduction") / [11](/docs/11/textsearch-intro.html "PostgreSQL 11 -
12.1. Introduction") / [10](/docs/10/textsearch-intro.html "PostgreSQL 10 -
12.1. Introduction") / [9.6](/docs/9.6/textsearch-intro.html "PostgreSQL 9.6 -
12.1. Introduction") / [9.5](/docs/9.5/textsearch-intro.html "PostgreSQL 9.5 -
12.1. Introduction") / [9.4](/docs/9.4/textsearch-intro.html "PostgreSQL 9.4 -
12.1. Introduction") / [9.3](/docs/9.3/textsearch-intro.html "PostgreSQL 9.3 -
12.1. Introduction") / [9.2](/docs/9.2/textsearch-intro.html "PostgreSQL 9.2 -
12.1. Introduction") / [9.1](/docs/9.1/textsearch-intro.html "PostgreSQL 9.1 -
12.1. Introduction") / [9.0](/docs/9.0/textsearch-intro.html "PostgreSQL 9.0 -
12.1. Introduction") / [8.4](/docs/8.4/textsearch-intro.html "PostgreSQL 8.4 -
12.1. Introduction") / [8.3](/docs/8.3/textsearch-intro.html "PostgreSQL 8.3 -
12.1. Introduction")

__

12.1. Introduction  
---  
[Prev](textsearch.html "Chapter 12. Full Text Search")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-tables.html "12.2. Tables and Indexes")  
  
* * *

## 12.1. Introduction #

[12.1.1. What Is a Document?](textsearch-intro.html#TEXTSEARCH-DOCUMENT)

[12.1.2. Basic Text Matching](textsearch-intro.html#TEXTSEARCH-MATCHING)

[12.1.3. Configurations](textsearch-intro.html#TEXTSEARCH-INTRO-
CONFIGURATIONS)

Full Text Searching (or just _text search_) provides the capability to
identify natural-language _documents_ that satisfy a _query_ , and optionally
to sort them by relevance to the query. The most common type of search is to
find all documents containing given _query terms_ and return them in order of
their _similarity_ to the query. Notions of `query` and `similarity` are very
flexible and depend on the specific application. The simplest search considers
`query` as a set of words and `similarity` as the frequency of query words in
the document.

Textual search operators have existed in databases for years. PostgreSQL has
`~`, `~*`, `LIKE`, and `ILIKE` operators for textual data types, but they lack
many essential properties required by modern information systems:

  * There is no linguistic support, even for English. Regular expressions are not sufficient because they cannot easily handle derived words, e.g., `satisfies` and `satisfy`. You might miss documents that contain `satisfies`, although you probably would like to find them when searching for `satisfy`. It is possible to use `OR` to search for multiple derived forms, but this is tedious and error-prone (some words can have several thousand derivatives).

  * They provide no ordering (ranking) of search results, which makes them ineffective when thousands of matching documents are found.

  * They tend to be slow because there is no index support, so they must process all documents for every search.

Full text indexing allows documents to be _preprocessed_ and an index saved
for later rapid searching. Preprocessing includes:

  * _Parsing documents into _tokens__. It is useful to identify various classes of tokens, e.g., numbers, words, complex words, email addresses, so that they can be processed differently. In principle token classes depend on the specific application, but for most purposes it is adequate to use a predefined set of classes. PostgreSQL uses a _parser_ to perform this step. A standard parser is provided, and custom parsers can be created for specific needs.

  * _Converting tokens into _lexemes__. A lexeme is a string, just like a token, but it has been _normalized_ so that different forms of the same word are made alike. For example, normalization almost always includes folding upper-case letters to lower-case, and often involves removal of suffixes (such as `s` or `es` in English). This allows searches to find variant forms of the same word, without tediously entering all the possible variants. Also, this step typically eliminates _stop words_ , which are words that are so common that they are useless for searching. (In short, then, tokens are raw fragments of the document text, while lexemes are words that are believed useful for indexing and searching.) PostgreSQL uses _dictionaries_ to perform this step. Various standard dictionaries are provided, and custom ones can be created for specific needs.

  * _Storing preprocessed documents optimized for searching_. For example, each document can be represented as a sorted array of normalized lexemes. Along with the lexemes it is often desirable to store positional information to use for _proximity ranking_ , so that a document that contains a more “dense” region of query words is assigned a higher rank than one with scattered query words.

Dictionaries allow fine-grained control over how tokens are normalized. With
appropriate dictionaries, you can:

  * Define stop words that should not be indexed.

  * Map synonyms to a single word using Ispell.

  * Map phrases to a single word using a thesaurus.

  * Map different variations of a word to a canonical form using an Ispell dictionary.

  * Map different variations of a word to a canonical form using Snowball stemmer rules.

A data type `tsvector` is provided for storing preprocessed documents, along
with a type `tsquery` for representing processed queries ([Section
8.11](datatype-textsearch.html "8.11. Text Search Types")). There are many
functions and operators available for these data types ([Section
9.13](functions-textsearch.html "9.13. Text Search Functions and Operators")),
the most important of which is the match operator `@@`, which we introduce in
[Section 12.1.2](textsearch-intro.html#TEXTSEARCH-MATCHING "12.1.2. Basic Text
Matching"). Full text searches can be accelerated using indexes ([Section
12.9](textsearch-indexes.html "12.9. Preferred Index Types for Text Search")).

### 12.1.1. What Is a Document? #

A _document_ is the unit of searching in a full text search system; for
example, a magazine article or email message. The text search engine must be
able to parse documents and store associations of lexemes (key words) with
their parent document. Later, these associations are used to search for
documents that contain query words.

For searches within PostgreSQL, a document is normally a textual field within
a row of a database table, or possibly a combination (concatenation) of such
fields, perhaps stored in several tables or obtained dynamically. In other
words, a document can be constructed from different parts for indexing and it
might not be stored anywhere as a whole. For example:

    
    
    SELECT title || ' ' ||  author || ' ' ||  abstract || ' ' || body AS document
    FROM messages
    WHERE mid = 12;
    
    SELECT m.title || ' ' || m.author || ' ' || m.abstract || ' ' || d.body AS document
    FROM messages m, docs d
    WHERE m.mid = d.did AND m.mid = 12;
    

### Note

Actually, in these example queries, `coalesce` should be used to prevent a
single `NULL` attribute from causing a `NULL` result for the whole document.

Another possibility is to store the documents as simple text files in the file
system. In this case, the database can be used to store the full text index
and to execute searches, and some unique identifier can be used to retrieve
the document from the file system. However, retrieving files from outside the
database requires superuser permissions or special function support, so this
is usually less convenient than keeping all the data inside PostgreSQL. Also,
keeping everything inside the database allows easy access to document metadata
to assist in indexing and display.

For text search purposes, each document must be reduced to the preprocessed
`tsvector` format. Searching and ranking are performed entirely on the
`tsvector` representation of a document — the original text need only be
retrieved when the document has been selected for display to a user. We
therefore often speak of the `tsvector` as being the document, but of course
it is only a compact representation of the full document.

### 12.1.2. Basic Text Matching #

Full text searching in PostgreSQL is based on the match operator `@@`, which
returns `true` if a `tsvector` (document) matches a `tsquery` (query). It
doesn't matter which data type is written first:

    
    
    SELECT 'a fat cat sat on a mat and ate a fat rat'::tsvector @@ 'cat & rat'::tsquery;
     ?column?
    ----------
     t
    
    SELECT 'fat & cow'::tsquery @@ 'a fat cat sat on a mat and ate a fat rat'::tsvector;
     ?column?
    ----------
     f
    

As the above example suggests, a `tsquery` is not just raw text, any more than
a `tsvector` is. A `tsquery` contains search terms, which must be already-
normalized lexemes, and may combine multiple terms using AND, OR, NOT, and
FOLLOWED BY operators. (For syntax details see [Section 8.11.2](datatype-
textsearch.html#DATATYPE-TSQUERY "8.11.2. tsquery").) There are functions
`to_tsquery`, `plainto_tsquery`, and `phraseto_tsquery` that are helpful in
converting user-written text into a proper `tsquery`, primarily by normalizing
words appearing in the text. Similarly, `to_tsvector` is used to parse and
normalize a document string. So in practice a text search match would look
more like this:

    
    
    SELECT to_tsvector('fat cats ate fat rats') @@ to_tsquery('fat & rat');
     ?column?
    ----------
     t
    

Observe that this match would not succeed if written as

    
    
    SELECT 'fat cats ate fat rats'::tsvector @@ to_tsquery('fat & rat');
     ?column?
    ----------
     f
    

since here no normalization of the word `rats` will occur. The elements of a
`tsvector` are lexemes, which are assumed already normalized, so `rats` does
not match `rat`.

The `@@` operator also supports `text` input, allowing explicit conversion of
a text string to `tsvector` or `tsquery` to be skipped in simple cases. The
variants available are:

    
    
    tsvector @@ tsquery
    tsquery  @@ tsvector
    text @@ tsquery
    text @@ text
    

The first two of these we saw already. The form `text` `@@` `tsquery` is
equivalent to `to_tsvector(x) @@ y`. The form `text` `@@` `text` is equivalent
to `to_tsvector(x) @@ plainto_tsquery(y)`.

Within a `tsquery`, the `&` (AND) operator specifies that both its arguments
must appear in the document to have a match. Similarly, the `|` (OR) operator
specifies that at least one of its arguments must appear, while the `!` (NOT)
operator specifies that its argument must _not_ appear in order to have a
match. For example, the query `fat & ! rat` matches documents that contain
`fat` but not `rat`.

Searching for phrases is possible with the help of the `<->` (FOLLOWED BY)
`tsquery` operator, which matches only if its arguments have matches that are
adjacent and in the given order. For example:

    
    
    SELECT to_tsvector('fatal error') @@ to_tsquery('fatal <-> error');
     ?column?
    ----------
     t
    
    SELECT to_tsvector('error is not fatal') @@ to_tsquery('fatal <-> error');
     ?column?
    ----------
     f
    

There is a more general version of the FOLLOWED BY operator having the form
`<_`N`_ >`, where _`N`_ is an integer standing for the difference between the
positions of the matching lexemes. `<1>` is the same as `<->`, while `<2>`
allows exactly one other lexeme to appear between the matches, and so on. The
`phraseto_tsquery` function makes use of this operator to construct a
`tsquery` that can match a multi-word phrase when some of the words are stop
words. For example:

    
    
    SELECT phraseto_tsquery('cats ate rats');
           phraseto_tsquery
    -------------------------------
     'cat' <-> 'ate' <-> 'rat'
    
    SELECT phraseto_tsquery('the cats ate the rats');
           phraseto_tsquery
    -------------------------------
     'cat' <-> 'ate' <2> 'rat'
    

A special case that's sometimes useful is that `<0>` can be used to require
that two patterns match the same word.

Parentheses can be used to control nesting of the `tsquery` operators. Without
parentheses, `|` binds least tightly, then `&`, then `<->`, and `!` most
tightly.

It's worth noticing that the AND/OR/NOT operators mean something subtly
different when they are within the arguments of a FOLLOWED BY operator than
when they are not, because within FOLLOWED BY the exact position of the match
is significant. For example, normally `!x` matches only documents that do not
contain `x` anywhere. But `!x <-> y` matches `y` if it is not immediately
after an `x`; an occurrence of `x` elsewhere in the document does not prevent
a match. Another example is that `x & y` normally only requires that `x` and
`y` both appear somewhere in the document, but `(x & y) <-> z` requires `x`
and `y` to match at the same place, immediately before a `z`. Thus this query
behaves differently from `x <-> z & y <-> z`, which will match a document
containing two separate sequences `x z` and `y z`. (This specific query is
useless as written, since `x` and `y` could not match at the same place; but
with more complex situations such as prefix-match patterns, a query of this
form could be useful.)

### 12.1.3. Configurations #

The above are all simple text search examples. As mentioned before, full text
search functionality includes the ability to do many more things: skip
indexing certain words (stop words), process synonyms, and use sophisticated
parsing, e.g., parse based on more than just white space. This functionality
is controlled by _text search configurations_. PostgreSQL comes with
predefined configurations for many languages, and you can easily create your
own configurations. (psql's `\dF` command shows all available configurations.)

During installation an appropriate configuration is selected and
[default_text_search_config](runtime-config-client.html#GUC-DEFAULT-TEXT-
SEARCH-CONFIG) is set accordingly in `postgresql.conf`. If you are using the
same text search configuration for the entire cluster you can use the value in
`postgresql.conf`. To use different configurations throughout the cluster but
the same configuration within any one database, use `ALTER DATABASE ... SET`.
Otherwise, you can set `default_text_search_config` in each session.

Each text search function that depends on a configuration has an optional
`regconfig` argument, so that the configuration to use can be specified
explicitly. `default_text_search_config` is used only when this argument is
omitted.

To make it easier to build custom text search configurations, a configuration
is built up from simpler database objects. PostgreSQL's text search facility
provides four types of configuration-related database objects:

  * _Text search parsers_ break documents into tokens and classify each token (for example, as words or numbers).

  * _Text search dictionaries_ convert tokens to normalized form and reject stop words.

  * _Text search templates_ provide the functions underlying dictionaries. (A dictionary simply specifies a template and a set of parameters for the template.)

  * _Text search configurations_ select a parser and a set of dictionaries to use to normalize the tokens produced by the parser.

Text search parsers and templates are built from low-level C functions;
therefore it requires C programming ability to develop new ones, and superuser
privileges to install one into a database. (There are examples of add-on
parsers and templates in the `contrib/` area of the PostgreSQL distribution.)
Since dictionaries and configurations just parameterize and connect together
some underlying parsers and templates, no special privilege is needed to
create a new dictionary or configuration. Examples of creating custom
dictionaries and configurations appear later in this chapter.

* * *

[Prev](textsearch.html "Chapter 12. Full Text Search")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-tables.html "12.2. Tables and Indexes")  
---|---|---  
Chapter 12. Full Text Search  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.2. Tables and Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-intro.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

