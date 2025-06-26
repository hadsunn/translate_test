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

Supported Versions: [Current](/docs/current/plpython-transactions.html
"PostgreSQL 17 - 46.8. Transaction Management") ([17](/docs/17/plpython-
transactions.html "PostgreSQL 17 - 46.8. Transaction Management")) /
[16](/docs/16/plpython-transactions.html "PostgreSQL 16 - 46.8. Transaction
Management") / [15](/docs/15/plpython-transactions.html "PostgreSQL 15 -
46.8. Transaction Management") / [14](/docs/14/plpython-transactions.html
"PostgreSQL 14 - 46.8. Transaction Management") / [13](/docs/13/plpython-
transactions.html "PostgreSQL 13 - 46.8. Transaction Management")

Development Versions: [18](/docs/18/plpython-transactions.html "PostgreSQL 18
- 46.8. Transaction Management") / [devel](/docs/devel/plpython-
transactions.html "PostgreSQL devel - 46.8. Transaction Management")

Unsupported versions: [12](/docs/12/plpython-transactions.html "PostgreSQL 12
- 46.8. Transaction Management") / [11](/docs/11/plpython-transactions.html
"PostgreSQL 11 - 46.8. Transaction Management")

__

46.8. Transaction Management  
---  
[Prev](plpython-subtransaction.html "46.7. Explicit Subtransactions")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-util.html "46.9. Utility Functions")  
  
* * *

## 46.8. Transaction Management #

In a procedure called from the top level or an anonymous code block (`DO`
command) called from the top level it is possible to control transactions. To
commit the current transaction, call `plpy.commit()`. To roll back the current
transaction, call `plpy.rollback()`. (Note that it is not possible to run the
SQL commands `COMMIT` or `ROLLBACK` via `plpy.execute` or similar. It has to
be done using these functions.) After a transaction is ended, a new
transaction is automatically started, so there is no separate function for
that.

Here is an example:

    
    
    CREATE PROCEDURE transaction_test1()
    LANGUAGE plpython3u
    AS $$
    for i in range(0, 10):
        plpy.execute("INSERT INTO test1 (a) VALUES (%d)" % i)
        if i % 2 == 0:
            plpy.commit()
        else:
            plpy.rollback()
    $$;
    
    CALL transaction_test1();
    

Transactions cannot be ended when an explicit subtransaction is active.

* * *

[Prev](plpython-subtransaction.html "46.7. Explicit Subtransactions")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-util.html "46.9. Utility Functions")  
---|---|---  
46.7. Explicit Subtransactions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.9. Utility Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-transactions.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

