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

Supported Versions: [Current](/docs/current/trigger-datachanges.html
"PostgreSQL 17 - 39.2. Visibility of Data Changes") ([17](/docs/17/trigger-
datachanges.html "PostgreSQL 17 - 39.2. Visibility of Data Changes")) /
[16](/docs/16/trigger-datachanges.html "PostgreSQL 16 - 39.2. Visibility of
Data Changes") / [15](/docs/15/trigger-datachanges.html "PostgreSQL 15 -
39.2. Visibility of Data Changes") / [14](/docs/14/trigger-datachanges.html
"PostgreSQL 14 - 39.2. Visibility of Data Changes") / [13](/docs/13/trigger-
datachanges.html "PostgreSQL 13 - 39.2. Visibility of Data Changes")

Development Versions: [18](/docs/18/trigger-datachanges.html "PostgreSQL 18 -
39.2. Visibility of Data Changes") / [devel](/docs/devel/trigger-
datachanges.html "PostgreSQL devel - 39.2. Visibility of Data Changes")

Unsupported versions: [12](/docs/12/trigger-datachanges.html "PostgreSQL 12 -
39.2. Visibility of Data Changes") / [11](/docs/11/trigger-datachanges.html
"PostgreSQL 11 - 39.2. Visibility of Data Changes") / [10](/docs/10/trigger-
datachanges.html "PostgreSQL 10 - 39.2. Visibility of Data Changes") /
[9.6](/docs/9.6/trigger-datachanges.html "PostgreSQL 9.6 - 39.2. Visibility of
Data Changes") / [9.5](/docs/9.5/trigger-datachanges.html "PostgreSQL 9.5 -
39.2. Visibility of Data Changes") / [9.4](/docs/9.4/trigger-datachanges.html
"PostgreSQL 9.4 - 39.2. Visibility of Data Changes") /
[9.3](/docs/9.3/trigger-datachanges.html "PostgreSQL 9.3 - 39.2. Visibility of
Data Changes") / [9.2](/docs/9.2/trigger-datachanges.html "PostgreSQL 9.2 -
39.2. Visibility of Data Changes") / [9.1](/docs/9.1/trigger-datachanges.html
"PostgreSQL 9.1 - 39.2. Visibility of Data Changes") /
[9.0](/docs/9.0/trigger-datachanges.html "PostgreSQL 9.0 - 39.2. Visibility of
Data Changes") / [8.4](/docs/8.4/trigger-datachanges.html "PostgreSQL 8.4 -
39.2. Visibility of Data Changes") / [8.3](/docs/8.3/trigger-datachanges.html
"PostgreSQL 8.3 - 39.2. Visibility of Data Changes") /
[8.2](/docs/8.2/trigger-datachanges.html "PostgreSQL 8.2 - 39.2. Visibility of
Data Changes") / [8.1](/docs/8.1/trigger-datachanges.html "PostgreSQL 8.1 -
39.2. Visibility of Data Changes") / [8.0](/docs/8.0/trigger-datachanges.html
"PostgreSQL 8.0 - 39.2. Visibility of Data Changes") /
[7.4](/docs/7.4/trigger-datachanges.html "PostgreSQL 7.4 - 39.2. Visibility of
Data Changes") / [7.3](/docs/7.3/trigger-datachanges.html "PostgreSQL 7.3 -
39.2. Visibility of Data Changes") / [7.2](/docs/7.2/trigger-datachanges.html
"PostgreSQL 7.2 - 39.2. Visibility of Data Changes") /
[7.1](/docs/7.1/trigger-datachanges.html "PostgreSQL 7.1 - 39.2. Visibility of
Data Changes")

__

39.2. Visibility of Data Changes  
---  
[Prev](trigger-definition.html "39.1. Overview of Trigger Behavior")  | [Up](triggers.html "Chapter 39. Triggers") | Chapter 39. Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](trigger-interface.html "39.3. Writing Trigger Functions in C")  
  
* * *

## 39.2. Visibility of Data Changes #

If you execute SQL commands in your trigger function, and these commands
access the table that the trigger is for, then you need to be aware of the
data visibility rules, because they determine whether these SQL commands will
see the data change that the trigger is fired for. Briefly:

  * Statement-level triggers follow simple visibility rules: none of the changes made by a statement are visible to statement-level `BEFORE` triggers, whereas all modifications are visible to statement-level `AFTER` triggers.

  * The data change (insertion, update, or deletion) causing the trigger to fire is naturally _not_ visible to SQL commands executed in a row-level `BEFORE` trigger, because it hasn't happened yet.

  * However, SQL commands executed in a row-level `BEFORE` trigger _will_ see the effects of data changes for rows previously processed in the same outer command. This requires caution, since the ordering of these change events is not in general predictable; an SQL command that affects multiple rows can visit the rows in any order.

  * Similarly, a row-level `INSTEAD OF` trigger will see the effects of data changes made by previous firings of `INSTEAD OF` triggers in the same outer command.

  * When a row-level `AFTER` trigger is fired, all data changes made by the outer command are already complete, and are visible to the invoked trigger function.

If your trigger function is written in any of the standard procedural
languages, then the above statements apply only if the function is declared
`VOLATILE`. Functions that are declared `STABLE` or `IMMUTABLE` will not see
changes made by the calling command in any case.

Further information about data visibility rules can be found in [Section
47.5](spi-visibility.html "47.5. Visibility of Data Changes"). The example in
[Section 39.4](trigger-example.html "39.4. A Complete Trigger Example")
contains a demonstration of these rules.

* * *

[Prev](trigger-definition.html "39.1. Overview of Trigger Behavior")  | [Up](triggers.html "Chapter 39. Triggers") |  [Next](trigger-interface.html "39.3. Writing Trigger Functions in C")  
---|---|---  
39.1. Overview of Trigger Behavior  | [Home](index.html "PostgreSQL 16.9 Documentation") |  39.3. Writing Trigger Functions in C  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/trigger-datachanges.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

