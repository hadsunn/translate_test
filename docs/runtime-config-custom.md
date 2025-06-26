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

Supported Versions: [Current](/docs/current/runtime-config-custom.html
"PostgreSQL 17 - 20.16. Customized Options") ([17](/docs/17/runtime-config-
custom.html "PostgreSQL 17 - 20.16. Customized Options")) /
[16](/docs/16/runtime-config-custom.html "PostgreSQL 16 - 20.16. Customized
Options") / [15](/docs/15/runtime-config-custom.html "PostgreSQL 15 -
20.16. Customized Options") / [14](/docs/14/runtime-config-custom.html
"PostgreSQL 14 - 20.16. Customized Options") / [13](/docs/13/runtime-config-
custom.html "PostgreSQL 13 - 20.16. Customized Options")

Development Versions: [18](/docs/18/runtime-config-custom.html "PostgreSQL 18
- 20.16. Customized Options") / [devel](/docs/devel/runtime-config-custom.html
"PostgreSQL devel - 20.16. Customized Options")

Unsupported versions: [12](/docs/12/runtime-config-custom.html "PostgreSQL 12
- 20.16. Customized Options") / [11](/docs/11/runtime-config-custom.html
"PostgreSQL 11 - 20.16. Customized Options") / [10](/docs/10/runtime-config-
custom.html "PostgreSQL 10 - 20.16. Customized Options") /
[9.6](/docs/9.6/runtime-config-custom.html "PostgreSQL 9.6 - 20.16. Customized
Options") / [9.5](/docs/9.5/runtime-config-custom.html "PostgreSQL 9.5 -
20.16. Customized Options") / [9.4](/docs/9.4/runtime-config-custom.html
"PostgreSQL 9.4 - 20.16. Customized Options") / [9.3](/docs/9.3/runtime-
config-custom.html "PostgreSQL 9.3 - 20.16. Customized Options") /
[9.2](/docs/9.2/runtime-config-custom.html "PostgreSQL 9.2 - 20.16. Customized
Options") / [9.1](/docs/9.1/runtime-config-custom.html "PostgreSQL 9.1 -
20.16. Customized Options") / [9.0](/docs/9.0/runtime-config-custom.html
"PostgreSQL 9.0 - 20.16. Customized Options") / [8.4](/docs/8.4/runtime-
config-custom.html "PostgreSQL 8.4 - 20.16. Customized Options") /
[8.3](/docs/8.3/runtime-config-custom.html "PostgreSQL 8.3 - 20.16. Customized
Options") / [8.2](/docs/8.2/runtime-config-custom.html "PostgreSQL 8.2 -
20.16. Customized Options") / [8.1](/docs/8.1/runtime-config-custom.html
"PostgreSQL 8.1 - 20.16. Customized Options")

__

20.16. Customized Options  
---  
[Prev](runtime-config-preset.html "20.15. Preset Options")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-developer.html "20.17. Developer Options")  
  
* * *

## 20.16. Customized Options #

This feature was designed to allow parameters not normally known to PostgreSQL
to be added by add-on modules (such as procedural languages). This allows
extension modules to be configured in the standard ways.

Custom options have two-part names: an extension name, then a dot, then the
parameter name proper, much like qualified names in SQL. An example is
`plpgsql.variable_conflict`.

Because custom options may need to be set in processes that have not loaded
the relevant extension module, PostgreSQL will accept a setting for any two-
part parameter name. Such variables are treated as placeholders and have no
function until the module that defines them is loaded. When an extension
module is loaded, it will add its variable definitions and convert any
placeholder values according to those definitions. If there are any
unrecognized placeholders that begin with its extension name, warnings are
issued and those placeholders are removed.

* * *

[Prev](runtime-config-preset.html "20.15. Preset Options")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-developer.html "20.17. Developer Options")  
---|---|---  
20.15. Preset Options  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.17. Developer Options  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-custom.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

