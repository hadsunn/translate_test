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

Supported Versions: [Current](/docs/current/nls-translator.html "PostgreSQL 17
- 57.1. For the Translator") ([17](/docs/17/nls-translator.html "PostgreSQL 17
- 57.1. For the Translator")) / [16](/docs/16/nls-translator.html "PostgreSQL
16 - 57.1. For the Translator") / [15](/docs/15/nls-translator.html
"PostgreSQL 15 - 57.1. For the Translator") / [14](/docs/14/nls-
translator.html "PostgreSQL 14 - 57.1. For the Translator") /
[13](/docs/13/nls-translator.html "PostgreSQL 13 - 57.1. For the Translator")

Development Versions: [18](/docs/18/nls-translator.html "PostgreSQL 18 -
57.1. For the Translator") / [devel](/docs/devel/nls-translator.html
"PostgreSQL devel - 57.1. For the Translator")

Unsupported versions: [12](/docs/12/nls-translator.html "PostgreSQL 12 -
57.1. For the Translator") / [11](/docs/11/nls-translator.html "PostgreSQL 11
- 57.1. For the Translator") / [10](/docs/10/nls-translator.html "PostgreSQL
10 - 57.1. For the Translator") / [9.6](/docs/9.6/nls-translator.html
"PostgreSQL 9.6 - 57.1. For the Translator") / [9.5](/docs/9.5/nls-
translator.html "PostgreSQL 9.5 - 57.1. For the Translator") /
[9.4](/docs/9.4/nls-translator.html "PostgreSQL 9.4 - 57.1. For the
Translator") / [9.3](/docs/9.3/nls-translator.html "PostgreSQL 9.3 - 57.1. For
the Translator") / [9.2](/docs/9.2/nls-translator.html "PostgreSQL 9.2 -
57.1. For the Translator") / [9.1](/docs/9.1/nls-translator.html "PostgreSQL
9.1 - 57.1. For the Translator") / [9.0](/docs/9.0/nls-translator.html
"PostgreSQL 9.0 - 57.1. For the Translator") / [8.4](/docs/8.4/nls-
translator.html "PostgreSQL 8.4 - 57.1. For the Translator") /
[8.3](/docs/8.3/nls-translator.html "PostgreSQL 8.3 - 57.1. For the
Translator") / [8.2](/docs/8.2/nls-translator.html "PostgreSQL 8.2 - 57.1. For
the Translator")

__

57.1. For the Translator  
---  
[Prev](nls.html "Chapter 57. Native Language Support")  | [Up](nls.html "Chapter 57. Native Language Support") | Chapter 57. Native Language Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](nls-programmer.html "57.2. For the Programmer")  
  
* * *

## 57.1. For the Translator #

[57.1.1. Requirements](nls-translator.html#NLS-TRANSLATOR-REQUIREMENTS)

[57.1.2. Concepts](nls-translator.html#NLS-TRANSLATOR-CONCEPTS)

[57.1.3. Creating and Maintaining Message Catalogs](nls-translator.html#NLS-
TRANSLATOR-MESSAGE-CATALOGS)

[57.1.4. Editing the PO Files](nls-translator.html#NLS-TRANSLATOR-EDITING-PO)

PostgreSQL programs (server and client) can issue their messages in your
favorite language — if the messages have been translated. Creating and
maintaining translated message sets needs the help of people who speak their
own language well and want to contribute to the PostgreSQL effort. You do not
have to be a programmer at all to do this. This section explains how to help.

### 57.1.1. Requirements #

We won't judge your language skills — this section is about software tools.
Theoretically, you only need a text editor. But this is only in the unlikely
event that you do not want to try out your translated messages. When you
configure your source tree, be sure to use the `--enable-nls` option. This
will also check for the libintl library and the `msgfmt` program, which all
end users will need anyway. To try out your work, follow the applicable
portions of the installation instructions.

If you want to start a new translation effort or want to do a message catalog
merge (described later), you will need the programs `xgettext` and `msgmerge`,
respectively, in a GNU-compatible implementation. Later, we will try to
arrange it so that if you use a packaged source distribution, you won't need
`xgettext`. (If working from Git, you will still need it.) GNU Gettext 0.10.36
or later is currently recommended.

Your local gettext implementation should come with its own documentation. Some
of that is probably duplicated in what follows, but for additional details you
should look there.

### 57.1.2. Concepts #

The pairs of original (English) messages and their (possibly) translated
equivalents are kept in _message catalogs_ , one for each program (although
related programs can share a message catalog) and for each target language.
There are two file formats for message catalogs: The first is the “PO” file
(for Portable Object), which is a plain text file with special syntax that
translators edit. The second is the “MO” file (for Machine Object), which is a
binary file generated from the respective PO file and is used while the
internationalized program is run. Translators do not deal with MO files; in
fact hardly anyone does.

The extension of the message catalog file is to no surprise either `.po` or
`.mo`. The base name is either the name of the program it accompanies, or the
language the file is for, depending on the situation. This is a bit confusing.
Examples are `psql.po` (PO file for psql) or `fr.mo` (MO file in French).

The file format of the PO files is illustrated here:

    
    
    # comment
    
    msgid "original string"
    msgstr "translated string"
    
    msgid "more original"
    msgstr "another translated"
    "string can be broken up like this"
    
    ...
    

The msgid lines are extracted from the program source. (They need not be, but
this is the most common way.) The msgstr lines are initially empty and are
filled in with useful strings by the translator. The strings can contain
C-style escape characters and can be continued across lines as illustrated.
(The next line must start at the beginning of the line.)

The # character introduces a comment. If whitespace immediately follows the #
character, then this is a comment maintained by the translator. There can also
be automatic comments, which have a non-whitespace character immediately
following the #. These are maintained by the various tools that operate on the
PO files and are intended to aid the translator.

    
    
    #. automatic comment
    #: filename.c:1023
    #, flags, flags
    

The #. style comments are extracted from the source file where the message is
used. Possibly the programmer has inserted information for the translator,
such as about expected alignment. The #: comments indicate the exact locations
where the message is used in the source. The translator need not look at the
program source, but can if there is doubt about the correct translation. The
#, comments contain flags that describe the message in some way. There are
currently two flags: `fuzzy` is set if the message has possibly been outdated
because of changes in the program source. The translator can then verify this
and possibly remove the fuzzy flag. Note that fuzzy messages are not made
available to the end user. The other flag is `c-format`, which indicates that
the message is a `printf`-style format template. This means that the
translation should also be a format string with the same number and type of
placeholders. There are tools that can verify this, which key off the c-format
flag.

### 57.1.3. Creating and Maintaining Message Catalogs #

OK, so how does one create a “blank” message catalog? First, go into the
directory that contains the program whose messages you want to translate. If
there is a file `nls.mk`, then this program has been prepared for translation.

If there are already some `.po` files, then someone has already done some
translation work. The files are named `_`language`_.po`, where _`language`_ is
the [ISO 639-1 two-letter language code (in lower
case)](https://www.loc.gov/standards/iso639-2/php/English_list.php), e.g.,
`fr.po` for French. If there is really a need for more than one translation
effort per language then the files can also be named `_`language`_
__`region`_.po` where _`region`_ is the [ISO 3166-1 two-letter country code
(in upper case)](https://www.iso.org/iso-3166-country-codes.html), e.g.,
`pt_BR.po` for Portuguese in Brazil. If you find the language you wanted you
can just start working on that file.

If you need to start a new translation effort, then first run the command:

    
    
    make init-po
    

This will create a file `_`progname`_.pot`. (`.pot` to distinguish it from PO
files that are “in production”. The `T` stands for “template”.) Copy this file
to `_`language`_.po` and edit it. To make it known that the new language is
available, also edit the file `po/LINGUAS` and add the language (or language
and country) code next to languages already listed, like:

    
    
    de fr
    

(Other languages can appear, of course.)

As the underlying program or library changes, messages might be changed or
added by the programmers. In this case you do not need to start from scratch.
Instead, run the command:

    
    
    make update-po
    

which will create a new blank message catalog file (the pot file you started
with) and will merge it with the existing PO files. If the merge algorithm is
not sure about a particular message it marks it “fuzzy” as explained above.
The new PO file is saved with a `.po.new` extension.

### 57.1.4. Editing the PO Files #

The PO files can be edited with a regular text editor. There are also several
specialized editors for PO files which can help the process with translation-
specific features. There is (unsurprisingly) a PO mode for Emacs, which can be
quite useful.

The translator should only change the area between the quotes after the msgstr
directive, add comments, and alter the fuzzy flag.

The PO files need not be completely filled in. The software will automatically
fall back to the original string if no translation (or an empty translation)
is available. It is no problem to submit incomplete translations for
inclusions in the source tree; that gives room for other people to pick up
your work. However, you are encouraged to give priority to removing fuzzy
entries after doing a merge. Remember that fuzzy entries will not be
installed; they only serve as reference for what might be the right
translation.

Here are some things to keep in mind while editing the translations:

  * Make sure that if the original ends with a newline, the translation does, too. Similarly for tabs, etc.

  * If the original is a `printf` format string, the translation also needs to be. The translation also needs to have the same format specifiers in the same order. Sometimes the natural rules of the language make this impossible or at least awkward. In that case you can modify the format specifiers like this:
        
        msgstr "Die Datei %2$s hat %1$u Zeichen."
        

Then the first placeholder will actually use the second argument from the
list. The `_`digits`_ $` needs to follow the % immediately, before any other
format manipulators. (This feature really exists in the `printf` family of
functions. You might not have heard of it before because there is little use
for it outside of message internationalization.)

  * If the original string contains a linguistic mistake, report that (or fix it yourself in the program source) and translate normally. The corrected string can be merged in when the program sources have been updated. If the original string contains a factual mistake, report that (or fix it yourself) and do not translate it. Instead, you can mark the string with a comment in the PO file.

  * Maintain the style and tone of the original string. Specifically, messages that are not sentences (`cannot open file %s`) should probably not start with a capital letter (if your language distinguishes letter case) or end with a period (if your language uses punctuation marks). It might help to read [Section 56.3](error-style-guide.html "56.3. Error Message Style Guide").

  * If you don't know what a message means, or if it is ambiguous, ask on the developers' mailing list. Chances are that English speaking end users might also not understand it or find it ambiguous, so it's best to improve the message.

* * *

[Prev](nls.html "Chapter 57. Native Language Support")  | [Up](nls.html "Chapter 57. Native Language Support") |  [Next](nls-programmer.html "57.2. For the Programmer")  
---|---|---  
Chapter 57. Native Language Support  | [Home](index.html "PostgreSQL 16.9 Documentation") |  57.2. For the Programmer  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/nls-translator.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

