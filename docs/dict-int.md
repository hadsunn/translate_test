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

Supported Versions: [Current](/docs/current/dict-int.html "PostgreSQL 17 -
F.13. dict_int — example full-text search dictionary for integers")
([17](/docs/17/dict-int.html "PostgreSQL 17 - F.13. dict_int — example full-
text search dictionary for integers")) / [16](/docs/16/dict-int.html
"PostgreSQL 16 - F.13. dict_int — example full-text search dictionary for
integers") / [15](/docs/15/dict-int.html "PostgreSQL 15 - F.13. dict_int —
example full-text search dictionary for integers") / [14](/docs/14/dict-
int.html "PostgreSQL 14 - F.13. dict_int — example full-text search dictionary
for integers") / [13](/docs/13/dict-int.html "PostgreSQL 13 - F.13. dict_int —
example full-text search dictionary for integers")

Development Versions: [18](/docs/18/dict-int.html "PostgreSQL 18 -
F.13. dict_int — example full-text search dictionary for integers") /
[devel](/docs/devel/dict-int.html "PostgreSQL devel - F.13. dict_int — example
full-text search dictionary for integers")

Unsupported versions: [12](/docs/12/dict-int.html "PostgreSQL 12 -
F.13. dict_int — example full-text search dictionary for integers") /
[11](/docs/11/dict-int.html "PostgreSQL 11 - F.13. dict_int — example full-
text search dictionary for integers") / [10](/docs/10/dict-int.html
"PostgreSQL 10 - F.13. dict_int — example full-text search dictionary for
integers") / [9.6](/docs/9.6/dict-int.html "PostgreSQL 9.6 - F.13. dict_int —
example full-text search dictionary for integers") / [9.5](/docs/9.5/dict-
int.html "PostgreSQL 9.5 - F.13. dict_int — example full-text search
dictionary for integers") / [9.4](/docs/9.4/dict-int.html "PostgreSQL 9.4 -
F.13. dict_int — example full-text search dictionary for integers") /
[9.3](/docs/9.3/dict-int.html "PostgreSQL 9.3 - F.13. dict_int — example full-
text search dictionary for integers") / [9.2](/docs/9.2/dict-int.html
"PostgreSQL 9.2 - F.13. dict_int — example full-text search dictionary for
integers") / [9.1](/docs/9.1/dict-int.html "PostgreSQL 9.1 - F.13. dict_int —
example full-text search dictionary for integers") / [9.0](/docs/9.0/dict-
int.html "PostgreSQL 9.0 - F.13. dict_int — example full-text search
dictionary for integers") / [8.4](/docs/8.4/dict-int.html "PostgreSQL 8.4 -
F.13. dict_int — example full-text search dictionary for integers") /
[8.3](/docs/8.3/dict-int.html "PostgreSQL 8.3 - F.13. dict_int — example full-
text search dictionary for integers")

__

F.13. dict_int — example full-text search dictionary for integers  
---  
[Prev](contrib-dblink-build-sql-update.html "dblink_build_sql_update")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](dict-xsyn.html "F.14. dict_xsyn — example synonym full-text search dictionary")  
  
* * *

## F.13. dict_int — example full-text search dictionary for integers #

[F.13.1. Configuration](dict-int.html#DICT-INT-CONFIG)

[F.13.2. Usage](dict-int.html#DICT-INT-USAGE)

`dict_int` is an example of an add-on dictionary template for full-text
search. The motivation for this example dictionary is to control the indexing
of integers (signed and unsigned), allowing such numbers to be indexed while
preventing excessive growth in the number of unique words, which greatly
affects the performance of searching.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.13.1. Configuration #

The dictionary accepts three options:

  * The `maxlen` parameter specifies the maximum number of digits allowed in an integer word. The default value is 6.

  * The `rejectlong` parameter specifies whether an overlength integer should be truncated or ignored. If `rejectlong` is `false` (the default), the dictionary returns the first `maxlen` digits of the integer. If `rejectlong` is `true`, the dictionary treats an overlength integer as a stop word, so that it will not be indexed. Note that this also means that such an integer cannot be searched for.

  * The `absval` parameter specifies whether leading “`+`” or “`-`” signs should be removed from integer words. The default is `false`. When `true`, the sign is removed before `maxlen` is applied.

### F.13.2. Usage #

Installing the `dict_int` extension creates a text search template
`intdict_template` and a dictionary `intdict` based on it, with the default
parameters. You can alter the parameters, for example

    
    
    mydb# ALTER TEXT SEARCH DICTIONARY intdict (MAXLEN = 4, REJECTLONG = true);
    ALTER TEXT SEARCH DICTIONARY
    

or create new dictionaries based on the template.

To test the dictionary, you can try

    
    
    mydb# select ts_lexize('intdict', '12345678');
     ts_lexize
    -----------
     {123456}
    

but real-world usage will involve including it in a text search configuration
as described in [Chapter 12](textsearch.html "Chapter 12. Full Text Search").
That might look like this:

    
    
    ALTER TEXT SEARCH CONFIGURATION english
        ALTER MAPPING FOR int, uint WITH intdict;
    

* * *

[Prev](contrib-dblink-build-sql-update.html "dblink_build_sql_update")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](dict-xsyn.html "F.14. dict_xsyn — example synonym full-text search dictionary")  
---|---|---  
dblink_build_sql_update  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.14. dict_xsyn — example synonym full-text search dictionary  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dict-int.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

