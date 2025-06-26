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

Supported Versions: [Current](/docs/current/installation.html "PostgreSQL 17 -
Chapter 17. Installation from Source Code") ([17](/docs/17/installation.html
"PostgreSQL 17 - Chapter 17. Installation from Source Code")) /
[16](/docs/16/installation.html "PostgreSQL 16 - Chapter 17. Installation from
Source Code") / [15](/docs/15/installation.html "PostgreSQL 15 -
Chapter 17. Installation from Source Code") / [14](/docs/14/installation.html
"PostgreSQL 14 - Chapter 17. Installation from Source Code") /
[13](/docs/13/installation.html "PostgreSQL 13 - Chapter 17. Installation from
Source Code")

Development Versions: [18](/docs/18/installation.html "PostgreSQL 18 -
Chapter 17. Installation from Source Code") /
[devel](/docs/devel/installation.html "PostgreSQL devel -
Chapter 17. Installation from Source Code")

Unsupported versions: [12](/docs/12/installation.html "PostgreSQL 12 -
Chapter 17. Installation from Source Code") / [11](/docs/11/installation.html
"PostgreSQL 11 - Chapter 17. Installation from Source Code") /
[10](/docs/10/installation.html "PostgreSQL 10 - Chapter 17. Installation from
Source Code") / [9.6](/docs/9.6/installation.html "PostgreSQL 9.6 -
Chapter 17. Installation from Source Code") /
[9.5](/docs/9.5/installation.html "PostgreSQL 9.5 - Chapter 17. Installation
from Source Code") / [9.4](/docs/9.4/installation.html "PostgreSQL 9.4 -
Chapter 17. Installation from Source Code") /
[9.3](/docs/9.3/installation.html "PostgreSQL 9.3 - Chapter 17. Installation
from Source Code") / [9.2](/docs/9.2/installation.html "PostgreSQL 9.2 -
Chapter 17. Installation from Source Code") /
[9.1](/docs/9.1/installation.html "PostgreSQL 9.1 - Chapter 17. Installation
from Source Code") / [9.0](/docs/9.0/installation.html "PostgreSQL 9.0 -
Chapter 17. Installation from Source Code") /
[8.4](/docs/8.4/installation.html "PostgreSQL 8.4 - Chapter 17. Installation
from Source Code") / [8.3](/docs/8.3/installation.html "PostgreSQL 8.3 -
Chapter 17. Installation from Source Code") /
[8.2](/docs/8.2/installation.html "PostgreSQL 8.2 - Chapter 17. Installation
from Source Code") / [8.1](/docs/8.1/installation.html "PostgreSQL 8.1 -
Chapter 17. Installation from Source Code") /
[8.0](/docs/8.0/installation.html "PostgreSQL 8.0 - Chapter 17. Installation
from Source Code") / [7.4](/docs/7.4/installation.html "PostgreSQL 7.4 -
Chapter 17. Installation from Source Code") /
[7.3](/docs/7.3/installation.html "PostgreSQL 7.3 - Chapter 17. Installation
from Source Code") / [7.2](/docs/7.2/installation.html "PostgreSQL 7.2 -
Chapter 17. Installation from Source Code") /
[7.1](/docs/7.1/installation.html "PostgreSQL 7.1 - Chapter 17. Installation
from Source Code")

__

Chapter 17. Installation from Source Code  
---  
[Prev](install-binaries.html "Chapter 16. Installation from Binaries")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-requirements.html "17.1. Requirements")  
  
* * *

## Chapter 17. Installation from Source Code

**Table of Contents**

[17.1. Requirements](install-requirements.html)

[17.2. Getting the Source](install-getsource.html)

[17.3. Building and Installation with Autoconf and Make](install-make.html)

    

[17.3.1. Short Version](install-make.html#INSTALL-SHORT-MAKE)

[17.3.2. Installation Procedure](install-make.html#INSTALL-PROCEDURE-MAKE)

[17.3.3. `configure` Options](install-make.html#CONFIGURE-OPTIONS)

[17.3.4. `configure` Environment Variables](install-make.html#CONFIGURE-
ENVVARS)

[17.4. Building and Installation with Meson](install-meson.html)

    

[17.4.1. Short Version](install-meson.html#INSTALL-SHORT-MESON)

[17.4.2. Installation Procedure](install-meson.html#INSTALL-PROCEDURE-MESON)

[17.4.3. `meson setup` Options](install-meson.html#MESON-OPTIONS)

[17.5. Post-Installation Setup](install-post.html)

    

[17.5.1. Shared Libraries](install-post.html#INSTALL-POST-SHLIBS)

[17.5.2. Environment Variables](install-post.html#INSTALL-POST-ENV-VARS)

[17.6. Supported Platforms](supported-platforms.html)

[17.7. Platform-Specific Notes](installation-platform-notes.html)

    

[17.7.1. AIX](installation-platform-notes.html#INSTALLATION-NOTES-AIX)

[17.7.2. Cygwin](installation-platform-notes.html#INSTALLATION-NOTES-CYGWIN)

[17.7.3. macOS](installation-platform-notes.html#INSTALLATION-NOTES-MACOS)

[17.7.4. MinGW/Native Windows](installation-platform-notes.html#INSTALLATION-
NOTES-MINGW)

[17.7.5. Solaris](installation-platform-notes.html#INSTALLATION-NOTES-SOLARIS)

This chapter describes the installation of PostgreSQL using the source code
distribution. If you are installing a pre-packaged distribution, such as an
RPM or Debian package, ignore this chapter and see [Chapter 16](install-
binaries.html "Chapter 16. Installation from Binaries") instead.

If you are building PostgreSQL for Microsoft Windows, read this chapter if you
intend to build with MinGW or Cygwin; but if you intend to build with
Microsoft's Visual C++, see [Chapter 18](install-windows.html
"Chapter 18. Installation from Source Code on Windows") instead.

* * *

[Prev](install-binaries.html "Chapter 16. Installation from Binaries")  | [Up](admin.html "Part III. Server Administration") |  [Next](install-requirements.html "17.1. Requirements")  
---|---|---  
Chapter 16. Installation from Binaries  | [Home](index.html "PostgreSQL 16.9 Documentation") |  17.1. Requirements  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/installation.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

