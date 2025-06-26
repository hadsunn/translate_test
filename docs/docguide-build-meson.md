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

Supported Versions: [Current](/docs/current/docguide-build-meson.html
"PostgreSQL 17 - J.4. Building the Documentation with Meson")
([17](/docs/17/docguide-build-meson.html "PostgreSQL 17 - J.4. Building the
Documentation with Meson")) / [16](/docs/16/docguide-build-meson.html
"PostgreSQL 16 - J.4. Building the Documentation with Meson")

Development Versions: [18](/docs/18/docguide-build-meson.html "PostgreSQL 18 -
J.4. Building the Documentation with Meson") / [devel](/docs/devel/docguide-
build-meson.html "PostgreSQL devel - J.4. Building the Documentation with
Meson")

__

J.4. Building the Documentation with Meson  
---  
[Prev](docguide-build.html "J.3. Building the Documentation with Make")  | [Up](docguide.html "Appendix J. Documentation") | Appendix J. Documentation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](docguide-authoring.html "J.5. Documentation Authoring")  
  
* * *

## J.4. Building the Documentation with Meson #

Two options are provided for building the documentation using Meson. Change to
the `build` directory before running one of these commands, or add `-C build`
to the command.

To build just the HTML version of the documentation:

    
    
    build$ **ninja docs**
    

To build all forms of the documentation:

    
    
    build$ **ninja alldocs**
    

The output appears in the subdirectory `build/doc/src/sgml`.

* * *

[Prev](docguide-build.html "J.3. Building the Documentation with Make")  | [Up](docguide.html "Appendix J. Documentation") |  [Next](docguide-authoring.html "J.5. Documentation Authoring")  
---|---|---  
J.3. Building the Documentation with Make  | [Home](index.html "PostgreSQL 16.9 Documentation") |  J.5. Documentation Authoring  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/docguide-build-meson.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

