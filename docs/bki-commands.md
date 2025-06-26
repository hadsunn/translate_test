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

Supported Versions: [Current](/docs/current/bki-commands.html "PostgreSQL 17 -
75.4. BKI Commands") ([17](/docs/17/bki-commands.html "PostgreSQL 17 -
75.4. BKI Commands")) / [16](/docs/16/bki-commands.html "PostgreSQL 16 -
75.4. BKI Commands") / [15](/docs/15/bki-commands.html "PostgreSQL 15 -
75.4. BKI Commands") / [14](/docs/14/bki-commands.html "PostgreSQL 14 -
75.4. BKI Commands") / [13](/docs/13/bki-commands.html "PostgreSQL 13 -
75.4. BKI Commands")

Development Versions: [18](/docs/18/bki-commands.html "PostgreSQL 18 -
75.4. BKI Commands") / [devel](/docs/devel/bki-commands.html "PostgreSQL devel
- 75.4. BKI Commands")

Unsupported versions: [12](/docs/12/bki-commands.html "PostgreSQL 12 -
75.4. BKI Commands") / [11](/docs/11/bki-commands.html "PostgreSQL 11 -
75.4. BKI Commands") / [10](/docs/10/bki-commands.html "PostgreSQL 10 -
75.4. BKI Commands") / [9.6](/docs/9.6/bki-commands.html "PostgreSQL 9.6 -
75.4. BKI Commands") / [9.5](/docs/9.5/bki-commands.html "PostgreSQL 9.5 -
75.4. BKI Commands") / [9.4](/docs/9.4/bki-commands.html "PostgreSQL 9.4 -
75.4. BKI Commands") / [9.3](/docs/9.3/bki-commands.html "PostgreSQL 9.3 -
75.4. BKI Commands") / [9.2](/docs/9.2/bki-commands.html "PostgreSQL 9.2 -
75.4. BKI Commands") / [9.1](/docs/9.1/bki-commands.html "PostgreSQL 9.1 -
75.4. BKI Commands") / [9.0](/docs/9.0/bki-commands.html "PostgreSQL 9.0 -
75.4. BKI Commands") / [8.4](/docs/8.4/bki-commands.html "PostgreSQL 8.4 -
75.4. BKI Commands") / [8.3](/docs/8.3/bki-commands.html "PostgreSQL 8.3 -
75.4. BKI Commands") / [8.2](/docs/8.2/bki-commands.html "PostgreSQL 8.2 -
75.4. BKI Commands") / [8.1](/docs/8.1/bki-commands.html "PostgreSQL 8.1 -
75.4. BKI Commands") / [8.0](/docs/8.0/bki-commands.html "PostgreSQL 8.0 -
75.4. BKI Commands") / [7.4](/docs/7.4/bki-commands.html "PostgreSQL 7.4 -
75.4. BKI Commands") / [7.3](/docs/7.3/bki-commands.html "PostgreSQL 7.3 -
75.4. BKI Commands") / [7.2](/docs/7.2/bki-commands.html "PostgreSQL 7.2 -
75.4. BKI Commands") / [7.1](/docs/7.1/bki-commands.html "PostgreSQL 7.1 -
75.4. BKI Commands")

__

75.4. BKI Commands  
---  
[Prev](bki-format.html "75.3. BKI File Format")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") | Chapter 75. System Catalog Declarations and Initial Contents | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](bki-structure.html "75.5. Structure of the Bootstrap BKI File")  
  
* * *

## 75.4. BKI Commands #

`create` _`tablename`_ _`tableoid`_ [`bootstrap`] [`shared_relation`] [`rowtype_oid` _`oid`_] (_`name1`_ = _`type1`_ [`FORCE NOT NULL` | `FORCE NULL` ] [, _`name2`_ = _`type2`_ [`FORCE NOT NULL` | `FORCE NULL` ], ...])
    

Create a table named _`tablename`_ , and having the OID _`tableoid`_ , with
the columns given in parentheses.

The following column types are supported directly by `bootstrap.c`: `bool`,
`bytea`, `char` (1 byte), `name`, `int2`, `int4`, `regproc`, `regclass`,
`regtype`, `text`, `oid`, `tid`, `xid`, `cid`, `int2vector`, `oidvector`,
`_int4` (array), `_text` (array), `_oid` (array), `_char` (array), `_aclitem`
(array). Although it is possible to create tables containing columns of other
types, this cannot be done until after `pg_type` has been created and filled
with appropriate entries. (That effectively means that only these column types
can be used in bootstrap catalogs, but non-bootstrap catalogs can contain any
built-in type.)

When `bootstrap` is specified, the table will only be created on disk; nothing
is entered into `pg_class`, `pg_attribute`, etc., for it. Thus the table will
not be accessible by ordinary SQL operations until such entries are made the
hard way (with `insert` commands). This option is used for creating `pg_class`
etc. themselves.

The table is created as shared if `shared_relation` is specified. The table's
row type OID (`pg_type` OID) can optionally be specified via the `rowtype_oid`
clause; if not specified, an OID is automatically generated for it. (The
`rowtype_oid` clause is useless if `bootstrap` is specified, but it can be
provided anyway for documentation.)

`open` _`tablename`_

    

Open the table named _`tablename`_ for insertion of data. Any currently open
table is closed.

`close` _`tablename`_

    

Close the open table. The name of the table must be given as a cross-check.

`insert` `(` [_`oid_value`_] _`value1`_ _`value2`_ ... `)`

    

Insert a new row into the open table using _`value1`_ , _`value2`_ , etc., for
its column values.

NULL values can be specified using the special key word `_null_`. Values that
do not look like identifiers or digit strings must be single-quoted. (To
include a single quote in a value, write it twice. Escape-string-style
backslash escapes are allowed in the string, too.)

`declare` [`unique`] `index` _`indexname`_ _`indexoid`_ `on` _`tablename`_
`using` _`amname`_ `(` _`opclass1`_ _`name1`_ [, ...] `)`

    

Create an index named _`indexname`_ , having OID _`indexoid`_ , on the table
named _`tablename`_ , using the _`amname`_ access method. The fields to index
are called _`name1`_ , _`name2`_ etc., and the operator classes to use are
_`opclass1`_ , _`opclass2`_ etc., respectively. The index file is created and
appropriate catalog entries are made for it, but the index contents are not
initialized by this command.

`declare toast` _`toasttableoid`_ _`toastindexoid`_ `on` _`tablename`_

    

Create a TOAST table for the table named _`tablename`_. The TOAST table is
assigned OID _`toasttableoid`_ and its index is assigned OID
_`toastindexoid`_. As with `declare index`, filling of the index is postponed.

`build indices`

    

Fill in the indices that have previously been declared.

* * *

[Prev](bki-format.html "75.3. BKI File Format")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") |  [Next](bki-structure.html "75.5. Structure of the Bootstrap BKI File")  
---|---|---  
75.3. BKI File Format  | [Home](index.html "PostgreSQL 16.9 Documentation") |  75.5. Structure of the Bootstrap BKI File  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/bki-commands.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

