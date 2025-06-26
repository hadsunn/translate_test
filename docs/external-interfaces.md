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

Supported Versions: [Current](/docs/current/external-interfaces.html
"PostgreSQL 17 - H.1. Client Interfaces") ([17](/docs/17/external-
interfaces.html "PostgreSQL 17 - H.1. Client Interfaces")) /
[16](/docs/16/external-interfaces.html "PostgreSQL 16 - H.1. Client
Interfaces") / [15](/docs/15/external-interfaces.html "PostgreSQL 15 -
H.1. Client Interfaces") / [14](/docs/14/external-interfaces.html "PostgreSQL
14 - H.1. Client Interfaces") / [13](/docs/13/external-interfaces.html
"PostgreSQL 13 - H.1. Client Interfaces")

Development Versions: [18](/docs/18/external-interfaces.html "PostgreSQL 18 -
H.1. Client Interfaces") / [devel](/docs/devel/external-interfaces.html
"PostgreSQL devel - H.1. Client Interfaces")

Unsupported versions: [12](/docs/12/external-interfaces.html "PostgreSQL 12 -
H.1. Client Interfaces") / [11](/docs/11/external-interfaces.html "PostgreSQL
11 - H.1. Client Interfaces") / [10](/docs/10/external-interfaces.html
"PostgreSQL 10 - H.1. Client Interfaces") / [9.6](/docs/9.6/external-
interfaces.html "PostgreSQL 9.6 - H.1. Client Interfaces") /
[9.5](/docs/9.5/external-interfaces.html "PostgreSQL 9.5 - H.1. Client
Interfaces") / [9.4](/docs/9.4/external-interfaces.html "PostgreSQL 9.4 -
H.1. Client Interfaces") / [9.3](/docs/9.3/external-interfaces.html
"PostgreSQL 9.3 - H.1. Client Interfaces") / [9.2](/docs/9.2/external-
interfaces.html "PostgreSQL 9.2 - H.1. Client Interfaces") /
[9.1](/docs/9.1/external-interfaces.html "PostgreSQL 9.1 - H.1. Client
Interfaces") / [9.0](/docs/9.0/external-interfaces.html "PostgreSQL 9.0 -
H.1. Client Interfaces") / [8.4](/docs/8.4/external-interfaces.html
"PostgreSQL 8.4 - H.1. Client Interfaces") / [8.3](/docs/8.3/external-
interfaces.html "PostgreSQL 8.3 - H.1. Client Interfaces") /
[8.2](/docs/8.2/external-interfaces.html "PostgreSQL 8.2 - H.1. Client
Interfaces")

__

H.1. Client Interfaces  
---  
[Prev](external-projects.html "Appendix H. External Projects")  | [Up](external-projects.html "Appendix H. External Projects") | Appendix H. External Projects | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](external-admin-tools.html "H.2. Administration Tools")  
  
* * *

## H.1. Client Interfaces #

There are only two client interfaces included in the base PostgreSQL
distribution:

  * [libpq](libpq.html "Chapter 34. libpq — C Library") is included because it is the primary C language interface, and because many other client interfaces are built on top of it.

  * [ECPG](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") is included because it depends on the server-side SQL grammar, and is therefore sensitive to changes in PostgreSQL itself.

All other language interfaces are external projects and are distributed
separately. A [list of language
interfaces](https://wiki.postgresql.org/wiki/List_of_drivers) is maintained on
the PostgreSQL wiki. Note that some of these packages are not released under
the same license as PostgreSQL. For more information on each language
interface, including licensing terms, refer to its website and documentation.

<https://wiki.postgresql.org/wiki/List_of_drivers>

* * *

[Prev](external-projects.html "Appendix H. External Projects")  | [Up](external-projects.html "Appendix H. External Projects") |  [Next](external-admin-tools.html "H.2. Administration Tools")  
---|---|---  
Appendix H. External Projects  | [Home](index.html "PostgreSQL 16.9 Documentation") |  H.2. Administration Tools  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/external-interfaces.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

