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

Supported Versions: [16](/docs/16/install-windows.html "PostgreSQL 16 -
Chapter 18. Installation from Source Code on Windows") /
[15](/docs/15/install-windows.html "PostgreSQL 15 - Chapter 18. Installation
from Source Code on Windows") / [14](/docs/14/install-windows.html "PostgreSQL
14 - Chapter 18. Installation from Source Code on Windows") /
[13](/docs/13/install-windows.html "PostgreSQL 13 - Chapter 18. Installation
from Source Code on Windows")

Unsupported versions: [12](/docs/12/install-windows.html "PostgreSQL 12 -
Chapter 18. Installation from Source Code on Windows") /
[11](/docs/11/install-windows.html "PostgreSQL 11 - Chapter 18. Installation
from Source Code on Windows") / [10](/docs/10/install-windows.html "PostgreSQL
10 - Chapter 18. Installation from Source Code on Windows") /
[9.6](/docs/9.6/install-windows.html "PostgreSQL 9.6 -
Chapter 18. Installation from Source Code on Windows") /
[9.5](/docs/9.5/install-windows.html "PostgreSQL 9.5 -
Chapter 18. Installation from Source Code on Windows") /
[9.4](/docs/9.4/install-windows.html "PostgreSQL 9.4 -
Chapter 18. Installation from Source Code on Windows") /
[9.3](/docs/9.3/install-windows.html "PostgreSQL 9.3 -
Chapter 18. Installation from Source Code on Windows") /
[9.2](/docs/9.2/install-windows.html "PostgreSQL 9.2 -
Chapter 18. Installation from Source Code on Windows") /
[9.1](/docs/9.1/install-windows.html "PostgreSQL 9.1 -
Chapter 18. Installation from Source Code on Windows") /
[9.0](/docs/9.0/install-windows.html "PostgreSQL 9.0 -
Chapter 18. Installation from Source Code on Windows")

__

Chapter 18. Installation from Source Code on Windows  
---  
[Prev](installation-platform-notes.html "17.7. Platform-Specific Notes")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-windows-full.html "18.1. Building with Visual C++ or the  Microsoft Windows SDK")  
  
* * *

## Chapter 18. Installation from Source Code on Windows

**Table of Contents**

[18.1. Building with Visual C++ or the Microsoft Windows SDK](install-windows-
full.html)

    

[18.1.1. Requirements](install-windows-full.html#INSTALL-WINDOWS-FULL-
REQUIREMENTS)

[18.1.2. Special Considerations for 64-Bit Windows](install-windows-
full.html#INSTALL-WINDOWS-FULL-64-BIT)

[18.1.3. Building](install-windows-full.html#INSTALL-WINDOWS-FULL-BUILD)

[18.1.4. Cleaning and Installing](install-windows-full.html#INSTALL-WINDOWS-
FULL-CLEAN-INST)

[18.1.5. Running the Regression Tests](install-windows-full.html#INSTALL-
WINDOWS-FULL-REG-TESTS)

It is recommended that most users download the binary distribution for
Windows, available as a graphical installer package from the PostgreSQL
website at <https://www.postgresql.org/download/>. Building from source is
only intended for people developing PostgreSQL or extensions.

There are several different ways of building PostgreSQL on Windows. The
simplest way to build with Microsoft tools is to install Visual Studio 2022
and use the included compiler. It is also possible to build with the full
Microsoft Visual C++ 2015 to 2022. In some cases that requires the
installation of the Windows SDK in addition to the compiler.

It is also possible to build PostgreSQL using the GNU compiler tools provided
by MinGW, or using Cygwin for older versions of Windows.

Building using MinGW or Cygwin uses the normal build system, see [Chapter
17](installation.html "Chapter 17. Installation from Source Code") and the
specific notes in [Section 17.7.4](installation-platform-
notes.html#INSTALLATION-NOTES-MINGW "17.7.4. MinGW/Native Windows") and
[Section 17.7.2](installation-platform-notes.html#INSTALLATION-NOTES-CYGWIN
"17.7.2. Cygwin"). To produce native 64 bit binaries in these environments,
use the tools from MinGW-w64. These tools can also be used to cross-compile
for 32 bit and 64 bit Windows targets on other hosts, such as Linux and macOS.
Cygwin is not recommended for running a production server, and it should only
be used for running on older versions of Windows where the native build does
not work. The official binaries are built using Visual Studio.

Native builds of psql don't support command line editing. The Cygwin build
does support command line editing, so it should be used where psql is needed
for interactive use on Windows.

* * *

[Prev](installation-platform-notes.html "17.7. Platform-Specific Notes")  | [Up](admin.html "Part III. Server Administration") |  [Next](install-windows-full.html "18.1. Building with Visual C++ or the  Microsoft Windows SDK")  
---|---|---  
17.7. Platform-Specific Notes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  18.1. Building with Visual C++ or the Microsoft Windows SDK  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/install-windows.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

