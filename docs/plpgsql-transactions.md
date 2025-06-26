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

Supported Versions: [Current](/docs/current/plpgsql-transactions.html
"PostgreSQL 17 - 43.8. Transaction Management") ([17](/docs/17/plpgsql-
transactions.html "PostgreSQL 17 - 43.8. Transaction Management")) /
[16](/docs/16/plpgsql-transactions.html "PostgreSQL 16 - 43.8. Transaction
Management") / [15](/docs/15/plpgsql-transactions.html "PostgreSQL 15 -
43.8. Transaction Management") / [14](/docs/14/plpgsql-transactions.html
"PostgreSQL 14 - 43.8. Transaction Management") / [13](/docs/13/plpgsql-
transactions.html "PostgreSQL 13 - 43.8. Transaction Management")

Development Versions: [18](/docs/18/plpgsql-transactions.html "PostgreSQL 18 -
43.8. Transaction Management") / [devel](/docs/devel/plpgsql-transactions.html
"PostgreSQL devel - 43.8. Transaction Management")

Unsupported versions: [12](/docs/12/plpgsql-transactions.html "PostgreSQL 12 -
43.8. Transaction Management") / [11](/docs/11/plpgsql-transactions.html
"PostgreSQL 11 - 43.8. Transaction Management")

__

43.8. Transaction Management  
---  
[Prev](plpgsql-cursors.html "43.7. Cursors")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-errors-and-messages.html "43.9. Errors and Messages")  
  
* * *

## 43.8. Transaction Management #

In procedures invoked by the `CALL` command as well as in anonymous code
blocks (`DO` command), it is possible to end transactions using the commands
`COMMIT` and `ROLLBACK`. A new transaction is started automatically after a
transaction is ended using these commands, so there is no separate `START
TRANSACTION` command. (Note that `BEGIN` and `END` have different meanings in
PL/pgSQL.)

Here is a simple example:

    
    
    CREATE PROCEDURE transaction_test1()
    LANGUAGE plpgsql
    AS $$
    BEGIN
        FOR i IN 0..9 LOOP
            INSERT INTO test1 (a) VALUES (i);
            IF i % 2 = 0 THEN
                COMMIT;
            ELSE
                ROLLBACK;
            END IF;
        END LOOP;
    END;
    $$;
    
    CALL transaction_test1();
    

A new transaction starts out with default transaction characteristics such as
transaction isolation level. In cases where transactions are committed in a
loop, it might be desirable to start new transactions automatically with the
same characteristics as the previous one. The commands `COMMIT AND CHAIN` and
`ROLLBACK AND CHAIN` accomplish this.

Transaction control is only possible in `CALL` or `DO` invocations from the
top level or nested `CALL` or `DO` invocations without any other intervening
command. For example, if the call stack is `CALL proc1()` → `CALL proc2()` →
`CALL proc3()`, then the second and third procedures can perform transaction
control actions. But if the call stack is `CALL proc1()` → `SELECT func2()` →
`CALL proc3()`, then the last procedure cannot do transaction control, because
of the `SELECT` in between.

Special considerations apply to cursor loops. Consider this example:

    
    
    CREATE PROCEDURE transaction_test2()
    LANGUAGE plpgsql
    AS $$
    DECLARE
        r RECORD;
    BEGIN
        FOR r IN SELECT * FROM test2 ORDER BY x LOOP
            INSERT INTO test1 (a) VALUES (r.x);
            COMMIT;
        END LOOP;
    END;
    $$;
    
    CALL transaction_test2();
    

Normally, cursors are automatically closed at transaction commit. However, a
cursor created as part of a loop like this is automatically converted to a
holdable cursor by the first `COMMIT` or `ROLLBACK`. That means that the
cursor is fully evaluated at the first `COMMIT` or `ROLLBACK` rather than row
by row. The cursor is still removed automatically after the loop, so this is
mostly invisible to the user.

Transaction commands are not allowed in cursor loops driven by commands that
are not read-only (for example `UPDATE ... RETURNING`).

A transaction cannot be ended inside a block with exception handlers.

* * *

[Prev](plpgsql-cursors.html "43.7. Cursors")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-errors-and-messages.html "43.9. Errors and Messages")  
---|---|---  
43.7. Cursors  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.9. Errors and Messages  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-transactions.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

