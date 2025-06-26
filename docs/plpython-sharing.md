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

Supported Versions: [Current](/docs/current/plpython-sharing.html "PostgreSQL
17 - 46.3. Sharing Data") ([17](/docs/17/plpython-sharing.html "PostgreSQL 17
- 46.3. Sharing Data")) / [16](/docs/16/plpython-sharing.html "PostgreSQL 16 -
46.3. Sharing Data") / [15](/docs/15/plpython-sharing.html "PostgreSQL 15 -
46.3. Sharing Data") / [14](/docs/14/plpython-sharing.html "PostgreSQL 14 -
46.3. Sharing Data") / [13](/docs/13/plpython-sharing.html "PostgreSQL 13 -
46.3. Sharing Data")

Development Versions: [18](/docs/18/plpython-sharing.html "PostgreSQL 18 -
46.3. Sharing Data") / [devel](/docs/devel/plpython-sharing.html "PostgreSQL
devel - 46.3. Sharing Data")

Unsupported versions: [12](/docs/12/plpython-sharing.html "PostgreSQL 12 -
46.3. Sharing Data") / [11](/docs/11/plpython-sharing.html "PostgreSQL 11 -
46.3. Sharing Data") / [10](/docs/10/plpython-sharing.html "PostgreSQL 10 -
46.3. Sharing Data") / [9.6](/docs/9.6/plpython-sharing.html "PostgreSQL 9.6 -
46.3. Sharing Data") / [9.5](/docs/9.5/plpython-sharing.html "PostgreSQL 9.5 -
46.3. Sharing Data") / [9.4](/docs/9.4/plpython-sharing.html "PostgreSQL 9.4 -
46.3. Sharing Data") / [9.3](/docs/9.3/plpython-sharing.html "PostgreSQL 9.3 -
46.3. Sharing Data") / [9.2](/docs/9.2/plpython-sharing.html "PostgreSQL 9.2 -
46.3. Sharing Data") / [9.1](/docs/9.1/plpython-sharing.html "PostgreSQL 9.1 -
46.3. Sharing Data") / [9.0](/docs/9.0/plpython-sharing.html "PostgreSQL 9.0 -
46.3. Sharing Data")

__

46.3. Sharing Data  
---  
[Prev](plpython-data.html "46.2. Data Values")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-do.html "46.4. Anonymous Code Blocks")  
  
* * *

## 46.3. Sharing Data #

The global dictionary `SD` is available to store private data between repeated
calls to the same function. The global dictionary `GD` is public data, that is
available to all Python functions within a session; use with care.

Each function gets its own execution environment in the Python interpreter, so
that global data and function arguments from `myfunc` are not available to
`myfunc2`. The exception is the data in the `GD` dictionary, as mentioned
above.

* * *

[Prev](plpython-data.html "46.2. Data Values")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-do.html "46.4. Anonymous Code Blocks")  
---|---|---  
46.2. Data Values  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.4. Anonymous Code Blocks  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-sharing.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

