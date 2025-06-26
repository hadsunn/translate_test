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

Supported Versions: [Current](/docs/current/charset.html "PostgreSQL 17 -
Chapter 24. Localization") ([17](/docs/17/charset.html "PostgreSQL 17 -
Chapter 24. Localization")) / [16](/docs/16/charset.html "PostgreSQL 16 -
Chapter 24. Localization") / [15](/docs/15/charset.html "PostgreSQL 15 -
Chapter 24. Localization") / [14](/docs/14/charset.html "PostgreSQL 14 -
Chapter 24. Localization") / [13](/docs/13/charset.html "PostgreSQL 13 -
Chapter 24. Localization")

Development Versions: [18](/docs/18/charset.html "PostgreSQL 18 -
Chapter 24. Localization") / [devel](/docs/devel/charset.html "PostgreSQL
devel - Chapter 24. Localization")

Unsupported versions: [12](/docs/12/charset.html "PostgreSQL 12 -
Chapter 24. Localization") / [11](/docs/11/charset.html "PostgreSQL 11 -
Chapter 24. Localization") / [10](/docs/10/charset.html "PostgreSQL 10 -
Chapter 24. Localization") / [9.6](/docs/9.6/charset.html "PostgreSQL 9.6 -
Chapter 24. Localization") / [9.5](/docs/9.5/charset.html "PostgreSQL 9.5 -
Chapter 24. Localization") / [9.4](/docs/9.4/charset.html "PostgreSQL 9.4 -
Chapter 24. Localization") / [9.3](/docs/9.3/charset.html "PostgreSQL 9.3 -
Chapter 24. Localization") / [9.2](/docs/9.2/charset.html "PostgreSQL 9.2 -
Chapter 24. Localization") / [9.1](/docs/9.1/charset.html "PostgreSQL 9.1 -
Chapter 24. Localization") / [9.0](/docs/9.0/charset.html "PostgreSQL 9.0 -
Chapter 24. Localization") / [8.4](/docs/8.4/charset.html "PostgreSQL 8.4 -
Chapter 24. Localization") / [8.3](/docs/8.3/charset.html "PostgreSQL 8.3 -
Chapter 24. Localization") / [8.2](/docs/8.2/charset.html "PostgreSQL 8.2 -
Chapter 24. Localization") / [8.1](/docs/8.1/charset.html "PostgreSQL 8.1 -
Chapter 24. Localization") / [8.0](/docs/8.0/charset.html "PostgreSQL 8.0 -
Chapter 24. Localization") / [7.4](/docs/7.4/charset.html "PostgreSQL 7.4 -
Chapter 24. Localization") / [7.3](/docs/7.3/charset.html "PostgreSQL 7.3 -
Chapter 24. Localization") / [7.2](/docs/7.2/charset.html "PostgreSQL 7.2 -
Chapter 24. Localization") / [7.1](/docs/7.1/charset.html "PostgreSQL 7.1 -
Chapter 24. Localization")

__

Chapter 24. Localization  
---  
[Prev](manage-ag-tablespaces.html "23.6. Tablespaces")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](locale.html "24.1. Locale Support")  
  
* * *

## Chapter 24. Localization

**Table of Contents**

[24.1. Locale Support](locale.html)

    

[24.1.1. Overview](locale.html#LOCALE-OVERVIEW)

[24.1.2. Behavior](locale.html#LOCALE-BEHAVIOR)

[24.1.3. Selecting Locales](locale.html#LOCALE-SELECTING-LOCALES)

[24.1.4. Locale Providers](locale.html#LOCALE-PROVIDERS)

[24.1.5. ICU Locales](locale.html#ICU-LOCALES)

[24.1.6. Problems](locale.html#LOCALE-PROBLEMS)

[24.2. Collation Support](collation.html)

    

[24.2.1. Concepts](collation.html#COLLATION-CONCEPTS)

[24.2.2. Managing Collations](collation.html#COLLATION-MANAGING)

[24.2.3. ICU Custom Collations](collation.html#ICU-CUSTOM-COLLATIONS)

[24.3. Character Set Support](multibyte.html)

    

[24.3.1. Supported Character Sets](multibyte.html#MULTIBYTE-CHARSET-SUPPORTED)

[24.3.2. Setting the Character Set](multibyte.html#MULTIBYTE-SETTING)

[24.3.3. Automatic Character Set Conversion Between Server and
Client](multibyte.html#MULTIBYTE-AUTOMATIC-CONVERSION)

[24.3.4. Available Character Set Conversions](multibyte.html#MULTIBYTE-
CONVERSIONS-SUPPORTED)

[24.3.5. Further Reading](multibyte.html#MULTIBYTE-FURTHER-READING)

This chapter describes the available localization features from the point of
view of the administrator. PostgreSQL supports two localization facilities:

  * Using the locale features of the operating system to provide locale-specific collation order, number formatting, translated messages, and other aspects. This is covered in [Section 24.1](locale.html "24.1. Locale Support") and [Section 24.2](collation.html "24.2. Collation Support").

  * Providing a number of different character sets to support storing text in all kinds of languages, and providing character set translation between client and server. This is covered in [Section 24.3](multibyte.html "24.3. Character Set Support").

* * *

[Prev](manage-ag-tablespaces.html "23.6. Tablespaces")  | [Up](admin.html "Part III. Server Administration") |  [Next](locale.html "24.1. Locale Support")  
---|---|---  
23.6. Tablespaces  | [Home](index.html "PostgreSQL 16.9 Documentation") |  24.1. Locale Support  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/charset.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

