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

Supported Versions: [Current](/docs/current/system-catalog-declarations.html
"PostgreSQL 17 - 75.1. System Catalog Declaration Rules")
([17](/docs/17/system-catalog-declarations.html "PostgreSQL 17 - 75.1. System
Catalog Declaration Rules")) / [16](/docs/16/system-catalog-declarations.html
"PostgreSQL 16 - 75.1. System Catalog Declaration Rules") /
[15](/docs/15/system-catalog-declarations.html "PostgreSQL 15 - 75.1. System
Catalog Declaration Rules") / [14](/docs/14/system-catalog-declarations.html
"PostgreSQL 14 - 75.1. System Catalog Declaration Rules") /
[13](/docs/13/system-catalog-declarations.html "PostgreSQL 13 - 75.1. System
Catalog Declaration Rules")

Development Versions: [18](/docs/18/system-catalog-declarations.html
"PostgreSQL 18 - 75.1. System Catalog Declaration Rules") /
[devel](/docs/devel/system-catalog-declarations.html "PostgreSQL devel -
75.1. System Catalog Declaration Rules")

Unsupported versions: [12](/docs/12/system-catalog-declarations.html
"PostgreSQL 12 - 75.1. System Catalog Declaration Rules") /
[11](/docs/11/system-catalog-declarations.html "PostgreSQL 11 - 75.1. System
Catalog Declaration Rules")

__

75.1. System Catalog Declaration Rules  
---  
[Prev](bki.html "Chapter 75. System Catalog Declarations and Initial Contents")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") | Chapter 75. System Catalog Declarations and Initial Contents | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](system-catalog-initial-data.html "75.2. System Catalog Initial Data")  
  
* * *

## 75.1. System Catalog Declaration Rules #

The key part of a catalog header file is a C structure definition describing
the layout of each row of the catalog. This begins with a `CATALOG` macro,
which so far as the C compiler is concerned is just shorthand for `typedef
struct FormData__`catalogname`_`. Each field in the struct gives rise to a
catalog column. Fields can be annotated using the BKI property macros
described in `genbki.h`, for example to define a default value for a field or
mark it as nullable or not nullable. The `CATALOG` line can also be annotated,
with some other BKI property macros described in `genbki.h`, to define other
properties of the catalog as a whole, such as whether it is a shared relation.

The system catalog cache code (and most catalog-munging code in general)
assumes that the fixed-length portions of all system catalog tuples are in
fact present, because it maps this C struct declaration onto them. Thus, all
variable-length fields and nullable fields must be placed at the end, and they
cannot be accessed as struct fields. For example, if you tried to set
`pg_type`.`typrelid` to be NULL, it would fail when some piece of code tried
to reference `typetup->typrelid` (or worse, `typetup->typelem`, because that
follows `typrelid`). This would result in random errors or even segmentation
violations.

As a partial guard against this type of error, variable-length or nullable
fields should not be made directly visible to the C compiler. This is
accomplished by wrapping them in `#ifdef CATALOG_VARLEN` ... `#endif` (where
`CATALOG_VARLEN` is a symbol that is never defined). This prevents C code from
carelessly trying to access fields that might not be there or might be at some
other offset. As an independent guard against creating incorrect rows, we
require all columns that should be non-nullable to be marked so in
`pg_attribute`. The bootstrap code will automatically mark catalog columns as
`NOT NULL` if they are fixed-width and are not preceded by any nullable or
variable-width column. Where this rule is inadequate, you can force correct
marking by using `BKI_FORCE_NOT_NULL` and `BKI_FORCE_NULL` annotations as
needed.

Frontend code should not include any `pg_xxx.h` catalog header file, as these
files may contain C code that won't compile outside the backend. (Typically,
that happens because these files also contain declarations for functions in
`src/backend/catalog/` files.) Instead, frontend code may include the
corresponding generated `pg_xxx_d.h` header, which will contain OID `#define`s
and any other data that might be of use on the client side. If you want macros
or other code in a catalog header to be visible to frontend code, write
`#ifdef EXPOSE_TO_CLIENT_CODE` ... `#endif` around that section to instruct
`genbki.pl` to copy that section to the `pg_xxx_d.h` header.

A few of the catalogs are so fundamental that they can't even be created by
the BKI `create` command that's used for most catalogs, because that command
needs to write information into these catalogs to describe the new catalog.
These are called _bootstrap_ catalogs, and defining one takes a lot of extra
work: you have to manually prepare appropriate entries for them in the pre-
loaded contents of `pg_class` and `pg_type`, and those entries will need to be
updated for subsequent changes to the catalog's structure. (Bootstrap catalogs
also need pre-loaded entries in `pg_attribute`, but fortunately `genbki.pl`
handles that chore nowadays.) Avoid making new catalogs be bootstrap catalogs
if at all possible.

* * *

[Prev](bki.html "Chapter 75. System Catalog Declarations and Initial Contents")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") |  [Next](system-catalog-initial-data.html "75.2. System Catalog Initial Data")  
---|---|---  
Chapter 75. System Catalog Declarations and Initial Contents  | [Home](index.html "PostgreSQL 16.9 Documentation") |  75.2. System Catalog Initial Data  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/system-catalog-
declarations.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

