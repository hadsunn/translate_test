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

Supported Versions: [Current](/docs/current/textsearch-parsers.html
"PostgreSQL 17 - 12.5. Parsers") ([17](/docs/17/textsearch-parsers.html
"PostgreSQL 17 - 12.5. Parsers")) / [16](/docs/16/textsearch-parsers.html
"PostgreSQL 16 - 12.5. Parsers") / [15](/docs/15/textsearch-parsers.html
"PostgreSQL 15 - 12.5. Parsers") / [14](/docs/14/textsearch-parsers.html
"PostgreSQL 14 - 12.5. Parsers") / [13](/docs/13/textsearch-parsers.html
"PostgreSQL 13 - 12.5. Parsers")

Development Versions: [18](/docs/18/textsearch-parsers.html "PostgreSQL 18 -
12.5. Parsers") / [devel](/docs/devel/textsearch-parsers.html "PostgreSQL
devel - 12.5. Parsers")

Unsupported versions: [12](/docs/12/textsearch-parsers.html "PostgreSQL 12 -
12.5. Parsers") / [11](/docs/11/textsearch-parsers.html "PostgreSQL 11 -
12.5. Parsers") / [10](/docs/10/textsearch-parsers.html "PostgreSQL 10 -
12.5. Parsers") / [9.6](/docs/9.6/textsearch-parsers.html "PostgreSQL 9.6 -
12.5. Parsers") / [9.5](/docs/9.5/textsearch-parsers.html "PostgreSQL 9.5 -
12.5. Parsers") / [9.4](/docs/9.4/textsearch-parsers.html "PostgreSQL 9.4 -
12.5. Parsers") / [9.3](/docs/9.3/textsearch-parsers.html "PostgreSQL 9.3 -
12.5. Parsers") / [9.2](/docs/9.2/textsearch-parsers.html "PostgreSQL 9.2 -
12.5. Parsers") / [9.1](/docs/9.1/textsearch-parsers.html "PostgreSQL 9.1 -
12.5. Parsers") / [9.0](/docs/9.0/textsearch-parsers.html "PostgreSQL 9.0 -
12.5. Parsers") / [8.4](/docs/8.4/textsearch-parsers.html "PostgreSQL 8.4 -
12.5. Parsers") / [8.3](/docs/8.3/textsearch-parsers.html "PostgreSQL 8.3 -
12.5. Parsers")

__

12.5. Parsers  
---  
[Prev](textsearch-features.html "12.4. Additional Features")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-dictionaries.html "12.6. Dictionaries")  
  
* * *

## 12.5. Parsers #

Text search parsers are responsible for splitting raw document text into
_tokens_ and identifying each token's type, where the set of possible types is
defined by the parser itself. Note that a parser does not modify the text at
all — it simply identifies plausible word boundaries. Because of this limited
scope, there is less need for application-specific custom parsers than there
is for custom dictionaries. At present PostgreSQL provides just one built-in
parser, which has been found to be useful for a wide range of applications.

The built-in parser is named `pg_catalog.default`. It recognizes 23 token
types, shown in [Table 12.1](textsearch-parsers.html#TEXTSEARCH-DEFAULT-PARSER
"Table 12.1. Default Parser's Token Types").

**Table  12.1. Default Parser's Token Types**

Alias | Description | Example  
---|---|---  
`asciiword` | Word, all ASCII letters | `elephant`  
`word` | Word, all letters | `mañana`  
`numword` | Word, letters and digits | `beta1`  
`asciihword` | Hyphenated word, all ASCII | `up-to-date`  
`hword` | Hyphenated word, all letters | `lógico-matemática`  
`numhword` | Hyphenated word, letters and digits | `postgresql-beta1`  
`hword_asciipart` | Hyphenated word part, all ASCII | `postgresql` in the context `postgresql-beta1`  
`hword_part` | Hyphenated word part, all letters | `lógico` or `matemática` in the context `lógico-matemática`  
`hword_numpart` | Hyphenated word part, letters and digits | `beta1` in the context `postgresql-beta1`  
`email` | Email address | `foo@example.com`  
`protocol` | Protocol head | `http://`  
`url` | URL | `example.com/stuff/index.html`  
`host` | Host | `example.com`  
`url_path` | URL path | `/stuff/index.html`, in the context of a URL  
`file` | File or path name | `/usr/local/foo.txt`, if not within a URL  
`sfloat` | Scientific notation | `-1.234e56`  
`float` | Decimal notation | `-1.234`  
`int` | Signed integer | `-1234`  
`uint` | Unsigned integer | `1234`  
`version` | Version number | `8.3.0`  
`tag` | XML tag | `<a href="dictionaries.html">`  
`entity` | XML entity | `&amp;`  
`blank` | Space symbols | (any whitespace or punctuation not otherwise recognized)  
  
  

### Note

The parser's notion of a “letter” is determined by the database's locale
setting, specifically `lc_ctype`. Words containing only the basic ASCII
letters are reported as a separate token type, since it is sometimes useful to
distinguish them. In most European languages, token types `word` and
`asciiword` should be treated alike.

`email` does not support all valid email characters as defined by [RFC
5322](https://datatracker.ietf.org/doc/html/rfc5322). Specifically, the only
non-alphanumeric characters supported for email user names are period, dash,
and underscore.

`tag` does not support all valid tag names as defined by [W3C Recommendation,
XML](https://www.w3.org/TR/xml/). Specifically, the only tag names supported
are those starting with an ASCII letter, underscore, or colon, and containing
only letters, digits, hyphens, underscores, periods, and colons. `tag` also
includes XML comments starting with `<!--` and ending with `-->`, and XML
declarations (but note that this includes anything starting with `<?x` and
ending with `>`).

It is possible for the parser to produce overlapping tokens from the same
piece of text. As an example, a hyphenated word will be reported both as the
entire word and as each component:

    
    
    SELECT alias, description, token FROM ts_debug('foo-bar-beta1');
          alias      |               description                |     token
    -----------------+------------------------------------------+---------------
     numhword        | Hyphenated word, letters and digits      | foo-bar-beta1
     hword_asciipart | Hyphenated word part, all ASCII          | foo
     blank           | Space symbols                            | -
     hword_asciipart | Hyphenated word part, all ASCII          | bar
     blank           | Space symbols                            | -
     hword_numpart   | Hyphenated word part, letters and digits | beta1
    

This behavior is desirable since it allows searches to work for both the whole
compound word and for components. Here is another instructive example:

    
    
    SELECT alias, description, token FROM ts_debug('http://example.com/stuff/index.html');
      alias   |  description  |            token
    ----------+---------------+------------------------------
     protocol | Protocol head | http://
     url      | URL           | example.com/stuff/index.html
     host     | Host          | example.com
     url_path | URL path      | /stuff/index.html
    

* * *

[Prev](textsearch-features.html "12.4. Additional Features")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-dictionaries.html "12.6. Dictionaries")  
---|---|---  
12.4. Additional Features  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.6. Dictionaries  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-parsers.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

