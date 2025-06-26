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

Supported Versions: [Current](/docs/current/docguide-build.html "PostgreSQL 17
- J.3. Building the Documentation with Make") ([17](/docs/17/docguide-
build.html "PostgreSQL 17 - J.3. Building the Documentation with Make")) /
[16](/docs/16/docguide-build.html "PostgreSQL 16 - J.3. Building the
Documentation with Make") / [15](/docs/15/docguide-build.html "PostgreSQL 15 -
J.3. Building the Documentation with Make") / [14](/docs/14/docguide-
build.html "PostgreSQL 14 - J.3. Building the Documentation with Make") /
[13](/docs/13/docguide-build.html "PostgreSQL 13 - J.3. Building the
Documentation with Make")

Development Versions: [18](/docs/18/docguide-build.html "PostgreSQL 18 -
J.3. Building the Documentation with Make") / [devel](/docs/devel/docguide-
build.html "PostgreSQL devel - J.3. Building the Documentation with Make")

Unsupported versions: [12](/docs/12/docguide-build.html "PostgreSQL 12 -
J.3. Building the Documentation with Make") / [11](/docs/11/docguide-
build.html "PostgreSQL 11 - J.3. Building the Documentation with Make") /
[10](/docs/10/docguide-build.html "PostgreSQL 10 - J.3. Building the
Documentation with Make") / [9.6](/docs/9.6/docguide-build.html "PostgreSQL
9.6 - J.3. Building the Documentation with Make") / [9.5](/docs/9.5/docguide-
build.html "PostgreSQL 9.5 - J.3. Building the Documentation with Make") /
[9.4](/docs/9.4/docguide-build.html "PostgreSQL 9.4 - J.3. Building the
Documentation with Make") / [9.3](/docs/9.3/docguide-build.html "PostgreSQL
9.3 - J.3. Building the Documentation with Make") / [9.2](/docs/9.2/docguide-
build.html "PostgreSQL 9.2 - J.3. Building the Documentation with Make") /
[9.1](/docs/9.1/docguide-build.html "PostgreSQL 9.1 - J.3. Building the
Documentation with Make") / [9.0](/docs/9.0/docguide-build.html "PostgreSQL
9.0 - J.3. Building the Documentation with Make") / [8.4](/docs/8.4/docguide-
build.html "PostgreSQL 8.4 - J.3. Building the Documentation with Make") /
[8.3](/docs/8.3/docguide-build.html "PostgreSQL 8.3 - J.3. Building the
Documentation with Make") / [8.2](/docs/8.2/docguide-build.html "PostgreSQL
8.2 - J.3. Building the Documentation with Make") / [8.1](/docs/8.1/docguide-
build.html "PostgreSQL 8.1 - J.3. Building the Documentation with Make") /
[8.0](/docs/8.0/docguide-build.html "PostgreSQL 8.0 - J.3. Building the
Documentation with Make") / [7.4](/docs/7.4/docguide-build.html "PostgreSQL
7.4 - J.3. Building the Documentation with Make")

__

J.3. Building the Documentation with Make  
---  
[Prev](docguide-toolsets.html "J.2. Tool Sets")  | [Up](docguide.html "Appendix J. Documentation") | Appendix J. Documentation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](docguide-build-meson.html "J.4. Building the Documentation with Meson")  
  
* * *

## J.3. Building the Documentation with Make #

[J.3.1. HTML](docguide-build.html#DOCGUIDE-BUILD-HTML)

[J.3.2. Manpages](docguide-build.html#DOCGUIDE-BUILD-MANPAGES)

[J.3.3. PDF](docguide-build.html#DOCGUIDE-BUILD-PDF)

[J.3.4. Plain Text Files](docguide-build.html#DOCGUIDE-BUILD-PLAIN-TEXT)

[J.3.5. Syntax Check](docguide-build.html#DOCGUIDE-BUILD-SYNTAX-CHECK)

Once you have everything set up, change to the directory `doc/src/sgml` and
run one of the commands described in the following subsections to build the
documentation. (Remember to use GNU make.)

### J.3.1. HTML #

To build the HTML version of the documentation:

    
    
    doc/src/sgml$ **make html**
    

This is also the default target. The output appears in the subdirectory
`html`.

To produce HTML documentation with the stylesheet used on
[postgresql.org](https://www.postgresql.org/docs/current/) instead of the
default simple style use:

    
    
    doc/src/sgml$ **make STYLE=website html**
    

If the `STYLE=website` option is used, the generated HTML files include
references to stylesheets hosted on
[postgresql.org](https://www.postgresql.org/docs/current/) and require network
access to view.

### J.3.2. Manpages #

We use the DocBook XSL stylesheets to convert DocBook `refentry` pages to
*roff output suitable for man pages. To create the man pages, use the command:

    
    
    doc/src/sgml$ **make man**
    

### J.3.3. PDF #

To produce a PDF rendition of the documentation using FOP, you can use one of
the following commands, depending on the preferred paper format:

  * For A4 format:
        
        doc/src/sgml$ **make postgres-A4.pdf**
        

  * For U.S. letter format:
        
        doc/src/sgml$ **make postgres-US.pdf**
        

Because the PostgreSQL documentation is fairly big, FOP will require a
significant amount of memory. Because of that, on some systems, the build will
fail with a memory-related error message. This can usually be fixed by
configuring Java heap settings in the configuration file `~/.foprc`, for
example:

    
    
    # FOP binary distribution
    FOP_OPTS='-Xmx1500m'
    # Debian
    JAVA_ARGS='-Xmx1500m'
    # Red Hat
    ADDITIONAL_FLAGS='-Xmx1500m'
    

There is a minimum amount of memory that is required, and to some extent more
memory appears to make things a bit faster. On systems with very little memory
(less than 1 GB), the build will either be very slow due to swapping or will
not work at all.

In its default configuration FOP will emit an `INFO` message for each page.
The log level can be changed via `~/.foprc`:

    
    
    LOGCHOICE=-Dorg.apache.commons.logging.Log=​org.apache.commons.logging.impl.SimpleLog
    LOGLEVEL=-Dorg.apache.commons.logging.simplelog.defaultlog=WARN
    

Other XSL-FO processors can also be used manually, but the automated build
process only supports FOP.

### J.3.4. Plain Text Files #

The installation instructions are also distributed as plain text, in case they
are needed in a situation where better reading tools are not available. The
`INSTALL` file corresponds to [Chapter 17](installation.html
"Chapter 17. Installation from Source Code"), with some minor changes to
account for the different context. To recreate the file, change to the
directory `doc/src/sgml` and enter **`make INSTALL`**. Building text output
requires Pandoc version 1.13 or newer as an additional build tool.

In the past, the release notes and regression testing instructions were also
distributed as plain text, but this practice has been discontinued.

### J.3.5. Syntax Check #

Building the documentation can take very long. But there is a method to just
check the correct syntax of the documentation files, which only takes a few
seconds:

    
    
    doc/src/sgml$ **make check**
    

* * *

[Prev](docguide-toolsets.html "J.2. Tool Sets")  | [Up](docguide.html "Appendix J. Documentation") |  [Next](docguide-build-meson.html "J.4. Building the Documentation with Meson")  
---|---|---  
J.2. Tool Sets  | [Home](index.html "PostgreSQL 16.9 Documentation") |  J.4. Building the Documentation with Meson  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/docguide-build.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

