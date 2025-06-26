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

Supported Versions: [Current](/docs/current/nls.html "PostgreSQL 17 -
Chapter 57. Native Language Support") ([17](/docs/17/nls.html "PostgreSQL 17 -
Chapter 57. Native Language Support")) / [16](/docs/16/nls.html "PostgreSQL 16
- Chapter 57. Native Language Support") / [15](/docs/15/nls.html "PostgreSQL
15 - Chapter 57. Native Language Support") / [14](/docs/14/nls.html
"PostgreSQL 14 - Chapter 57. Native Language Support") /
[13](/docs/13/nls.html "PostgreSQL 13 - Chapter 57. Native Language Support")

Development Versions: [18](/docs/18/nls.html "PostgreSQL 18 -
Chapter 57. Native Language Support") / [devel](/docs/devel/nls.html
"PostgreSQL devel - Chapter 57. Native Language Support")

Unsupported versions: [12](/docs/12/nls.html "PostgreSQL 12 -
Chapter 57. Native Language Support") / [11](/docs/11/nls.html "PostgreSQL 11
- Chapter 57. Native Language Support") / [10](/docs/10/nls.html "PostgreSQL
10 - Chapter 57. Native Language Support") / [9.6](/docs/9.6/nls.html
"PostgreSQL 9.6 - Chapter 57. Native Language Support") /
[9.5](/docs/9.5/nls.html "PostgreSQL 9.5 - Chapter 57. Native Language
Support") / [9.4](/docs/9.4/nls.html "PostgreSQL 9.4 - Chapter 57. Native
Language Support") / [9.3](/docs/9.3/nls.html "PostgreSQL 9.3 -
Chapter 57. Native Language Support") / [9.2](/docs/9.2/nls.html "PostgreSQL
9.2 - Chapter 57. Native Language Support") / [9.1](/docs/9.1/nls.html
"PostgreSQL 9.1 - Chapter 57. Native Language Support") /
[9.0](/docs/9.0/nls.html "PostgreSQL 9.0 - Chapter 57. Native Language
Support") / [8.4](/docs/8.4/nls.html "PostgreSQL 8.4 - Chapter 57. Native
Language Support") / [8.3](/docs/8.3/nls.html "PostgreSQL 8.3 -
Chapter 57. Native Language Support") / [8.2](/docs/8.2/nls.html "PostgreSQL
8.2 - Chapter 57. Native Language Support") / [8.1](/docs/8.1/nls.html
"PostgreSQL 8.1 - Chapter 57. Native Language Support") /
[8.0](/docs/8.0/nls.html "PostgreSQL 8.0 - Chapter 57. Native Language
Support") / [7.4](/docs/7.4/nls.html "PostgreSQL 7.4 - Chapter 57. Native
Language Support") / [7.3](/docs/7.3/nls.html "PostgreSQL 7.3 -
Chapter 57. Native Language Support") / [7.2](/docs/7.2/nls.html "PostgreSQL
7.2 - Chapter 57. Native Language Support")

__

Chapter 57. Native Language Support  
---  
[Prev](source-conventions.html "56.4. Miscellaneous Coding Conventions")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](nls-translator.html "57.1. For the Translator")  
  
* * *

## Chapter 57. Native Language Support

**Table of Contents**

[57.1. For the Translator](nls-translator.html)

    

[57.1.1. Requirements](nls-translator.html#NLS-TRANSLATOR-REQUIREMENTS)

[57.1.2. Concepts](nls-translator.html#NLS-TRANSLATOR-CONCEPTS)

[57.1.3. Creating and Maintaining Message Catalogs](nls-translator.html#NLS-
TRANSLATOR-MESSAGE-CATALOGS)

[57.1.4. Editing the PO Files](nls-translator.html#NLS-TRANSLATOR-EDITING-PO)

[57.2. For the Programmer](nls-programmer.html)

    

[57.2.1. Mechanics](nls-programmer.html#NLS-MECHANICS)

[57.2.2. Message-Writing Guidelines](nls-programmer.html#NLS-GUIDELINES)

* * *

[Prev](source-conventions.html "56.4. Miscellaneous Coding Conventions")  | [Up](internals.html "Part VII. Internals") |  [Next](nls-translator.html "57.1. For the Translator")  
---|---|---  
56.4. Miscellaneous Coding Conventions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  57.1. For the Translator  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/nls.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

