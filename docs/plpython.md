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

Supported Versions: [Current](/docs/current/plpython.html "PostgreSQL 17 -
Chapter 46. PL/Python — Python Procedural Language")
([17](/docs/17/plpython.html "PostgreSQL 17 - Chapter 46. PL/Python — Python
Procedural Language")) / [16](/docs/16/plpython.html "PostgreSQL 16 -
Chapter 46. PL/Python — Python Procedural Language") /
[15](/docs/15/plpython.html "PostgreSQL 15 - Chapter 46. PL/Python — Python
Procedural Language") / [14](/docs/14/plpython.html "PostgreSQL 14 -
Chapter 46. PL/Python — Python Procedural Language") /
[13](/docs/13/plpython.html "PostgreSQL 13 - Chapter 46. PL/Python — Python
Procedural Language")

Development Versions: [18](/docs/18/plpython.html "PostgreSQL 18 -
Chapter 46. PL/Python — Python Procedural Language") /
[devel](/docs/devel/plpython.html "PostgreSQL devel - Chapter 46. PL/Python —
Python Procedural Language")

Unsupported versions: [12](/docs/12/plpython.html "PostgreSQL 12 -
Chapter 46. PL/Python — Python Procedural Language") /
[11](/docs/11/plpython.html "PostgreSQL 11 - Chapter 46. PL/Python — Python
Procedural Language") / [10](/docs/10/plpython.html "PostgreSQL 10 -
Chapter 46. PL/Python — Python Procedural Language") /
[9.6](/docs/9.6/plpython.html "PostgreSQL 9.6 - Chapter 46. PL/Python — Python
Procedural Language") / [9.5](/docs/9.5/plpython.html "PostgreSQL 9.5 -
Chapter 46. PL/Python — Python Procedural Language") /
[9.4](/docs/9.4/plpython.html "PostgreSQL 9.4 - Chapter 46. PL/Python — Python
Procedural Language") / [9.3](/docs/9.3/plpython.html "PostgreSQL 9.3 -
Chapter 46. PL/Python — Python Procedural Language") /
[9.2](/docs/9.2/plpython.html "PostgreSQL 9.2 - Chapter 46. PL/Python — Python
Procedural Language") / [9.1](/docs/9.1/plpython.html "PostgreSQL 9.1 -
Chapter 46. PL/Python — Python Procedural Language") /
[9.0](/docs/9.0/plpython.html "PostgreSQL 9.0 - Chapter 46. PL/Python — Python
Procedural Language") / [8.4](/docs/8.4/plpython.html "PostgreSQL 8.4 -
Chapter 46. PL/Python — Python Procedural Language") /
[8.3](/docs/8.3/plpython.html "PostgreSQL 8.3 - Chapter 46. PL/Python — Python
Procedural Language") / [8.2](/docs/8.2/plpython.html "PostgreSQL 8.2 -
Chapter 46. PL/Python — Python Procedural Language") /
[8.1](/docs/8.1/plpython.html "PostgreSQL 8.1 - Chapter 46. PL/Python — Python
Procedural Language") / [8.0](/docs/8.0/plpython.html "PostgreSQL 8.0 -
Chapter 46. PL/Python — Python Procedural Language") /
[7.4](/docs/7.4/plpython.html "PostgreSQL 7.4 - Chapter 46. PL/Python — Python
Procedural Language") / [7.3](/docs/7.3/plpython.html "PostgreSQL 7.3 -
Chapter 46. PL/Python — Python Procedural Language") /
[7.2](/docs/7.2/plpython.html "PostgreSQL 7.2 - Chapter 46. PL/Python — Python
Procedural Language")

__

Chapter 46. PL/Python — Python Procedural Language  
---  
[Prev](plperl-under-the-hood.html "45.8. PL/Perl Under the Hood")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-funcs.html "46.1. PL/Python Functions")  
  
* * *

## Chapter 46. PL/Python — Python Procedural Language

**Table of Contents**

[46.1. PL/Python Functions](plpython-funcs.html)

[46.2. Data Values](plpython-data.html)

    

[46.2.1. Data Type Mapping](plpython-data.html#PLPYTHON-DATA-TYPE-MAPPING)

[46.2.2. Null, None](plpython-data.html#PLPYTHON-DATA-NULL)

[46.2.3. Arrays, Lists](plpython-data.html#PLPYTHON-ARRAYS)

[46.2.4. Composite Types](plpython-data.html#PLPYTHON-DATA-COMPOSITE-TYPES)

[46.2.5. Set-Returning Functions](plpython-data.html#PLPYTHON-DATA-SET-
RETURNING-FUNCS)

[46.3. Sharing Data](plpython-sharing.html)

[46.4. Anonymous Code Blocks](plpython-do.html)

[46.5. Trigger Functions](plpython-trigger.html)

[46.6. Database Access](plpython-database.html)

    

[46.6.1. Database Access Functions](plpython-database.html#PLPYTHON-DATABASE-
ACCESS-FUNCS)

[46.6.2. Trapping Errors](plpython-database.html#PLPYTHON-TRAPPING)

[46.7. Explicit Subtransactions](plpython-subtransaction.html)

    

[46.7.1. Subtransaction Context Managers](plpython-
subtransaction.html#PLPYTHON-SUBTRANSACTION-CONTEXT-MANAGERS)

[46.8. Transaction Management](plpython-transactions.html)

[46.9. Utility Functions](plpython-util.html)

[46.10. Python 2 vs. Python 3](plpython-python23.html)

[46.11. Environment Variables](plpython-envar.html)

The PL/Python procedural language allows PostgreSQL functions and procedures
to be written in the [Python language](https://www.python.org).

To install PL/Python in a particular database, use `CREATE EXTENSION
plpython3u`.

### Tip

If a language is installed into `template1`, all subsequently created
databases will have the language installed automatically.

PL/Python is only available as an “untrusted” language, meaning it does not
offer any way of restricting what users can do in it and is therefore named
`plpython3u`. A trusted variant `plpython` might become available in the
future if a secure execution mechanism is developed in Python. The writer of a
function in untrusted PL/Python must take care that the function cannot be
used to do anything unwanted, since it will be able to do anything that could
be done by a user logged in as the database administrator. Only superusers can
create functions in untrusted languages such as `plpython3u`.

### Note

Users of source packages must specially enable the build of PL/Python during
the installation process. (Refer to the installation instructions for more
information.) Users of binary packages might find PL/Python in a separate
subpackage.

* * *

[Prev](plperl-under-the-hood.html "45.8. PL/Perl Under the Hood")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](plpython-funcs.html "46.1. PL/Python Functions")  
---|---|---  
45.8. PL/Perl Under the Hood  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.1. PL/Python Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

