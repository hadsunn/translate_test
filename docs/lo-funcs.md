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

Supported Versions: [Current](/docs/current/lo-funcs.html "PostgreSQL 17 -
35.4. Server-Side Functions") ([17](/docs/17/lo-funcs.html "PostgreSQL 17 -
35.4. Server-Side Functions")) / [16](/docs/16/lo-funcs.html "PostgreSQL 16 -
35.4. Server-Side Functions") / [15](/docs/15/lo-funcs.html "PostgreSQL 15 -
35.4. Server-Side Functions") / [14](/docs/14/lo-funcs.html "PostgreSQL 14 -
35.4. Server-Side Functions") / [13](/docs/13/lo-funcs.html "PostgreSQL 13 -
35.4. Server-Side Functions")

Development Versions: [18](/docs/18/lo-funcs.html "PostgreSQL 18 -
35.4. Server-Side Functions") / [devel](/docs/devel/lo-funcs.html "PostgreSQL
devel - 35.4. Server-Side Functions")

Unsupported versions: [12](/docs/12/lo-funcs.html "PostgreSQL 12 -
35.4. Server-Side Functions") / [11](/docs/11/lo-funcs.html "PostgreSQL 11 -
35.4. Server-Side Functions") / [10](/docs/10/lo-funcs.html "PostgreSQL 10 -
35.4. Server-Side Functions") / [9.6](/docs/9.6/lo-funcs.html "PostgreSQL 9.6
- 35.4. Server-Side Functions") / [9.5](/docs/9.5/lo-funcs.html "PostgreSQL
9.5 - 35.4. Server-Side Functions") / [9.4](/docs/9.4/lo-funcs.html
"PostgreSQL 9.4 - 35.4. Server-Side Functions") / [9.3](/docs/9.3/lo-
funcs.html "PostgreSQL 9.3 - 35.4. Server-Side Functions") /
[9.2](/docs/9.2/lo-funcs.html "PostgreSQL 9.2 - 35.4. Server-Side Functions")
/ [9.1](/docs/9.1/lo-funcs.html "PostgreSQL 9.1 - 35.4. Server-Side
Functions") / [9.0](/docs/9.0/lo-funcs.html "PostgreSQL 9.0 - 35.4. Server-
Side Functions") / [8.4](/docs/8.4/lo-funcs.html "PostgreSQL 8.4 -
35.4. Server-Side Functions") / [8.3](/docs/8.3/lo-funcs.html "PostgreSQL 8.3
- 35.4. Server-Side Functions") / [8.2](/docs/8.2/lo-funcs.html "PostgreSQL
8.2 - 35.4. Server-Side Functions") / [8.1](/docs/8.1/lo-funcs.html
"PostgreSQL 8.1 - 35.4. Server-Side Functions") / [8.0](/docs/8.0/lo-
funcs.html "PostgreSQL 8.0 - 35.4. Server-Side Functions") /
[7.4](/docs/7.4/lo-funcs.html "PostgreSQL 7.4 - 35.4. Server-Side Functions")
/ [7.3](/docs/7.3/lo-funcs.html "PostgreSQL 7.3 - 35.4. Server-Side
Functions") / [7.2](/docs/7.2/lo-funcs.html "PostgreSQL 7.2 - 35.4. Server-
Side Functions") / [7.1](/docs/7.1/lo-funcs.html "PostgreSQL 7.1 -
35.4. Server-Side Functions")

__

35.4. Server-Side Functions  
---  
[Prev](lo-interfaces.html "35.3. Client Interfaces")  | [Up](largeobjects.html "Chapter 35. Large Objects") | Chapter 35. Large Objects | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](lo-examplesect.html "35.5. Example Program")  
  
* * *

## 35.4. Server-Side Functions #

Server-side functions tailored for manipulating large objects from SQL are
listed in [Table 35.1](lo-funcs.html#LO-FUNCS-TABLE "Table 35.1. SQL-Oriented
Large Object Functions").

**Table  35.1. SQL-Oriented Large Object Functions**

Function Description Example(s)  
---  
`lo_from_bytea` ( _`loid`_ `oid`, _`data`_ `bytea` ) → `oid` Creates a large
object and stores _`data`_ in it. If _`loid`_ is zero then the system will
choose a free OID, otherwise that OID is used (with an error if some large
object already has that OID). On success, the large object's OID is returned.
`lo_from_bytea(0, '\xffffff00')` → `24528`  
`lo_put` ( _`loid`_ `oid`, _`offset`_ `bigint`, _`data`_ `bytea` ) → `void`
Writes _`data`_ starting at the given offset within the large object; the
large object is enlarged if necessary. `lo_put(24528, 1, '\xaa')` →  
`lo_get` ( _`loid`_ `oid` [, _`offset`_ `bigint`, _`length`_ `integer` ] ) →
`bytea` Extracts the large object's contents, or a substring thereof.
`lo_get(24528, 0, 3)` → `\xffaaff`  
  
  

There are additional server-side functions corresponding to each of the
client-side functions described earlier; indeed, for the most part the client-
side functions are simply interfaces to the equivalent server-side functions.
The ones just as convenient to call via SQL commands are `lo_creat`,
`lo_create`, `lo_unlink`, `lo_import`, and `lo_export`. Here are examples of
their use:

    
    
    CREATE TABLE image (
        name            text,
        raster          oid
    );
    
    SELECT lo_creat(-1);       -- returns OID of new, empty large object
    
    SELECT lo_create(43213);   -- attempts to create large object with OID 43213
    
    SELECT lo_unlink(173454);  -- deletes large object with OID 173454
    
    INSERT INTO image (name, raster)
        VALUES ('beautiful image', lo_import('/etc/motd'));
    
    INSERT INTO image (name, raster)  -- same as above, but specify OID to use
        VALUES ('beautiful image', lo_import('/etc/motd', 68583));
    
    SELECT lo_export(image.raster, '/tmp/motd') FROM image
        WHERE name = 'beautiful image';
    

The server-side `lo_import` and `lo_export` functions behave considerably
differently from their client-side analogs. These two functions read and write
files in the server's file system, using the permissions of the database's
owning user. Therefore, by default their use is restricted to superusers. In
contrast, the client-side import and export functions read and write files in
the client's file system, using the permissions of the client program. The
client-side functions do not require any database privileges, except the
privilege to read or write the large object in question.

### Caution

It is possible to [GRANT](sql-grant.html "GRANT") use of the server-side
`lo_import` and `lo_export` functions to non-superusers, but careful
consideration of the security implications is required. A malicious user of
such privileges could easily parlay them into becoming superuser (for example
by rewriting server configuration files), or could attack the rest of the
server's file system without bothering to obtain database superuser privileges
as such. _Access to roles having such privilege must therefore be guarded just
as carefully as access to superuser roles._ Nonetheless, if use of server-side
`lo_import` or `lo_export` is needed for some routine task, it's safer to use
a role with such privileges than one with full superuser privileges, as that
helps to reduce the risk of damage from accidental errors.

The functionality of `lo_read` and `lo_write` is also available via server-
side calls, but the names of the server-side functions differ from the client
side interfaces in that they do not contain underscores. You must call these
functions as `loread` and `lowrite`.

* * *

[Prev](lo-interfaces.html "35.3. Client Interfaces")  | [Up](largeobjects.html "Chapter 35. Large Objects") |  [Next](lo-examplesect.html "35.5. Example Program")  
---|---|---  
35.3. Client Interfaces  | [Home](index.html "PostgreSQL 16.9 Documentation") |  35.5. Example Program  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/lo-funcs.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

