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

Supported Versions: [Current](/docs/current/catalog-pg-type.html "PostgreSQL
17 - 53.64. pg_type") ([17](/docs/17/catalog-pg-type.html "PostgreSQL 17 -
53.64. pg_type")) / [16](/docs/16/catalog-pg-type.html "PostgreSQL 16 -
53.64. pg_type") / [15](/docs/15/catalog-pg-type.html "PostgreSQL 15 -
53.64. pg_type") / [14](/docs/14/catalog-pg-type.html "PostgreSQL 14 -
53.64. pg_type") / [13](/docs/13/catalog-pg-type.html "PostgreSQL 13 -
53.64. pg_type")

Development Versions: [18](/docs/18/catalog-pg-type.html "PostgreSQL 18 -
53.64. pg_type") / [devel](/docs/devel/catalog-pg-type.html "PostgreSQL devel
- 53.64. pg_type")

Unsupported versions: [12](/docs/12/catalog-pg-type.html "PostgreSQL 12 -
53.64. pg_type") / [11](/docs/11/catalog-pg-type.html "PostgreSQL 11 -
53.64. pg_type") / [10](/docs/10/catalog-pg-type.html "PostgreSQL 10 -
53.64. pg_type") / [9.6](/docs/9.6/catalog-pg-type.html "PostgreSQL 9.6 -
53.64. pg_type") / [9.5](/docs/9.5/catalog-pg-type.html "PostgreSQL 9.5 -
53.64. pg_type") / [9.4](/docs/9.4/catalog-pg-type.html "PostgreSQL 9.4 -
53.64. pg_type") / [9.3](/docs/9.3/catalog-pg-type.html "PostgreSQL 9.3 -
53.64. pg_type") / [9.2](/docs/9.2/catalog-pg-type.html "PostgreSQL 9.2 -
53.64. pg_type") / [9.1](/docs/9.1/catalog-pg-type.html "PostgreSQL 9.1 -
53.64. pg_type") / [9.0](/docs/9.0/catalog-pg-type.html "PostgreSQL 9.0 -
53.64. pg_type") / [8.4](/docs/8.4/catalog-pg-type.html "PostgreSQL 8.4 -
53.64. pg_type") / [8.3](/docs/8.3/catalog-pg-type.html "PostgreSQL 8.3 -
53.64. pg_type") / [8.2](/docs/8.2/catalog-pg-type.html "PostgreSQL 8.2 -
53.64. pg_type") / [8.1](/docs/8.1/catalog-pg-type.html "PostgreSQL 8.1 -
53.64. pg_type") / [8.0](/docs/8.0/catalog-pg-type.html "PostgreSQL 8.0 -
53.64. pg_type") / [7.4](/docs/7.4/catalog-pg-type.html "PostgreSQL 7.4 -
53.64. pg_type") / [7.3](/docs/7.3/catalog-pg-type.html "PostgreSQL 7.3 -
53.64. pg_type") / [7.2](/docs/7.2/catalog-pg-type.html "PostgreSQL 7.2 -
53.64. pg_type") / [7.1](/docs/7.1/catalog-pg-type.html "PostgreSQL 7.1 -
53.64. pg_type")

__

53.64. `pg_type`  
---  
[Prev](catalog-pg-ts-template.html "53.63. pg_ts_template")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-user-mapping.html "53.65. pg_user_mapping")  
  
* * *

## 53.64. `pg_type` #

The catalog `pg_type` stores information about data types. Base types and enum
types (scalar types) are created with [`CREATE TYPE`](sql-createtype.html
"CREATE TYPE"), and domains with [`CREATE DOMAIN`](sql-createdomain.html
"CREATE DOMAIN"). A composite type is automatically created for each table in
the database, to represent the row structure of the table. It is also possible
to create composite types with `CREATE TYPE AS`.

**Table  53.64. `pg_type` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`typname` `name` Data type name  
`typnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this type  
`typowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the type  
`typlen` `int2` For a fixed-size type, `typlen` is the number of bytes in the
internal representation of the type. But for a variable-length type, `typlen`
is negative. -1 indicates a “varlena” type (one that has a length word), -2
indicates a null-terminated C string.  
`typbyval` `bool` `typbyval` determines whether internal routines pass a value
of this type by value or by reference. `typbyval` had better be false if
`typlen` is not 1, 2, or 4 (or 8 on machines where Datum is 8 bytes).
Variable-length types are always passed by reference. Note that `typbyval` can
be false even if the length would allow pass-by-value.  
`typtype` `char` `typtype` is `b` for a base type, `c` for a composite type
(e.g., a table's row type), `d` for a domain, `e` for an enum type, `p` for a
pseudo-type, `r` for a range type, or `m` for a multirange type. See also
`typrelid` and `typbasetype`.  
`typcategory` `char` `typcategory` is an arbitrary classification of data
types that is used by the parser to determine which implicit casts should be
“preferred”. See [Table 53.65](catalog-pg-type.html#CATALOG-TYPCATEGORY-TABLE
"Table 53.65. typcategory Codes").  
`typispreferred` `bool` True if the type is a preferred cast target within its
`typcategory`  
`typisdefined` `bool` True if the type is defined, false if this is a
placeholder entry for a not-yet-defined type. When `typisdefined` is false,
nothing except the type name, namespace, and OID can be relied on.  
`typdelim` `char` Character that separates two values of this type when
parsing array input. Note that the delimiter is associated with the array
element data type, not the array data type.  
`typrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) If this is a composite type (see `typtype`), then
this column points to the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry that defines the corresponding table. (For a free-
standing composite type, the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry doesn't really represent a table, but it is needed
anyway for the type's [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute") entries to link to.) Zero for non-composite types.  
`typsubscript` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Subscripting handler function's OID, or zero if this
type doesn't support subscripting. Types that are “true” array types have
`typsubscript` = `array_subscript_handler`, but other types may have other
handler functions to implement specialized subscripting behavior.  
`typelem` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) If `typelem` is not zero then it identifies another
row in `pg_type`, defining the type yielded by subscripting. This should be
zero if `typsubscript` is zero. However, it can be zero when `typsubscript`
isn't zero, if the handler doesn't need `typelem` to determine the
subscripting result type. Note that a `typelem` dependency is considered to
imply physical containment of the element type in this type; so DDL changes on
the element type might be restricted by the presence of this type.  
`typarray` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) If `typarray` is not zero then it identifies another
row in `pg_type`, which is the “true” array type having this type as element  
`typinput` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Input conversion function (text format)  
`typoutput` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Output conversion function (text format)  
`typreceive` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Input conversion function (binary format), or zero if
none  
`typsend` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Output conversion function (binary format), or zero
if none  
`typmodin` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Type modifier input function, or zero if type does
not support modifiers  
`typmodout` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Type modifier output function, or zero to use the
standard format  
`typanalyze` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Custom [ANALYZE](sql-analyze.html "ANALYZE")
function, or zero to use the standard function  
`typalign` `char` `typalign` is the alignment required when storing a value of
this type. It applies to storage on disk as well as most representations of
the value inside PostgreSQL. When multiple values are stored consecutively,
such as in the representation of a complete row on disk, padding is inserted
before a datum of this type so that it begins on the specified boundary. The
alignment reference is the beginning of the first datum in the sequence.
Possible values are:

  * `c` = `char` alignment, i.e., no alignment needed.
  * `s` = `short` alignment (2 bytes on most machines).
  * `i` = `int` alignment (4 bytes on most machines).
  * `d` = `double` alignment (8 bytes on many machines, but by no means all).

  
`typstorage` `char` `typstorage` tells for varlena types (those with `typlen`
= -1) if the type is prepared for toasting and what the default strategy for
attributes of this type should be. Possible values are:

  * `p` (plain): Values must always be stored plain (non-varlena types always use this value).
  * `e` (external): Values can be stored in a secondary “TOAST” relation (if relation has one, see `pg_class.reltoastrelid`).
  * `m` (main): Values can be compressed and stored inline.
  * `x` (extended): Values can be compressed and/or moved to a secondary relation.

`x` is the usual choice for toast-able types. Note that `m` values can also be
moved out to secondary storage, but only as a last resort (`e` and `x` values
are moved first).  
`typnotnull` `bool` `typnotnull` represents a not-null constraint on a type.
Used for domains only.  
`typbasetype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) If this is a domain (see `typtype`), then
`typbasetype` identifies the type that this one is based on. Zero if this type
is not a domain.  
`typtypmod` `int4` Domains use `typtypmod` to record the `typmod` to be
applied to their base type (-1 if base type does not use a `typmod`). -1 if
this type is not a domain.  
`typndims` `int4` `typndims` is the number of array dimensions for a domain
over an array (that is, `typbasetype` is an array type). Zero for types other
than domains over array types.  
`typcollation` `oid` (references [`pg_collation`](catalog-pg-collation.html
"53.12. pg_collation").`oid`) `typcollation` specifies the collation of the
type. If the type does not support collations, this will be zero. A base type
that supports collations will have a nonzero value here, typically
`DEFAULT_COLLATION_OID`. A domain over a collatable type can have a collation
OID different from its base type's, if one was specified for the domain.  
`typdefaultbin` `pg_node_tree` If `typdefaultbin` is not null, it is the
`nodeToString()` representation of a default expression for the type. This is
only used for domains.  
`typdefault` `text` `typdefault` is null if the type has no associated default
value. If `typdefaultbin` is not null, `typdefault` must contain a human-
readable version of the default expression represented by `typdefaultbin`. If
`typdefaultbin` is null and `typdefault` is not, then `typdefault` is the
external representation of the type's default value, which can be fed to the
type's input converter to produce a constant.  
`typacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

### Note

For fixed-width types used in system tables, it is critical that the size and
alignment defined in `pg_type` agree with the way that the compiler will lay
out the column in a structure representing a table row.

[Table 53.65](catalog-pg-type.html#CATALOG-TYPCATEGORY-TABLE
"Table 53.65. typcategory Codes") lists the system-defined values of
`typcategory`. Any future additions to this list will also be upper-case ASCII
letters. All other ASCII characters are reserved for user-defined categories.

**Table  53.65. `typcategory` Codes**

Code | Category  
---|---  
`A` | Array types  
`B` | Boolean types  
`C` | Composite types  
`D` | Date/time types  
`E` | Enum types  
`G` | Geometric types  
`I` | Network address types  
`N` | Numeric types  
`P` | Pseudo-types  
`R` | Range types  
`S` | String types  
`T` | Timespan types  
`U` | User-defined types  
`V` | Bit-string types  
`X` | `unknown` type  
`Z` | Internal-use types  
  
  

* * *

[Prev](catalog-pg-ts-template.html "53.63. pg_ts_template")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-user-mapping.html "53.65. pg_user_mapping")  
---|---|---  
53.63. `pg_ts_template`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.65. `pg_user_mapping`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-type.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

