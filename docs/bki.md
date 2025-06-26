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

Supported Versions: [Current](/docs/current/bki.html "PostgreSQL 17 -
Chapter 75. System Catalog Declarations and Initial Contents")
([17](/docs/17/bki.html "PostgreSQL 17 - Chapter 75. System Catalog
Declarations and Initial Contents")) / [16](/docs/16/bki.html "PostgreSQL 16 -
Chapter 75. System Catalog Declarations and Initial Contents") /
[15](/docs/15/bki.html "PostgreSQL 15 - Chapter 75. System Catalog
Declarations and Initial Contents") / [14](/docs/14/bki.html "PostgreSQL 14 -
Chapter 75. System Catalog Declarations and Initial Contents") /
[13](/docs/13/bki.html "PostgreSQL 13 - Chapter 75. System Catalog
Declarations and Initial Contents")

Development Versions: [18](/docs/18/bki.html "PostgreSQL 18 -
Chapter 75. System Catalog Declarations and Initial Contents") /
[devel](/docs/devel/bki.html "PostgreSQL devel - Chapter 75. System Catalog
Declarations and Initial Contents")

Unsupported versions: [12](/docs/12/bki.html "PostgreSQL 12 -
Chapter 75. System Catalog Declarations and Initial Contents") /
[11](/docs/11/bki.html "PostgreSQL 11 - Chapter 75. System Catalog
Declarations and Initial Contents") / [10](/docs/10/bki.html "PostgreSQL 10 -
Chapter 75. System Catalog Declarations and Initial Contents") /
[9.6](/docs/9.6/bki.html "PostgreSQL 9.6 - Chapter 75. System Catalog
Declarations and Initial Contents") / [9.5](/docs/9.5/bki.html "PostgreSQL 9.5
- Chapter 75. System Catalog Declarations and Initial Contents") /
[9.4](/docs/9.4/bki.html "PostgreSQL 9.4 - Chapter 75. System Catalog
Declarations and Initial Contents") / [9.3](/docs/9.3/bki.html "PostgreSQL 9.3
- Chapter 75. System Catalog Declarations and Initial Contents") /
[9.2](/docs/9.2/bki.html "PostgreSQL 9.2 - Chapter 75. System Catalog
Declarations and Initial Contents") / [9.1](/docs/9.1/bki.html "PostgreSQL 9.1
- Chapter 75. System Catalog Declarations and Initial Contents") /
[9.0](/docs/9.0/bki.html "PostgreSQL 9.0 - Chapter 75. System Catalog
Declarations and Initial Contents") / [8.4](/docs/8.4/bki.html "PostgreSQL 8.4
- Chapter 75. System Catalog Declarations and Initial Contents") /
[8.3](/docs/8.3/bki.html "PostgreSQL 8.3 - Chapter 75. System Catalog
Declarations and Initial Contents") / [8.2](/docs/8.2/bki.html "PostgreSQL 8.2
- Chapter 75. System Catalog Declarations and Initial Contents") /
[8.1](/docs/8.1/bki.html "PostgreSQL 8.1 - Chapter 75. System Catalog
Declarations and Initial Contents") / [8.0](/docs/8.0/bki.html "PostgreSQL 8.0
- Chapter 75. System Catalog Declarations and Initial Contents") /
[7.4](/docs/7.4/bki.html "PostgreSQL 7.4 - Chapter 75. System Catalog
Declarations and Initial Contents") / [7.3](/docs/7.3/bki.html "PostgreSQL 7.3
- Chapter 75. System Catalog Declarations and Initial Contents") /
[7.2](/docs/7.2/bki.html "PostgreSQL 7.2 - Chapter 75. System Catalog
Declarations and Initial Contents") / [7.1](/docs/7.1/bki.html "PostgreSQL 7.1
- Chapter 75. System Catalog Declarations and Initial Contents")

__

Chapter 75. System Catalog Declarations and Initial Contents  
---  
[Prev](two-phase.html "74.4. Two-Phase Transactions")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](system-catalog-declarations.html "75.1. System Catalog Declaration Rules")  
  
* * *

## Chapter 75. System Catalog Declarations and Initial Contents

**Table of Contents**

[75.1. System Catalog Declaration Rules](system-catalog-declarations.html)

[75.2. System Catalog Initial Data](system-catalog-initial-data.html)

    

[75.2.1. Data File Format](system-catalog-initial-data.html#SYSTEM-CATALOG-
INITIAL-DATA-FORMAT)

[75.2.2. OID Assignment](system-catalog-initial-data.html#SYSTEM-CATALOG-OID-
ASSIGNMENT)

[75.2.3. OID Reference Lookup](system-catalog-initial-data.html#SYSTEM-
CATALOG-OID-REFERENCES)

[75.2.4. Automatic Creation of Array Types](system-catalog-initial-
data.html#SYSTEM-CATALOG-AUTO-ARRAY-TYPES)

[75.2.5. Recipes for Editing Data Files](system-catalog-initial-
data.html#SYSTEM-CATALOG-RECIPES)

[75.3. BKI File Format](bki-format.html)

[75.4. BKI Commands](bki-commands.html)

[75.5. Structure of the Bootstrap BKI File](bki-structure.html)

[75.6. BKI Example](bki-example.html)

PostgreSQL uses many different system catalogs to keep track of the existence
and properties of database objects, such as tables and functions. Physically
there is no difference between a system catalog and a plain user table, but
the backend C code knows the structure and properties of each catalog, and can
manipulate it directly at a low level. Thus, for example, it is inadvisable to
attempt to alter the structure of a catalog on-the-fly; that would break
assumptions built into the C code about how rows of the catalog are laid out.
But the structure of the catalogs can change between major versions.

The structures of the catalogs are declared in specially formatted C header
files in the `src/include/catalog/` directory of the source tree. For each
catalog there is a header file named after the catalog (e.g., `pg_class.h` for
`pg_class`), which defines the set of columns the catalog has, as well as some
other basic properties such as its OID.

Many of the catalogs have initial data that must be loaded into them during
the “bootstrap” phase of initdb, to bring the system up to a point where it is
capable of executing SQL commands. (For example, `pg_class.h` must contain an
entry for itself, as well as one for each other system catalog and index.)
This initial data is kept in editable form in data files that are also stored
in the `src/include/catalog/` directory. For example, `pg_proc.dat` describes
all the initial rows that must be inserted into the `pg_proc` catalog.

To create the catalog files and load this initial data into them, a backend
running in bootstrap mode reads a BKI (Backend Interface) file containing
commands and initial data. The `postgres.bki` file used in this mode is
prepared from the aforementioned header and data files, while building a
PostgreSQL distribution, by a Perl script named `genbki.pl`. Although it's
specific to a particular PostgreSQL release, `postgres.bki` is platform-
independent and is installed in the `share` subdirectory of the installation
tree.

`genbki.pl` also produces a derived header file for each catalog, for example
`pg_class_d.h` for the `pg_class` catalog. This file contains automatically-
generated macro definitions, and may contain other macros, enum declarations,
and so on that can be useful for client C code that reads a particular
catalog.

Most PostgreSQL developers don't need to be directly concerned with the BKI
file, but almost any nontrivial feature addition in the backend will require
modifying the catalog header files and/or initial data files. The rest of this
chapter gives some information about that, and for completeness describes the
BKI file format.

* * *

[Prev](two-phase.html "74.4. Two-Phase Transactions")  | [Up](internals.html "Part VII. Internals") |  [Next](system-catalog-declarations.html "75.1. System Catalog Declaration Rules")  
---|---|---  
74.4. Two-Phase Transactions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  75.1. System Catalog Declaration Rules  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/bki.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

