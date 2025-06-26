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

Supported Versions: [Current](/docs/current/xfunc-internal.html "PostgreSQL 17
- 38.9. Internal Functions") ([17](/docs/17/xfunc-internal.html "PostgreSQL 17
- 38.9. Internal Functions")) / [16](/docs/16/xfunc-internal.html "PostgreSQL
16 - 38.9. Internal Functions") / [15](/docs/15/xfunc-internal.html
"PostgreSQL 15 - 38.9. Internal Functions") / [14](/docs/14/xfunc-
internal.html "PostgreSQL 14 - 38.9. Internal Functions") /
[13](/docs/13/xfunc-internal.html "PostgreSQL 13 - 38.9. Internal Functions")

Development Versions: [18](/docs/18/xfunc-internal.html "PostgreSQL 18 -
38.9. Internal Functions") / [devel](/docs/devel/xfunc-internal.html
"PostgreSQL devel - 38.9. Internal Functions")

Unsupported versions: [12](/docs/12/xfunc-internal.html "PostgreSQL 12 -
38.9. Internal Functions") / [11](/docs/11/xfunc-internal.html "PostgreSQL 11
- 38.9. Internal Functions") / [10](/docs/10/xfunc-internal.html "PostgreSQL
10 - 38.9. Internal Functions") / [9.6](/docs/9.6/xfunc-internal.html
"PostgreSQL 9.6 - 38.9. Internal Functions") / [9.5](/docs/9.5/xfunc-
internal.html "PostgreSQL 9.5 - 38.9. Internal Functions") /
[9.4](/docs/9.4/xfunc-internal.html "PostgreSQL 9.4 - 38.9. Internal
Functions") / [9.3](/docs/9.3/xfunc-internal.html "PostgreSQL 9.3 -
38.9. Internal Functions") / [9.2](/docs/9.2/xfunc-internal.html "PostgreSQL
9.2 - 38.9. Internal Functions") / [9.1](/docs/9.1/xfunc-internal.html
"PostgreSQL 9.1 - 38.9. Internal Functions") / [9.0](/docs/9.0/xfunc-
internal.html "PostgreSQL 9.0 - 38.9. Internal Functions") /
[8.4](/docs/8.4/xfunc-internal.html "PostgreSQL 8.4 - 38.9. Internal
Functions") / [8.3](/docs/8.3/xfunc-internal.html "PostgreSQL 8.3 -
38.9. Internal Functions") / [8.2](/docs/8.2/xfunc-internal.html "PostgreSQL
8.2 - 38.9. Internal Functions") / [8.1](/docs/8.1/xfunc-internal.html
"PostgreSQL 8.1 - 38.9. Internal Functions") / [8.0](/docs/8.0/xfunc-
internal.html "PostgreSQL 8.0 - 38.9. Internal Functions") /
[7.4](/docs/7.4/xfunc-internal.html "PostgreSQL 7.4 - 38.9. Internal
Functions") / [7.3](/docs/7.3/xfunc-internal.html "PostgreSQL 7.3 -
38.9. Internal Functions") / [7.2](/docs/7.2/xfunc-internal.html "PostgreSQL
7.2 - 38.9. Internal Functions") / [7.1](/docs/7.1/xfunc-internal.html
"PostgreSQL 7.1 - 38.9. Internal Functions")

__

38.9. Internal Functions  
---  
[Prev](xfunc-pl.html "38.8. Procedural Language Functions")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xfunc-c.html "38.10. C-Language Functions")  
  
* * *

## 38.9. Internal Functions #

Internal functions are functions written in C that have been statically linked
into the PostgreSQL server. The “body” of the function definition specifies
the C-language name of the function, which need not be the same as the name
being declared for SQL use. (For reasons of backward compatibility, an empty
body is accepted as meaning that the C-language function name is the same as
the SQL name.)

Normally, all internal functions present in the server are declared during the
initialization of the database cluster (see [Section 19.2](creating-
cluster.html "19.2. Creating a Database Cluster")), but a user could use
`CREATE FUNCTION` to create additional alias names for an internal function.
Internal functions are declared in `CREATE FUNCTION` with language name
`internal`. For instance, to create an alias for the `sqrt` function:

    
    
    CREATE FUNCTION square_root(double precision) RETURNS double precision
        AS 'dsqrt'
        LANGUAGE internal
        STRICT;
    

(Most internal functions expect to be declared “strict”.)

### Note

Not all “predefined” functions are “internal” in the above sense. Some
predefined functions are written in SQL.

* * *

[Prev](xfunc-pl.html "38.8. Procedural Language Functions")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xfunc-c.html "38.10. C-Language Functions")  
---|---|---  
38.8. Procedural Language Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.10. C-Language Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xfunc-internal.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

