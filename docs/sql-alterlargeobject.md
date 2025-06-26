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

Supported Versions: [Current](/docs/current/sql-alterlargeobject.html
"PostgreSQL 17 - ALTER LARGE OBJECT") ([17](/docs/17/sql-alterlargeobject.html
"PostgreSQL 17 - ALTER LARGE OBJECT")) / [16](/docs/16/sql-
alterlargeobject.html "PostgreSQL 16 - ALTER LARGE OBJECT") /
[15](/docs/15/sql-alterlargeobject.html "PostgreSQL 15 - ALTER LARGE OBJECT")
/ [14](/docs/14/sql-alterlargeobject.html "PostgreSQL 14 - ALTER LARGE
OBJECT") / [13](/docs/13/sql-alterlargeobject.html "PostgreSQL 13 - ALTER
LARGE OBJECT")

Development Versions: [18](/docs/18/sql-alterlargeobject.html "PostgreSQL 18 -
ALTER LARGE OBJECT") / [devel](/docs/devel/sql-alterlargeobject.html
"PostgreSQL devel - ALTER LARGE OBJECT")

Unsupported versions: [12](/docs/12/sql-alterlargeobject.html "PostgreSQL 12 -
ALTER LARGE OBJECT") / [11](/docs/11/sql-alterlargeobject.html "PostgreSQL 11
- ALTER LARGE OBJECT") / [10](/docs/10/sql-alterlargeobject.html "PostgreSQL
10 - ALTER LARGE OBJECT") / [9.6](/docs/9.6/sql-alterlargeobject.html
"PostgreSQL 9.6 - ALTER LARGE OBJECT") / [9.5](/docs/9.5/sql-
alterlargeobject.html "PostgreSQL 9.5 - ALTER LARGE OBJECT") /
[9.4](/docs/9.4/sql-alterlargeobject.html "PostgreSQL 9.4 - ALTER LARGE
OBJECT") / [9.3](/docs/9.3/sql-alterlargeobject.html "PostgreSQL 9.3 - ALTER
LARGE OBJECT") / [9.2](/docs/9.2/sql-alterlargeobject.html "PostgreSQL 9.2 -
ALTER LARGE OBJECT") / [9.1](/docs/9.1/sql-alterlargeobject.html "PostgreSQL
9.1 - ALTER LARGE OBJECT") / [9.0](/docs/9.0/sql-alterlargeobject.html
"PostgreSQL 9.0 - ALTER LARGE OBJECT")

__

ALTER LARGE OBJECT  
---  
[Prev](sql-alterlanguage.html "ALTER LANGUAGE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altermaterializedview.html "ALTER MATERIALIZED VIEW")  
  
* * *

## ALTER LARGE OBJECT

ALTER LARGE OBJECT — change the definition of a large object

## Synopsis

    
    
    ALTER LARGE OBJECT _large_object_oid_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    

## Description

`ALTER LARGE OBJECT` changes the definition of a large object.

You must own the large object to use `ALTER LARGE OBJECT`. To alter the owner,
you must also be able to `SET ROLE` to the new owning role. (However, a
superuser can alter any large object anyway.) Currently, the only
functionality is to assign a new owner, so both restrictions always apply.

## Parameters

_`large_object_oid`_

    

OID of the large object to be altered

_`new_owner`_

    

The new owner of the large object

## Compatibility

There is no `ALTER LARGE OBJECT` statement in the SQL standard.

## See Also

[Chapter 35](largeobjects.html "Chapter 35. Large Objects")

* * *

[Prev](sql-alterlanguage.html "ALTER LANGUAGE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altermaterializedview.html "ALTER MATERIALIZED VIEW")  
---|---|---  
ALTER LANGUAGE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER MATERIALIZED VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterlargeobject.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

