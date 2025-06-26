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

Supported Versions: [Current](/docs/current/pgsurgery.html "PostgreSQL 17 -
F.34. pg_surgery — perform low-level surgery on relation data")
([17](/docs/17/pgsurgery.html "PostgreSQL 17 - F.34. pg_surgery — perform low-
level surgery on relation data")) / [16](/docs/16/pgsurgery.html "PostgreSQL
16 - F.34. pg_surgery — perform low-level surgery on relation data") /
[15](/docs/15/pgsurgery.html "PostgreSQL 15 - F.34. pg_surgery — perform low-
level surgery on relation data") / [14](/docs/14/pgsurgery.html "PostgreSQL 14
- F.34. pg_surgery — perform low-level surgery on relation data")

Development Versions: [18](/docs/18/pgsurgery.html "PostgreSQL 18 -
F.34. pg_surgery — perform low-level surgery on relation data") /
[devel](/docs/devel/pgsurgery.html "PostgreSQL devel - F.34. pg_surgery —
perform low-level surgery on relation data")

__

F.34. pg_surgery — perform low-level surgery on relation data  
---  
[Prev](pgstattuple.html "F.33. pgstattuple — obtain tuple-level statistics")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgtrgm.html "F.35. pg_trgm —  support for similarity of text using trigram matching")  
  
* * *

## F.34. pg_surgery — perform low-level surgery on relation data #

[F.34.1. Functions](pgsurgery.html#PGSURGERY-FUNCS)

[F.34.2. Authors](pgsurgery.html#PGSURGERY-AUTHORS)

The `pg_surgery` module provides various functions to perform surgery on a
damaged relation. These functions are unsafe by design and using them may
corrupt (or further corrupt) your database. For example, these functions can
easily be used to make a table inconsistent with its own indexes, to cause
`UNIQUE` or `FOREIGN KEY` constraint violations, or even to make tuples
visible which, when read, will cause a database server crash. They should be
used with great caution and only as a last resort.

### F.34.1. Functions #

`heap_force_kill(regclass, tid[]) returns void`

    

`heap_force_kill` marks “used” line pointers as “dead” without examining the
tuples. The intended use of this function is to forcibly remove tuples that
are not otherwise accessible. For example:

    
    
    test=> select * from t1 where ctid = '(0, 1)';
    ERROR:  could not access status of transaction 4007513275
    DETAIL:  Could not open file "pg_xact/0EED": No such file or directory.
    
    test=# select heap_force_kill('t1'::regclass, ARRAY['(0, 1)']::tid[]);
     heap_force_kill
    -----------------
    
    (1 row)
    
    test=# select * from t1 where ctid = '(0, 1)';
    (0 rows)
    
    

`heap_force_freeze(regclass, tid[]) returns void`

    

`heap_force_freeze` marks tuples as frozen without examining the tuple data.
The intended use of this function is to make accessible tuples which are
inaccessible due to corrupted visibility information, or which prevent the
table from being successfully vacuumed due to corrupted visibility
information. For example:

    
    
    test=> vacuum t1;
    ERROR:  found xmin 507 from before relfrozenxid 515
    CONTEXT:  while scanning block 0 of relation "public.t1"
    
    test=# select ctid from t1 where xmin = 507;
     ctid
    -------
     (0,3)
    (1 row)
    
    test=# select heap_force_freeze('t1'::regclass, ARRAY['(0, 3)']::tid[]);
     heap_force_freeze
    -------------------
    
    (1 row)
    
    test=# select ctid from t1 where xmin = 2;
     ctid
    -------
     (0,3)
    (1 row)
    
    

### F.34.2. Authors #

Ashutosh Sharma `<[ashu.coek88@gmail.com](mailto:ashu.coek88@gmail.com)>`

* * *

[Prev](pgstattuple.html "F.33. pgstattuple — obtain tuple-level statistics")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pgtrgm.html "F.35. pg_trgm —  support for similarity of text using trigram matching")  
---|---|---  
F.33. pgstattuple — obtain tuple-level statistics  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.35. pg_trgm — support for similarity of text using trigram matching  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgsurgery.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

