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

Supported Versions: [Current](/docs/current/source-format.html "PostgreSQL 17
- 56.1. Formatting") ([17](/docs/17/source-format.html "PostgreSQL 17 -
56.1. Formatting")) / [16](/docs/16/source-format.html "PostgreSQL 16 -
56.1. Formatting") / [15](/docs/15/source-format.html "PostgreSQL 15 -
56.1. Formatting") / [14](/docs/14/source-format.html "PostgreSQL 14 -
56.1. Formatting") / [13](/docs/13/source-format.html "PostgreSQL 13 -
56.1. Formatting")

Development Versions: [18](/docs/18/source-format.html "PostgreSQL 18 -
56.1. Formatting") / [devel](/docs/devel/source-format.html "PostgreSQL devel
- 56.1. Formatting")

Unsupported versions: [12](/docs/12/source-format.html "PostgreSQL 12 -
56.1. Formatting") / [11](/docs/11/source-format.html "PostgreSQL 11 -
56.1. Formatting") / [10](/docs/10/source-format.html "PostgreSQL 10 -
56.1. Formatting") / [9.6](/docs/9.6/source-format.html "PostgreSQL 9.6 -
56.1. Formatting") / [9.5](/docs/9.5/source-format.html "PostgreSQL 9.5 -
56.1. Formatting") / [9.4](/docs/9.4/source-format.html "PostgreSQL 9.4 -
56.1. Formatting") / [9.3](/docs/9.3/source-format.html "PostgreSQL 9.3 -
56.1. Formatting") / [9.2](/docs/9.2/source-format.html "PostgreSQL 9.2 -
56.1. Formatting") / [9.1](/docs/9.1/source-format.html "PostgreSQL 9.1 -
56.1. Formatting") / [9.0](/docs/9.0/source-format.html "PostgreSQL 9.0 -
56.1. Formatting") / [8.4](/docs/8.4/source-format.html "PostgreSQL 8.4 -
56.1. Formatting") / [8.3](/docs/8.3/source-format.html "PostgreSQL 8.3 -
56.1. Formatting") / [8.2](/docs/8.2/source-format.html "PostgreSQL 8.2 -
56.1. Formatting")

__

56.1. Formatting  
---  
[Prev](source.html "Chapter 56. PostgreSQL Coding Conventions")  | [Up](source.html "Chapter 56. PostgreSQL Coding Conventions") | Chapter 56. PostgreSQL Coding Conventions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](error-message-reporting.html "56.2. Reporting Errors Within the Server")  
  
* * *

## 56.1. Formatting #

Source code formatting uses 4 column tab spacing, with tabs preserved (i.e.,
tabs are not expanded to spaces). Each logical indentation level is one
additional tab stop.

Layout rules (brace positioning, etc.) follow BSD conventions. In particular,
curly braces for the controlled blocks of `if`, `while`, `switch`, etc. go on
their own lines.

Limit line lengths so that the code is readable in an 80-column window. (This
doesn't mean that you must never go past 80 columns. For instance, breaking a
long error message string in arbitrary places just to keep the code within 80
columns is probably not a net gain in readability.)

To maintain a consistent coding style, do not use C++ style comments (`//`
comments). pgindent will replace them with `/* ... */`.

The preferred style for multi-line comment blocks is

    
    
    /*
     * comment text begins here
     * and continues here
     */
    

Note that comment blocks that begin in column 1 will be preserved as-is by
pgindent, but it will re-flow indented comment blocks as though they were
plain text. If you want to preserve the line breaks in an indented block, add
dashes like this:

    
    
        /*----------
         * comment text begins here
         * and continues here
         *----------
         */
    

While submitted patches do not absolutely have to follow these formatting
rules, it's a good idea to do so. Your code will get run through pgindent
before the next release, so there's no point in making it look nice under some
other set of formatting conventions. A good rule of thumb for patches is “make
the new code look like the existing code around it”.

The `src/tools/editors` directory contains sample settings files that can be
used with the Emacs, xemacs or vim editors to help ensure that they format
code according to these conventions.

If you'd like to run pgindent locally to help make your code match project
style, see the `src/tools/pgindent` directory.

The text browsing tools more and less can be invoked as:

    
    
    more -x4
    less -x4
    

to make them show tabs appropriately.

* * *

[Prev](source.html "Chapter 56. PostgreSQL Coding Conventions")  | [Up](source.html "Chapter 56. PostgreSQL Coding Conventions") |  [Next](error-message-reporting.html "56.2. Reporting Errors Within the Server")  
---|---|---  
Chapter 56. PostgreSQL Coding Conventions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  56.2. Reporting Errors Within the Server  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/source-format.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

