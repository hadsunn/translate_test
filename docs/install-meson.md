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

Supported Versions: [Current](/docs/current/install-meson.html "PostgreSQL 17
- 17.4. Building and Installation with Meson") ([17](/docs/17/install-
meson.html "PostgreSQL 17 - 17.4. Building and Installation with Meson")) /
[16](/docs/16/install-meson.html "PostgreSQL 16 - 17.4. Building and
Installation with Meson")

Development Versions: [18](/docs/18/install-meson.html "PostgreSQL 18 -
17.4. Building and Installation with Meson") / [devel](/docs/devel/install-
meson.html "PostgreSQL devel - 17.4. Building and Installation with Meson")

__

17.4. Building and Installation with Meson  
---  
[Prev](install-make.html "17.3. Building and Installation with Autoconf and Make")  | [Up](installation.html "Chapter 17. Installation from Source Code") | Chapter 17. Installation from Source Code | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-post.html "17.5. Post-Installation Setup")  
  
* * *

## 17.4. Building and Installation with Meson #

[17.4.1. Short Version](install-meson.html#INSTALL-SHORT-MESON)

[17.4.2. Installation Procedure](install-meson.html#INSTALL-PROCEDURE-MESON)

[17.4.3. `meson setup` Options](install-meson.html#MESON-OPTIONS)

### 17.4.1. Short Version #

    
    
    meson setup build --prefix=/usr/local/pgsql
    cd build
    ninja
    su
    ninja install
    adduser postgres
    mkdir -p /usr/local/pgsql/data
    chown postgres /usr/local/pgsql/data
    su - postgres
    /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
    /usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
    /usr/local/pgsql/bin/createdb test
    /usr/local/pgsql/bin/psql test
    

The long version is the rest of this section.

### 17.4.2. Installation Procedure #

  1. **Configuration**

The first step of the installation procedure is to configure the build tree
for your system and choose the options you would like. To create and configure
the build directory, you can start with the `meson setup` command.

         
         **meson setup build**
         

The setup command takes a `builddir` and a `srcdir` argument. If no `srcdir`
is given, Meson will deduce the `srcdir` based on the current directory and
the location of `meson.build`. The `builddir` is mandatory.

Running `meson setup` loads the build configuration file and sets up the build
directory. Additionally, you can also pass several build options to Meson.
Some commonly used options are mentioned in the subsequent sections. For
example:

         
         # configure with a different installation prefix
         meson setup build --prefix=/home/user/pg-install
         
         # configure to generate a debug build
         meson setup build --buildtype=debug
         
         # configure to build with OpenSSL support
         meson setup build -Dssl=openssl
         

Setting up the build directory is a one-time step. To reconfigure before a new
build, you can simply use the `meson configure` command

         
         meson configure -Dcassert=true
         

`meson configure`'s commonly used command-line options are explained in
[Section 17.4.3](install-meson.html#MESON-OPTIONS "17.4.3. meson setup
Options").

  2. **Build**

By default, Meson uses the [Ninja](https://ninja-build.org/) build tool. To
build PostgreSQL from source using Meson, you can simply use the `ninja`
command in the build directory.

         
         ninja
         

Ninja will automatically detect the number of CPUs in your computer and
parallelize itself accordingly. You can override the number of parallel
processes used with the command line argument `-j`.

It should be noted that after the initial configure step, `ninja` is the only
command you ever need to type to compile. No matter how you alter your source
tree (short of moving it to a completely new location), Meson will detect the
changes and regenerate itself accordingly. This is especially handy if you
have multiple build directories. Often one of them is used for development
(the "debug" build) and others only every now and then (such as a "static
analysis" build). Any configuration can be built just by cd'ing to the
corresponding directory and running Ninja.

If you'd like to build with a backend other than ninja, you can use configure
with the `--backend` option to select the one you want to use and then build
using `meson compile`. To learn more about these backends and other arguments
you can provide to ninja, you can refer to the [Meson
documentation](https://mesonbuild.com/Running-Meson.html#building-from-the-
source).

  3. **Regression Tests**

If you want to test the newly built server before you install it, you can run
the regression tests at this point. The regression tests are a test suite to
verify that PostgreSQL runs on your machine in the way the developers expected
it to. Type:

         
         **meson test**
         

(This won't work as root; do it as an unprivileged user.) See [Chapter
33](regress.html "Chapter 33. Regression Tests") for detailed information
about interpreting the test results. You can repeat this test at any later
time by issuing the same command.

To run pg_regress and pg_isolation_regress tests against a running postgres
instance, specify **`--setup running`** as an argument to **`meson test`**.

  4. **Installing the Files**

### Note

If you are upgrading an existing system be sure to read [Section
19.6](upgrading.html "19.6. Upgrading a PostgreSQL Cluster"), which has
instructions about upgrading a cluster.

Once PostgreSQL is built, you can install it by simply running the `ninja
install` command.

         
         ninja install
         

This will install files into the directories that were specified in [Step
1](install-meson.html#MESON-CONFIGURE "Configuration"). Make sure that you
have appropriate permissions to write into that area. You might need to do
this step as root. Alternatively, you can create the target directories in
advance and arrange for appropriate permissions to be granted. The standard
installation provides all the header files needed for client application
development as well as for server-side program development, such as custom
functions or data types written in C.

`ninja install` should work for most cases, but if you'd like to use more
options (such as `--quiet` to suppress extra output), you could also use
`meson install` instead. You can learn more about [meson
install](https://mesonbuild.com/Commands.html#install) and its options in the
Meson documentation.

**Uninstallation:  ** To undo the installation, you can use the `ninja
uninstall` command.

**Cleaning:  ** After the installation, you can free disk space by removing
the built files from the source tree with the `ninja clean` command.

### 17.4.3. `meson setup` Options #

`meson setup`'s command-line options are explained below. This list is not
exhaustive (use `meson configure --help` to get one that is). The options not
covered here are meant for advanced use-cases, and are documented in the
standard [Meson
documentation](https://mesonbuild.com/Commands.html#configure). These
arguments can be used with `meson setup` as well.

#### 17.4.3.1. Installation Locations #

These options control where `ninja install` (or `meson install`) will put the
files. The `--prefix` option (example [Section 17.4.1](install-
meson.html#INSTALL-SHORT-MESON "17.4.1. Short Version")) is sufficient for
most cases. If you have special needs, you can customize the installation
subdirectories with the other options described in this section. Beware
however that changing the relative locations of the different subdirectories
may render the installation non-relocatable, meaning you won't be able to move
it after installation. (The `man` and `doc` locations are not affected by this
restriction.) For relocatable installs, you might want to use the
`-Drpath=false` option described later.

`--prefix=_`PREFIX`_` #

    

Install all files under the directory _`PREFIX`_ instead of `/usr/local/pgsql`
(on Unix based systems) or `_`current drive letter`_ :/usr/local/pgsql` (on
Windows). The actual files will be installed into various subdirectories; no
files will ever be installed directly into the _`PREFIX`_ directory.

`--bindir=_`DIRECTORY`_` #

    

Specifies the directory for executable programs. The default is `_`PREFIX`_
/bin`.

`--sysconfdir=_`DIRECTORY`_` #

    

Sets the directory for various configuration files, `_`PREFIX`_ /etc` by
default.

`--libdir=_`DIRECTORY`_` #

    

Sets the location to install libraries and dynamically loadable modules. The
default is `_`PREFIX`_ /lib`.

`--includedir=_`DIRECTORY`_` #

    

Sets the directory for installing C and C++ header files. The default is
`_`PREFIX`_ /include`.

`--datadir=_`DIRECTORY`_` #

    

Sets the directory for read-only data files used by the installed programs.
The default is `_`PREFIX`_ /share`. Note that this has nothing to do with
where your database files will be placed.

`--localedir=_`DIRECTORY`_` #

    

Sets the directory for installing locale data, in particular message
translation catalog files. The default is `_`DATADIR`_ /locale`.

`--mandir=_`DIRECTORY`_` #

    

The man pages that come with PostgreSQL will be installed under this
directory, in their respective `man _`x`_` subdirectories. The default is
`_`DATADIR`_ /man`.

### Note

Care has been taken to make it possible to install PostgreSQL into shared
installation locations (such as `/usr/local/include`) without interfering with
the namespace of the rest of the system. First, the string “`/postgresql`” is
automatically appended to `datadir`, `sysconfdir`, and `docdir`, unless the
fully expanded directory name already contains the string “`postgres`” or
“`pgsql`”. For example, if you choose `/usr/local` as prefix, the
documentation will be installed in `/usr/local/doc/postgresql`, but if the
prefix is `/opt/postgres`, then it will be in `/opt/postgres/doc`. The public
C header files of the client interfaces are installed into `includedir` and
are namespace-clean. The internal header files and the server header files are
installed into private directories under `includedir`. See the documentation
of each interface for information about how to access its header files.
Finally, a private subdirectory will also be created, if appropriate, under
`libdir` for dynamically loadable modules.

#### 17.4.3.2. PostgreSQL Features #

The options described in this section enable building of various optional
PostgreSQL features. Most of these require additional software, as described
in [Section 17.1](install-requirements.html "17.1. Requirements"), and will be
automatically enabled if the required software is found. You can change this
behavior by manually setting these features to `enabled` to require them or
`disabled` to not build with them.

To specify PostgreSQL-specific options, the name of the option must be
prefixed by `-D`.

`-Dnls={ auto | enabled | disabled }` #
    

Enables or disables Native Language Support (NLS), that is, the ability to
display a program's messages in a language other than English. Defaults to
auto and will be enabled automatically if an implementation of the Gettext API
is found.

`-Dplperl={ auto | enabled | disabled }` #
    

Build the PL/Perl server-side language. Defaults to auto.

`-Dplpython={ auto | enabled | disabled }` #
    

Build the PL/Python server-side language. Defaults to auto.

`-Dpltcl={ auto | enabled | disabled }` #
    

Build the PL/Tcl server-side language. Defaults to auto.

`-Dtcl_version=_`TCL_VERSION`_` #

    

Specifies the Tcl version to use when building PL/Tcl.

`-Dicu={ auto | enabled | disabled }` #
    

Build with support for the ICU library, enabling use of ICU collation features
(see [Section 24.2](collation.html "24.2. Collation Support")). Defaults to
auto and requires the ICU4C package to be installed. The minimum required
version of ICU4C is currently 4.2.

`-Dllvm={ auto | enabled | disabled }` #
    

Build with support for LLVM based JIT compilation (see [Chapter 32](jit.html
"Chapter 32. Just-in-Time Compilation \(JIT\)")). This requires the LLVM
library to be installed. The minimum required version of LLVM is currently
3.9. Disabled by default.

`llvm-config` will be used to find the required compilation options. `llvm-
config`, and then `llvm-config-$version` for all supported versions, will be
searched for in your `PATH`. If that would not yield the desired program, use
`LLVM_CONFIG` to specify a path to the correct `llvm-config`.

`-Dlz4={ auto | enabled | disabled }` #
    

Build with LZ4 compression support. Defaults to auto.

`-Dzstd={ auto | enabled | disabled }` #
    

Build with Zstandard compression support. Defaults to auto.

`-Dssl={ auto | _`LIBRARY`_ }` #
    

Build with support for SSL (encrypted) connections. The only _`LIBRARY`_
supported is `openssl`. This requires the OpenSSL package to be installed.
Building with this will check for the required header files and libraries to
make sure that your OpenSSL installation is sufficient before proceeding. The
default for this option is auto.

`-Dgssapi={ auto | enabled | disabled }` #
    

Build with support for GSSAPI authentication. MIT Kerberos is required to be
installed for GSSAPI. On many systems, the GSSAPI system (a part of the MIT
Kerberos installation) is not installed in a location that is searched by
default (e.g., `/usr/include`, `/usr/lib`). In those cases, PostgreSQL will
query `pkg-config` to detect the required compiler and linker options.
Defaults to auto. `meson configure` will check for the required header files
and libraries to make sure that your GSSAPI installation is sufficient before
proceeding.

`-Dldap={ auto | enabled | disabled }` #
    

Build with LDAP support for authentication and connection parameter lookup
(see [Section 34.18](libpq-ldap.html "34.18. LDAP Lookup of Connection
Parameters") and [Section 21.10](auth-ldap.html "21.10. LDAP Authentication")
for more information). On Unix, this requires the OpenLDAP package to be
installed. On Windows, the default WinLDAP library is used. Defaults to auto.
`meson configure` will check for the required header files and libraries to
make sure that your OpenLDAP installation is sufficient before proceeding.

`-Dpam={ auto | enabled | disabled }` #
    

Build with PAM (Pluggable Authentication Modules) support. Defaults to auto.

`-Dbsd_auth={ auto | enabled | disabled }` #
    

Build with BSD Authentication support. (The BSD Authentication framework is
currently only available on OpenBSD.) Defaults to auto.

`-Dsystemd={ auto | enabled | disabled }` #
    

Build with support for systemd service notifications. This improves
integration if the server is started under systemd but has no impact
otherwise; see [Section 19.3](server-start.html "19.3. Starting the Database
Server") for more information. Defaults to auto. libsystemd and the associated
header files need to be installed to use this option.

`-Dbonjour={ auto | enabled | disabled }` #
    

Build with support for Bonjour automatic service discovery. Defaults to auto
and requires Bonjour support in your operating system. Recommended on macOS.

`-Duuid=_`LIBRARY`_` #

    

Build the [uuid-ossp](uuid-ossp.html "F.49. uuid-ossp — a UUID generator")
module (which provides functions to generate UUIDs), using the specified UUID
library. _`LIBRARY`_ must be one of:

  * `none` to not build the uuid module. This is the default.

  * `bsd` to use the UUID functions found in FreeBSD, and some other BSD-derived systems

  * `e2fs` to use the UUID library created by the `e2fsprogs` project; this library is present in most Linux systems and in macOS, and can be obtained for other platforms as well

  * `ossp` to use the [OSSP UUID library](http://www.ossp.org/pkg/lib/uuid/)

`-Dlibxml={ auto | enabled | disabled }` #
    

Build with libxml2, enabling SQL/XML support. Defaults to auto. Libxml2
version 2.6.23 or later is required for this feature.

To use a libxml2 installation that is in an unusual location, you can set
`pkg-config`-related environment variables (see its documentation).

`-Dlibxslt={ auto | enabled | disabled }` #
    

Build with libxslt, enabling the [xml2](xml2.html "F.50. xml2 — XPath querying
and XSLT functionality") module to perform XSL transformations of XML.
`-Dlibxml` must be specified as well. Defaults to auto.

#### 17.4.3.3. Anti-Features #

`-Dreadline={ auto | enabled | disabled }` #
    

Allows use of the Readline library (and libedit as well). This option defaults
to auto and enables command-line editing and history in psql and is strongly
recommended.

`-Dlibedit_preferred={ true | false }` #
    

Setting this to true favors the use of the BSD-licensed libedit library rather
than GPL-licensed Readline. This option is significant only if you have both
libraries installed; the default is false, that is to use Readline.

`-Dzlib={ auto | enabled | disabled }` #
    

Enables use of the Zlib library. It defaults to auto and enables support for
compressed archives in pg_dump, pg_restore and pg_basebackup and is
recommended.

`-Dspinlocks={ true | false }` #
    

This option is set to true by default; setting it to false will allow the
build to succeed even if PostgreSQL has no CPU spinlock support for the
platform. The lack of spinlock support will result in very poor performance;
therefore, this option should only be changed if the build aborts and informs
you that the platform lacks spinlock support. If setting this option to false
is required to build PostgreSQL on your platform, please report the problem to
the PostgreSQL developers.

`-Datomics={ true | false }` #
    

This option is set to true by default; setting it to false will disable use of
CPU atomic operations. The option does nothing on platforms that lack such
operations. On platforms that do have them, disabling atomics will result in
poor performance. Changing this option is only useful for debugging or making
performance comparisons.

#### 17.4.3.4. Build Process Details #

`--auto-features={ auto | enabled | disabled }` #
    

Setting this option allows you to override the value of all “auto” features
(features that are enabled automatically if the required software is found).
This can be useful when you want to disable or enable all the “optional”
features at once without having to set each of them manually. The default
value for this parameter is auto.

`--backend=_`BACKEND`_` #

    

The default backend Meson uses is ninja and that should suffice for most use
cases. However, if you'd like to fully integrate with Visual Studio, you can
set the `BACKEND` to `vs`.

`-Dc_args=_`OPTIONS`_` #

    

This option can be used to pass extra options to the C compiler.

`-Dc_link_args=_`OPTIONS`_` #

    

This option can be used to pass extra options to the C linker.

`-Dextra_include_dirs=_`DIRECTORIES`_` #

    

_`DIRECTORIES`_ is a comma-separated list of directories that will be added to
the list the compiler searches for header files. If you have optional packages
(such as GNU Readline) installed in a non-standard location, you have to use
this option and probably also the corresponding `-Dextra_lib_dirs` option.

Example: `-Dextra_include_dirs=/opt/gnu/include,/usr/sup/include`.

`-Dextra_lib_dirs=_`DIRECTORIES`_` #

    

_`DIRECTORIES`_ is a comma-separated list of directories to search for
libraries. You will probably have to use this option (and the corresponding
`-Dextra_include_dirs` option) if you have packages installed in non-standard
locations.

Example: `-Dextra_lib_dirs=/opt/gnu/lib,/usr/sup/lib`.

`-Dsystem_tzdata=_`DIRECTORY`_` #

    

PostgreSQL includes its own time zone database, which it requires for date and
time operations. This time zone database is in fact compatible with the IANA
time zone database provided by many operating systems such as FreeBSD, Linux,
and Solaris, so it would be redundant to install it again. When this option is
used, the system-supplied time zone database in _`DIRECTORY`_ is used instead
of the one included in the PostgreSQL source distribution. _`DIRECTORY`_ must
be specified as an absolute path. `/usr/share/zoneinfo` is a likely directory
on some operating systems. Note that the installation routine will not detect
mismatching or erroneous time zone data. If you use this option, you are
advised to run the regression tests to verify that the time zone data you have
pointed to works correctly with PostgreSQL.

This option is mainly aimed at binary package distributors who know their
target operating system well. The main advantage of using this option is that
the PostgreSQL package won't need to be upgraded whenever any of the many
local daylight-saving time rules change. Another advantage is that PostgreSQL
can be cross-compiled more straightforwardly if the time zone database files
do not need to be built during the installation.

`-Dextra_version=_`STRING`_` #

    

Append _`STRING`_ to the PostgreSQL version number. You can use this, for
example, to mark binaries built from unreleased Git snapshots or containing
custom patches with an extra version string, such as a `git describe`
identifier or a distribution package release number.

`-Drpath={ true | false }` #
    

This option is set to true by default. If set to false, do not mark
PostgreSQL's executables to indicate that they should search for shared
libraries in the installation's library directory (see `--libdir`). On most
platforms, this marking uses an absolute path to the library directory, so
that it will be unhelpful if you relocate the installation later. However, you
will then need to provide some other way for the executables to find the
shared libraries. Typically this requires configuring the operating system's
dynamic linker to search the library directory; see [Section 17.5.1](install-
post.html#INSTALL-POST-SHLIBS "17.5.1. Shared Libraries") for more detail.

`-D _`BINARY_NAME`_ =_`PATH`_` #

    

If a program required to build PostgreSQL (with or without optional flags) is
stored at a non-standard path, you can specify it manually to `meson
configure`. The complete list of programs for which this is supported can be
found by running `meson configure`. Example:

    
    
    meson configure -DBISON=PATH_TO_BISON

#### 17.4.3.5. Documentation #

See [Section J.2](docguide-toolsets.html "J.2. Tool Sets") for the tools
needed for building the documentation.

`-Ddocs={ auto | enabled | disabled }` #
    

Enables building the documentation in HTML and man format. It defaults to
auto.

`-Ddocs_pdf={ auto | enabled | disabled }` #
    

Enables building the documentation in PDF format. It defaults to auto.

`-Ddocs_html_style={ simple | website }` #
    

Controls which CSS stylesheet is used. The default is `simple`. If set to
`website`, the HTML documentation will reference the stylesheet for
[postgresql.org](https://www.postgresql.org/docs/current/).

#### 17.4.3.6. Miscellaneous #

`-Dpgport=_`NUMBER`_` #

    

Set _`NUMBER`_ as the default port number for server and clients. The default
is 5432. The port can always be changed later on, but if you specify it here
then both server and clients will have the same default compiled in, which can
be very convenient. Usually the only good reason to select a non-default value
is if you intend to run multiple PostgreSQL servers on the same machine.

`-Dkrb_srvnam=_`NAME`_` #

    

The default name of the Kerberos service principal used by GSSAPI. `postgres`
is the default. There's usually no reason to change this unless you are
building for a Windows environment, in which case it must be set to upper case
`POSTGRES`.

`-Dsegsize=_`SEGSIZE`_` #

    

Set the _segment size_ , in gigabytes. Large tables are divided into multiple
operating-system files, each of size equal to the segment size. This avoids
problems with file size limits that exist on many platforms. The default
segment size, 1 gigabyte, is safe on all supported platforms. If your
operating system has “largefile” support (which most do, nowadays), you can
use a larger segment size. This can be helpful to reduce the number of file
descriptors consumed when working with very large tables. But be careful not
to select a value larger than is supported by your platform and the file
systems you intend to use. Other tools you might wish to use, such as tar,
could also set limits on the usable file size. It is recommended, though not
absolutely required, that this value be a power of 2.

`-Dblocksize=_`BLOCKSIZE`_` #

    

Set the _block size_ , in kilobytes. This is the unit of storage and I/O
within tables. The default, 8 kilobytes, is suitable for most situations; but
other values may be useful in special cases. The value must be a power of 2
between 1 and 32 (kilobytes).

`-Dwal_blocksize=_`BLOCKSIZE`_` #

    

Set the _WAL block size_ , in kilobytes. This is the unit of storage and I/O
within the WAL log. The default, 8 kilobytes, is suitable for most situations;
but other values may be useful in special cases. The value must be a power of
2 between 1 and 64 (kilobytes).

#### 17.4.3.7. Developer Options #

Most of the options in this section are only of interest for developing or
debugging PostgreSQL. They are not recommended for production builds, except
for `--debug`, which can be useful to enable detailed bug reports in the
unlucky event that you encounter a bug. On platforms supporting DTrace,
`-Ddtrace` may also be reasonable to use in production.

When building an installation that will be used to develop code inside the
server, it is recommended to use at least the `--buildtype=debug` and
`-Dcassert` options.

`--buildtype=_`BUILDTYPE`_` #

    

This option can be used to specify the buildtype to use; defaults to
`debugoptimized`. If you'd like finer control on the debug symbols and
optimization levels than what this option provides, you can refer to the
`--debug` and `--optimization` flags.

The following build types are generally used: `plain`, `debug`,
`debugoptimized` and `release`. More information about them can be found in
the [Meson documentation](https://mesonbuild.com/Running-
Meson.html#configuring-the-build-directory).

`--debug` #

    

Compiles all programs and libraries with debugging symbols. This means that
you can run the programs in a debugger to analyze problems. This enlarges the
size of the installed executables considerably, and on non-GCC compilers it
usually also disables compiler optimization, causing slowdowns. However,
having the symbols available is extremely helpful for dealing with any
problems that might arise. Currently, this option is recommended for
production installations only if you use GCC. But you should always have it on
if you are doing development work or running a beta version.

`--optimization`=_`LEVEL`_ #

    

Specify the optimization level. `LEVEL` can be set to any of {0,g,1,2,3,s}.

`--werror` #

    

Setting this option asks the compiler to treat warnings as errors. This can be
useful for code development.

`-Dcassert={ true | false }` #
    

Enables _assertion_ checks in the server, which test for many “cannot happen”
conditions. This is invaluable for code development purposes, but the tests
slow down the server significantly. Also, having the tests turned on won't
necessarily enhance the stability of your server! The assertion checks are not
categorized for severity, and so what might be a relatively harmless bug will
still lead to server restarts if it triggers an assertion failure. This option
is not recommended for production use, but you should have it on for
development work or when running a beta version.

`-Dtap_tests={ auto | enabled | disabled }` #
    

Enable tests using the Perl TAP tools. Defaults to auto and requires a Perl
installation and the Perl module `IPC::Run`. See [Section 33.4](regress-
tap.html "33.4. TAP Tests") for more information.

`-DPG_TEST_EXTRA=_`TEST_SUITES`_` #

    

Enable test suites which require special software to run. This option accepts
arguments via a whitespace-separated list. See [Section 33.1.3](regress-
run.html#REGRESS-ADDITIONAL "33.1.3. Additional Test Suites") for details.

`-Db_coverage={ true | false }` #
    

If using GCC, all programs and libraries are compiled with code coverage
testing instrumentation. When run, they generate files in the build directory
with code coverage metrics. See [Section 33.5](regress-coverage.html
"33.5. Test Coverage Examination") for more information. This option is for
use only with GCC and when doing development work.

`-Ddtrace={ auto | enabled | disabled }` #
    

Enabling this compiles PostgreSQL with support for the dynamic tracing tool
DTrace. See [Section 28.5](dynamic-trace.html "28.5. Dynamic Tracing") for
more information.

To point to the `dtrace` program, the `DTRACE` option can be set. This will
often be necessary because `dtrace` is typically installed under `/usr/sbin`,
which might not be in your `PATH`.

`-Dsegsize_blocks=SEGSIZE_BLOCKS` #

    

Specify the relation segment size in blocks. If both `-Dsegsize` and this
option are specified, this option wins. This option is only for developers, to
test segment related code.

* * *

[Prev](install-make.html "17.3. Building and Installation with Autoconf and Make")  | [Up](installation.html "Chapter 17. Installation from Source Code") |  [Next](install-post.html "17.5. Post-Installation Setup")  
---|---|---  
17.3. Building and Installation with Autoconf and Make  | [Home](index.html "PostgreSQL 16.9 Documentation") |  17.5. Post-Installation Setup  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/install-meson.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

