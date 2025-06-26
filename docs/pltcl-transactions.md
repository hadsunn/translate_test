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

Supported Versions: [Current](/docs/current/pltcl-transactions.html
"PostgreSQL 17 - 44.10. Transaction Management") ([17](/docs/17/pltcl-
transactions.html "PostgreSQL 17 - 44.10. Transaction Management")) /
[16](/docs/16/pltcl-transactions.html "PostgreSQL 16 - 44.10. Transaction
Management") / [15](/docs/15/pltcl-transactions.html "PostgreSQL 15 -
44.10. Transaction Management") / [14](/docs/14/pltcl-transactions.html
"PostgreSQL 14 - 44.10. Transaction Management") / [13](/docs/13/pltcl-
transactions.html "PostgreSQL 13 - 44.10. Transaction Management")

Development Versions: [18](/docs/18/pltcl-transactions.html "PostgreSQL 18 -
44.10. Transaction Management") / [devel](/docs/devel/pltcl-transactions.html
"PostgreSQL devel - 44.10. Transaction Management")

Unsupported versions: [12](/docs/12/pltcl-transactions.html "PostgreSQL 12 -
44.10. Transaction Management") / [11](/docs/11/pltcl-transactions.html
"PostgreSQL 11 - 44.10. Transaction Management")

__

44.10. Transaction Management  
---  
[Prev](pltcl-subtransactions.html "44.9. Explicit Subtransactions in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-config.html "44.11. PL/Tcl Configuration")  
  
* * *

## 44.10. Transaction Management #

In a procedure called from the top level or an anonymous code block (`DO`
command) called from the top level it is possible to control transactions. To
commit the current transaction, call the `commit` command. To roll back the
current transaction, call the `rollback` command. (Note that it is not
possible to run the SQL commands `COMMIT` or `ROLLBACK` via `spi_exec` or
similar. It has to be done using these functions.) After a transaction is
ended, a new transaction is automatically started, so there is no separate
command for that.

Here is an example:

    
    
    CREATE PROCEDURE transaction_test1()
    LANGUAGE pltcl
    AS $$
    for {set i 0} {$i < 10} {incr i} {
        spi_exec "INSERT INTO test1 (a) VALUES ($i)"
        if {$i % 2 == 0} {
            commit
        } else {
            rollback
        }
    }
    $$;
    
    CALL transaction_test1();
    

Transactions cannot be ended when an explicit subtransaction is active.

* * *

[Prev](pltcl-subtransactions.html "44.9. Explicit Subtransactions in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-config.html "44.11. PL/Tcl Configuration")  
---|---|---  
44.9. Explicit Subtransactions in PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.11. PL/Tcl Configuration  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-transactions.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

