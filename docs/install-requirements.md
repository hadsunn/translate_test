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

Supported Versions: [Current](/docs/current/install-requirements.html
"PostgreSQL 17 - 17.1. Requirements") ([17](/docs/17/install-requirements.html
"PostgreSQL 17 - 17.1. Requirements")) / [16](/docs/16/install-
requirements.html "PostgreSQL 16 - 17.1. Requirements") /
[15](/docs/15/install-requirements.html "PostgreSQL 15 - 17.1. Requirements")
/ [14](/docs/14/install-requirements.html "PostgreSQL 14 -
17.1. Requirements") / [13](/docs/13/install-requirements.html "PostgreSQL 13
- 17.1. Requirements")

Development Versions: [18](/docs/18/install-requirements.html "PostgreSQL 18 -
17.1. Requirements") / [devel](/docs/devel/install-requirements.html
"PostgreSQL devel - 17.1. Requirements")

Unsupported versions: [12](/docs/12/install-requirements.html "PostgreSQL 12 -
17.1. Requirements") / [11](/docs/11/install-requirements.html "PostgreSQL 11
- 17.1. Requirements") / [10](/docs/10/install-requirements.html "PostgreSQL
10 - 17.1. Requirements") / [9.6](/docs/9.6/install-requirements.html
"PostgreSQL 9.6 - 17.1. Requirements") / [9.5](/docs/9.5/install-
requirements.html "PostgreSQL 9.5 - 17.1. Requirements") /
[9.4](/docs/9.4/install-requirements.html "PostgreSQL 9.4 -
17.1. Requirements") / [9.3](/docs/9.3/install-requirements.html "PostgreSQL
9.3 - 17.1. Requirements") / [9.2](/docs/9.2/install-requirements.html
"PostgreSQL 9.2 - 17.1. Requirements") / [9.1](/docs/9.1/install-
requirements.html "PostgreSQL 9.1 - 17.1. Requirements") /
[9.0](/docs/9.0/install-requirements.html "PostgreSQL 9.0 -
17.1. Requirements") / [8.4](/docs/8.4/install-requirements.html "PostgreSQL
8.4 - 17.1. Requirements") / [8.3](/docs/8.3/install-requirements.html
"PostgreSQL 8.3 - 17.1. Requirements") / [8.2](/docs/8.2/install-
requirements.html "PostgreSQL 8.2 - 17.1. Requirements") /
[8.1](/docs/8.1/install-requirements.html "PostgreSQL 8.1 -
17.1. Requirements") / [8.0](/docs/8.0/install-requirements.html "PostgreSQL
8.0 - 17.1. Requirements") / [7.4](/docs/7.4/install-requirements.html
"PostgreSQL 7.4 - 17.1. Requirements") / [7.3](/docs/7.3/install-
requirements.html "PostgreSQL 7.3 - 17.1. Requirements") /
[7.2](/docs/7.2/install-requirements.html "PostgreSQL 7.2 -
17.1. Requirements") / [7.1](/docs/7.1/install-requirements.html "PostgreSQL
7.1 - 17.1. Requirements")

__

17.1. Requirements  
---  
[Prev](installation.html "Chapter 17. Installation from Source Code")  | [Up](installation.html "Chapter 17. Installation from Source Code") | Chapter 17. Installation from Source Code | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-getsource.html "17.2. Getting the Source")  
  
* * *

## 17.1. Requirements #

In general, a modern Unix-compatible platform should be able to run
PostgreSQL. The platforms that had received specific testing at the time of
release are described in [Section 17.6](supported-platforms.html
"17.6. Supported Platforms") below.

The following software packages are required for building PostgreSQL:

  * GNU make version 3.81 or newer is required; other make programs or older GNU make versions will _not_ work. (GNU make is sometimes installed under the name `gmake`.) To test for GNU make enter:
        
        **make --version**
        

  * Alternatively, PostgreSQL can be built using [Meson](https://mesonbuild.com/). This is currently experimental and only works when building from a Git checkout (not from a distribution tarball). If you choose to use Meson, then you don't need GNU make, but the other requirements below still apply.

The minimum required version of Meson is 0.54.

  * You need an ISO/ANSI C compiler (at least C99-compliant). Recent versions of GCC are recommended, but PostgreSQL is known to build using a wide variety of compilers from different vendors.

  * tar is required to unpack the source distribution, in addition to either gzip or bzip2.

  * The GNU Readline library is used by default. It allows psql (the PostgreSQL command line SQL interpreter) to remember each command you type, and allows you to use arrow keys to recall and edit previous commands. This is very helpful and is strongly recommended. If you don't want to use it then you must specify the `--without-readline` option to `configure`. As an alternative, you can often use the BSD-licensed `libedit` library, originally developed on NetBSD. The `libedit` library is GNU Readline-compatible and is used if `libreadline` is not found, or if `--with-libedit-preferred` is used as an option to `configure`. If you are using a package-based Linux distribution, be aware that you need both the `readline` and `readline-devel` packages, if those are separate in your distribution.

  * The zlib compression library is used by default. If you don't want to use it then you must specify the `--without-zlib` option to `configure`. Using this option disables support for compressed archives in pg_dump and pg_restore.

  * The ICU library is used by default. If you don't want to use it then you must specify the `--without-icu` option to `configure`. Using this option disables support for ICU collation features (see [Section 24.2](collation.html "24.2. Collation Support")).

ICU support requires the ICU4C package to be installed. The minimum required
version of ICU4C is currently 4.2.

By default, pkg-config will be used to find the required compilation options.
This is supported for ICU4C version 4.6 and later. For older versions, or if
pkg-config is not available, the variables `ICU_CFLAGS` and `ICU_LIBS` can be
specified to `configure`, like in this example:

        
        ./configure ... ICU_CFLAGS='-I/some/where/include' ICU_LIBS='-L/some/where/lib -licui18n -licuuc -licudata'
        

(If ICU4C is in the default search path for the compiler, then you still need
to specify nonempty strings in order to avoid use of pkg-config, for example,
`ICU_CFLAGS=' '`.)

The following packages are optional. They are not required in the default
configuration, but they are needed when certain build options are enabled, as
explained below:

  * To build the server programming language PL/Perl you need a full Perl installation, including the `libperl` library and the header files. The minimum required version is Perl 5.14. Since PL/Perl will be a shared library, the  `libperl` library must be a shared library also on most platforms. This appears to be the default in recent Perl versions, but it was not in earlier versions, and in any case it is the choice of whomever installed Perl at your site. `configure` will fail if building PL/Perl is selected but it cannot find a shared `libperl`. In that case, you will have to rebuild and install Perl manually to be able to build PL/Perl. During the configuration process for Perl, request a shared library.

If you intend to make more than incidental use of PL/Perl, you should ensure
that the Perl installation was built with the `usemultiplicity` option enabled
(`perl -V` will show whether this is the case).

  * To build the PL/Python server programming language, you need a Python installation with the header files and the sysconfig module. The minimum required version is Python 3.2.

Since PL/Python will be a shared library, the  `libpython` library must be a
shared library also on most platforms. This is not the case in a default
Python installation built from source, but a shared library is available in
many operating system distributions. `configure` will fail if building
PL/Python is selected but it cannot find a shared `libpython`. That might mean
that you either have to install additional packages or rebuild (part of) your
Python installation to provide this shared library. When building from source,
run Python's configure with the `--enable-shared` flag.

  * To build the PL/Tcl procedural language, you of course need a Tcl installation. The minimum required version is Tcl 8.4.

  * To enable Native Language Support (NLS), that is, the ability to display a program's messages in a language other than English, you need an implementation of the Gettext API. Some operating systems have this built-in (e.g., Linux, NetBSD, Solaris), for other systems you can download an add-on package from <https://www.gnu.org/software/gettext/>. If you are using the Gettext implementation in the GNU C library, then you will additionally need the GNU Gettext package for some utility programs. For any of the other implementations you will not need it.

  * You need OpenSSL, if you want to support encrypted client connections. OpenSSL is also required for random number generation on platforms that do not have `/dev/urandom` (except Windows). The minimum required version is 1.0.1.

  * You need MIT Kerberos (for GSSAPI), OpenLDAP, and/or PAM, if you want to support authentication using those services.

  * You need LZ4, if you want to support compression of data with that method; see [default_toast_compression](runtime-config-client.html#GUC-DEFAULT-TOAST-COMPRESSION) and [wal_compression](runtime-config-wal.html#GUC-WAL-COMPRESSION).

  * You need Zstandard, if you want to support compression of data with that method; see [wal_compression](runtime-config-wal.html#GUC-WAL-COMPRESSION). The minimum required version is 1.4.0.

  * To build the PostgreSQL documentation, there is a separate set of requirements; see [Section J.2](docguide-toolsets.html "J.2. Tool Sets").

If you are building from a Git tree instead of using a released source
package, or if you want to do server development, you also need the following
packages:

  * Flex and Bison are needed to build from a Git checkout, or if you changed the actual scanner and parser definition files. If you need them, be sure to get Flex 2.5.35 or later and Bison 2.3 or later. Other lex and yacc programs cannot be used.

  * Perl 5.14 or later is needed to build from a Git checkout, or if you changed the input files for any of the build steps that use Perl scripts. If building on Windows you will need Perl in any case. Perl is also required to run some test suites.

If you need to get a GNU package, you can find it at your local GNU mirror
site (see <https://www.gnu.org/prep/ftp> for a list) or at
<ftp://ftp.gnu.org/gnu/>.

* * *

[Prev](installation.html "Chapter 17. Installation from Source Code")  | [Up](installation.html "Chapter 17. Installation from Source Code") |  [Next](install-getsource.html "17.2. Getting the Source")  
---|---|---  
Chapter 17. Installation from Source Code  | [Home](index.html "PostgreSQL 16.9 Documentation") |  17.2. Getting the Source  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/install-requirements.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

