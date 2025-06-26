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

Supported Versions: [Current](/docs/current/supported-platforms.html
"PostgreSQL 17 - 17.6. Supported Platforms") ([17](/docs/17/supported-
platforms.html "PostgreSQL 17 - 17.6. Supported Platforms")) /
[16](/docs/16/supported-platforms.html "PostgreSQL 16 - 17.6. Supported
Platforms") / [15](/docs/15/supported-platforms.html "PostgreSQL 15 -
17.6. Supported Platforms") / [14](/docs/14/supported-platforms.html
"PostgreSQL 14 - 17.6. Supported Platforms") / [13](/docs/13/supported-
platforms.html "PostgreSQL 13 - 17.6. Supported Platforms")

Development Versions: [18](/docs/18/supported-platforms.html "PostgreSQL 18 -
17.6. Supported Platforms") / [devel](/docs/devel/supported-platforms.html
"PostgreSQL devel - 17.6. Supported Platforms")

Unsupported versions: [12](/docs/12/supported-platforms.html "PostgreSQL 12 -
17.6. Supported Platforms") / [11](/docs/11/supported-platforms.html
"PostgreSQL 11 - 17.6. Supported Platforms") / [10](/docs/10/supported-
platforms.html "PostgreSQL 10 - 17.6. Supported Platforms") /
[9.6](/docs/9.6/supported-platforms.html "PostgreSQL 9.6 - 17.6. Supported
Platforms") / [9.5](/docs/9.5/supported-platforms.html "PostgreSQL 9.5 -
17.6. Supported Platforms") / [9.4](/docs/9.4/supported-platforms.html
"PostgreSQL 9.4 - 17.6. Supported Platforms") / [9.3](/docs/9.3/supported-
platforms.html "PostgreSQL 9.3 - 17.6. Supported Platforms") /
[9.2](/docs/9.2/supported-platforms.html "PostgreSQL 9.2 - 17.6. Supported
Platforms") / [9.1](/docs/9.1/supported-platforms.html "PostgreSQL 9.1 -
17.6. Supported Platforms") / [9.0](/docs/9.0/supported-platforms.html
"PostgreSQL 9.0 - 17.6. Supported Platforms") / [8.4](/docs/8.4/supported-
platforms.html "PostgreSQL 8.4 - 17.6. Supported Platforms") /
[8.3](/docs/8.3/supported-platforms.html "PostgreSQL 8.3 - 17.6. Supported
Platforms") / [8.2](/docs/8.2/supported-platforms.html "PostgreSQL 8.2 -
17.6. Supported Platforms") / [8.1](/docs/8.1/supported-platforms.html
"PostgreSQL 8.1 - 17.6. Supported Platforms") / [8.0](/docs/8.0/supported-
platforms.html "PostgreSQL 8.0 - 17.6. Supported Platforms") /
[7.4](/docs/7.4/supported-platforms.html "PostgreSQL 7.4 - 17.6. Supported
Platforms") / [7.3](/docs/7.3/supported-platforms.html "PostgreSQL 7.3 -
17.6. Supported Platforms") / [7.2](/docs/7.2/supported-platforms.html
"PostgreSQL 7.2 - 17.6. Supported Platforms") / [7.1](/docs/7.1/supported-
platforms.html "PostgreSQL 7.1 - 17.6. Supported Platforms")

__

17.6. Supported Platforms  
---  
[Prev](install-post.html "17.5. Post-Installation Setup")  | [Up](installation.html "Chapter 17. Installation from Source Code") | Chapter 17. Installation from Source Code | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](installation-platform-notes.html "17.7. Platform-Specific Notes")  
  
* * *

## 17.6. Supported Platforms #

A platform (that is, a CPU architecture and operating system combination) is
considered supported by the PostgreSQL development community if the code
contains provisions to work on that platform and it has recently been verified
to build and pass its regression tests on that platform. Currently, most
testing of platform compatibility is done automatically by test machines in
the [PostgreSQL Build Farm](https://buildfarm.postgresql.org/). If you are
interested in using PostgreSQL on a platform that is not represented in the
build farm, but on which the code works or can be made to work, you are
strongly encouraged to set up a build farm member machine so that continued
compatibility can be assured.

In general, PostgreSQL can be expected to work on these CPU architectures:
x86, PowerPC, S/390, SPARC, ARM, MIPS, RISC-V, and PA-RISC, including big-
endian, little-endian, 32-bit, and 64-bit variants where applicable. It is
often possible to build on an unsupported CPU type by configuring with
`--disable-spinlocks`, but performance will be poor.

PostgreSQL can be expected to work on current versions of these operating
systems: Linux, Windows, FreeBSD, OpenBSD, NetBSD, DragonFlyBSD, macOS, AIX,
Solaris, and illumos. Other Unix-like systems may also work but are not
currently being tested. In most cases, all CPU architectures supported by a
given operating system will work. Look in [Section 17.7](installation-
platform-notes.html "17.7. Platform-Specific Notes") below to see if there is
information specific to your operating system, particularly if using an older
system.

If you have installation problems on a platform that is known to be supported
according to recent build farm results, please report it to `<[pgsql-
bugs@lists.postgresql.org](mailto:pgsql-bugs@lists.postgresql.org)>`. If you
are interested in porting PostgreSQL to a new platform, `<[pgsql-
hackers@lists.postgresql.org](mailto:pgsql-hackers@lists.postgresql.org)>` is
the appropriate place to discuss that.

Historical versions of PostgreSQL or POSTGRES also ran on CPU architectures
including Alpha, Itanium, M32R, M68K, M88K, NS32K, SuperH, and VAX, and
operating systems including 4.3BSD, BEOS, BSD/OS, DG/UX, Dynix, HP-UX, IRIX,
NeXTSTEP, QNX, SCO, SINIX, Sprite, SunOS, Tru64 UNIX, and ULTRIX.

* * *

[Prev](install-post.html "17.5. Post-Installation Setup")  | [Up](installation.html "Chapter 17. Installation from Source Code") |  [Next](installation-platform-notes.html "17.7. Platform-Specific Notes")  
---|---|---  
17.5. Post-Installation Setup  | [Home](index.html "PostgreSQL 16.9 Documentation") |  17.7. Platform-Specific Notes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/supported-platforms.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

