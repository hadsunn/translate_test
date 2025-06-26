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

Supported Versions: [Current](/docs/current/installation-platform-notes.html
"PostgreSQL 17 - 17.7. Platform-Specific Notes") ([17](/docs/17/installation-
platform-notes.html "PostgreSQL 17 - 17.7. Platform-Specific Notes")) /
[16](/docs/16/installation-platform-notes.html "PostgreSQL 16 -
17.7. Platform-Specific Notes") / [15](/docs/15/installation-platform-
notes.html "PostgreSQL 15 - 17.7. Platform-Specific Notes") /
[14](/docs/14/installation-platform-notes.html "PostgreSQL 14 -
17.7. Platform-Specific Notes") / [13](/docs/13/installation-platform-
notes.html "PostgreSQL 13 - 17.7. Platform-Specific Notes")

Development Versions: [18](/docs/18/installation-platform-notes.html
"PostgreSQL 18 - 17.7. Platform-Specific Notes") /
[devel](/docs/devel/installation-platform-notes.html "PostgreSQL devel -
17.7. Platform-Specific Notes")

Unsupported versions: [12](/docs/12/installation-platform-notes.html
"PostgreSQL 12 - 17.7. Platform-Specific Notes") / [11](/docs/11/installation-
platform-notes.html "PostgreSQL 11 - 17.7. Platform-Specific Notes") /
[10](/docs/10/installation-platform-notes.html "PostgreSQL 10 -
17.7. Platform-Specific Notes") / [9.6](/docs/9.6/installation-platform-
notes.html "PostgreSQL 9.6 - 17.7. Platform-Specific Notes") /
[9.5](/docs/9.5/installation-platform-notes.html "PostgreSQL 9.5 -
17.7. Platform-Specific Notes") / [9.4](/docs/9.4/installation-platform-
notes.html "PostgreSQL 9.4 - 17.7. Platform-Specific Notes") /
[9.3](/docs/9.3/installation-platform-notes.html "PostgreSQL 9.3 -
17.7. Platform-Specific Notes") / [9.2](/docs/9.2/installation-platform-
notes.html "PostgreSQL 9.2 - 17.7. Platform-Specific Notes") /
[9.1](/docs/9.1/installation-platform-notes.html "PostgreSQL 9.1 -
17.7. Platform-Specific Notes") / [9.0](/docs/9.0/installation-platform-
notes.html "PostgreSQL 9.0 - 17.7. Platform-Specific Notes") /
[8.4](/docs/8.4/installation-platform-notes.html "PostgreSQL 8.4 -
17.7. Platform-Specific Notes")

__

17.7. Platform-Specific Notes  
---  
[Prev](supported-platforms.html "17.6. Supported Platforms")  | [Up](installation.html "Chapter 17. Installation from Source Code") | Chapter 17. Installation from Source Code | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-windows.html "Chapter 18. Installation from Source Code on Windows")  
  
* * *

## 17.7. Platform-Specific Notes #

[17.7.1. AIX](installation-platform-notes.html#INSTALLATION-NOTES-AIX)

[17.7.2. Cygwin](installation-platform-notes.html#INSTALLATION-NOTES-CYGWIN)

[17.7.3. macOS](installation-platform-notes.html#INSTALLATION-NOTES-MACOS)

[17.7.4. MinGW/Native Windows](installation-platform-notes.html#INSTALLATION-
NOTES-MINGW)

[17.7.5. Solaris](installation-platform-notes.html#INSTALLATION-NOTES-SOLARIS)

This section documents additional platform-specific issues regarding the
installation and setup of PostgreSQL. Be sure to read the installation
instructions, and in particular [Section 17.1](install-requirements.html
"17.1. Requirements") as well. Also, check [Chapter 33](regress.html
"Chapter 33. Regression Tests") regarding the interpretation of regression
test results.

Platforms that are not covered here have no known platform-specific
installation issues.

### 17.7.1. AIX #

You can use GCC or the native IBM compiler `xlc` to build PostgreSQL on AIX.

AIX versions before 7.1 are no longer tested nor supported by the PostgreSQL
community.

#### 17.7.1.1. Memory Management #

AIX can be somewhat peculiar with regards to the way it does memory
management. You can have a server with many multiples of gigabytes of RAM
free, but still get out of memory or address space errors when running
applications. One example is loading of extensions failing with unusual
errors. For example, running as the owner of the PostgreSQL installation:

    
    
    =# CREATE EXTENSION plperl;
    ERROR:  could not load library "/opt/dbs/pgsql/lib/plperl.so": A memory address is not in the address space for the process.
    

Running as a non-owner in the group possessing the PostgreSQL installation:

    
    
    =# CREATE EXTENSION plperl;
    ERROR:  could not load library "/opt/dbs/pgsql/lib/plperl.so": Bad address
    

Another example is out of memory errors in the PostgreSQL server logs, with
every memory allocation near or greater than 256 MB failing.

The overall cause of all these problems is the default bittedness and memory
model used by the server process. By default, all binaries built on AIX are
32-bit. This does not depend upon hardware type or kernel in use. These 32-bit
processes are limited to 4 GB of memory laid out in 256 MB segments using one
of a few models. The default allows for less than 256 MB in the heap as it
shares a single segment with the stack.

In the case of the `plperl` example, above, check your umask and the
permissions of the binaries in your PostgreSQL installation. The binaries
involved in that example were 32-bit and installed as mode 750 instead of 755.
Due to the permissions being set in this fashion, only the owner or a member
of the possessing group can load the library. Since it isn't world-readable,
the loader places the object into the process' heap instead of the shared
library segments where it would otherwise be placed.

The “ideal” solution for this is to use a 64-bit build of PostgreSQL, but that
is not always practical, because systems with 32-bit processors can build, but
not run, 64-bit binaries.

If a 32-bit binary is desired, set `LDR_CNTRL` to `MAXDATA=0x _`n`_ 0000000`,
where 1 <= n <= 8, before starting the PostgreSQL server, and try different
values and `postgresql.conf` settings to find a configuration that works
satisfactorily. This use of `LDR_CNTRL` tells AIX that you want the server to
have `MAXDATA` bytes set aside for the heap, allocated in 256 MB segments.
When you find a workable configuration, `ldedit` can be used to modify the
binaries so that they default to using the desired heap size. PostgreSQL can
also be rebuilt, passing `configure LDFLAGS="-Wl,-bmaxdata:0x _`n`_ 0000000"`
to achieve the same effect.

For a 64-bit build, set `OBJECT_MODE` to 64 and pass `CC="gcc -maix64"` and
`LDFLAGS="-Wl,-bbigtoc"` to `configure`. (Options for `xlc` might differ.) If
you omit the export of `OBJECT_MODE`, your build may fail with linker errors.
When `OBJECT_MODE` is set, it tells AIX's build utilities such as `ar`, `as`,
and `ld` what type of objects to default to handling.

By default, overcommit of paging space can happen. While we have not seen this
occur, AIX will kill processes when it runs out of memory and the overcommit
is accessed. The closest to this that we have seen is fork failing because the
system decided that there was not enough memory for another process. Like many
other parts of AIX, the paging space allocation method and out-of-memory kill
is configurable on a system- or process-wide basis if this becomes a problem.

### 17.7.2. Cygwin #

PostgreSQL can be built using Cygwin, a Linux-like environment for Windows,
but that method is inferior to the native Windows build (see [Chapter
18](install-windows.html "Chapter 18. Installation from Source Code on
Windows")) and running a server under Cygwin is no longer recommended.

When building from source, proceed according to the Unix-style installation
procedure (i.e., `./configure; make`; etc.), noting the following Cygwin-
specific differences:

  * Set your path to use the Cygwin bin directory before the Windows utilities. This will help prevent problems with compilation.

  * The `adduser` command is not supported; use the appropriate user management application on Windows. Otherwise, skip this step.

  * The `su` command is not supported; use ssh to simulate su on Windows. Otherwise, skip this step.

  * OpenSSL is not supported.

  * Start `cygserver` for shared memory support. To do this, enter the command `/usr/sbin/cygserver &`. This program needs to be running anytime you start the PostgreSQL server or initialize a database cluster (`initdb`). The default `cygserver` configuration may need to be changed (e.g., increase `SEMMNS`) to prevent PostgreSQL from failing due to a lack of system resources.

  * Building might fail on some systems where a locale other than C is in use. To fix this, set the locale to C by doing `export LANG=C.utf8` before building, and then setting it back to the previous setting after you have installed PostgreSQL.

  * The parallel regression tests (`make check`) can generate spurious regression test failures due to overflowing the `listen()` backlog queue which causes connection refused errors or hangs. You can limit the number of connections using the make variable `MAX_CONNECTIONS` thus:
        
        make MAX_CONNECTIONS=5 check
        

(On some systems you can have up to about 10 simultaneous connections.)

It is possible to install `cygserver` and the PostgreSQL server as Windows NT
services. For information on how to do this, please refer to the `README`
document included with the PostgreSQL binary package on Cygwin. It is
installed in the directory `/usr/share/doc/Cygwin`.

### 17.7.3. macOS #

To build PostgreSQL from source on macOS, you will need to install Apple's
command line developer tools, which can be done by issuing

    
    
    xcode-select --install
    

(note that this will pop up a GUI dialog window for confirmation). You may or
may not wish to also install Xcode.

On recent macOS releases, it's necessary to embed the “sysroot” path in the
include switches used to find some system header files. This results in the
outputs of the configure script varying depending on which SDK version was
used during configure. That shouldn't pose any problem in simple scenarios,
but if you are trying to do something like building an extension on a
different machine than the server code was built on, you may need to force use
of a different sysroot path. To do that, set `PG_SYSROOT`, for example

    
    
    make PG_SYSROOT=_/desired/path_ all
    

To find out the appropriate path on your machine, run

    
    
    xcrun --show-sdk-path
    

Note that building an extension using a different sysroot version than was
used to build the core server is not really recommended; in the worst case it
could result in hard-to-debug ABI inconsistencies.

You can also select a non-default sysroot path when configuring, by specifying
`PG_SYSROOT` to configure:

    
    
    ./configure ... PG_SYSROOT=_/desired/path_
    

This would primarily be useful to cross-compile for some other macOS version.
There is no guarantee that the resulting executables will run on the current
host.

To suppress the `-isysroot` options altogether, use

    
    
    ./configure ... PG_SYSROOT=none
    

(any nonexistent pathname will work). This might be useful if you wish to
build with a non-Apple compiler, but beware that that case is not tested or
supported by the PostgreSQL developers.

macOS's “System Integrity Protection” (SIP) feature breaks `make check`,
because it prevents passing the needed setting of `DYLD_LIBRARY_PATH` down to
the executables being tested. You can work around that by doing `make install`
before `make check`. Most PostgreSQL developers just turn off SIP, though.

### 17.7.4. MinGW/Native Windows #

PostgreSQL for Windows can be built using MinGW, a Unix-like build environment
for Microsoft operating systems, or using Microsoft's Visual C++ compiler
suite. The MinGW build procedure uses the normal build system described in
this chapter; the Visual C++ build works completely differently and is
described in [Chapter 18](install-windows.html "Chapter 18. Installation from
Source Code on Windows").

The native Windows port requires a 32 or 64-bit version of Windows 2000 or
later. Earlier operating systems do not have sufficient infrastructure (but
Cygwin may be used on those). MinGW, the Unix-like build tools, and MSYS, a
collection of Unix tools required to run shell scripts like `configure`, can
be downloaded from <http://www.mingw.org/>. Neither is required to run the
resulting binaries; they are needed only for creating the binaries.

To build 64 bit binaries using MinGW, install the 64 bit tool set from
<https://mingw-w64.org/>, put its bin directory in the `PATH`, and run
`configure` with the `--host=x86_64-w64-mingw32` option.

After you have everything installed, it is suggested that you run psql under
`CMD.EXE`, as the MSYS console has buffering issues.

#### 17.7.4.1. Collecting Crash Dumps on Windows #

If PostgreSQL on Windows crashes, it has the ability to generate minidumps
that can be used to track down the cause for the crash, similar to core dumps
on Unix. These dumps can be read using the Windows Debugger Tools or using
Visual Studio. To enable the generation of dumps on Windows, create a
subdirectory named `crashdumps` inside the cluster data directory. The dumps
will then be written into this directory with a unique name based on the
identifier of the crashing process and the current time of the crash.

### 17.7.5. Solaris #

PostgreSQL is well-supported on Solaris. The more up to date your operating
system, the fewer issues you will experience.

#### 17.7.5.1. Required Tools #

You can build with either GCC or Sun's compiler suite. For better code
optimization, Sun's compiler is strongly recommended on the SPARC
architecture. If you are using Sun's compiler, be careful not to select
`/usr/ucb/cc`; use `/opt/SUNWspro/bin/cc`.

You can download Sun Studio from <https://www.oracle.com/technetwork/server-
storage/solarisstudio/downloads/>. Many GNU tools are integrated into Solaris
10, or they are present on the Solaris companion CD. If you need packages for
older versions of Solaris, you can find these tools at
<http://www.sunfreeware.com>. If you prefer sources, look at
<https://www.gnu.org/prep/ftp>.

#### 17.7.5.2. configure Complains About a Failed Test Program #

If `configure` complains about a failed test program, this is probably a case
of the run-time linker being unable to find some library, probably libz,
libreadline or some other non-standard library such as libssl. To point it to
the right location, set the `LDFLAGS` environment variable on the `configure`
command line, e.g.,

    
    
    configure ... LDFLAGS="-R /usr/sfw/lib:/opt/sfw/lib:/usr/local/lib"
    

See the ld man page for more information.

#### 17.7.5.3. Compiling for Optimal Performance #

On the SPARC architecture, Sun Studio is strongly recommended for compilation.
Try using the `-xO5` optimization flag to generate significantly faster
binaries. Do not use any flags that modify behavior of floating-point
operations and `errno` processing (e.g., `-fast`).

If you do not have a reason to use 64-bit binaries on SPARC, prefer the 32-bit
version. The 64-bit operations are slower and 64-bit binaries are slower than
the 32-bit variants. On the other hand, 32-bit code on the AMD64 CPU family is
not native, so 32-bit code is significantly slower on that CPU family.

#### 17.7.5.4. Using DTrace for Tracing PostgreSQL #

Yes, using DTrace is possible. See [Section 28.5](dynamic-trace.html
"28.5. Dynamic Tracing") for further information.

If you see the linking of the `postgres` executable abort with an error
message like:

    
    
    Undefined                       first referenced
     symbol                             in file
    AbortTransaction                    utils/probes.o
    CommitTransaction                   utils/probes.o
    ld: fatal: Symbol referencing errors. No output written to postgres
    collect2: ld returned 1 exit status
    make: *** [postgres] Error 1
    

your DTrace installation is too old to handle probes in static functions. You
need Solaris 10u4 or newer to use DTrace.

* * *

[Prev](supported-platforms.html "17.6. Supported Platforms")  | [Up](installation.html "Chapter 17. Installation from Source Code") |  [Next](install-windows.html "Chapter 18. Installation from Source Code on Windows")  
---|---|---  
17.6. Supported Platforms  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 18. Installation from Source Code on Windows  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/installation-platform-
notes.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

