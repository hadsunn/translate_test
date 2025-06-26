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

Supported Versions: [Current](/docs/current/nls-programmer.html "PostgreSQL 17
- 57.2. For the Programmer") ([17](/docs/17/nls-programmer.html "PostgreSQL 17
- 57.2. For the Programmer")) / [16](/docs/16/nls-programmer.html "PostgreSQL
16 - 57.2. For the Programmer") / [15](/docs/15/nls-programmer.html
"PostgreSQL 15 - 57.2. For the Programmer") / [14](/docs/14/nls-
programmer.html "PostgreSQL 14 - 57.2. For the Programmer") /
[13](/docs/13/nls-programmer.html "PostgreSQL 13 - 57.2. For the Programmer")

Development Versions: [18](/docs/18/nls-programmer.html "PostgreSQL 18 -
57.2. For the Programmer") / [devel](/docs/devel/nls-programmer.html
"PostgreSQL devel - 57.2. For the Programmer")

Unsupported versions: [12](/docs/12/nls-programmer.html "PostgreSQL 12 -
57.2. For the Programmer") / [11](/docs/11/nls-programmer.html "PostgreSQL 11
- 57.2. For the Programmer") / [10](/docs/10/nls-programmer.html "PostgreSQL
10 - 57.2. For the Programmer") / [9.6](/docs/9.6/nls-programmer.html
"PostgreSQL 9.6 - 57.2. For the Programmer") / [9.5](/docs/9.5/nls-
programmer.html "PostgreSQL 9.5 - 57.2. For the Programmer") /
[9.4](/docs/9.4/nls-programmer.html "PostgreSQL 9.4 - 57.2. For the
Programmer") / [9.3](/docs/9.3/nls-programmer.html "PostgreSQL 9.3 - 57.2. For
the Programmer") / [9.2](/docs/9.2/nls-programmer.html "PostgreSQL 9.2 -
57.2. For the Programmer") / [9.1](/docs/9.1/nls-programmer.html "PostgreSQL
9.1 - 57.2. For the Programmer") / [9.0](/docs/9.0/nls-programmer.html
"PostgreSQL 9.0 - 57.2. For the Programmer") / [8.4](/docs/8.4/nls-
programmer.html "PostgreSQL 8.4 - 57.2. For the Programmer") /
[8.3](/docs/8.3/nls-programmer.html "PostgreSQL 8.3 - 57.2. For the
Programmer") / [8.2](/docs/8.2/nls-programmer.html "PostgreSQL 8.2 - 57.2. For
the Programmer") / [8.1](/docs/8.1/nls-programmer.html "PostgreSQL 8.1 -
57.2. For the Programmer") / [8.0](/docs/8.0/nls-programmer.html "PostgreSQL
8.0 - 57.2. For the Programmer") / [7.4](/docs/7.4/nls-programmer.html
"PostgreSQL 7.4 - 57.2. For the Programmer") / [7.3](/docs/7.3/nls-
programmer.html "PostgreSQL 7.3 - 57.2. For the Programmer") /
[7.2](/docs/7.2/nls-programmer.html "PostgreSQL 7.2 - 57.2. For the
Programmer")

__

57.2. For the Programmer  
---  
[Prev](nls-translator.html "57.1. For the Translator")  | [Up](nls.html "Chapter 57. Native Language Support") | Chapter 57. Native Language Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plhandler.html "Chapter 58. Writing a Procedural Language Handler")  
  
* * *

## 57.2. For the Programmer #

[57.2.1. Mechanics](nls-programmer.html#NLS-MECHANICS)

[57.2.2. Message-Writing Guidelines](nls-programmer.html#NLS-GUIDELINES)

### 57.2.1. Mechanics #

This section describes how to implement native language support in a program
or library that is part of the PostgreSQL distribution. Currently, it only
applies to C programs.

**Adding NLS Support to a Program**

  1. Insert this code into the start-up sequence of the program:
         
         #ifdef ENABLE_NLS
         #include <locale.h>
         #endif
         
         ...
         
         #ifdef ENABLE_NLS
         setlocale(LC_ALL, "");
         bindtextdomain("_progname_ ", LOCALEDIR);
         textdomain("_progname_ ");
         #endif
         

(The _`progname`_ can actually be chosen freely.)

  2. Wherever a message that is a candidate for translation is found, a call to `gettext()` needs to be inserted. E.g.:
         
         fprintf(stderr, "panic level %d\n", lvl);
         

would be changed to:

         
         fprintf(stderr, gettext("panic level %d\n"), lvl);
         

(`gettext` is defined as a no-op if NLS support is not configured.)

This tends to add a lot of clutter. One common shortcut is to use:

         
         #define _(x) gettext(x)
         

Another solution is feasible if the program does much of its communication
through one or a few functions, such as `ereport()` in the backend. Then you
make this function call `gettext` internally on all input strings.

  3. Add a file `nls.mk` in the directory with the program sources. This file will be read as a makefile. The following variable assignments need to be made here:

`CATALOG_NAME`

    

The program name, as provided in the `textdomain()` call.

`GETTEXT_FILES`

    

List of files that contain translatable strings, i.e., those marked with
`gettext` or an alternative solution. Eventually, this will include nearly all
source files of the program. If this list gets too long you can make the first
“file” be a `+` and the second word be a file that contains one file name per
line.

`GETTEXT_TRIGGERS`

    

The tools that generate message catalogs for the translators to work on need
to know what function calls contain translatable strings. By default, only
`gettext()` calls are known. If you used `_` or other identifiers you need to
list them here. If the translatable string is not the first argument, the item
needs to be of the form `func:2` (for the second argument). If you have a
function that supports pluralized messages, the item should look like
`func:1,2` (identifying the singular and plural message arguments).

  4. Add a file `po/LINGUAS`, which will contain the list of provided translations — initially empty.

The build system will automatically take care of building and installing the
message catalogs.

### 57.2.2. Message-Writing Guidelines #

Here are some guidelines for writing messages that are easily translatable.

  * Do not construct sentences at run-time, like:
        
        printf("Files were %s.\n", flag ? "copied" : "removed");
        

The word order within the sentence might be different in other languages.
Also, even if you remember to call `gettext()` on each fragment, the fragments
might not translate well separately. It's better to duplicate a little code so
that each message to be translated is a coherent whole. Only numbers, file
names, and such-like run-time variables should be inserted at run time into a
message text.

  * For similar reasons, this won't work:
        
        printf("copied %d file%s", n, n!=1 ? "s" : "");
        

because it assumes how the plural is formed. If you figured you could solve it
like this:

        
        if (n==1)
            printf("copied 1 file");
        else
            printf("copied %d files", n):
        

then be disappointed. Some languages have more than two forms, with some
peculiar rules. It's often best to design the message to avoid the issue
altogether, for instance like this:

        
        printf("number of copied files: %d", n);
        

If you really want to construct a properly pluralized message, there is
support for this, but it's a bit awkward. When generating a primary or detail
error message in `ereport()`, you can write something like this:

        
        errmsg_plural("copied %d file",
                      "copied %d files",
                      n,
                      n)
        

The first argument is the format string appropriate for English singular form,
the second is the format string appropriate for English plural form, and the
third is the integer control value that determines which plural form to use.
Subsequent arguments are formatted per the format string as usual. (Normally,
the pluralization control value will also be one of the values to be
formatted, so it has to be written twice.) In English it only matters whether
_`n`_ is 1 or not 1, but in other languages there can be many different plural
forms. The translator sees the two English forms as a group and has the
opportunity to supply multiple substitute strings, with the appropriate one
being selected based on the run-time value of _`n`_.

If you need to pluralize a message that isn't going directly to an `errmsg` or
`errdetail` report, you have to use the underlying function `ngettext`. See
the gettext documentation.

  * If you want to communicate something to the translator, such as about how a message is intended to line up with other output, precede the occurrence of the string with a comment that starts with `translator`, e.g.:
        
        /* translator: This message is not what it seems to be. */
        

These comments are copied to the message catalog files so that the translators
can see them.

* * *

[Prev](nls-translator.html "57.1. For the Translator")  | [Up](nls.html "Chapter 57. Native Language Support") |  [Next](plhandler.html "Chapter 58. Writing a Procedural Language Handler")  
---|---|---  
57.1. For the Translator  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 58. Writing a Procedural Language Handler  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/nls-programmer.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

