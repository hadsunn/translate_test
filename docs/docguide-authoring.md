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

Supported Versions: [Current](/docs/current/docguide-authoring.html
"PostgreSQL 17 - J.5. Documentation Authoring") ([17](/docs/17/docguide-
authoring.html "PostgreSQL 17 - J.5. Documentation Authoring")) /
[16](/docs/16/docguide-authoring.html "PostgreSQL 16 - J.5. Documentation
Authoring") / [15](/docs/15/docguide-authoring.html "PostgreSQL 15 -
J.5. Documentation Authoring") / [14](/docs/14/docguide-authoring.html
"PostgreSQL 14 - J.5. Documentation Authoring") / [13](/docs/13/docguide-
authoring.html "PostgreSQL 13 - J.5. Documentation Authoring")

Development Versions: [18](/docs/18/docguide-authoring.html "PostgreSQL 18 -
J.5. Documentation Authoring") / [devel](/docs/devel/docguide-authoring.html
"PostgreSQL devel - J.5. Documentation Authoring")

Unsupported versions: [12](/docs/12/docguide-authoring.html "PostgreSQL 12 -
J.5. Documentation Authoring") / [11](/docs/11/docguide-authoring.html
"PostgreSQL 11 - J.5. Documentation Authoring") / [10](/docs/10/docguide-
authoring.html "PostgreSQL 10 - J.5. Documentation Authoring") /
[9.6](/docs/9.6/docguide-authoring.html "PostgreSQL 9.6 - J.5. Documentation
Authoring") / [9.5](/docs/9.5/docguide-authoring.html "PostgreSQL 9.5 -
J.5. Documentation Authoring") / [9.4](/docs/9.4/docguide-authoring.html
"PostgreSQL 9.4 - J.5. Documentation Authoring") / [9.3](/docs/9.3/docguide-
authoring.html "PostgreSQL 9.3 - J.5. Documentation Authoring") /
[9.2](/docs/9.2/docguide-authoring.html "PostgreSQL 9.2 - J.5. Documentation
Authoring") / [9.1](/docs/9.1/docguide-authoring.html "PostgreSQL 9.1 -
J.5. Documentation Authoring") / [9.0](/docs/9.0/docguide-authoring.html
"PostgreSQL 9.0 - J.5. Documentation Authoring") / [8.4](/docs/8.4/docguide-
authoring.html "PostgreSQL 8.4 - J.5. Documentation Authoring") /
[8.3](/docs/8.3/docguide-authoring.html "PostgreSQL 8.3 - J.5. Documentation
Authoring") / [8.2](/docs/8.2/docguide-authoring.html "PostgreSQL 8.2 -
J.5. Documentation Authoring") / [8.1](/docs/8.1/docguide-authoring.html
"PostgreSQL 8.1 - J.5. Documentation Authoring") / [8.0](/docs/8.0/docguide-
authoring.html "PostgreSQL 8.0 - J.5. Documentation Authoring") /
[7.4](/docs/7.4/docguide-authoring.html "PostgreSQL 7.4 - J.5. Documentation
Authoring")

__

J.5. Documentation Authoring  
---  
[Prev](docguide-build-meson.html "J.4. Building the Documentation with Meson")  | [Up](docguide.html "Appendix J. Documentation") | Appendix J. Documentation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](docguide-style.html "J.6. Style Guide")  
  
* * *

## J.5. Documentation Authoring #

[J.5.1. Emacs](docguide-authoring.html#DOCGUIDE-AUTHORING-EMACS)

The documentation sources are most conveniently modified with an editor that
has a mode for editing XML, and even more so if it has some awareness of XML
schema languages so that it can know about DocBook syntax specifically.

Note that for historical reasons the documentation source files are named with
an extension `.sgml` even though they are now XML files. So you might need to
adjust your editor configuration to set the correct mode.

### J.5.1. Emacs #

nXML Mode, which ships with Emacs, is the most common mode for editing XML
documents with Emacs. It will allow you to use Emacs to insert tags and check
markup consistency, and it supports DocBook out of the box. Check the [nXML
manual](https://www.gnu.org/software/emacs/manual/html_mono/nxml-mode.html)
for detailed documentation.

`src/tools/editors/emacs.samples` contains recommended settings for this mode.

* * *

[Prev](docguide-build-meson.html "J.4. Building the Documentation with Meson")  | [Up](docguide.html "Appendix J. Documentation") |  [Next](docguide-style.html "J.6. Style Guide")  
---|---|---  
J.4. Building the Documentation with Meson  | [Home](index.html "PostgreSQL 16.9 Documentation") |  J.6. Style Guide  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/docguide-authoring.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

