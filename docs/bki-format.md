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

Supported Versions: [Current](/docs/current/bki-format.html "PostgreSQL 17 -
75.3. BKI File Format") ([17](/docs/17/bki-format.html "PostgreSQL 17 -
75.3. BKI File Format")) / [16](/docs/16/bki-format.html "PostgreSQL 16 -
75.3. BKI File Format") / [15](/docs/15/bki-format.html "PostgreSQL 15 -
75.3. BKI File Format") / [14](/docs/14/bki-format.html "PostgreSQL 14 -
75.3. BKI File Format") / [13](/docs/13/bki-format.html "PostgreSQL 13 -
75.3. BKI File Format")

Development Versions: [18](/docs/18/bki-format.html "PostgreSQL 18 - 75.3. BKI
File Format") / [devel](/docs/devel/bki-format.html "PostgreSQL devel -
75.3. BKI File Format")

Unsupported versions: [12](/docs/12/bki-format.html "PostgreSQL 12 - 75.3. BKI
File Format") / [11](/docs/11/bki-format.html "PostgreSQL 11 - 75.3. BKI File
Format") / [10](/docs/10/bki-format.html "PostgreSQL 10 - 75.3. BKI File
Format") / [9.6](/docs/9.6/bki-format.html "PostgreSQL 9.6 - 75.3. BKI File
Format") / [9.5](/docs/9.5/bki-format.html "PostgreSQL 9.5 - 75.3. BKI File
Format") / [9.4](/docs/9.4/bki-format.html "PostgreSQL 9.4 - 75.3. BKI File
Format") / [9.3](/docs/9.3/bki-format.html "PostgreSQL 9.3 - 75.3. BKI File
Format") / [9.2](/docs/9.2/bki-format.html "PostgreSQL 9.2 - 75.3. BKI File
Format") / [9.1](/docs/9.1/bki-format.html "PostgreSQL 9.1 - 75.3. BKI File
Format") / [9.0](/docs/9.0/bki-format.html "PostgreSQL 9.0 - 75.3. BKI File
Format") / [8.4](/docs/8.4/bki-format.html "PostgreSQL 8.4 - 75.3. BKI File
Format") / [8.3](/docs/8.3/bki-format.html "PostgreSQL 8.3 - 75.3. BKI File
Format") / [8.2](/docs/8.2/bki-format.html "PostgreSQL 8.2 - 75.3. BKI File
Format")

__

75.3. BKI File Format  
---  
[Prev](system-catalog-initial-data.html "75.2. System Catalog Initial Data")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") | Chapter 75. System Catalog Declarations and Initial Contents | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](bki-commands.html "75.4. BKI Commands")  
  
* * *

## 75.3. BKI File Format #

This section describes how the PostgreSQL backend interprets BKI files. This
description will be easier to understand if the `postgres.bki` file is at hand
as an example.

BKI input consists of a sequence of commands. Commands are made up of a number
of tokens, depending on the syntax of the command. Tokens are usually
separated by whitespace, but need not be if there is no ambiguity. There is no
special command separator; the next token that syntactically cannot belong to
the preceding command starts a new one. (Usually you would put a new command
on a new line, for clarity.) Tokens can be certain key words, special
characters (parentheses, commas, etc.), identifiers, numbers, or single-quoted
strings. Everything is case sensitive.

Lines starting with `#` are ignored.

* * *

[Prev](system-catalog-initial-data.html "75.2. System Catalog Initial Data")  | [Up](bki.html "Chapter 75. System Catalog Declarations and Initial Contents") |  [Next](bki-commands.html "75.4. BKI Commands")  
---|---|---  
75.2. System Catalog Initial Data  | [Home](index.html "PostgreSQL 16.9 Documentation") |  75.4. BKI Commands  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/bki-format.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

