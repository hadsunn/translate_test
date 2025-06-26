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

Supported Versions: [Current](/docs/current/textsearch-configuration.html
"PostgreSQL 17 - 12.7. Configuration Example") ([17](/docs/17/textsearch-
configuration.html "PostgreSQL 17 - 12.7. Configuration Example")) /
[16](/docs/16/textsearch-configuration.html "PostgreSQL 16 -
12.7. Configuration Example") / [15](/docs/15/textsearch-configuration.html
"PostgreSQL 15 - 12.7. Configuration Example") / [14](/docs/14/textsearch-
configuration.html "PostgreSQL 14 - 12.7. Configuration Example") /
[13](/docs/13/textsearch-configuration.html "PostgreSQL 13 -
12.7. Configuration Example")

Development Versions: [18](/docs/18/textsearch-configuration.html "PostgreSQL
18 - 12.7. Configuration Example") / [devel](/docs/devel/textsearch-
configuration.html "PostgreSQL devel - 12.7. Configuration Example")

Unsupported versions: [12](/docs/12/textsearch-configuration.html "PostgreSQL
12 - 12.7. Configuration Example") / [11](/docs/11/textsearch-
configuration.html "PostgreSQL 11 - 12.7. Configuration Example") /
[10](/docs/10/textsearch-configuration.html "PostgreSQL 10 -
12.7. Configuration Example") / [9.6](/docs/9.6/textsearch-configuration.html
"PostgreSQL 9.6 - 12.7. Configuration Example") / [9.5](/docs/9.5/textsearch-
configuration.html "PostgreSQL 9.5 - 12.7. Configuration Example") /
[9.4](/docs/9.4/textsearch-configuration.html "PostgreSQL 9.4 -
12.7. Configuration Example") / [9.3](/docs/9.3/textsearch-configuration.html
"PostgreSQL 9.3 - 12.7. Configuration Example") / [9.2](/docs/9.2/textsearch-
configuration.html "PostgreSQL 9.2 - 12.7. Configuration Example") /
[9.1](/docs/9.1/textsearch-configuration.html "PostgreSQL 9.1 -
12.7. Configuration Example") / [9.0](/docs/9.0/textsearch-configuration.html
"PostgreSQL 9.0 - 12.7. Configuration Example") / [8.4](/docs/8.4/textsearch-
configuration.html "PostgreSQL 8.4 - 12.7. Configuration Example") /
[8.3](/docs/8.3/textsearch-configuration.html "PostgreSQL 8.3 -
12.7. Configuration Example")

__

12.7. Configuration Example  
---  
[Prev](textsearch-dictionaries.html "12.6. Dictionaries")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-debugging.html "12.8. Testing and Debugging Text Search")  
  
* * *

## 12.7. Configuration Example #

A text search configuration specifies all options necessary to transform a
document into a `tsvector`: the parser to use to break text into tokens, and
the dictionaries to use to transform each token into a lexeme. Every call of
`to_tsvector` or `to_tsquery` needs a text search configuration to perform its
processing. The configuration parameter [default_text_search_config](runtime-
config-client.html#GUC-DEFAULT-TEXT-SEARCH-CONFIG) specifies the name of the
default configuration, which is the one used by text search functions if an
explicit configuration parameter is omitted. It can be set in
`postgresql.conf`, or set for an individual session using the `SET` command.

Several predefined text search configurations are available, and you can
create custom configurations easily. To facilitate management of text search
objects, a set of SQL commands is available, and there are several psql
commands that display information about text search objects ([Section
12.10](textsearch-psql.html "12.10. psql Support")).

As an example we will create a configuration `pg`, starting by duplicating the
built-in `english` configuration:

    
    
    CREATE TEXT SEARCH CONFIGURATION public.pg ( COPY = pg_catalog.english );
    

We will use a PostgreSQL-specific synonym list and store it in
`$SHAREDIR/tsearch_data/pg_dict.syn`. The file contents look like:

    
    
    postgres    pg
    pgsql       pg
    postgresql  pg
    

We define the synonym dictionary like this:

    
    
    CREATE TEXT SEARCH DICTIONARY pg_dict (
        TEMPLATE = synonym,
        SYNONYMS = pg_dict
    );
    

Next we register the Ispell dictionary `english_ispell`, which has its own
configuration files:

    
    
    CREATE TEXT SEARCH DICTIONARY english_ispell (
        TEMPLATE = ispell,
        DictFile = english,
        AffFile = english,
        StopWords = english
    );
    

Now we can set up the mappings for words in configuration `pg`:

    
    
    ALTER TEXT SEARCH CONFIGURATION pg
        ALTER MAPPING FOR asciiword, asciihword, hword_asciipart,
                          word, hword, hword_part
        WITH pg_dict, english_ispell, english_stem;
    

We choose not to index or search some token types that the built-in
configuration does handle:

    
    
    ALTER TEXT SEARCH CONFIGURATION pg
        DROP MAPPING FOR email, url, url_path, sfloat, float;
    

Now we can test our configuration:

    
    
    SELECT * FROM ts_debug('public.pg', '
    PostgreSQL, the highly scalable, SQL compliant, open source object-relational
    database management system, is now undergoing beta testing of the next
    version of our software.
    ');
    

The next step is to set the session to use the new configuration, which was
created in the `public` schema:

    
    
    => \dF
       List of text search configurations
     Schema  | Name | Description
    ---------+------+-------------
     public  | pg   |
    
    SET default_text_search_config = 'public.pg';
    SET
    
    SHOW default_text_search_config;
     default_text_search_config
    ----------------------------
     public.pg
    

* * *

[Prev](textsearch-dictionaries.html "12.6. Dictionaries")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-debugging.html "12.8. Testing and Debugging Text Search")  
---|---|---  
12.6. Dictionaries  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.8. Testing and Debugging Text Search  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-
configuration.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

