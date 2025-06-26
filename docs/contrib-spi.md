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

Supported Versions: [Current](/docs/current/contrib-spi.html "PostgreSQL 17 -
F.41. spi — Server Programming Interface features/examples")
([17](/docs/17/contrib-spi.html "PostgreSQL 17 - F.41. spi — Server
Programming Interface features/examples")) / [16](/docs/16/contrib-spi.html
"PostgreSQL 16 - F.41. spi — Server Programming Interface features/examples")
/ [15](/docs/15/contrib-spi.html "PostgreSQL 15 - F.41. spi — Server
Programming Interface features/examples") / [14](/docs/14/contrib-spi.html
"PostgreSQL 14 - F.41. spi — Server Programming Interface features/examples")
/ [13](/docs/13/contrib-spi.html "PostgreSQL 13 - F.41. spi — Server
Programming Interface features/examples")

Development Versions: [18](/docs/18/contrib-spi.html "PostgreSQL 18 -
F.41. spi — Server Programming Interface features/examples") /
[devel](/docs/devel/contrib-spi.html "PostgreSQL devel - F.41. spi — Server
Programming Interface features/examples")

Unsupported versions: [12](/docs/12/contrib-spi.html "PostgreSQL 12 -
F.41. spi — Server Programming Interface features/examples") /
[11](/docs/11/contrib-spi.html "PostgreSQL 11 - F.41. spi — Server Programming
Interface features/examples") / [10](/docs/10/contrib-spi.html "PostgreSQL 10
- F.41. spi — Server Programming Interface features/examples") /
[9.6](/docs/9.6/contrib-spi.html "PostgreSQL 9.6 - F.41. spi — Server
Programming Interface features/examples") / [9.5](/docs/9.5/contrib-spi.html
"PostgreSQL 9.5 - F.41. spi — Server Programming Interface features/examples")
/ [9.4](/docs/9.4/contrib-spi.html "PostgreSQL 9.4 - F.41. spi — Server
Programming Interface features/examples") / [9.3](/docs/9.3/contrib-spi.html
"PostgreSQL 9.3 - F.41. spi — Server Programming Interface features/examples")
/ [9.2](/docs/9.2/contrib-spi.html "PostgreSQL 9.2 - F.41. spi — Server
Programming Interface features/examples") / [9.1](/docs/9.1/contrib-spi.html
"PostgreSQL 9.1 - F.41. spi — Server Programming Interface features/examples")
/ [9.0](/docs/9.0/contrib-spi.html "PostgreSQL 9.0 - F.41. spi — Server
Programming Interface features/examples") / [8.4](/docs/8.4/contrib-spi.html
"PostgreSQL 8.4 - F.41. spi — Server Programming Interface features/examples")
/ [8.3](/docs/8.3/contrib-spi.html "PostgreSQL 8.3 - F.41. spi — Server
Programming Interface features/examples")

__

F.41. spi — Server Programming Interface features/examples  
---  
[Prev](sepgsql.html "F.40. sepgsql —  SELinux-, label-based mandatory access control \(MAC\) security module")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sslinfo.html "F.42. sslinfo — obtain client SSL information")  
  
* * *

## F.41. spi — Server Programming Interface features/examples #

[F.41.1. refint — Functions for Implementing Referential Integrity](contrib-
spi.html#CONTRIB-SPI-REFINT)

[F.41.2. autoinc — Functions for Autoincrementing Fields](contrib-
spi.html#CONTRIB-SPI-AUTOINC)

[F.41.3. insert_username — Functions for Tracking Who Changed a
Table](contrib-spi.html#CONTRIB-SPI-INSERT-USERNAME)

[F.41.4. moddatetime — Functions for Tracking Last Modification Time](contrib-
spi.html#CONTRIB-SPI-MODDATETIME)

The spi module provides several workable examples of using the [Server
Programming Interface](spi.html "Chapter 47. Server Programming Interface")
(SPI) and triggers. While these functions are of some value in their own
right, they are even more useful as examples to modify for your own purposes.
The functions are general enough to be used with any table, but you have to
specify table and field names (as described below) while creating a trigger.

Each of the groups of functions described below is provided as a separately-
installable extension.

### F.41.1. refint — Functions for Implementing Referential Integrity #

`check_primary_key()` and `check_foreign_key()` are used to check foreign key
constraints. (This functionality is long since superseded by the built-in
foreign key mechanism, of course, but the module is still useful as an
example.)

`check_primary_key()` checks the referencing table. To use, create a `BEFORE
INSERT OR UPDATE` trigger using this function on a table referencing another
table. Specify as the trigger arguments: the referencing table's column
name(s) which form the foreign key, the referenced table name, and the column
names in the referenced table which form the primary/unique key. To handle
multiple foreign keys, create a trigger for each reference.

`check_foreign_key()` checks the referenced table. To use, create a `BEFORE
DELETE OR UPDATE` trigger using this function on a table referenced by other
table(s). Specify as the trigger arguments: the number of referencing tables
for which the function has to perform checking, the action if a referencing
key is found (`cascade` — to delete the referencing row, `restrict` — to abort
transaction if referencing keys exist, `setnull` — to set referencing key
fields to null), the triggered table's column names which form the
primary/unique key, then the referencing table name and column names (repeated
for as many referencing tables as were specified by first argument). Note that
the primary/unique key columns should be marked NOT NULL and should have a
unique index.

There are examples in `refint.example`.

### F.41.2. autoinc — Functions for Autoincrementing Fields #

`autoinc()` is a trigger that stores the next value of a sequence into an
integer field. This has some overlap with the built-in “serial column”
feature, but it is not the same: `autoinc()` will override attempts to
substitute a different field value during inserts, and optionally it can be
used to increment the field during updates, too.

To use, create a `BEFORE INSERT` (or optionally `BEFORE INSERT OR UPDATE`)
trigger using this function. Specify two trigger arguments: the name of the
integer column to be modified, and the name of the sequence object that will
supply values. (Actually, you can specify any number of pairs of such names,
if you'd like to update more than one autoincrementing column.)

There is an example in `autoinc.example`.

### F.41.3. insert_username — Functions for Tracking Who Changed a Table #

`insert_username()` is a trigger that stores the current user's name into a
text field. This can be useful for tracking who last modified a particular row
within a table.

To use, create a `BEFORE INSERT` and/or `UPDATE` trigger using this function.
Specify a single trigger argument: the name of the text column to be modified.

There is an example in `insert_username.example`.

### F.41.4. moddatetime — Functions for Tracking Last Modification Time #

`moddatetime()` is a trigger that stores the current time into a `timestamp`
field. This can be useful for tracking the last modification time of a
particular row within a table.

To use, create a `BEFORE UPDATE` trigger using this function. Specify a single
trigger argument: the name of the column to be modified. The column must be of
type `timestamp` or `timestamp with time zone`.

There is an example in `moddatetime.example`.

* * *

[Prev](sepgsql.html "F.40. sepgsql —  SELinux-, label-based mandatory access control \(MAC\) security module")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](sslinfo.html "F.42. sslinfo — obtain client SSL information")  
---|---|---  
F.40. sepgsql — SELinux-, label-based mandatory access control (MAC) security module  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.42. sslinfo — obtain client SSL information  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-spi.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

