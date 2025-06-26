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

Supported Versions: [Current](/docs/current/uuid-ossp.html "PostgreSQL 17 -
F.49. uuid-ossp — a UUID generator") ([17](/docs/17/uuid-ossp.html "PostgreSQL
17 - F.49. uuid-ossp — a UUID generator")) / [16](/docs/16/uuid-ossp.html
"PostgreSQL 16 - F.49. uuid-ossp — a UUID generator") / [15](/docs/15/uuid-
ossp.html "PostgreSQL 15 - F.49. uuid-ossp — a UUID generator") /
[14](/docs/14/uuid-ossp.html "PostgreSQL 14 - F.49. uuid-ossp — a UUID
generator") / [13](/docs/13/uuid-ossp.html "PostgreSQL 13 - F.49. uuid-ossp —
a UUID generator")

Development Versions: [18](/docs/18/uuid-ossp.html "PostgreSQL 18 -
F.49. uuid-ossp — a UUID generator") / [devel](/docs/devel/uuid-ossp.html
"PostgreSQL devel - F.49. uuid-ossp — a UUID generator")

Unsupported versions: [12](/docs/12/uuid-ossp.html "PostgreSQL 12 -
F.49. uuid-ossp — a UUID generator") / [11](/docs/11/uuid-ossp.html
"PostgreSQL 11 - F.49. uuid-ossp — a UUID generator") / [10](/docs/10/uuid-
ossp.html "PostgreSQL 10 - F.49. uuid-ossp — a UUID generator") /
[9.6](/docs/9.6/uuid-ossp.html "PostgreSQL 9.6 - F.49. uuid-ossp — a UUID
generator") / [9.5](/docs/9.5/uuid-ossp.html "PostgreSQL 9.5 - F.49. uuid-ossp
— a UUID generator") / [9.4](/docs/9.4/uuid-ossp.html "PostgreSQL 9.4 -
F.49. uuid-ossp — a UUID generator") / [9.3](/docs/9.3/uuid-ossp.html
"PostgreSQL 9.3 - F.49. uuid-ossp — a UUID generator") / [9.2](/docs/9.2/uuid-
ossp.html "PostgreSQL 9.2 - F.49. uuid-ossp — a UUID generator") /
[9.1](/docs/9.1/uuid-ossp.html "PostgreSQL 9.1 - F.49. uuid-ossp — a UUID
generator") / [9.0](/docs/9.0/uuid-ossp.html "PostgreSQL 9.0 - F.49. uuid-ossp
— a UUID generator") / [8.4](/docs/8.4/uuid-ossp.html "PostgreSQL 8.4 -
F.49. uuid-ossp — a UUID generator") / [8.3](/docs/8.3/uuid-ossp.html
"PostgreSQL 8.3 - F.49. uuid-ossp — a UUID generator")

__

F.49. uuid-ossp — a UUID generator  
---  
[Prev](unaccent.html "F.48. unaccent — a text search dictionary which removes diacritics")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xml2.html "F.50. xml2 — XPath querying and XSLT functionality")  
  
* * *

## F.49. uuid-ossp — a UUID generator #

[F.49.1. `uuid-ossp` Functions](uuid-ossp.html#UUID-OSSP-FUNCTIONS-SECT)

[F.49.2. Building `uuid-ossp`](uuid-ossp.html#UUID-OSSP-BUILDING)

[F.49.3. Author](uuid-ossp.html#UUID-OSSP-AUTHOR)

The `uuid-ossp` module provides functions to generate universally unique
identifiers (UUIDs) using one of several standard algorithms. There are also
functions to produce certain special UUID constants. This module is only
necessary for special requirements beyond what is available in core
PostgreSQL. See [Section 9.14](functions-uuid.html "9.14. UUID Functions") for
built-in ways to generate UUIDs.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.49.1. `uuid-ossp` Functions #

[Table F.34](uuid-ossp.html#UUID-OSSP-FUNCTIONS "Table F.34. Functions for
UUID Generation") shows the functions available to generate UUIDs. The
relevant standards ITU-T Rec. X.667, ISO/IEC 9834-8:2005, and [RFC
4122](https://datatracker.ietf.org/doc/html/rfc4122) specify four algorithms
for generating UUIDs, identified by the version numbers 1, 3, 4, and 5. (There
is no version 2 algorithm.) Each of these algorithms could be suitable for a
different set of applications.

**Table  F.34. Functions for UUID Generation**

Function Description  
---  
`uuid_generate_v1` () → `uuid` Generates a version 1 UUID. This involves the
MAC address of the computer and a time stamp. Note that UUIDs of this kind
reveal the identity of the computer that created the identifier and the time
at which it did so, which might make it unsuitable for certain security-
sensitive applications.  
`uuid_generate_v1mc` () → `uuid` Generates a version 1 UUID, but uses a random
multicast MAC address instead of the real MAC address of the computer.  
`uuid_generate_v3` ( _`namespace`_ `uuid`, _`name`_ `text` ) → `uuid`
Generates a version 3 UUID in the given namespace using the specified input
name. The namespace should be one of the special constants produced by the
`uuid_ns_*()` functions shown in [Table F.35](uuid-ossp.html#UUID-OSSP-
CONSTANTS "Table F.35. Functions Returning UUID Constants"). (It could be any
UUID in theory.) The name is an identifier in the selected namespace. For
example:

    
    
    SELECT uuid_generate_v3(uuid_ns_url(), 'http://www.postgresql.org');
    

The name parameter will be MD5-hashed, so the cleartext cannot be derived from
the generated UUID. The generation of UUIDs by this method has no random or
environment-dependent element and is therefore reproducible.  
`uuid_generate_v4` () → `uuid` Generates a version 4 UUID, which is derived
entirely from random numbers.  
`uuid_generate_v5` ( _`namespace`_ `uuid`, _`name`_ `text` ) → `uuid`
Generates a version 5 UUID, which works like a version 3 UUID except that
SHA-1 is used as a hashing method. Version 5 should be preferred over version
3 because SHA-1 is thought to be more secure than MD5.  
  
  

**Table  F.35. Functions Returning UUID Constants**

Function Description  
---  
`uuid_nil` () → `uuid` Returns a “nil” UUID constant, which does not occur as
a real UUID.  
`uuid_ns_dns` () → `uuid` Returns a constant designating the DNS namespace for
UUIDs.  
`uuid_ns_url` () → `uuid` Returns a constant designating the URL namespace for
UUIDs.  
`uuid_ns_oid` () → `uuid` Returns a constant designating the ISO object
identifier (OID) namespace for UUIDs. (This pertains to ASN.1 OIDs, which are
unrelated to the OIDs used in PostgreSQL.)  
`uuid_ns_x500` () → `uuid` Returns a constant designating the X.500
distinguished name (DN) namespace for UUIDs.  
  
  

### F.49.2. Building `uuid-ossp` #

Historically this module depended on the OSSP UUID library, which accounts for
the module's name. While the OSSP UUID library can still be found at
<http://www.ossp.org/pkg/lib/uuid/>, it is not well maintained, and is
becoming increasingly difficult to port to newer platforms. `uuid-ossp` can
now be built without the OSSP library on some platforms. On FreeBSD and some
other BSD-derived platforms, suitable UUID creation functions are included in
the core `libc` library. On Linux, macOS, and some other platforms, suitable
functions are provided in the `libuuid` library, which originally came from
the `e2fsprogs` project (though on modern Linux it is considered part of
`util-linux-ng`). When invoking `configure`, specify `--with-uuid=bsd` to use
the BSD functions, or `--with-uuid=e2fs` to use `e2fsprogs`' `libuuid`, or
`--with-uuid=ossp` to use the OSSP UUID library. More than one of these
libraries might be available on a particular machine, so `configure` does not
automatically choose one.

### F.49.3. Author #

Peter Eisentraut `<[peter_e@gmx.net](mailto:peter_e@gmx.net)>`

* * *

[Prev](unaccent.html "F.48. unaccent — a text search dictionary which removes diacritics")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](xml2.html "F.50. xml2 — XPath querying and XSLT functionality")  
---|---|---  
F.48. unaccent — a text search dictionary which removes diacritics  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.50. xml2 — XPath querying and XSLT functionality  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/uuid-ossp.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

