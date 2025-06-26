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

Supported Versions: [Current](/docs/current/plpython-util.html "PostgreSQL 17
- 46.9. Utility Functions") ([17](/docs/17/plpython-util.html "PostgreSQL 17 -
46.9. Utility Functions")) / [16](/docs/16/plpython-util.html "PostgreSQL 16 -
46.9. Utility Functions") / [15](/docs/15/plpython-util.html "PostgreSQL 15 -
46.9. Utility Functions") / [14](/docs/14/plpython-util.html "PostgreSQL 14 -
46.9. Utility Functions") / [13](/docs/13/plpython-util.html "PostgreSQL 13 -
46.9. Utility Functions")

Development Versions: [18](/docs/18/plpython-util.html "PostgreSQL 18 -
46.9. Utility Functions") / [devel](/docs/devel/plpython-util.html "PostgreSQL
devel - 46.9. Utility Functions")

Unsupported versions: [12](/docs/12/plpython-util.html "PostgreSQL 12 -
46.9. Utility Functions") / [11](/docs/11/plpython-util.html "PostgreSQL 11 -
46.9. Utility Functions") / [10](/docs/10/plpython-util.html "PostgreSQL 10 -
46.9. Utility Functions") / [9.6](/docs/9.6/plpython-util.html "PostgreSQL 9.6
- 46.9. Utility Functions") / [9.5](/docs/9.5/plpython-util.html "PostgreSQL
9.5 - 46.9. Utility Functions") / [9.4](/docs/9.4/plpython-util.html
"PostgreSQL 9.4 - 46.9. Utility Functions") / [9.3](/docs/9.3/plpython-
util.html "PostgreSQL 9.3 - 46.9. Utility Functions") /
[9.2](/docs/9.2/plpython-util.html "PostgreSQL 9.2 - 46.9. Utility Functions")
/ [9.1](/docs/9.1/plpython-util.html "PostgreSQL 9.1 - 46.9. Utility
Functions") / [9.0](/docs/9.0/plpython-util.html "PostgreSQL 9.0 -
46.9. Utility Functions")

__

46.9. Utility Functions  
---  
[Prev](plpython-transactions.html "46.8. Transaction Management")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-python23.html "46.10. Python 2 vs. Python 3")  
  
* * *

## 46.9. Utility Functions #

The `plpy` module also provides the functions

`plpy.debug(_`msg, **kwargs`_)`  
---  
`plpy.log(_`msg, **kwargs`_)`  
`plpy.info(_`msg, **kwargs`_)`  
`plpy.notice(_`msg, **kwargs`_)`  
`plpy.warning(_`msg, **kwargs`_)`  
`plpy.error(_`msg, **kwargs`_)`  
`plpy.fatal(_`msg, **kwargs`_)`  
  
`plpy.error` and `plpy.fatal` actually raise a Python exception which, if
uncaught, propagates out to the calling query, causing the current transaction
or subtransaction to be aborted. `raise plpy.Error(_`msg`_)` and `raise
plpy.Fatal(_`msg`_)` are equivalent to calling `plpy.error(_`msg`_)` and
`plpy.fatal(_`msg`_)`, respectively but the `raise` form does not allow
passing keyword arguments. The other functions only generate messages of
different priority levels. Whether messages of a particular priority are
reported to the client, written to the server log, or both is controlled by
the [log_min_messages](runtime-config-logging.html#GUC-LOG-MIN-MESSAGES) and
[client_min_messages](runtime-config-client.html#GUC-CLIENT-MIN-MESSAGES)
configuration variables. See [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") for more information.

The _`msg`_ argument is given as a positional argument. For backward
compatibility, more than one positional argument can be given. In that case,
the string representation of the tuple of positional arguments becomes the
message reported to the client.

The following keyword-only arguments are accepted:

`detail`  
---  
`hint`  
`sqlstate`  
`schema_name`  
`table_name`  
`column_name`  
`datatype_name`  
`constraint_name`  
  
The string representation of the objects passed as keyword-only arguments is
used to enrich the messages reported to the client. For example:

    
    
    CREATE FUNCTION raise_custom_exception() RETURNS void AS $$
    plpy.error("custom exception message",
               detail="some info about exception",
               hint="hint for users")
    $$ LANGUAGE plpython3u;
    
    =# SELECT raise_custom_exception();
    ERROR:  plpy.Error: custom exception message
    DETAIL:  some info about exception
    HINT:  hint for users
    CONTEXT:  Traceback (most recent call last):
      PL/Python function "raise_custom_exception", line 4, in <module>
        hint="hint for users")
    PL/Python function "raise_custom_exception"
    

Another set of utility functions are `plpy.quote_literal(_`string`_)`,
`plpy.quote_nullable(_`string`_)`, and `plpy.quote_ident(_`string`_)`. They
are equivalent to the built-in quoting functions described in [Section
9.4](functions-string.html "9.4. String Functions and Operators"). They are
useful when constructing ad-hoc queries. A PL/Python equivalent of dynamic SQL
from [Example 43.1](plpgsql-statements.html#PLPGSQL-QUOTE-LITERAL-EXAMPLE
"Example 43.1. Quoting Values in Dynamic Queries") would be:

    
    
    plpy.execute("UPDATE tbl SET %s = %s WHERE key = %s" % (
        plpy.quote_ident(colname),
        plpy.quote_nullable(newvalue),
        plpy.quote_literal(keyvalue)))
    

* * *

[Prev](plpython-transactions.html "46.8. Transaction Management")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-python23.html "46.10. Python 2 vs. Python 3")  
---|---|---  
46.8. Transaction Management  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.10. Python 2 vs. Python 3  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-util.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

