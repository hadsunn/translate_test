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

Supported Versions: [Current](/docs/current/pltcl-subtransactions.html
"PostgreSQL 17 - 44.9. Explicit Subtransactions in PL/Tcl")
([17](/docs/17/pltcl-subtransactions.html "PostgreSQL 17 - 44.9. Explicit
Subtransactions in PL/Tcl")) / [16](/docs/16/pltcl-subtransactions.html
"PostgreSQL 16 - 44.9. Explicit Subtransactions in PL/Tcl") /
[15](/docs/15/pltcl-subtransactions.html "PostgreSQL 15 - 44.9. Explicit
Subtransactions in PL/Tcl") / [14](/docs/14/pltcl-subtransactions.html
"PostgreSQL 14 - 44.9. Explicit Subtransactions in PL/Tcl") /
[13](/docs/13/pltcl-subtransactions.html "PostgreSQL 13 - 44.9. Explicit
Subtransactions in PL/Tcl")

Development Versions: [18](/docs/18/pltcl-subtransactions.html "PostgreSQL 18
- 44.9. Explicit Subtransactions in PL/Tcl") / [devel](/docs/devel/pltcl-
subtransactions.html "PostgreSQL devel - 44.9. Explicit Subtransactions in
PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-subtransactions.html "PostgreSQL 12
- 44.9. Explicit Subtransactions in PL/Tcl") / [11](/docs/11/pltcl-
subtransactions.html "PostgreSQL 11 - 44.9. Explicit Subtransactions in
PL/Tcl") / [10](/docs/10/pltcl-subtransactions.html "PostgreSQL 10 -
44.9. Explicit Subtransactions in PL/Tcl")

__

44.9. Explicit Subtransactions in PL/Tcl  
---  
[Prev](pltcl-error-handling.html "44.8. Error Handling in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-transactions.html "44.10. Transaction Management")  
  
* * *

## 44.9. Explicit Subtransactions in PL/Tcl #

Recovering from errors caused by database access as described in [Section
44.8](pltcl-error-handling.html "44.8. Error Handling in PL/Tcl") can lead to
an undesirable situation where some operations succeed before one of them
fails, and after recovering from that error the data is left in an
inconsistent state. PL/Tcl offers a solution to this problem in the form of
explicit subtransactions.

Consider a function that implements a transfer between two accounts:

    
    
    CREATE FUNCTION transfer_funds() RETURNS void AS $$
        if [catch {
            spi_exec "UPDATE accounts SET balance = balance - 100 WHERE account_name = 'joe'"
            spi_exec "UPDATE accounts SET balance = balance + 100 WHERE account_name = 'mary'"
        } errormsg] {
            set result [format "error transferring funds: %s" $errormsg]
        } else {
            set result "funds transferred successfully"
        }
        spi_exec "INSERT INTO operations (result) VALUES ('[quote $result]')"
    $$ LANGUAGE pltcl;
    

If the second `UPDATE` statement results in an exception being raised, this
function will log the failure, but the result of the first `UPDATE` will
nevertheless be committed. In other words, the funds will be withdrawn from
Joe's account, but will not be transferred to Mary's account. This happens
because each `spi_exec` is a separate subtransaction, and only one of those
subtransactions got rolled back.

To handle such cases, you can wrap multiple database operations in an explicit
subtransaction, which will succeed or roll back as a whole. PL/Tcl provides a
`subtransaction` command to manage this. We can rewrite our function as:

    
    
    CREATE FUNCTION transfer_funds2() RETURNS void AS $$
        if [catch {
            subtransaction {
                spi_exec "UPDATE accounts SET balance = balance - 100 WHERE account_name = 'joe'"
                spi_exec "UPDATE accounts SET balance = balance + 100 WHERE account_name = 'mary'"
            }
        } errormsg] {
            set result [format "error transferring funds: %s" $errormsg]
        } else {
            set result "funds transferred successfully"
        }
        spi_exec "INSERT INTO operations (result) VALUES ('[quote $result]')"
    $$ LANGUAGE pltcl;
    

Note that use of `catch` is still required for this purpose. Otherwise the
error would propagate to the top level of the function, preventing the desired
insertion into the `operations` table. The `subtransaction` command does not
trap errors, it only assures that all database operations executed inside its
scope will be rolled back together when an error is reported.

A rollback of an explicit subtransaction occurs on any error reported by the
contained Tcl code, not only errors originating from database access. Thus a
regular Tcl exception raised inside a `subtransaction` command will also cause
the subtransaction to be rolled back. However, non-error exits out of the
contained Tcl code (for instance, due to `return`) do not cause a rollback.

* * *

[Prev](pltcl-error-handling.html "44.8. Error Handling in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-transactions.html "44.10. Transaction Management")  
---|---|---  
44.8. Error Handling in PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.10. Transaction Management  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-subtransactions.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

