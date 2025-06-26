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

Supported Versions: [Current](/docs/current/catalog-pg-cast.html "PostgreSQL
17 - 53.10. pg_cast") ([17](/docs/17/catalog-pg-cast.html "PostgreSQL 17 -
53.10. pg_cast")) / [16](/docs/16/catalog-pg-cast.html "PostgreSQL 16 -
53.10. pg_cast") / [15](/docs/15/catalog-pg-cast.html "PostgreSQL 15 -
53.10. pg_cast") / [14](/docs/14/catalog-pg-cast.html "PostgreSQL 14 -
53.10. pg_cast") / [13](/docs/13/catalog-pg-cast.html "PostgreSQL 13 -
53.10. pg_cast")

Development Versions: [18](/docs/18/catalog-pg-cast.html "PostgreSQL 18 -
53.10. pg_cast") / [devel](/docs/devel/catalog-pg-cast.html "PostgreSQL devel
- 53.10. pg_cast")

Unsupported versions: [12](/docs/12/catalog-pg-cast.html "PostgreSQL 12 -
53.10. pg_cast") / [11](/docs/11/catalog-pg-cast.html "PostgreSQL 11 -
53.10. pg_cast") / [10](/docs/10/catalog-pg-cast.html "PostgreSQL 10 -
53.10. pg_cast") / [9.6](/docs/9.6/catalog-pg-cast.html "PostgreSQL 9.6 -
53.10. pg_cast") / [9.5](/docs/9.5/catalog-pg-cast.html "PostgreSQL 9.5 -
53.10. pg_cast") / [9.4](/docs/9.4/catalog-pg-cast.html "PostgreSQL 9.4 -
53.10. pg_cast") / [9.3](/docs/9.3/catalog-pg-cast.html "PostgreSQL 9.3 -
53.10. pg_cast") / [9.2](/docs/9.2/catalog-pg-cast.html "PostgreSQL 9.2 -
53.10. pg_cast") / [9.1](/docs/9.1/catalog-pg-cast.html "PostgreSQL 9.1 -
53.10. pg_cast") / [9.0](/docs/9.0/catalog-pg-cast.html "PostgreSQL 9.0 -
53.10. pg_cast") / [8.4](/docs/8.4/catalog-pg-cast.html "PostgreSQL 8.4 -
53.10. pg_cast") / [8.3](/docs/8.3/catalog-pg-cast.html "PostgreSQL 8.3 -
53.10. pg_cast") / [8.2](/docs/8.2/catalog-pg-cast.html "PostgreSQL 8.2 -
53.10. pg_cast") / [8.1](/docs/8.1/catalog-pg-cast.html "PostgreSQL 8.1 -
53.10. pg_cast") / [8.0](/docs/8.0/catalog-pg-cast.html "PostgreSQL 8.0 -
53.10. pg_cast") / [7.4](/docs/7.4/catalog-pg-cast.html "PostgreSQL 7.4 -
53.10. pg_cast") / [7.3](/docs/7.3/catalog-pg-cast.html "PostgreSQL 7.3 -
53.10. pg_cast")

__

53.10. `pg_cast`  
---  
[Prev](catalog-pg-auth-members.html "53.9. pg_auth_members")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-class.html "53.11. pg_class")  
  
* * *

## 53.10. `pg_cast` #

The catalog `pg_cast` stores data type conversion paths, both built-in and
user-defined.

It should be noted that `pg_cast` does not represent every type conversion
that the system knows how to perform; only those that cannot be deduced from
some generic rule. For example, casting between a domain and its base type is
not explicitly represented in `pg_cast`. Another important exception is that
“automatic I/O conversion casts”, those performed using a data type's own I/O
functions to convert to or from `text` or other string types, are not
explicitly represented in `pg_cast`.

**Table  53.10. `pg_cast` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`castsource` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) OID of the source data type  
`casttarget` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) OID of the target data type  
`castfunc` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) The OID of the function to use to perform this cast.
Zero is stored if the cast method doesn't require a function.  
`castcontext` `char` Indicates what contexts the cast can be invoked in. `e`
means only as an explicit cast (using `CAST` or `::` syntax). `a` means
implicitly in assignment to a target column, as well as explicitly. `i` means
implicitly in expressions, as well as the other cases.  
`castmethod` `char` Indicates how the cast is performed. `f` means that the
function specified in the `castfunc` field is used. `i` means that the
input/output functions are used. `b` means that the types are binary-
coercible, thus no conversion is required.  
  
  

The cast functions listed in `pg_cast` must always take the cast source type
as their first argument type, and return the cast destination type as their
result type. A cast function can have up to three arguments. The second
argument, if present, must be type `integer`; it receives the type modifier
associated with the destination type, or -1 if there is none. The third
argument, if present, must be type `boolean`; it receives `true` if the cast
is an explicit cast, `false` otherwise.

It is legitimate to create a `pg_cast` entry in which the source and target
types are the same, if the associated function takes more than one argument.
Such entries represent “length coercion functions” that coerce values of the
type to be legal for a particular type modifier value.

When a `pg_cast` entry has different source and target types and a function
that takes more than one argument, it represents converting from one type to
another and applying a length coercion in a single step. When no such entry is
available, coercion to a type that uses a type modifier involves two steps,
one to convert between data types and a second to apply the modifier.

* * *

[Prev](catalog-pg-auth-members.html "53.9. pg_auth_members")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-class.html "53.11. pg_class")  
---|---|---  
53.9. `pg_auth_members`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.11. `pg_class`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-cast.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

