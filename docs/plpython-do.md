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

Supported Versions: [Current](/docs/current/plpython-do.html "PostgreSQL 17 -
46.4. Anonymous Code Blocks") ([17](/docs/17/plpython-do.html "PostgreSQL 17 -
46.4. Anonymous Code Blocks")) / [16](/docs/16/plpython-do.html "PostgreSQL 16
- 46.4. Anonymous Code Blocks") / [15](/docs/15/plpython-do.html "PostgreSQL
15 - 46.4. Anonymous Code Blocks") / [14](/docs/14/plpython-do.html
"PostgreSQL 14 - 46.4. Anonymous Code Blocks") / [13](/docs/13/plpython-
do.html "PostgreSQL 13 - 46.4. Anonymous Code Blocks")

Development Versions: [18](/docs/18/plpython-do.html "PostgreSQL 18 -
46.4. Anonymous Code Blocks") / [devel](/docs/devel/plpython-do.html
"PostgreSQL devel - 46.4. Anonymous Code Blocks")

Unsupported versions: [12](/docs/12/plpython-do.html "PostgreSQL 12 -
46.4. Anonymous Code Blocks") / [11](/docs/11/plpython-do.html "PostgreSQL 11
- 46.4. Anonymous Code Blocks") / [10](/docs/10/plpython-do.html "PostgreSQL
10 - 46.4. Anonymous Code Blocks") / [9.6](/docs/9.6/plpython-do.html
"PostgreSQL 9.6 - 46.4. Anonymous Code Blocks") / [9.5](/docs/9.5/plpython-
do.html "PostgreSQL 9.5 - 46.4. Anonymous Code Blocks") /
[9.4](/docs/9.4/plpython-do.html "PostgreSQL 9.4 - 46.4. Anonymous Code
Blocks") / [9.3](/docs/9.3/plpython-do.html "PostgreSQL 9.3 - 46.4. Anonymous
Code Blocks") / [9.2](/docs/9.2/plpython-do.html "PostgreSQL 9.2 -
46.4. Anonymous Code Blocks") / [9.1](/docs/9.1/plpython-do.html "PostgreSQL
9.1 - 46.4. Anonymous Code Blocks") / [9.0](/docs/9.0/plpython-do.html
"PostgreSQL 9.0 - 46.4. Anonymous Code Blocks")

__

46.4. Anonymous Code Blocks  
---  
[Prev](plpython-sharing.html "46.3. Sharing Data")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-trigger.html "46.5. Trigger Functions")  
  
* * *

## 46.4. Anonymous Code Blocks #

PL/Python also supports anonymous code blocks called with the [DO](sql-do.html
"DO") statement:

    
    
    DO $$
        # PL/Python code
    $$ LANGUAGE plpython3u;
    

An anonymous code block receives no arguments, and whatever value it might
return is discarded. Otherwise it behaves just like a function.

* * *

[Prev](plpython-sharing.html "46.3. Sharing Data")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-trigger.html "46.5. Trigger Functions")  
---|---|---  
46.3. Sharing Data  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.5. Trigger Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-do.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

