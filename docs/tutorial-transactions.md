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

Supported Versions: [Current](/docs/current/tutorial-transactions.html
"PostgreSQL 17 - 3.4. Transactions") ([17](/docs/17/tutorial-transactions.html
"PostgreSQL 17 - 3.4. Transactions")) / [16](/docs/16/tutorial-
transactions.html "PostgreSQL 16 - 3.4. Transactions") /
[15](/docs/15/tutorial-transactions.html "PostgreSQL 15 - 3.4. Transactions")
/ [14](/docs/14/tutorial-transactions.html "PostgreSQL 14 -
3.4. Transactions") / [13](/docs/13/tutorial-transactions.html "PostgreSQL 13
- 3.4. Transactions")

Development Versions: [18](/docs/18/tutorial-transactions.html "PostgreSQL 18
- 3.4. Transactions") / [devel](/docs/devel/tutorial-transactions.html
"PostgreSQL devel - 3.4. Transactions")

Unsupported versions: [12](/docs/12/tutorial-transactions.html "PostgreSQL 12
- 3.4. Transactions") / [11](/docs/11/tutorial-transactions.html "PostgreSQL
11 - 3.4. Transactions") / [10](/docs/10/tutorial-transactions.html
"PostgreSQL 10 - 3.4. Transactions") / [9.6](/docs/9.6/tutorial-
transactions.html "PostgreSQL 9.6 - 3.4. Transactions") /
[9.5](/docs/9.5/tutorial-transactions.html "PostgreSQL 9.5 -
3.4. Transactions") / [9.4](/docs/9.4/tutorial-transactions.html "PostgreSQL
9.4 - 3.4. Transactions") / [9.3](/docs/9.3/tutorial-transactions.html
"PostgreSQL 9.3 - 3.4. Transactions") / [9.2](/docs/9.2/tutorial-
transactions.html "PostgreSQL 9.2 - 3.4. Transactions") /
[9.1](/docs/9.1/tutorial-transactions.html "PostgreSQL 9.1 -
3.4. Transactions") / [9.0](/docs/9.0/tutorial-transactions.html "PostgreSQL
9.0 - 3.4. Transactions") / [8.4](/docs/8.4/tutorial-transactions.html
"PostgreSQL 8.4 - 3.4. Transactions") / [8.3](/docs/8.3/tutorial-
transactions.html "PostgreSQL 8.3 - 3.4. Transactions") /
[8.2](/docs/8.2/tutorial-transactions.html "PostgreSQL 8.2 -
3.4. Transactions") / [8.1](/docs/8.1/tutorial-transactions.html "PostgreSQL
8.1 - 3.4. Transactions") / [8.0](/docs/8.0/tutorial-transactions.html
"PostgreSQL 8.0 - 3.4. Transactions") / [7.4](/docs/7.4/tutorial-
transactions.html "PostgreSQL 7.4 - 3.4. Transactions") /
[7.3](/docs/7.3/tutorial-transactions.html "PostgreSQL 7.3 -
3.4. Transactions") / [7.2](/docs/7.2/tutorial-transactions.html "PostgreSQL
7.2 - 3.4. Transactions")

__

3.4. Transactions  
---  
[Prev](tutorial-fk.html "3.3. Foreign Keys")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") | Chapter 3. Advanced Features | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-window.html "3.5. Window Functions")  
  
* * *

## 3.4. Transactions #

_Transactions_ are a fundamental concept of all database systems. The
essential point of a transaction is that it bundles multiple steps into a
single, all-or-nothing operation. The intermediate states between the steps
are not visible to other concurrent transactions, and if some failure occurs
that prevents the transaction from completing, then none of the steps affect
the database at all.

For example, consider a bank database that contains balances for various
customer accounts, as well as total deposit balances for branches. Suppose
that we want to record a payment of $100.00 from Alice's account to Bob's
account. Simplifying outrageously, the SQL commands for this might look like:

    
    
    UPDATE accounts SET balance = balance - 100.00
        WHERE name = 'Alice';
    UPDATE branches SET balance = balance - 100.00
        WHERE name = (SELECT branch_name FROM accounts WHERE name = 'Alice');
    UPDATE accounts SET balance = balance + 100.00
        WHERE name = 'Bob';
    UPDATE branches SET balance = balance + 100.00
        WHERE name = (SELECT branch_name FROM accounts WHERE name = 'Bob');
    

The details of these commands are not important here; the important point is
that there are several separate updates involved to accomplish this rather
simple operation. Our bank's officers will want to be assured that either all
these updates happen, or none of them happen. It would certainly not do for a
system failure to result in Bob receiving $100.00 that was not debited from
Alice. Nor would Alice long remain a happy customer if she was debited without
Bob being credited. We need a guarantee that if something goes wrong partway
through the operation, none of the steps executed so far will take effect.
Grouping the updates into a _transaction_ gives us this guarantee. A
transaction is said to be _atomic_ : from the point of view of other
transactions, it either happens completely or not at all.

We also want a guarantee that once a transaction is completed and acknowledged
by the database system, it has indeed been permanently recorded and won't be
lost even if a crash ensues shortly thereafter. For example, if we are
recording a cash withdrawal by Bob, we do not want any chance that the debit
to his account will disappear in a crash just after he walks out the bank
door. A transactional database guarantees that all the updates made by a
transaction are logged in permanent storage (i.e., on disk) before the
transaction is reported complete.

Another important property of transactional databases is closely related to
the notion of atomic updates: when multiple transactions are running
concurrently, each one should not be able to see the incomplete changes made
by others. For example, if one transaction is busy totalling all the branch
balances, it would not do for it to include the debit from Alice's branch but
not the credit to Bob's branch, nor vice versa. So transactions must be all-
or-nothing not only in terms of their permanent effect on the database, but
also in terms of their visibility as they happen. The updates made so far by
an open transaction are invisible to other transactions until the transaction
completes, whereupon all the updates become visible simultaneously.

In PostgreSQL, a transaction is set up by surrounding the SQL commands of the
transaction with `BEGIN` and `COMMIT` commands. So our banking transaction
would actually look like:

    
    
    BEGIN;
    UPDATE accounts SET balance = balance - 100.00
        WHERE name = 'Alice';
    -- etc etc
    COMMIT;
    

If, partway through the transaction, we decide we do not want to commit
(perhaps we just noticed that Alice's balance went negative), we can issue the
command `ROLLBACK` instead of `COMMIT`, and all our updates so far will be
canceled.

PostgreSQL actually treats every SQL statement as being executed within a
transaction. If you do not issue a `BEGIN` command, then each individual
statement has an implicit `BEGIN` and (if successful) `COMMIT` wrapped around
it. A group of statements surrounded by `BEGIN` and `COMMIT` is sometimes
called a _transaction block_.

### Note

Some client libraries issue `BEGIN` and `COMMIT` commands automatically, so
that you might get the effect of transaction blocks without asking. Check the
documentation for the interface you are using.

It's possible to control the statements in a transaction in a more granular
fashion through the use of _savepoints_. Savepoints allow you to selectively
discard parts of the transaction, while committing the rest. After defining a
savepoint with `SAVEPOINT`, you can if needed roll back to the savepoint with
`ROLLBACK TO`. All the transaction's database changes between defining the
savepoint and rolling back to it are discarded, but changes earlier than the
savepoint are kept.

After rolling back to a savepoint, it continues to be defined, so you can roll
back to it several times. Conversely, if you are sure you won't need to roll
back to a particular savepoint again, it can be released, so the system can
free some resources. Keep in mind that either releasing or rolling back to a
savepoint will automatically release all savepoints that were defined after
it.

All this is happening within the transaction block, so none of it is visible
to other database sessions. When and if you commit the transaction block, the
committed actions become visible as a unit to other sessions, while the
rolled-back actions never become visible at all.

Remembering the bank database, suppose we debit $100.00 from Alice's account,
and credit Bob's account, only to find later that we should have credited
Wally's account. We could do it using savepoints like this:

    
    
    BEGIN;
    UPDATE accounts SET balance = balance - 100.00
        WHERE name = 'Alice';
    SAVEPOINT my_savepoint;
    UPDATE accounts SET balance = balance + 100.00
        WHERE name = 'Bob';
    -- oops ... forget that and use Wally's account
    ROLLBACK TO my_savepoint;
    UPDATE accounts SET balance = balance + 100.00
        WHERE name = 'Wally';
    COMMIT;
    

This example is, of course, oversimplified, but there's a lot of control
possible in a transaction block through the use of savepoints. Moreover,
`ROLLBACK TO` is the only way to regain control of a transaction block that
was put in aborted state by the system due to an error, short of rolling it
back completely and starting again.

* * *

[Prev](tutorial-fk.html "3.3. Foreign Keys")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") |  [Next](tutorial-window.html "3.5. Window Functions")  
---|---|---  
3.3. Foreign Keys  | [Home](index.html "PostgreSQL 16.9 Documentation") |  3.5. Window Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-transactions.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

