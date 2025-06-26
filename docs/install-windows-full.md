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

Supported Versions: [16](/docs/16/install-windows-full.html "PostgreSQL 16 -
18.1. Building with Visual C++ or the Microsoft Windows SDK") /
[15](/docs/15/install-windows-full.html "PostgreSQL 15 - 18.1. Building with
Visual C++ or the Microsoft Windows SDK") / [14](/docs/14/install-windows-
full.html "PostgreSQL 14 - 18.1. Building with Visual C++ or the Microsoft
Windows SDK") / [13](/docs/13/install-windows-full.html "PostgreSQL 13 -
18.1. Building with Visual C++ or the Microsoft Windows SDK")

Unsupported versions: [12](/docs/12/install-windows-full.html "PostgreSQL 12 -
18.1. Building with Visual C++ or the Microsoft Windows SDK") /
[11](/docs/11/install-windows-full.html "PostgreSQL 11 - 18.1. Building with
Visual C++ or the Microsoft Windows SDK") / [10](/docs/10/install-windows-
full.html "PostgreSQL 10 - 18.1. Building with Visual C++ or the Microsoft
Windows SDK") / [9.6](/docs/9.6/install-windows-full.html "PostgreSQL 9.6 -
18.1. Building with Visual C++ or the Microsoft Windows SDK") /
[9.5](/docs/9.5/install-windows-full.html "PostgreSQL 9.5 - 18.1. Building
with Visual C++ or the Microsoft Windows SDK") / [9.4](/docs/9.4/install-
windows-full.html "PostgreSQL 9.4 - 18.1. Building with Visual C++ or the
Microsoft Windows SDK") / [9.3](/docs/9.3/install-windows-full.html
"PostgreSQL 9.3 - 18.1. Building with Visual C++ or the Microsoft Windows
SDK") / [9.2](/docs/9.2/install-windows-full.html "PostgreSQL 9.2 -
18.1. Building with Visual C++ or the Microsoft Windows SDK") /
[9.1](/docs/9.1/install-windows-full.html "PostgreSQL 9.1 - 18.1. Building
with Visual C++ or the Microsoft Windows SDK") / [9.0](/docs/9.0/install-
windows-full.html "PostgreSQL 9.0 - 18.1. Building with Visual C++ or the
Microsoft Windows SDK")

__

18.1. Building with Visual C++ or the Microsoft Windows SDK  
---  
[Prev](install-windows.html "Chapter 18. Installation from Source Code on Windows")  | [Up](install-windows.html "Chapter 18. Installation from Source Code on Windows") | Chapter 18. Installation from Source Code on Windows | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime.html "Chapter 19. Server Setup and Operation")  
  
* * *

## 18.1. Building with Visual C++ or the Microsoft Windows SDK #

[18.1.1. Requirements](install-windows-full.html#INSTALL-WINDOWS-FULL-
REQUIREMENTS)

[18.1.2. Special Considerations for 64-Bit Windows](install-windows-
full.html#INSTALL-WINDOWS-FULL-64-BIT)

[18.1.3. Building](install-windows-full.html#INSTALL-WINDOWS-FULL-BUILD)

[18.1.4. Cleaning and Installing](install-windows-full.html#INSTALL-WINDOWS-
FULL-CLEAN-INST)

[18.1.5. Running the Regression Tests](install-windows-full.html#INSTALL-
WINDOWS-FULL-REG-TESTS)

PostgreSQL can be built using the Visual C++ compiler suite from Microsoft.
These compilers can be either from Visual Studio, Visual Studio Express or
some versions of the Microsoft Windows SDK. If you do not already have a
Visual Studio environment set up, the easiest ways are to use the compilers
from Visual Studio 2022 or those in the Windows SDK 10, which are both free
downloads from Microsoft.

Both 32-bit and 64-bit builds are possible with the Microsoft Compiler suite.
32-bit PostgreSQL builds are possible with Visual Studio 2015 to Visual Studio
2022, as well as standalone Windows SDK releases 10 and above. 64-bit
PostgreSQL builds are supported with Microsoft Windows SDK version 10 and
above or Visual Studio 2015 and above.

The tools for building using Visual C++ or Platform SDK are in the
`src\tools\msvc` directory. When building, make sure there are no tools from
MinGW or Cygwin present in your system PATH. Also, make sure you have all the
required Visual C++ tools available in the PATH. In Visual Studio, start the
Visual Studio Command Prompt. If you wish to build a 64-bit version, you must
use the 64-bit version of the command, and vice versa. Starting with Visual
Studio 2017 this can be done from the command line using `VsDevCmd.bat`, see
`-help` for the available options and their default values. `vsvars32.bat` is
available in Visual Studio 2015 and earlier versions for the same purpose.
From the Visual Studio Command Prompt, you can change the targeted CPU
architecture, build type, and target OS by using the `vcvarsall.bat` command,
e.g., `vcvarsall.bat x64 10.0.10240.0` to target Windows 10 with a 64-bit
release build. See `-help` for the other options of `vcvarsall.bat`. All
commands should be run from the `src\tools\msvc` directory.

Before you build, you can create the file `config.pl` to reflect any
configuration options you want to change, or the paths to any third party
libraries to use. The complete configuration is determined by first reading
and parsing the file `config_default.pl`, and then apply any changes from
`config.pl`. For example, to specify the location of your Python installation,
put the following in `config.pl`:

    
    
    $config->{python} = 'c:\python310';
    

You only need to specify those parameters that are different from what's in
`config_default.pl`.

If you need to set any other environment variables, create a file called
`buildenv.pl` and put the required commands there. For example, to add the
path for bison when it's not in the PATH, create a file containing:

    
    
    $ENV{PATH}=$ENV{PATH} . ';c:\some\where\bison\bin';
    

To pass additional command line arguments to the Visual Studio build command
(msbuild or vcbuild):

    
    
    $ENV{MSBFLAGS}="/m";
    

### 18.1.1. Requirements #

The following additional products are required to build PostgreSQL. Use the
`config.pl` file to specify which directories the libraries are available in.

Microsoft Windows SDK

    

If your build environment doesn't ship with a supported version of the
Microsoft Windows SDK it is recommended that you upgrade to the latest version
(currently version 10), available for download from
<https://www.microsoft.com/download>.

You must always include the Windows Headers and Libraries part of the SDK. If
you install a Windows SDK including the Visual C++ Compilers, you don't need
Visual Studio to build. Note that as of Version 8.0a the Windows SDK no longer
ships with a complete command-line build environment.

Strawberry Perl

    

Strawberry Perl is required to run the build generation scripts. MinGW or
Cygwin Perl will not work. It must also be present in the PATH. Binaries can
be downloaded from <https://strawberryperl.com>.

The following additional products are not required to get started, but are
required to build the complete package. Use the `config.pl` file to specify
which directories the libraries are available in.

Magicsplat Tcl

    

Required for building PL/Tcl. Binaries can be downloaded from
<https://www.magicsplat.com/tcl-installer/index.html>.

Bison and Flex

    

Bison and Flex are required to build from Git, but not required when building
from a release file. Only Bison versions 2.3 and later will work. Flex must be
version 2.5.35 or later.

Both Bison and Flex are included in the msys tool suite, available from
<http://www.mingw.org/wiki/MSYS> as part of the MinGW compiler suite.

You will need to add the directory containing `flex.exe` and `bison.exe` to
the PATH environment variable in `buildenv.pl` unless they are already in
PATH. In the case of MinGW, the directory is the `\msys\1.0\bin` subdirectory
of your MinGW installation directory.

### Note

The Bison distribution from GnuWin32 appears to have a bug that causes Bison
to malfunction when installed in a directory with spaces in the name, such as
the default location on English installations `C:\Program Files\GnuWin32`.
Consider installing into `C:\GnuWin32` or use the NTFS short name path to
GnuWin32 in your PATH environment setting (e.g., `C:\PROGRA~1\GnuWin32`).

Diff

    

Diff is required to run the regression tests, and can be downloaded from
<http://gnuwin32.sourceforge.net>.

Gettext

    

Gettext is required to build with NLS support, and can be downloaded from
<http://gnuwin32.sourceforge.net>. Note that binaries, dependencies and
developer files are all needed.

MIT Kerberos

    

Required for GSSAPI authentication support. MIT Kerberos can be downloaded
from <https://web.mit.edu/Kerberos/dist/index.html>.

libxml2 and libxslt

    

Required for XML support. Binaries can be downloaded from
<https://zlatkovic.com/pub/libxml> or source from <http://xmlsoft.org>. Note
that libxml2 requires iconv, which is available from the same download
location.

LZ4

    

Required for supporting LZ4 compression. Binaries and source can be downloaded
from <https://github.com/lz4/lz4/releases>.

Zstandard

    

Required for supporting Zstandard compression. Binaries and source can be
downloaded from <https://github.com/facebook/zstd/releases>.

OpenSSL

    

Required for SSL support. Binaries can be downloaded from
<https://slproweb.com/products/Win32OpenSSL.html> or source from
<https://www.openssl.org>.

ossp-uuid

    

Required for UUID-OSSP support (contrib only). Source can be downloaded from
<http://www.ossp.org/pkg/lib/uuid/>.

Python

    

Required for building PL/Python. Binaries can be downloaded from
<https://www.python.org>.

zlib

    

Required for compression support in pg_dump and pg_restore. Binaries can be
downloaded from <https://www.zlib.net>.

### 18.1.2. Special Considerations for 64-Bit Windows #

PostgreSQL will only build for the x64 architecture on 64-bit Windows.

Mixing 32- and 64-bit versions in the same build tree is not supported. The
build system will automatically detect if it's running in a 32- or 64-bit
environment, and build PostgreSQL accordingly. For this reason, it is
important to start the correct command prompt before building.

To use a server-side third party library such as Python or OpenSSL, this
library _must_ also be 64-bit. There is no support for loading a 32-bit
library in a 64-bit server. Several of the third party libraries that
PostgreSQL supports may only be available in 32-bit versions, in which case
they cannot be used with 64-bit PostgreSQL.

### 18.1.3. Building #

To build all of PostgreSQL in release configuration (the default), run the
command:

    
    
    **build**
    

To build all of PostgreSQL in debug configuration, run the command:

    
    
    **build DEBUG**
    

To build just a single project, for example psql, run the commands:

    
    
    **build psql**
    **build DEBUG psql**
    

To change the default build configuration to debug, put the following in the
`buildenv.pl` file:

    
    
    $ENV{CONFIG}="Debug";
    

It is also possible to build from inside the Visual Studio GUI. In this case,
you need to run:

    
    
    **perl mkvcbuild.pl**
    

from the command prompt, and then open the generated `pgsql.sln` (in the root
directory of the source tree) in Visual Studio.

### 18.1.4. Cleaning and Installing #

Most of the time, the automatic dependency tracking in Visual Studio will
handle changed files. But if there have been large changes, you may need to
clean the installation. To do this, simply run the `clean.bat` command, which
will automatically clean out all generated files. You can also run it with the
_`dist`_ parameter, in which case it will behave like **`make distclean`** and
remove the flex/bison output files as well.

By default, all files are written into a subdirectory of the `debug` or
`release` directories. To install these files using the standard layout, and
also generate the files required to initialize and use the database, run the
command:

    
    
    **install c:\destination\directory**
    

If you want to install only the client applications and interface libraries,
then you can use these commands:

    
    
    **install c:\destination\directory client**
    

### 18.1.5. Running the Regression Tests #

To run the regression tests, make sure you have completed the build of all
required parts first. Also, make sure that the DLLs required to load all parts
of the system (such as the Perl and Python DLLs for the procedural languages)
are present in the system path. If they are not, set it through the
`buildenv.pl` file. To run the tests, run one of the following commands from
the `src\tools\msvc` directory:

    
    
    **vcregress check**
    **vcregress installcheck**
    **vcregress plcheck**
    **vcregress contribcheck**
    **vcregress modulescheck**
    **vcregress ecpgcheck**
    **vcregress isolationcheck**
    **vcregress bincheck**
    **vcregress recoverycheck**
    **vcregress taptest**
    

To change the schedule used (default is parallel), append it to the command
line like:

    
    
    **vcregress check serial**
    

`vcregress taptest` can be used to run the TAP tests of a target directory,
like:

    
    
    **vcregress taptest src\bin\initdb\**
    

For more information about the regression tests, see [Chapter 33](regress.html
"Chapter 33. Regression Tests").

Running the regression tests on client programs with `vcregress bincheck`, on
recovery tests with `vcregress recoverycheck`, or TAP tests specified with
`vcregress taptest` requires an additional Perl module to be installed:

IPC::Run

    

As of this writing, `IPC::Run` is not included in the ActiveState Perl
installation, nor in the ActiveState Perl Package Manager (PPM) library. To
install, download the `IPC-Run-<version>.tar.gz` source archive from CPAN, at
<https://metacpan.org/dist/IPC-Run>, and uncompress. Edit the `buildenv.pl`
file, and add a PERL5LIB variable to point to the `lib` subdirectory from the
extracted archive. For example:

    
    
    $ENV{PERL5LIB}=$ENV{PERL5LIB} . ';c:\IPC-Run-0.94\lib';
    

The TAP tests run with `vcregress` support the environment variables
`PROVE_TESTS`, that is expanded automatically using the name patterns given,
and `PROVE_FLAGS`. These can be set on a Windows terminal, before running
`vcregress`:

    
    
    set PROVE_FLAGS=--timer --jobs 2
    set PROVE_TESTS=t/020*.pl t/010*.pl
    

It is also possible to set up those parameters in `buildenv.pl`:

    
    
    $ENV{PROVE_FLAGS}='--timer --jobs 2'
    $ENV{PROVE_TESTS}='t/020*.pl t/010*.pl'
    

Additionally, the behavior of TAP tests can be controlled by a set of
environment variables, see [Section 33.4.1](regress-tap.html#REGRESS-TAP-VARS
"33.4.1. Environment Variables").

Some of the TAP tests depend on a set of external commands that would
optionally trigger tests related to them. Each one of those variables can be
set or unset in `buildenv.pl`:

`GZIP_PROGRAM`

    

Path to a gzip command. The default is `gzip`, which will search for a command
by that name in the configured `PATH`.

`LZ4`

    

Path to a lz4 command. The default is `lz4`, which will search for a command
by that name in the configured `PATH`.

`OPENSSL`

    

Path to an openssl command. The default is `openssl`, which will search for a
command by that name in the configured `PATH`.

`TAR`

    

Path to a tar command. The default is `tar`, which will search for a command
by that name in the configured `PATH`.

`ZSTD`

    

Path to a zstd command. The default is `zstd`, which will search for a command
by that name in the configured `PATH`.

* * *

[Prev](install-windows.html "Chapter 18. Installation from Source Code on Windows")  | [Up](install-windows.html "Chapter 18. Installation from Source Code on Windows") |  [Next](runtime.html "Chapter 19. Server Setup and Operation")  
---|---|---  
Chapter 18. Installation from Source Code on Windows  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 19. Server Setup and Operation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/install-windows-full.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

