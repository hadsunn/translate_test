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

Supported Versions: [Current](/docs/current/plpython-subtransaction.html
"PostgreSQL 17 - 46.7. Explicit Subtransactions") ([17](/docs/17/plpython-
subtransaction.html "PostgreSQL 17 - 46.7. Explicit Subtransactions")) /
[16](/docs/16/plpython-subtransaction.html "PostgreSQL 16 - 46.7. Explicit
Subtransactions") / [15](/docs/15/plpython-subtransaction.html "PostgreSQL 15
- 46.7. Explicit Subtransactions") / [14](/docs/14/plpython-
subtransaction.html "PostgreSQL 14 - 46.7. Explicit Subtransactions") /
[13](/docs/13/plpython-subtransaction.html "PostgreSQL 13 - 46.7. Explicit
Subtransactions")

Development Versions: [18](/docs/18/plpython-subtransaction.html "PostgreSQL
18 - 46.7. Explicit Subtransactions") / [devel](/docs/devel/plpython-
subtransaction.html "PostgreSQL devel - 46.7. Explicit Subtransactions")

Unsupported versions: [12](/docs/12/plpython-subtransaction.html "PostgreSQL
12 - 46.7. Explicit Subtransactions") / [11](/docs/11/plpython-
subtransaction.html "PostgreSQL 11 - 46.7. Explicit Subtransactions") /
[10](/docs/10/plpython-subtransaction.html "PostgreSQL 10 - 46.7. Explicit
Subtransactions") / [9.6](/docs/9.6/plpython-subtransaction.html "PostgreSQL
9.6 - 46.7. Explicit Subtransactions") / [9.5](/docs/9.5/plpython-
subtransaction.html "PostgreSQL 9.5 - 46.7. Explicit Subtransactions") /
[9.4](/docs/9.4/plpython-subtransaction.html "PostgreSQL 9.4 - 46.7. Explicit
Subtransactions") / [9.3](/docs/9.3/plpython-subtransaction.html "PostgreSQL
9.3 - 46.7. Explicit Subtransactions") / [9.2](/docs/9.2/plpython-
subtransaction.html "PostgreSQL 9.2 - 46.7. Explicit Subtransactions") /
[9.1](/docs/9.1/plpython-subtransaction.html "PostgreSQL 9.1 - 46.7. Explicit
Subtransactions")

__

46.7. Explicit Subtransactions  
---  
[Prev](plpython-database.html "46.6. Database Access")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-transactions.html "46.8. Transaction Management")  
  
* * *

## 46.7. Explicit Subtransactions #

[46.7.1. Subtransaction Context Managers](plpython-
subtransaction.html#PLPYTHON-SUBTRANSACTION-CONTEXT-MANAGERS)

Recovering from errors caused by database access as described in [Section
46.6.2](plpython-database.html#PLPYTHON-TRAPPING "46.6.2. Trapping Errors")
can lead to an undesirable situation where some operations succeed before one
of them fails, and after recovering from that error the data is left in an
inconsistent state. PL/Python offers a solution to this problem in the form of
explicit subtransactions.

### 46.7.1. Subtransaction Context Managers #

Consider a function that implements a transfer between two accounts:

    
    
    CREATE FUNCTION transfer_funds() RETURNS void AS $$
    try:
        plpy.execute("UPDATE accounts SET balance = balance - 100 WHERE account_name = 'joe'")
        plpy.execute("UPDATE accounts SET balance = balance + 100 WHERE account_name = 'mary'")
    except plpy.SPIError as e:
        result = "error transferring funds: %s" % e.args
    else:
        result = "funds transferred correctly"
    plan = plpy.prepare("INSERT INTO operations (result) VALUES ($1)", ["text"])
    plpy.execute(plan, [result])
    $$ LANGUAGE plpython3u;
    

If the second `UPDATE` statement results in an exception being raised, this
function will report the error, but the result of the first `UPDATE` will
nevertheless be committed. In other words, the funds will be withdrawn from
Joe's account, but will not be transferred to Mary's account.

To avoid such issues, you can wrap your `plpy.execute` calls in an explicit
subtransaction. The `plpy` module provides a helper object to manage explicit
subtransactions that gets created with the `plpy.subtransaction()` function.
Objects created by this function implement the [context manager
interface](https://docs.python.org/library/stdtypes.html#context-manager-
types). Using explicit subtransactions we can rewrite our function as:

    
    
    CREATE FUNCTION transfer_funds2() RETURNS void AS $$
    try:
        with plpy.subtransaction():
            plpy.execute("UPDATE accounts SET balance = balance - 100 WHERE account_name = 'joe'")
            plpy.execute("UPDATE accounts SET balance = balance + 100 WHERE account_name = 'mary'")
    except plpy.SPIError as e:
        result = "error transferring funds: %s" % e.args
    else:
        result = "funds transferred correctly"
    plan = plpy.prepare("INSERT INTO operations (result) VALUES ($1)", ["text"])
    plpy.execute(plan, [result])
    $$ LANGUAGE plpython3u;
    

Note that the use of `try`/`except` is still required. Otherwise the exception
would propagate to the top of the Python stack and would cause the whole
function to abort with a PostgreSQL error, so that the `operations` table
would not have any row inserted into it. The subtransaction context manager
does not trap errors, it only assures that all database operations executed
inside its scope will be atomically committed or rolled back. A rollback of
the subtransaction block occurs on any kind of exception exit, not only ones
caused by errors originating from database access. A regular Python exception
raised inside an explicit subtransaction block would also cause the
subtransaction to be rolled back.

* * *

[Prev](plpython-database.html "46.6. Database Access")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-transactions.html "46.8. Transaction Management")  
---|---|---  
46.6. Database Access  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.8. Transaction Management  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-subtransaction.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

