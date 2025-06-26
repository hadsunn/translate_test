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

Supported Versions: [Current](/docs/current/color-which.html "PostgreSQL 17 -
N.2. Configuring the Colors") ([17](/docs/17/color-which.html "PostgreSQL 17 -
N.2. Configuring the Colors")) / [16](/docs/16/color-which.html "PostgreSQL 16
- N.2. Configuring the Colors") / [15](/docs/15/color-which.html "PostgreSQL
15 - N.2. Configuring the Colors") / [14](/docs/14/color-which.html
"PostgreSQL 14 - N.2. Configuring the Colors") / [13](/docs/13/color-
which.html "PostgreSQL 13 - N.2. Configuring the Colors")

Development Versions: [18](/docs/18/color-which.html "PostgreSQL 18 -
N.2. Configuring the Colors") / [devel](/docs/devel/color-which.html
"PostgreSQL devel - N.2. Configuring the Colors")

__

N.2. Configuring the Colors  
---  
[Prev](color-when.html "N.1. When Color is Used")  | [Up](color.html "Appendix N. Color Support") | Appendix N. Color Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](appendix-obsolete.html "Appendix O. Obsolete or Renamed Features")  
  
* * *

## N.2. Configuring the Colors #

The actual colors to be used are configured using the environment variable
`PG_COLORS` (note plural). The value is a colon-separated list of `_`key`_
=_`value`_` pairs. The keys specify what the color is to be used for. The
values are SGR (Select Graphic Rendition) specifications, which are
interpreted by the terminal.

The following keys are currently in use:

`error`

    

used to highlight the text “error” in error messages

`warning`

    

used to highlight the text “warning” in warning messages

`note`

    

used to highlight the text “detail” and “hint” in such messages

`locus`

    

used to highlight location information (e.g., program name and file name) in
messages

The default value is `error=01;31:warning=01;35:note=01;36:locus=01` (`01;31`
= bold red, `01;35` = bold magenta, `01;36` = bold cyan, `01` = bold default
color).

### Tip

This color specification format is also used by other software packages such
as GCC, GNU coreutils, and GNU grep.

* * *

[Prev](color-when.html "N.1. When Color is Used")  | [Up](color.html "Appendix N. Color Support") |  [Next](appendix-obsolete.html "Appendix O. Obsolete or Renamed Features")  
---|---|---  
N.1. When Color is Used  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix O. Obsolete or Renamed Features  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/color-which.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

