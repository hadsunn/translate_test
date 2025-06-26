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

Supported Versions: [Current](/docs/current/catalog-pg-depend.html "PostgreSQL
17 - 53.18. pg_depend") ([17](/docs/17/catalog-pg-depend.html "PostgreSQL 17 -
53.18. pg_depend")) / [16](/docs/16/catalog-pg-depend.html "PostgreSQL 16 -
53.18. pg_depend") / [15](/docs/15/catalog-pg-depend.html "PostgreSQL 15 -
53.18. pg_depend") / [14](/docs/14/catalog-pg-depend.html "PostgreSQL 14 -
53.18. pg_depend") / [13](/docs/13/catalog-pg-depend.html "PostgreSQL 13 -
53.18. pg_depend")

Development Versions: [18](/docs/18/catalog-pg-depend.html "PostgreSQL 18 -
53.18. pg_depend") / [devel](/docs/devel/catalog-pg-depend.html "PostgreSQL
devel - 53.18. pg_depend")

Unsupported versions: [12](/docs/12/catalog-pg-depend.html "PostgreSQL 12 -
53.18. pg_depend") / [11](/docs/11/catalog-pg-depend.html "PostgreSQL 11 -
53.18. pg_depend") / [10](/docs/10/catalog-pg-depend.html "PostgreSQL 10 -
53.18. pg_depend") / [9.6](/docs/9.6/catalog-pg-depend.html "PostgreSQL 9.6 -
53.18. pg_depend") / [9.5](/docs/9.5/catalog-pg-depend.html "PostgreSQL 9.5 -
53.18. pg_depend") / [9.4](/docs/9.4/catalog-pg-depend.html "PostgreSQL 9.4 -
53.18. pg_depend") / [9.3](/docs/9.3/catalog-pg-depend.html "PostgreSQL 9.3 -
53.18. pg_depend") / [9.2](/docs/9.2/catalog-pg-depend.html "PostgreSQL 9.2 -
53.18. pg_depend") / [9.1](/docs/9.1/catalog-pg-depend.html "PostgreSQL 9.1 -
53.18. pg_depend") / [9.0](/docs/9.0/catalog-pg-depend.html "PostgreSQL 9.0 -
53.18. pg_depend") / [8.4](/docs/8.4/catalog-pg-depend.html "PostgreSQL 8.4 -
53.18. pg_depend") / [8.3](/docs/8.3/catalog-pg-depend.html "PostgreSQL 8.3 -
53.18. pg_depend") / [8.2](/docs/8.2/catalog-pg-depend.html "PostgreSQL 8.2 -
53.18. pg_depend") / [8.1](/docs/8.1/catalog-pg-depend.html "PostgreSQL 8.1 -
53.18. pg_depend") / [8.0](/docs/8.0/catalog-pg-depend.html "PostgreSQL 8.0 -
53.18. pg_depend") / [7.4](/docs/7.4/catalog-pg-depend.html "PostgreSQL 7.4 -
53.18. pg_depend") / [7.3](/docs/7.3/catalog-pg-depend.html "PostgreSQL 7.3 -
53.18. pg_depend")

__

53.18. `pg_depend`  
---  
[Prev](catalog-pg-default-acl.html "53.17. pg_default_acl")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-description.html "53.19. pg_description")  
  
* * *

## 53.18. `pg_depend` #

The catalog `pg_depend` records the dependency relationships between database
objects. This information allows `DROP` commands to find which other objects
must be dropped by `DROP CASCADE` or prevent dropping in the `DROP RESTRICT`
case.

See also [`pg_shdepend`](catalog-pg-shdepend.html "53.48. pg_shdepend"), which
performs a similar function for dependencies involving objects that are shared
across a database cluster.

**Table  53.18. `pg_depend` Columns**

Column Type Description  
---  
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
is in  
`refobjid` `oid` (references any OID column) The OID of the specific
referenced object  
`refobjsubid` `int4` For a table column, this is the column number (the
`refobjid` and `refclassid` refer to the table itself). For all other object
types, this column is zero.  
`deptype` `char` A code defining the specific semantics of this dependency
relationship; see text  
  
  

In all cases, a `pg_depend` entry indicates that the referenced object cannot
be dropped without also dropping the dependent object. However, there are
several subflavors identified by `deptype`:

`DEPENDENCY_NORMAL` (`n`)

    

A normal relationship between separately-created objects. The dependent object
can be dropped without affecting the referenced object. The referenced object
can only be dropped by specifying `CASCADE`, in which case the dependent
object is dropped, too. Example: a table column has a normal dependency on its
data type.

`DEPENDENCY_AUTO` (`a`)

    

The dependent object can be dropped separately from the referenced object, and
should be automatically dropped (regardless of `RESTRICT` or `CASCADE` mode)
if the referenced object is dropped. Example: a named constraint on a table is
made auto-dependent on the table, so that it will go away if the table is
dropped.

`DEPENDENCY_INTERNAL` (`i`)

    

The dependent object was created as part of creation of the referenced object,
and is really just a part of its internal implementation. A direct `DROP` of
the dependent object will be disallowed outright (we'll tell the user to issue
a `DROP` against the referenced object, instead). A `DROP` of the referenced
object will result in automatically dropping the dependent object whether
`CASCADE` is specified or not. If the dependent object has to be dropped due
to a dependency on some other object being removed, its drop is converted to a
drop of the referenced object, so that `NORMAL` and `AUTO` dependencies of the
dependent object behave much like they were dependencies of the referenced
object. Example: a view's `ON SELECT` rule is made internally dependent on the
view, preventing it from being dropped while the view remains. Dependencies of
the rule (such as tables it refers to) act as if they were dependencies of the
view.

`DEPENDENCY_PARTITION_PRI` (`P`)  
`DEPENDENCY_PARTITION_SEC` (`S`)

    

The dependent object was created as part of creation of the referenced object,
and is really just a part of its internal implementation; however, unlike
`INTERNAL`, there is more than one such referenced object. The dependent
object must not be dropped unless at least one of these referenced objects is
dropped; if any one is, the dependent object should be dropped whether or not
`CASCADE` is specified. Also unlike `INTERNAL`, a drop of some other object
that the dependent object depends on does not result in automatic deletion of
any partition-referenced object. Hence, if the drop does not cascade to at
least one of these objects via some other path, it will be refused. (In most
cases, the dependent object shares all its non-partition dependencies with at
least one partition-referenced object, so that this restriction does not
result in blocking any cascaded delete.) Primary and secondary partition
dependencies behave identically except that the primary dependency is
preferred for use in error messages; hence, a partition-dependent object
should have one primary partition dependency and one or more secondary
partition dependencies. Note that partition dependencies are made in addition
to, not instead of, any dependencies the object would normally have. This
simplifies `ATTACH/DETACH PARTITION` operations: the partition dependencies
need only be added or removed. Example: a child partitioned index is made
partition-dependent on both the partition table it is on and the parent
partitioned index, so that it goes away if either of those is dropped, but not
otherwise. The dependency on the parent index is primary, so that if the user
tries to drop the child partitioned index, the error message will suggest
dropping the parent index instead (not the table).

`DEPENDENCY_EXTENSION` (`e`)

    

The dependent object is a member of the _extension_ that is the referenced
object (see [`pg_extension`](catalog-pg-extension.html
"53.22. pg_extension")). The dependent object can be dropped only via [`DROP
EXTENSION`](sql-dropextension.html "DROP EXTENSION") on the referenced object.
Functionally this dependency type acts the same as an `INTERNAL` dependency,
but it's kept separate for clarity and to simplify pg_dump.

`DEPENDENCY_AUTO_EXTENSION` (`x`)

    

The dependent object is not a member of the extension that is the referenced
object (and so it should not be ignored by pg_dump), but it cannot function
without the extension and should be auto-dropped if the extension is. The
dependent object may be dropped on its own as well. Functionally this
dependency type acts the same as an `AUTO` dependency, but it's kept separate
for clarity and to simplify pg_dump.

Other dependency flavors might be needed in future.

Note that it's quite possible for two objects to be linked by more than one
`pg_depend` entry. For example, a child partitioned index would have both a
partition-type dependency on its associated partition table, and an auto
dependency on each column of that table that it indexes. This sort of
situation expresses the union of multiple dependency semantics. A dependent
object can be dropped without `CASCADE` if any of its dependencies satisfies
its condition for automatic dropping. Conversely, all the dependencies'
restrictions about which objects must be dropped together must be satisfied.

Most objects created during initdb are considered “pinned”, which means that
the system itself depends on them. Therefore, they are never allowed to be
dropped. Also, knowing that pinned objects will not be dropped, the dependency
mechanism doesn't bother to make `pg_depend` entries showing dependencies on
them. Thus, for example, a table column of type `numeric` notionally has a
`NORMAL` dependency on the `numeric` data type, but no such entry actually
appears in `pg_depend`.

* * *

[Prev](catalog-pg-default-acl.html "53.17. pg_default_acl")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-description.html "53.19. pg_description")  
---|---|---  
53.17. `pg_default_acl`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.19. `pg_description`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-depend.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

