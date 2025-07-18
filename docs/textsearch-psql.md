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

Supported Versions: [Current](/docs/current/textsearch-psql.html "PostgreSQL
17 - 12.10. psql Support") ([17](/docs/17/textsearch-psql.html "PostgreSQL 17
- 12.10. psql Support")) / [16](/docs/16/textsearch-psql.html "PostgreSQL 16 -
12.10. psql Support") / [15](/docs/15/textsearch-psql.html "PostgreSQL 15 -
12.10. psql Support") / [14](/docs/14/textsearch-psql.html "PostgreSQL 14 -
12.10. psql Support") / [13](/docs/13/textsearch-psql.html "PostgreSQL 13 -
12.10. psql Support")

Development Versions: [18](/docs/18/textsearch-psql.html "PostgreSQL 18 -
12.10. psql Support") / [devel](/docs/devel/textsearch-psql.html "PostgreSQL
devel - 12.10. psql Support")

Unsupported versions: [12](/docs/12/textsearch-psql.html "PostgreSQL 12 -
12.10. psql Support") / [11](/docs/11/textsearch-psql.html "PostgreSQL 11 -
12.10. psql Support") / [10](/docs/10/textsearch-psql.html "PostgreSQL 10 -
12.10. psql Support") / [9.6](/docs/9.6/textsearch-psql.html "PostgreSQL 9.6 -
12.10. psql Support") / [9.5](/docs/9.5/textsearch-psql.html "PostgreSQL 9.5 -
12.10. psql Support") / [9.4](/docs/9.4/textsearch-psql.html "PostgreSQL 9.4 -
12.10. psql Support") / [9.3](/docs/9.3/textsearch-psql.html "PostgreSQL 9.3 -
12.10. psql Support") / [9.2](/docs/9.2/textsearch-psql.html "PostgreSQL 9.2 -
12.10. psql Support") / [9.1](/docs/9.1/textsearch-psql.html "PostgreSQL 9.1 -
12.10. psql Support") / [9.0](/docs/9.0/textsearch-psql.html "PostgreSQL 9.0 -
12.10. psql Support") / [8.4](/docs/8.4/textsearch-psql.html "PostgreSQL 8.4 -
12.10. psql Support") / [8.3](/docs/8.3/textsearch-psql.html "PostgreSQL 8.3 -
12.10. psql Support")

__

12.10. psql Support  
---  
[Prev](textsearch-indexes.html "12.9. Preferred Index Types for Text Search")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-limitations.html "12.11. Limitations")  
  
* * *

## 12.10. psql Support #

Information about text search configuration objects can be obtained in psql
using a set of commands:

    
    
    \dF{d,p,t}[+] [PATTERN]
    

An optional `+` produces more details.

The optional parameter _`PATTERN`_ can be the name of a text search object,
optionally schema-qualified. If _`PATTERN`_ is omitted then information about
all visible objects will be displayed. _`PATTERN`_ can be a regular expression
and can provide _separate_ patterns for the schema and object names. The
following examples illustrate this:

    
    
    => \dF *fulltext*
           List of text search configurations
     Schema |  Name        | Description
    --------+--------------+-------------
     public | fulltext_cfg |
    
    
    
    => \dF *.fulltext*
           List of text search configurations
     Schema   |  Name        | Description
    ----------+----------------------------
     fulltext | fulltext_cfg |
     public   | fulltext_cfg |
    

The available commands are:

`\dF[+] [PATTERN]`

    

List text search configurations (add `+` for more detail).

    
    
    => \dF russian
                List of text search configurations
       Schema   |  Name   |            Description
    ------------+---------+------------------------------------
     pg_catalog | russian | configuration for russian language
    
    => \dF+ russian
    Text search configuration "pg_catalog.russian"
    Parser: "pg_catalog.default"
          Token      | Dictionaries
    -----------------+--------------
     asciihword      | english_stem
     asciiword       | english_stem
     email           | simple
     file            | simple
     float           | simple
     host            | simple
     hword           | russian_stem
     hword_asciipart | english_stem
     hword_numpart   | simple
     hword_part      | russian_stem
     int             | simple
     numhword        | simple
     numword         | simple
     sfloat          | simple
     uint            | simple
     url             | simple
     url_path        | simple
     version         | simple
     word            | russian_stem
    

`\dFd[+] [PATTERN]`

    

List text search dictionaries (add `+` for more detail).

    
    
    => \dFd
                                 List of text search dictionaries
       Schema   |      Name       |                        Description
    ------------+-----------------+-----------------------------------------------------------
     pg_catalog | arabic_stem     | snowball stemmer for arabic language
     pg_catalog | armenian_stem   | snowball stemmer for armenian language
     pg_catalog | basque_stem     | snowball stemmer for basque language
     pg_catalog | catalan_stem    | snowball stemmer for catalan language
     pg_catalog | danish_stem     | snowball stemmer for danish language
     pg_catalog | dutch_stem      | snowball stemmer for dutch language
     pg_catalog | english_stem    | snowball stemmer for english language
     pg_catalog | finnish_stem    | snowball stemmer for finnish language
     pg_catalog | french_stem     | snowball stemmer for french language
     pg_catalog | german_stem     | snowball stemmer for german language
     pg_catalog | greek_stem      | snowball stemmer for greek language
     pg_catalog | hindi_stem      | snowball stemmer for hindi language
     pg_catalog | hungarian_stem  | snowball stemmer for hungarian language
     pg_catalog | indonesian_stem | snowball stemmer for indonesian language
     pg_catalog | irish_stem      | snowball stemmer for irish language
     pg_catalog | italian_stem    | snowball stemmer for italian language
     pg_catalog | lithuanian_stem | snowball stemmer for lithuanian language
     pg_catalog | nepali_stem     | snowball stemmer for nepali language
     pg_catalog | norwegian_stem  | snowball stemmer for norwegian language
     pg_catalog | portuguese_stem | snowball stemmer for portuguese language
     pg_catalog | romanian_stem   | snowball stemmer for romanian language
     pg_catalog | russian_stem    | snowball stemmer for russian language
     pg_catalog | serbian_stem    | snowball stemmer for serbian language
     pg_catalog | simple          | simple dictionary: just lower case and check for stopword
     pg_catalog | spanish_stem    | snowball stemmer for spanish language
     pg_catalog | swedish_stem    | snowball stemmer for swedish language
     pg_catalog | tamil_stem      | snowball stemmer for tamil language
     pg_catalog | turkish_stem    | snowball stemmer for turkish language
     pg_catalog | yiddish_stem    | snowball stemmer for yiddish language
    

`\dFp[+] [PATTERN]`

    

List text search parsers (add `+` for more detail).

    
    
    => \dFp
            List of text search parsers
       Schema   |  Name   |     Description
    ------------+---------+---------------------
     pg_catalog | default | default word parser
    => \dFp+
        Text search parser "pg_catalog.default"
         Method      |    Function    | Description
    -----------------+----------------+-------------
     Start parse     | prsd_start     |
     Get next token  | prsd_nexttoken |
     End parse       | prsd_end       |
     Get headline    | prsd_headline  |
     Get token types | prsd_lextype   |
    
            Token types for parser "pg_catalog.default"
       Token name    |               Description
    -----------------+------------------------------------------
     asciihword      | Hyphenated word, all ASCII
     asciiword       | Word, all ASCII
     blank           | Space symbols
     email           | Email address
     entity          | XML entity
     file            | File or path name
     float           | Decimal notation
     host            | Host
     hword           | Hyphenated word, all letters
     hword_asciipart | Hyphenated word part, all ASCII
     hword_numpart   | Hyphenated word part, letters and digits
     hword_part      | Hyphenated word part, all letters
     int             | Signed integer
     numhword        | Hyphenated word, letters and digits
     numword         | Word, letters and digits
     protocol        | Protocol head
     sfloat          | Scientific notation
     tag             | XML tag
     uint            | Unsigned integer
     url             | URL
     url_path        | URL path
     version         | Version number
     word            | Word, all letters
    (23 rows)
    

`\dFt[+] [PATTERN]`

    

List text search templates (add `+` for more detail).

    
    
    => \dFt
                               List of text search templates
       Schema   |   Name    |                        Description
    ------------+-----------+-----------------------------------------------------------
     pg_catalog | ispell    | ispell dictionary
     pg_catalog | simple    | simple dictionary: just lower case and check for stopword
     pg_catalog | snowball  | snowball stemmer
     pg_catalog | synonym   | synonym dictionary: replace word by its synonym
     pg_catalog | thesaurus | thesaurus dictionary: phrase by phrase substitution
    

* * *

[Prev](textsearch-indexes.html "12.9. Preferred Index Types for Text Search")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-limitations.html "12.11. Limitations")  
---|---|---  
12.9. Preferred Index Types for Text Search  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.11. Limitations  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-psql.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

