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

Supported Versions: [Current](/docs/current/plpython-envar.html "PostgreSQL 17
- 46.11. Environment Variables") ([17](/docs/17/plpython-envar.html
"PostgreSQL 17 - 46.11. Environment Variables")) / [16](/docs/16/plpython-
envar.html "PostgreSQL 16 - 46.11. Environment Variables") /
[15](/docs/15/plpython-envar.html "PostgreSQL 15 - 46.11. Environment
Variables") / [14](/docs/14/plpython-envar.html "PostgreSQL 14 -
46.11. Environment Variables") / [13](/docs/13/plpython-envar.html "PostgreSQL
13 - 46.11. Environment Variables")

Development Versions: [18](/docs/18/plpython-envar.html "PostgreSQL 18 -
46.11. Environment Variables") / [devel](/docs/devel/plpython-envar.html
"PostgreSQL devel - 46.11. Environment Variables")

Unsupported versions: [12](/docs/12/plpython-envar.html "PostgreSQL 12 -
46.11. Environment Variables") / [11](/docs/11/plpython-envar.html "PostgreSQL
11 - 46.11. Environment Variables") / [10](/docs/10/plpython-envar.html
"PostgreSQL 10 - 46.11. Environment Variables") / [9.6](/docs/9.6/plpython-
envar.html "PostgreSQL 9.6 - 46.11. Environment Variables") /
[9.5](/docs/9.5/plpython-envar.html "PostgreSQL 9.5 - 46.11. Environment
Variables") / [9.4](/docs/9.4/plpython-envar.html "PostgreSQL 9.4 -
46.11. Environment Variables") / [9.3](/docs/9.3/plpython-envar.html
"PostgreSQL 9.3 - 46.11. Environment Variables") / [9.2](/docs/9.2/plpython-
envar.html "PostgreSQL 9.2 - 46.11. Environment Variables") /
[9.1](/docs/9.1/plpython-envar.html "PostgreSQL 9.1 - 46.11. Environment
Variables") / [9.0](/docs/9.0/plpython-envar.html "PostgreSQL 9.0 -
46.11. Environment Variables")

__

46.11. Environment Variables  
---  
[Prev](plpython-python23.html "46.10. Python 2 vs. Python 3")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi.html "Chapter 47. Server Programming Interface")  
  
* * *

## 46.11. Environment Variables #

Some of the environment variables that are accepted by the Python interpreter
can also be used to affect PL/Python behavior. They would need to be set in
the environment of the main PostgreSQL server process, for example in a start
script. The available environment variables depend on the version of Python;
see the Python documentation for details. At the time of this writing, the
following environment variables have an affect on PL/Python, assuming an
adequate Python version:

  * `PYTHONHOME`

  * `PYTHONPATH`

  * `PYTHONY2K`

  * `PYTHONOPTIMIZE`

  * `PYTHONDEBUG`

  * `PYTHONVERBOSE`

  * `PYTHONCASEOK`

  * `PYTHONDONTWRITEBYTECODE`

  * `PYTHONIOENCODING`

  * `PYTHONUSERBASE`

  * `PYTHONHASHSEED`

(It appears to be a Python implementation detail beyond the control of
PL/Python that some of the environment variables listed on the `python` man
page are only effective in a command-line interpreter and not an embedded
Python interpreter.)

* * *

[Prev](plpython-python23.html "46.10. Python 2 vs. Python 3")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](spi.html "Chapter 47. Server Programming Interface")  
---|---|---  
46.10. Python 2 vs. Python 3  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 47. Server Programming Interface  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-envar.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

