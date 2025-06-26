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

Supported Versions: [Current](/docs/current/install-post.html "PostgreSQL 17 -
17.5. Post-Installation Setup") ([17](/docs/17/install-post.html "PostgreSQL
17 - 17.5. Post-Installation Setup")) / [16](/docs/16/install-post.html
"PostgreSQL 16 - 17.5. Post-Installation Setup") / [15](/docs/15/install-
post.html "PostgreSQL 15 - 17.5. Post-Installation Setup") /
[14](/docs/14/install-post.html "PostgreSQL 14 - 17.5. Post-Installation
Setup") / [13](/docs/13/install-post.html "PostgreSQL 13 - 17.5. Post-
Installation Setup")

Development Versions: [18](/docs/18/install-post.html "PostgreSQL 18 -
17.5. Post-Installation Setup") / [devel](/docs/devel/install-post.html
"PostgreSQL devel - 17.5. Post-Installation Setup")

Unsupported versions: [12](/docs/12/install-post.html "PostgreSQL 12 -
17.5. Post-Installation Setup") / [11](/docs/11/install-post.html "PostgreSQL
11 - 17.5. Post-Installation Setup") / [10](/docs/10/install-post.html
"PostgreSQL 10 - 17.5. Post-Installation Setup") / [9.6](/docs/9.6/install-
post.html "PostgreSQL 9.6 - 17.5. Post-Installation Setup") /
[9.5](/docs/9.5/install-post.html "PostgreSQL 9.5 - 17.5. Post-Installation
Setup") / [9.4](/docs/9.4/install-post.html "PostgreSQL 9.4 - 17.5. Post-
Installation Setup") / [9.3](/docs/9.3/install-post.html "PostgreSQL 9.3 -
17.5. Post-Installation Setup") / [9.2](/docs/9.2/install-post.html
"PostgreSQL 9.2 - 17.5. Post-Installation Setup") / [9.1](/docs/9.1/install-
post.html "PostgreSQL 9.1 - 17.5. Post-Installation Setup") /
[9.0](/docs/9.0/install-post.html "PostgreSQL 9.0 - 17.5. Post-Installation
Setup") / [8.4](/docs/8.4/install-post.html "PostgreSQL 8.4 - 17.5. Post-
Installation Setup") / [8.3](/docs/8.3/install-post.html "PostgreSQL 8.3 -
17.5. Post-Installation Setup") / [8.2](/docs/8.2/install-post.html
"PostgreSQL 8.2 - 17.5. Post-Installation Setup") / [8.1](/docs/8.1/install-
post.html "PostgreSQL 8.1 - 17.5. Post-Installation Setup") /
[8.0](/docs/8.0/install-post.html "PostgreSQL 8.0 - 17.5. Post-Installation
Setup") / [7.4](/docs/7.4/install-post.html "PostgreSQL 7.4 - 17.5. Post-
Installation Setup") / [7.3](/docs/7.3/install-post.html "PostgreSQL 7.3 -
17.5. Post-Installation Setup") / [7.2](/docs/7.2/install-post.html
"PostgreSQL 7.2 - 17.5. Post-Installation Setup") / [7.1](/docs/7.1/install-
post.html "PostgreSQL 7.1 - 17.5. Post-Installation Setup")

__

17.5. Post-Installation Setup  
---  
[Prev](install-meson.html "17.4. Building and Installation with Meson")  | [Up](installation.html "Chapter 17. Installation from Source Code") | Chapter 17. Installation from Source Code | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](supported-platforms.html "17.6. Supported Platforms")  
  
* * *

## 17.5. Post-Installation Setup #

[17.5.1. Shared Libraries](install-post.html#INSTALL-POST-SHLIBS)

[17.5.2. Environment Variables](install-post.html#INSTALL-POST-ENV-VARS)

### 17.5.1. Shared Libraries #

On some systems with shared libraries you need to tell the system how to find
the newly installed shared libraries. The systems on which this is _not_
necessary include FreeBSD, Linux, NetBSD, OpenBSD, and Solaris.

The method to set the shared library search path varies between platforms, but
the most widely-used method is to set the environment variable
`LD_LIBRARY_PATH` like so: In Bourne shells (`sh`, `ksh`, `bash`, `zsh`):

    
    
    LD_LIBRARY_PATH=/usr/local/pgsql/lib
    export LD_LIBRARY_PATH
    

or in `csh` or `tcsh`:

    
    
    setenv LD_LIBRARY_PATH /usr/local/pgsql/lib
    

Replace `/usr/local/pgsql/lib` with whatever you set ``\--libdir`` to in [Step
1](install-make.html#CONFIGURE "Configuration"). You should put these commands
into a shell start-up file such as `/etc/profile` or `~/.bash_profile`. Some
good information about the caveats associated with this method can be found at
<http://xahlee.info/UnixResource_dir/_/ldpath.html>.

On some systems it might be preferable to set the environment variable
`LD_RUN_PATH` _before_ building.

On Cygwin, put the library directory in the `PATH` or move the `.dll` files
into the `bin` directory.

If in doubt, refer to the manual pages of your system (perhaps `ld.so` or
`rld`). If you later get a message like:

    
    
    psql: error in loading shared libraries
    libpq.so.2.1: cannot open shared object file: No such file or directory
    

then this step was necessary. Simply take care of it then.

If you are on Linux and you have root access, you can run:

    
    
    /sbin/ldconfig /usr/local/pgsql/lib
    

(or equivalent directory) after installation to enable the run-time linker to
find the shared libraries faster. Refer to the manual page of `ldconfig` for
more information. On FreeBSD, NetBSD, and OpenBSD the command is:

    
    
    /sbin/ldconfig -m /usr/local/pgsql/lib
    

instead. Other systems are not known to have an equivalent command.

### 17.5.2. Environment Variables #

If you installed into `/usr/local/pgsql` or some other location that is not
searched for programs by default, you should add `/usr/local/pgsql/bin` (or
whatever you set ``\--bindir`` to in [Step 1](install-make.html#CONFIGURE
"Configuration")) into your `PATH`. Strictly speaking, this is not necessary,
but it will make the use of PostgreSQL much more convenient.

To do this, add the following to your shell start-up file, such as
`~/.bash_profile` (or `/etc/profile`, if you want it to affect all users):

    
    
    PATH=/usr/local/pgsql/bin:$PATH
    export PATH
    

If you are using `csh` or `tcsh`, then use this command:

    
    
    set path = ( /usr/local/pgsql/bin $path )
    

To enable your system to find the man documentation, you need to add lines
like the following to a shell start-up file unless you installed into a
location that is searched by default:

    
    
    MANPATH=/usr/local/pgsql/share/man:$MANPATH
    export MANPATH
    

The environment variables `PGHOST` and `PGPORT` specify to client applications
the host and port of the database server, overriding the compiled-in defaults.
If you are going to run client applications remotely then it is convenient if
every user that plans to use the database sets `PGHOST`. This is not required,
however; the settings can be communicated via command line options to most
client programs.

* * *

[Prev](install-meson.html "17.4. Building and Installation with Meson")  | [Up](installation.html "Chapter 17. Installation from Source Code") |  [Next](supported-platforms.html "17.6. Supported Platforms")  
---|---|---  
17.4. Building and Installation with Meson  | [Home](index.html "PostgreSQL 16.9 Documentation") |  17.6. Supported Platforms  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/install-post.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

