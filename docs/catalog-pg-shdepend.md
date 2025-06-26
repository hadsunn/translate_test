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

Supported Versions: [Current](/docs/current/catalog-pg-shdepend.html
"PostgreSQL 17 - 53.48. pg_shdepend") ([17](/docs/17/catalog-pg-shdepend.html
"PostgreSQL 17 - 53.48. pg_shdepend")) / [16](/docs/16/catalog-pg-
shdepend.html "PostgreSQL 16 - 53.48. pg_shdepend") / [15](/docs/15/catalog-
pg-shdepend.html "PostgreSQL 15 - 53.48. pg_shdepend") /
[14](/docs/14/catalog-pg-shdepend.html "PostgreSQL 14 - 53.48. pg_shdepend") /
[13](/docs/13/catalog-pg-shdepend.html "PostgreSQL 13 - 53.48. pg_shdepend")

Development Versions: [18](/docs/18/catalog-pg-shdepend.html "PostgreSQL 18 -
53.48. pg_shdepend") / [devel](/docs/devel/catalog-pg-shdepend.html
"PostgreSQL devel - 53.48. pg_shdepend")

Unsupported versions: [12](/docs/12/catalog-pg-shdepend.html "PostgreSQL 12 -
53.48. pg_shdepend") / [11](/docs/11/catalog-pg-shdepend.html "PostgreSQL 11 -
53.48. pg_shdepend") / [10](/docs/10/catalog-pg-shdepend.html "PostgreSQL 10 -
53.48. pg_shdepend") / [9.6](/docs/9.6/catalog-pg-shdepend.html "PostgreSQL
9.6 - 53.48. pg_shdepend") / [9.5](/docs/9.5/catalog-pg-shdepend.html
"PostgreSQL 9.5 - 53.48. pg_shdepend") / [9.4](/docs/9.4/catalog-pg-
shdepend.html "PostgreSQL 9.4 - 53.48. pg_shdepend") /
[9.3](/docs/9.3/catalog-pg-shdepend.html "PostgreSQL 9.3 -
53.48. pg_shdepend") / [9.2](/docs/9.2/catalog-pg-shdepend.html "PostgreSQL
9.2 - 53.48. pg_shdepend") / [9.1](/docs/9.1/catalog-pg-shdepend.html
"PostgreSQL 9.1 - 53.48. pg_shdepend") / [9.0](/docs/9.0/catalog-pg-
shdepend.html "PostgreSQL 9.0 - 53.48. pg_shdepend") /
[8.4](/docs/8.4/catalog-pg-shdepend.html "PostgreSQL 8.4 -
53.48. pg_shdepend") / [8.3](/docs/8.3/catalog-pg-shdepend.html "PostgreSQL
8.3 - 53.48. pg_shdepend") / [8.2](/docs/8.2/catalog-pg-shdepend.html
"PostgreSQL 8.2 - 53.48. pg_shdepend") / [8.1](/docs/8.1/catalog-pg-
shdepend.html "PostgreSQL 8.1 - 53.48. pg_shdepend")

__

53.48. `pg_shdepend`  
---  
[Prev](catalog-pg-sequence.html "53.47. pg_sequence")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-shdescription.html "53.49. pg_shdescription")  
  
* * *

## 53.48. `pg_shdepend` #

The catalog `pg_shdepend` records the dependency relationships between
database objects and shared objects, such as roles. This information allows
PostgreSQL to ensure that those objects are unreferenced before attempting to
delete them.

See also [`pg_depend`](catalog-pg-depend.html "53.18. pg_depend"), which
performs a similar function for dependencies involving objects within a single
database.

Unlike most system catalogs, `pg_shdepend` is shared across all databases of a
cluster: there is only one copy of `pg_shdepend` per cluster, not one per
database.

**Table  53.48. `pg_shdepend` Columns**

Column Type Description  
---  
`dbid` `oid` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`oid`) The OID of the database the dependent object is
in, or zero for a shared object  
`classid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog the dependent object
is in  
`objid` `oid` (references any OID column) The OID of the specific dependent
object  
`objsubid` `int4` For a table column, this is the column number (the `objid`
and `classid` refer to the table itself). For all other object types, this
column is zero.  
`refclassid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog the referenced object
is in (must be a shared catalog)  
`refobjid` `oid` (references any OID column) The OID of the specific
referenced object  
`deptype` `char` A code defining the specific semantics of this dependency
relationship; see text  
  
  

In all cases, a `pg_shdepend` entry indicates that the referenced object
cannot be dropped without also dropping the dependent object. However, there
are several subflavors identified by `deptype`:

`SHARED_DEPENDENCY_OWNER` (`o`)

    

The referenced object (which must be a role) is the owner of the dependent
object.

`SHARED_DEPENDENCY_ACL` (`a`)

    

The referenced object (which must be a role) is mentioned in the ACL (access
control list, i.e., privileges list) of the dependent object. (A
`SHARED_DEPENDENCY_ACL` entry is not made for the owner of the object, since
the owner will have a `SHARED_DEPENDENCY_OWNER` entry anyway.)

`SHARED_DEPENDENCY_POLICY` (`r`)

    

The referenced object (which must be a role) is mentioned as the target of a
dependent policy object.

`SHARED_DEPENDENCY_TABLESPACE` (`t`)

    

The referenced object (which must be a tablespace) is mentioned as the
tablespace for a relation that doesn't have storage.

Other dependency flavors might be needed in future. Note in particular that
the current definition only supports roles and tablespaces as referenced
objects.

As in the `pg_depend` catalog, most objects created during initdb are
considered “pinned”. No entries are made in `pg_shdepend` that would have a
pinned object as either referenced or dependent object.

* * *

[Prev](catalog-pg-sequence.html "53.47. pg_sequence")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-shdescription.html "53.49. pg_shdescription")  
---|---|---  
53.47. `pg_sequence`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.49. `pg_shdescription`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-shdepend.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

