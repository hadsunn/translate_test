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

Supported Versions: [16](/docs/16/release-16-8.html "PostgreSQL 16 -
E.2. Release 16.8")

__

E.2. Release 16.8  
---  
[Prev](release-16-9.html "E.1. Release 16.9")  | [Up](release.html "Appendix E. Release Notes") | Appendix E. Release Notes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](release-16-7.html "E.3. Release 16.7")  
  
* * *

## E.2. Release 16.8 #

[E.2.1. Migration to Version 16.8](release-16-8.html#RELEASE-16-8-MIGRATION)

[E.2.2. Changes](release-16-8.html#RELEASE-16-8-CHANGES)

**Release date:  **2025-02-20

This release contains a few fixes from 16.7. For information about new
features in major release 16, see [Section E.10](release-16.html
"E.10. Release 16").

### E.2.1. Migration to Version 16.8 #

A dump/restore is not required for those running 16.X.

However, if you are upgrading from a version earlier than 16.5, see [Section
E.5](release-16-5.html "E.5. Release 16.5").

### E.2.2. Changes #

  * Improve behavior of libpq's quoting functions (Andres Freund, Tom Lane) [§](https://postgr.es/c/111f4dd27) [§](https://postgr.es/c/991a60a9f) [§](https://postgr.es/c/644b7d686)

The changes made for CVE-2025-1094 had one serious oversight:
`PQescapeLiteral()` and `PQescapeIdentifier()` failed to honor their string
length parameter, instead always reading to the input string's trailing null.
This resulted in including unwanted text in the output, if the caller intended
to truncate the string via the length parameter. With very bad luck it could
cause a crash due to reading off the end of memory.

In addition, modify all these quoting functions so that when invalid encoding
is detected, an invalid sequence is substituted for just the first byte of the
presumed character, not all of it. This reduces the risk of problems if a
calling application performs additional processing on the quoted string.

  * Fix meson build system to correctly detect availability of the `bsd_auth.h` system header (Nazir Bilal Yavuz) [§](https://postgr.es/c/01cdb98e4)

* * *

[Prev](release-16-9.html "E.1. Release 16.9")  | [Up](release.html "Appendix E. Release Notes") |  [Next](release-16-7.html "E.3. Release 16.7")  
---|---|---  
E.1. Release 16.9  | [Home](index.html "PostgreSQL 16.9 Documentation") |  E.3. Release 16.7  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/release-16-8.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

