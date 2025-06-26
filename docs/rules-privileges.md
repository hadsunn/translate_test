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

Supported Versions: [Current](/docs/current/rules-privileges.html "PostgreSQL
17 - 41.5. Rules and Privileges") ([17](/docs/17/rules-privileges.html
"PostgreSQL 17 - 41.5. Rules and Privileges")) / [16](/docs/16/rules-
privileges.html "PostgreSQL 16 - 41.5. Rules and Privileges") /
[15](/docs/15/rules-privileges.html "PostgreSQL 15 - 41.5. Rules and
Privileges") / [14](/docs/14/rules-privileges.html "PostgreSQL 14 -
41.5. Rules and Privileges") / [13](/docs/13/rules-privileges.html "PostgreSQL
13 - 41.5. Rules and Privileges")

Development Versions: [18](/docs/18/rules-privileges.html "PostgreSQL 18 -
41.5. Rules and Privileges") / [devel](/docs/devel/rules-privileges.html
"PostgreSQL devel - 41.5. Rules and Privileges")

Unsupported versions: [12](/docs/12/rules-privileges.html "PostgreSQL 12 -
41.5. Rules and Privileges") / [11](/docs/11/rules-privileges.html "PostgreSQL
11 - 41.5. Rules and Privileges") / [10](/docs/10/rules-privileges.html
"PostgreSQL 10 - 41.5. Rules and Privileges") / [9.6](/docs/9.6/rules-
privileges.html "PostgreSQL 9.6 - 41.5. Rules and Privileges") /
[9.5](/docs/9.5/rules-privileges.html "PostgreSQL 9.5 - 41.5. Rules and
Privileges") / [9.4](/docs/9.4/rules-privileges.html "PostgreSQL 9.4 -
41.5. Rules and Privileges") / [9.3](/docs/9.3/rules-privileges.html
"PostgreSQL 9.3 - 41.5. Rules and Privileges") / [9.2](/docs/9.2/rules-
privileges.html "PostgreSQL 9.2 - 41.5. Rules and Privileges") /
[9.1](/docs/9.1/rules-privileges.html "PostgreSQL 9.1 - 41.5. Rules and
Privileges") / [9.0](/docs/9.0/rules-privileges.html "PostgreSQL 9.0 -
41.5. Rules and Privileges") / [8.4](/docs/8.4/rules-privileges.html
"PostgreSQL 8.4 - 41.5. Rules and Privileges") / [8.3](/docs/8.3/rules-
privileges.html "PostgreSQL 8.3 - 41.5. Rules and Privileges") /
[8.2](/docs/8.2/rules-privileges.html "PostgreSQL 8.2 - 41.5. Rules and
Privileges") / [8.1](/docs/8.1/rules-privileges.html "PostgreSQL 8.1 -
41.5. Rules and Privileges") / [8.0](/docs/8.0/rules-privileges.html
"PostgreSQL 8.0 - 41.5. Rules and Privileges") / [7.4](/docs/7.4/rules-
privileges.html "PostgreSQL 7.4 - 41.5. Rules and Privileges")

__

41.5. Rules and Privileges  
---  
[Prev](rules-update.html "41.4. Rules on INSERT, UPDATE, and DELETE")  | [Up](rules.html "Chapter 41. The Rule System") | Chapter 41. The Rule System | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](rules-status.html "41.6. Rules and Command Status")  
  
* * *

## 41.5. Rules and Privileges #

Due to rewriting of queries by the PostgreSQL rule system, other tables/views
than those used in the original query get accessed. When update rules are
used, this can include write access to tables.

Rewrite rules don't have a separate owner. The owner of a relation (table or
view) is automatically the owner of the rewrite rules that are defined for it.
The PostgreSQL rule system changes the behavior of the default access control
system. With the exception of `SELECT` rules associated with security invoker
views (see [`CREATE VIEW`](sql-createview.html "CREATE VIEW")), all relations
that are used due to rules get checked against the privileges of the rule
owner, not the user invoking the rule. This means that, except for security
invoker views, users only need the required privileges for the tables/views
that are explicitly named in their queries.

For example: A user has a list of phone numbers where some of them are
private, the others are of interest for the assistant of the office. The user
can construct the following:

    
    
    CREATE TABLE phone_data (person text, phone text, private boolean);
    CREATE VIEW phone_number AS
        SELECT person, CASE WHEN NOT private THEN phone END AS phone
        FROM phone_data;
    GRANT SELECT ON phone_number TO assistant;
    

Nobody except that user (and the database superusers) can access the
`phone_data` table. But because of the `GRANT`, the assistant can run a
`SELECT` on the `phone_number` view. The rule system will rewrite the `SELECT`
from `phone_number` into a `SELECT` from `phone_data`. Since the user is the
owner of `phone_number` and therefore the owner of the rule, the read access
to `phone_data` is now checked against the user's privileges and the query is
permitted. The check for accessing `phone_number` is also performed, but this
is done against the invoking user, so nobody but the user and the assistant
can use it.

The privileges are checked rule by rule. So the assistant is for now the only
one who can see the public phone numbers. But the assistant can set up another
view and grant access to that to the public. Then, anyone can see the
`phone_number` data through the assistant's view. What the assistant cannot do
is to create a view that directly accesses `phone_data`. (Actually the
assistant can, but it will not work since every access will be denied during
the permission checks.) And as soon as the user notices that the assistant
opened their `phone_number` view, the user can revoke the assistant's access.
Immediately, any access to the assistant's view would fail.

One might think that this rule-by-rule checking is a security hole, but in
fact it isn't. But if it did not work this way, the assistant could set up a
table with the same columns as `phone_number` and copy the data to there once
per day. Then it's the assistant's own data and the assistant can grant access
to everyone they want. A `GRANT` command means, “I trust you”. If someone you
trust does the thing above, it's time to think it over and then use `REVOKE`.

Note that while views can be used to hide the contents of certain columns
using the technique shown above, they cannot be used to reliably conceal the
data in unseen rows unless the `security_barrier` flag has been set. For
example, the following view is insecure:

    
    
    CREATE VIEW phone_number AS
        SELECT person, phone FROM phone_data WHERE phone NOT LIKE '412%';
    

This view might seem secure, since the rule system will rewrite any `SELECT`
from `phone_number` into a `SELECT` from `phone_data` and add the
qualification that only entries where `phone` does not begin with 412 are
wanted. But if the user can create their own functions, it is not difficult to
convince the planner to execute the user-defined function prior to the `NOT
LIKE` expression. For example:

    
    
    CREATE FUNCTION tricky(text, text) RETURNS bool AS $$
    BEGIN
        RAISE NOTICE '% => %', $1, $2;
        RETURN true;
    END;
    $$ LANGUAGE plpgsql COST 0.0000000000000000000001;
    
    SELECT * FROM phone_number WHERE tricky(person, phone);
    

Every person and phone number in the `phone_data` table will be printed as a
`NOTICE`, because the planner will choose to execute the inexpensive `tricky`
function before the more expensive `NOT LIKE`. Even if the user is prevented
from defining new functions, built-in functions can be used in similar
attacks. (For example, most casting functions include their input values in
the error messages they produce.)

Similar considerations apply to update rules. In the examples of the previous
section, the owner of the tables in the example database could grant the
privileges `SELECT`, `INSERT`, `UPDATE`, and `DELETE` on the `shoelace` view
to someone else, but only `SELECT` on `shoelace_log`. The rule action to write
log entries will still be executed successfully, and that other user could see
the log entries. But they could not create fake entries, nor could they
manipulate or remove existing ones. In this case, there is no possibility of
subverting the rules by convincing the planner to alter the order of
operations, because the only rule which references `shoelace_log` is an
unqualified `INSERT`. This might not be true in more complex scenarios.

When it is necessary for a view to provide row-level security, the
`security_barrier` attribute should be applied to the view. This prevents
maliciously-chosen functions and operators from being passed values from rows
until after the view has done its work. For example, if the view shown above
had been created like this, it would be secure:

    
    
    CREATE VIEW phone_number WITH (security_barrier) AS
        SELECT person, phone FROM phone_data WHERE phone NOT LIKE '412%';
    

Views created with the `security_barrier` may perform far worse than views
created without this option. In general, there is no way to avoid this: the
fastest possible plan must be rejected if it may compromise security. For this
reason, this option is not enabled by default.

The query planner has more flexibility when dealing with functions that have
no side effects. Such functions are referred to as `LEAKPROOF`, and include
many simple, commonly used operators, such as many equality operators. The
query planner can safely allow such functions to be evaluated at any point in
the query execution process, since invoking them on rows invisible to the user
will not leak any information about the unseen rows. Further, functions which
do not take arguments or which are not passed any arguments from the security
barrier view do not have to be marked as `LEAKPROOF` to be pushed down, as
they never receive data from the view. In contrast, a function that might
throw an error depending on the values received as arguments (such as one that
throws an error in the event of overflow or division by zero) is not leak-
proof, and could provide significant information about the unseen rows if
applied before the security view's row filters.

It is important to understand that even a view created with the
`security_barrier` option is intended to be secure only in the limited sense
that the contents of the invisible tuples will not be passed to possibly-
insecure functions. The user may well have other means of making inferences
about the unseen data; for example, they can see the query plan using
`EXPLAIN`, or measure the run time of queries against the view. A malicious
attacker might be able to infer something about the amount of unseen data, or
even gain some information about the data distribution or most common values
(since these things may affect the run time of the plan; or even, since they
are also reflected in the optimizer statistics, the choice of plan). If these
types of "covert channel" attacks are of concern, it is probably unwise to
grant any access to the data at all.

* * *

[Prev](rules-update.html "41.4. Rules on INSERT, UPDATE, and DELETE")  | [Up](rules.html "Chapter 41. The Rule System") |  [Next](rules-status.html "41.6. Rules and Command Status")  
---|---|---  
41.4. Rules on `INSERT`, `UPDATE`, and `DELETE`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  41.6. Rules and Command Status  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/rules-privileges.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

