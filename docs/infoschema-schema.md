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

Supported Versions: [Current](/docs/current/infoschema-schema.html "PostgreSQL
17 - 37.1. The Schema") ([17](/docs/17/infoschema-schema.html "PostgreSQL 17 -
37.1. The Schema")) / [16](/docs/16/infoschema-schema.html "PostgreSQL 16 -
37.1. The Schema") / [15](/docs/15/infoschema-schema.html "PostgreSQL 15 -
37.1. The Schema") / [14](/docs/14/infoschema-schema.html "PostgreSQL 14 -
37.1. The Schema") / [13](/docs/13/infoschema-schema.html "PostgreSQL 13 -
37.1. The Schema")

Development Versions: [18](/docs/18/infoschema-schema.html "PostgreSQL 18 -
37.1. The Schema") / [devel](/docs/devel/infoschema-schema.html "PostgreSQL
devel - 37.1. The Schema")

Unsupported versions: [12](/docs/12/infoschema-schema.html "PostgreSQL 12 -
37.1. The Schema") / [11](/docs/11/infoschema-schema.html "PostgreSQL 11 -
37.1. The Schema") / [10](/docs/10/infoschema-schema.html "PostgreSQL 10 -
37.1. The Schema") / [9.6](/docs/9.6/infoschema-schema.html "PostgreSQL 9.6 -
37.1. The Schema") / [9.5](/docs/9.5/infoschema-schema.html "PostgreSQL 9.5 -
37.1. The Schema") / [9.4](/docs/9.4/infoschema-schema.html "PostgreSQL 9.4 -
37.1. The Schema") / [9.3](/docs/9.3/infoschema-schema.html "PostgreSQL 9.3 -
37.1. The Schema") / [9.2](/docs/9.2/infoschema-schema.html "PostgreSQL 9.2 -
37.1. The Schema") / [9.1](/docs/9.1/infoschema-schema.html "PostgreSQL 9.1 -
37.1. The Schema") / [9.0](/docs/9.0/infoschema-schema.html "PostgreSQL 9.0 -
37.1. The Schema") / [8.4](/docs/8.4/infoschema-schema.html "PostgreSQL 8.4 -
37.1. The Schema") / [8.3](/docs/8.3/infoschema-schema.html "PostgreSQL 8.3 -
37.1. The Schema") / [8.2](/docs/8.2/infoschema-schema.html "PostgreSQL 8.2 -
37.1. The Schema")

__

37.1. The Schema  
---  
[Prev](information-schema.html "Chapter 37. The Information Schema")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-datatypes.html "37.2. Data Types")  
  
* * *

## 37.1. The Schema #

The information schema itself is a schema named `information_schema`. This
schema automatically exists in all databases. The owner of this schema is the
initial database user in the cluster, and that user naturally has all the
privileges on this schema, including the ability to drop it (but the space
savings achieved by that are minuscule).

By default, the information schema is not in the schema search path, so you
need to access all objects in it through qualified names. Since the names of
some of the objects in the information schema are generic names that might
occur in user applications, you should be careful if you want to put the
information schema in the path.

* * *

[Prev](information-schema.html "Chapter 37. The Information Schema")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-datatypes.html "37.2. Data Types")  
---|---|---  
Chapter 37. The Information Schema  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.2. Data Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-schema.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

