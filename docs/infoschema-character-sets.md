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

Supported Versions: [Current](/docs/current/infoschema-character-sets.html
"PostgreSQL 17 - 37.7. character_sets") ([17](/docs/17/infoschema-character-
sets.html "PostgreSQL 17 - 37.7. character_sets")) / [16](/docs/16/infoschema-
character-sets.html "PostgreSQL 16 - 37.7. character_sets") /
[15](/docs/15/infoschema-character-sets.html "PostgreSQL 15 -
37.7. character_sets") / [14](/docs/14/infoschema-character-sets.html
"PostgreSQL 14 - 37.7. character_sets") / [13](/docs/13/infoschema-character-
sets.html "PostgreSQL 13 - 37.7. character_sets")

Development Versions: [18](/docs/18/infoschema-character-sets.html "PostgreSQL
18 - 37.7. character_sets") / [devel](/docs/devel/infoschema-character-
sets.html "PostgreSQL devel - 37.7. character_sets")

Unsupported versions: [12](/docs/12/infoschema-character-sets.html "PostgreSQL
12 - 37.7. character_sets") / [11](/docs/11/infoschema-character-sets.html
"PostgreSQL 11 - 37.7. character_sets") / [10](/docs/10/infoschema-character-
sets.html "PostgreSQL 10 - 37.7. character_sets") /
[9.6](/docs/9.6/infoschema-character-sets.html "PostgreSQL 9.6 -
37.7. character_sets") / [9.5](/docs/9.5/infoschema-character-sets.html
"PostgreSQL 9.5 - 37.7. character_sets") / [9.4](/docs/9.4/infoschema-
character-sets.html "PostgreSQL 9.4 - 37.7. character_sets") /
[9.3](/docs/9.3/infoschema-character-sets.html "PostgreSQL 9.3 -
37.7. character_sets") / [9.2](/docs/9.2/infoschema-character-sets.html
"PostgreSQL 9.2 - 37.7. character_sets") / [9.1](/docs/9.1/infoschema-
character-sets.html "PostgreSQL 9.1 - 37.7. character_sets")

__

37.7. `character_sets`  
---  
[Prev](infoschema-attributes.html "37.6. attributes")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-check-constraint-routine-usage.html "37.8. check_constraint_routine_usage")  
  
* * *

## 37.7. `character_sets` #

The view `character_sets` identifies the character sets available in the
current database. Since PostgreSQL does not support multiple character sets
within one database, this view only shows one, which is the database encoding.

Take note of how the following terms are used in the SQL standard:

character repertoire

    

An abstract collection of characters, for example `UNICODE`, `UCS`, or
`LATIN1`. Not exposed as an SQL object, but visible in this view.

character encoding form

    

An encoding of some character repertoire. Most older character repertoires
only use one encoding form, and so there are no separate names for them (e.g.,
`LATIN2` is an encoding form applicable to the `LATIN2` repertoire). But for
example Unicode has the encoding forms `UTF8`, `UTF16`, etc. (not all
supported by PostgreSQL). Encoding forms are not exposed as an SQL object, but
are visible in this view.

character set

    

A named SQL object that identifies a character repertoire, a character
encoding, and a default collation. A predefined character set would typically
have the same name as an encoding form, but users could define other names.
For example, the character set `UTF8` would typically identify the character
repertoire `UCS`, encoding form `UTF8`, and some default collation.

You can think of an “encoding” in PostgreSQL either as a character set or a
character encoding form. They will have the same name, and there can only be
one in one database.

**Table  37.5. `character_sets` Columns**

Column Type Description  
---  
`character_set_catalog` `sql_identifier` Character sets are currently not
implemented as schema objects, so this column is null.  
`character_set_schema` `sql_identifier` Character sets are currently not
implemented as schema objects, so this column is null.  
`character_set_name` `sql_identifier` Name of the character set, currently
implemented as showing the name of the database encoding  
`character_repertoire` `sql_identifier` Character repertoire, showing `UCS` if
the encoding is `UTF8`, else just the encoding name  
`form_of_use` `sql_identifier` Character encoding form, same as the database
encoding  
`default_collate_catalog` `sql_identifier` Name of the database containing the
default collation (always the current database, if any collation is
identified)  
`default_collate_schema` `sql_identifier` Name of the schema containing the
default collation  
`default_collate_name` `sql_identifier` Name of the default collation. The
default collation is identified as the collation that matches the `COLLATE`
and `CTYPE` settings of the current database. If there is no such collation,
then this column and the associated schema and catalog columns are null.  
  
  

* * *

[Prev](infoschema-attributes.html "37.6. attributes")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-check-constraint-routine-usage.html "37.8. check_constraint_routine_usage")  
---|---|---  
37.6. `attributes`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.8. `check_constraint_routine_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-character-
sets.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

