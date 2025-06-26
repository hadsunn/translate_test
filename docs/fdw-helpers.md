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

Supported Versions: [Current](/docs/current/fdw-helpers.html "PostgreSQL 17 -
59.3. Foreign Data Wrapper Helper Functions") ([17](/docs/17/fdw-helpers.html
"PostgreSQL 17 - 59.3. Foreign Data Wrapper Helper Functions")) /
[16](/docs/16/fdw-helpers.html "PostgreSQL 16 - 59.3. Foreign Data Wrapper
Helper Functions") / [15](/docs/15/fdw-helpers.html "PostgreSQL 15 -
59.3. Foreign Data Wrapper Helper Functions") / [14](/docs/14/fdw-helpers.html
"PostgreSQL 14 - 59.3. Foreign Data Wrapper Helper Functions") /
[13](/docs/13/fdw-helpers.html "PostgreSQL 13 - 59.3. Foreign Data Wrapper
Helper Functions")

Development Versions: [18](/docs/18/fdw-helpers.html "PostgreSQL 18 -
59.3. Foreign Data Wrapper Helper Functions") / [devel](/docs/devel/fdw-
helpers.html "PostgreSQL devel - 59.3. Foreign Data Wrapper Helper Functions")

Unsupported versions: [12](/docs/12/fdw-helpers.html "PostgreSQL 12 -
59.3. Foreign Data Wrapper Helper Functions") / [11](/docs/11/fdw-helpers.html
"PostgreSQL 11 - 59.3. Foreign Data Wrapper Helper Functions") /
[10](/docs/10/fdw-helpers.html "PostgreSQL 10 - 59.3. Foreign Data Wrapper
Helper Functions") / [9.6](/docs/9.6/fdw-helpers.html "PostgreSQL 9.6 -
59.3. Foreign Data Wrapper Helper Functions") / [9.5](/docs/9.5/fdw-
helpers.html "PostgreSQL 9.5 - 59.3. Foreign Data Wrapper Helper Functions") /
[9.4](/docs/9.4/fdw-helpers.html "PostgreSQL 9.4 - 59.3. Foreign Data Wrapper
Helper Functions") / [9.3](/docs/9.3/fdw-helpers.html "PostgreSQL 9.3 -
59.3. Foreign Data Wrapper Helper Functions") / [9.2](/docs/9.2/fdw-
helpers.html "PostgreSQL 9.2 - 59.3. Foreign Data Wrapper Helper Functions")

__

59.3. Foreign Data Wrapper Helper Functions  
---  
[Prev](fdw-callbacks.html "59.2. Foreign Data Wrapper Callback Routines")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") | Chapter 59. Writing a Foreign Data Wrapper | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](fdw-planning.html "59.4. Foreign Data Wrapper Query Planning")  
  
* * *

## 59.3. Foreign Data Wrapper Helper Functions #

Several helper functions are exported from the core server so that authors of
foreign data wrappers can get easy access to attributes of FDW-related
objects, such as FDW options. To use any of these functions, you need to
include the header file `foreign/foreign.h` in your source file. That header
also defines the struct types that are returned by these functions.

    
    
    ForeignDataWrapper *
    GetForeignDataWrapperExtended(Oid fdwid, bits16 flags);
    

This function returns a `ForeignDataWrapper` object for the foreign-data
wrapper with the given OID. A `ForeignDataWrapper` object contains properties
of the FDW (see `foreign/foreign.h` for details). `flags` is a bitwise-or'd
bit mask indicating an extra set of options. It can take the value
`FDW_MISSING_OK`, in which case a `NULL` result is returned to the caller
instead of an error for an undefined object.

    
    
    ForeignDataWrapper *
    GetForeignDataWrapper(Oid fdwid);
    

This function returns a `ForeignDataWrapper` object for the foreign-data
wrapper with the given OID. A `ForeignDataWrapper` object contains properties
of the FDW (see `foreign/foreign.h` for details).

    
    
    ForeignServer *
    GetForeignServerExtended(Oid serverid, bits16 flags);
    

This function returns a `ForeignServer` object for the foreign server with the
given OID. A `ForeignServer` object contains properties of the server (see
`foreign/foreign.h` for details). `flags` is a bitwise-or'd bit mask
indicating an extra set of options. It can take the value `FSV_MISSING_OK`, in
which case a `NULL` result is returned to the caller instead of an error for
an undefined object.

    
    
    ForeignServer *
    GetForeignServer(Oid serverid);
    

This function returns a `ForeignServer` object for the foreign server with the
given OID. A `ForeignServer` object contains properties of the server (see
`foreign/foreign.h` for details).

    
    
    UserMapping *
    GetUserMapping(Oid userid, Oid serverid);
    

This function returns a `UserMapping` object for the user mapping of the given
role on the given server. (If there is no mapping for the specific user, it
will return the mapping for `PUBLIC`, or throw error if there is none.) A
`UserMapping` object contains properties of the user mapping (see
`foreign/foreign.h` for details).

    
    
    ForeignTable *
    GetForeignTable(Oid relid);
    

This function returns a `ForeignTable` object for the foreign table with the
given OID. A `ForeignTable` object contains properties of the foreign table
(see `foreign/foreign.h` for details).

    
    
    List *
    GetForeignColumnOptions(Oid relid, AttrNumber attnum);
    

This function returns the per-column FDW options for the column with the given
foreign table OID and attribute number, in the form of a list of `DefElem`.
NIL is returned if the column has no options.

Some object types have name-based lookup functions in addition to the OID-
based ones:

    
    
    ForeignDataWrapper *
    GetForeignDataWrapperByName(const char *name, bool missing_ok);
    

This function returns a `ForeignDataWrapper` object for the foreign-data
wrapper with the given name. If the wrapper is not found, return NULL if
missing_ok is true, otherwise raise an error.

    
    
    ForeignServer *
    GetForeignServerByName(const char *name, bool missing_ok);
    

This function returns a `ForeignServer` object for the foreign server with the
given name. If the server is not found, return NULL if missing_ok is true,
otherwise raise an error.

* * *

[Prev](fdw-callbacks.html "59.2. Foreign Data Wrapper Callback Routines")  | [Up](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper") |  [Next](fdw-planning.html "59.4. Foreign Data Wrapper Query Planning")  
---|---|---  
59.2. Foreign Data Wrapper Callback Routines  | [Home](index.html "PostgreSQL 16.9 Documentation") |  59.4. Foreign Data Wrapper Query Planning  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/fdw-helpers.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

