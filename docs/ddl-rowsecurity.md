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

Supported Versions: [Current](/docs/current/ddl-rowsecurity.html "PostgreSQL
17 - 5.8. Row Security Policies") ([17](/docs/17/ddl-rowsecurity.html
"PostgreSQL 17 - 5.8. Row Security Policies")) / [16](/docs/16/ddl-
rowsecurity.html "PostgreSQL 16 - 5.8. Row Security Policies") /
[15](/docs/15/ddl-rowsecurity.html "PostgreSQL 15 - 5.8. Row Security
Policies") / [14](/docs/14/ddl-rowsecurity.html "PostgreSQL 14 - 5.8. Row
Security Policies") / [13](/docs/13/ddl-rowsecurity.html "PostgreSQL 13 -
5.8. Row Security Policies")

Development Versions: [18](/docs/18/ddl-rowsecurity.html "PostgreSQL 18 -
5.8. Row Security Policies") / [devel](/docs/devel/ddl-rowsecurity.html
"PostgreSQL devel - 5.8. Row Security Policies")

Unsupported versions: [12](/docs/12/ddl-rowsecurity.html "PostgreSQL 12 -
5.8. Row Security Policies") / [11](/docs/11/ddl-rowsecurity.html "PostgreSQL
11 - 5.8. Row Security Policies") / [10](/docs/10/ddl-rowsecurity.html
"PostgreSQL 10 - 5.8. Row Security Policies") / [9.6](/docs/9.6/ddl-
rowsecurity.html "PostgreSQL 9.6 - 5.8. Row Security Policies") /
[9.5](/docs/9.5/ddl-rowsecurity.html "PostgreSQL 9.5 - 5.8. Row Security
Policies")

__

5.8. Row Security Policies  
---  
[Prev](ddl-priv.html "5.7. Privileges")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-schemas.html "5.9. Schemas")  
  
* * *

## 5.8. Row Security Policies #

In addition to the SQL-standard [privilege system](ddl-priv.html
"5.7. Privileges") available through [GRANT](sql-grant.html "GRANT"), tables
can have _row security policies_ that restrict, on a per-user basis, which
rows can be returned by normal queries or inserted, updated, or deleted by
data modification commands. This feature is also known as _Row-Level
Security_. By default, tables do not have any policies, so that if a user has
access privileges to a table according to the SQL privilege system, all rows
within it are equally available for querying or updating.

When row security is enabled on a table (with [ALTER TABLE ... ENABLE ROW
LEVEL SECURITY](sql-altertable.html "ALTER TABLE")), all normal access to the
table for selecting rows or modifying rows must be allowed by a row security
policy. (However, the table's owner is typically not subject to row security
policies.) If no policy exists for the table, a default-deny policy is used,
meaning that no rows are visible or can be modified. Operations that apply to
the whole table, such as `TRUNCATE` and `REFERENCES`, are not subject to row
security.

Row security policies can be specific to commands, or to roles, or to both. A
policy can be specified to apply to `ALL` commands, or to `SELECT`, `INSERT`,
`UPDATE`, or `DELETE`. Multiple roles can be assigned to a given policy, and
normal role membership and inheritance rules apply.

To specify which rows are visible or modifiable according to a policy, an
expression is required that returns a Boolean result. This expression will be
evaluated for each row prior to any conditions or functions coming from the
user's query. (The only exceptions to this rule are `leakproof` functions,
which are guaranteed to not leak information; the optimizer may choose to
apply such functions ahead of the row-security check.) Rows for which the
expression does not return `true` will not be processed. Separate expressions
may be specified to provide independent control over the rows which are
visible and the rows which are allowed to be modified. Policy expressions are
run as part of the query and with the privileges of the user running the
query, although security-definer functions can be used to access data not
available to the calling user.

Superusers and roles with the `BYPASSRLS` attribute always bypass the row
security system when accessing a table. Table owners normally bypass row
security as well, though a table owner can choose to be subject to row
security with [ALTER TABLE ... FORCE ROW LEVEL SECURITY](sql-altertable.html
"ALTER TABLE").

Enabling and disabling row security, as well as adding policies to a table, is
always the privilege of the table owner only.

Policies are created using the [CREATE POLICY](sql-createpolicy.html "CREATE
POLICY") command, altered using the [ALTER POLICY](sql-alterpolicy.html "ALTER
POLICY") command, and dropped using the [DROP POLICY](sql-droppolicy.html
"DROP POLICY") command. To enable and disable row security for a given table,
use the [ALTER TABLE](sql-altertable.html "ALTER TABLE") command.

Each policy has a name and multiple policies can be defined for a table. As
policies are table-specific, each policy for a table must have a unique name.
Different tables may have policies with the same name.

When multiple policies apply to a given query, they are combined using either
`OR` (for permissive policies, which are the default) or using `AND` (for
restrictive policies). This is similar to the rule that a given role has the
privileges of all roles that they are a member of. Permissive vs. restrictive
policies are discussed further below.

As a simple example, here is how to create a policy on the `account` relation
to allow only members of the `managers` role to access rows, and only rows of
their accounts:

    
    
    CREATE TABLE accounts (manager text, company text, contact_email text);
    
    ALTER TABLE accounts ENABLE ROW LEVEL SECURITY;
    
    CREATE POLICY account_managers ON accounts TO managers
        USING (manager = current_user);
    

The policy above implicitly provides a `WITH CHECK` clause identical to its
`USING` clause, so that the constraint applies both to rows selected by a
command (so a manager cannot `SELECT`, `UPDATE`, or `DELETE` existing rows
belonging to a different manager) and to rows modified by a command (so rows
belonging to a different manager cannot be created via `INSERT` or `UPDATE`).

If no role is specified, or the special user name `PUBLIC` is used, then the
policy applies to all users on the system. To allow all users to access only
their own row in a `users` table, a simple policy can be used:

    
    
    CREATE POLICY user_policy ON users
        USING (user_name = current_user);
    

This works similarly to the previous example.

To use a different policy for rows that are being added to the table compared
to those rows that are visible, multiple policies can be combined. This pair
of policies would allow all users to view all rows in the `users` table, but
only modify their own:

    
    
    CREATE POLICY user_sel_policy ON users
        FOR SELECT
        USING (true);
    CREATE POLICY user_mod_policy ON users
        USING (user_name = current_user);
    

In a `SELECT` command, these two policies are combined using `OR`, with the
net effect being that all rows can be selected. In other command types, only
the second policy applies, so that the effects are the same as before.

Row security can also be disabled with the `ALTER TABLE` command. Disabling
row security does not remove any policies that are defined on the table; they
are simply ignored. Then all rows in the table are visible and modifiable,
subject to the standard SQL privileges system.

Below is a larger example of how this feature can be used in production
environments. The table `passwd` emulates a Unix password file:

    
    
    -- Simple passwd-file based example
    CREATE TABLE passwd (
      user_name             text UNIQUE NOT NULL,
      pwhash                text,
      uid                   int  PRIMARY KEY,
      gid                   int  NOT NULL,
      real_name             text NOT NULL,
      home_phone            text,
      extra_info            text,
      home_dir              text NOT NULL,
      shell                 text NOT NULL
    );
    
    CREATE ROLE admin;  -- Administrator
    CREATE ROLE bob;    -- Normal user
    CREATE ROLE alice;  -- Normal user
    
    -- Populate the table
    INSERT INTO passwd VALUES
      ('admin','xxx',0,0,'Admin','111-222-3333',null,'/root','/bin/dash');
    INSERT INTO passwd VALUES
      ('bob','xxx',1,1,'Bob','123-456-7890',null,'/home/bob','/bin/zsh');
    INSERT INTO passwd VALUES
      ('alice','xxx',2,1,'Alice','098-765-4321',null,'/home/alice','/bin/zsh');
    
    -- Be sure to enable row-level security on the table
    ALTER TABLE passwd ENABLE ROW LEVEL SECURITY;
    
    -- Create policies
    -- Administrator can see all rows and add any rows
    CREATE POLICY admin_all ON passwd TO admin USING (true) WITH CHECK (true);
    -- Normal users can view all rows
    CREATE POLICY all_view ON passwd FOR SELECT USING (true);
    -- Normal users can update their own records, but
    -- limit which shells a normal user is allowed to set
    CREATE POLICY user_mod ON passwd FOR UPDATE
      USING (current_user = user_name)
      WITH CHECK (
        current_user = user_name AND
        shell IN ('/bin/bash','/bin/sh','/bin/dash','/bin/zsh','/bin/tcsh')
      );
    
    -- Allow admin all normal rights
    GRANT SELECT, INSERT, UPDATE, DELETE ON passwd TO admin;
    -- Users only get select access on public columns
    GRANT SELECT
      (user_name, uid, gid, real_name, home_phone, extra_info, home_dir, shell)
      ON passwd TO public;
    -- Allow users to update certain columns
    GRANT UPDATE
      (pwhash, real_name, home_phone, extra_info, shell)
      ON passwd TO public;
    

As with any security settings, it's important to test and ensure that the
system is behaving as expected. Using the example above, this demonstrates
that the permission system is working properly.

    
    
    -- admin can view all rows and fields
    postgres=> set role admin;
    SET
    postgres=> table passwd;
     user_name | pwhash | uid | gid | real_name |  home_phone  | extra_info | home_dir    |   shell
    -----------+--------+-----+-----+-----------+--------------+------------+-------------+-----------
     admin     | xxx    |   0 |   0 | Admin     | 111-222-3333 |            | /root       | /bin/dash
     bob       | xxx    |   1 |   1 | Bob       | 123-456-7890 |            | /home/bob   | /bin/zsh
     alice     | xxx    |   2 |   1 | Alice     | 098-765-4321 |            | /home/alice | /bin/zsh
    (3 rows)
    
    -- Test what Alice is able to do
    postgres=> set role alice;
    SET
    postgres=> table passwd;
    ERROR:  permission denied for table passwd
    postgres=> select user_name,real_name,home_phone,extra_info,home_dir,shell from passwd;
     user_name | real_name |  home_phone  | extra_info | home_dir    |   shell
    -----------+-----------+--------------+------------+-------------+-----------
     admin     | Admin     | 111-222-3333 |            | /root       | /bin/dash
     bob       | Bob       | 123-456-7890 |            | /home/bob   | /bin/zsh
     alice     | Alice     | 098-765-4321 |            | /home/alice | /bin/zsh
    (3 rows)
    
    postgres=> update passwd set user_name = 'joe';
    ERROR:  permission denied for table passwd
    -- Alice is allowed to change her own real_name, but no others
    postgres=> update passwd set real_name = 'Alice Doe';
    UPDATE 1
    postgres=> update passwd set real_name = 'John Doe' where user_name = 'admin';
    UPDATE 0
    postgres=> update passwd set shell = '/bin/xx';
    ERROR:  new row violates WITH CHECK OPTION for "passwd"
    postgres=> delete from passwd;
    ERROR:  permission denied for table passwd
    postgres=> insert into passwd (user_name) values ('xxx');
    ERROR:  permission denied for table passwd
    -- Alice can change her own password; RLS silently prevents updating other rows
    postgres=> update passwd set pwhash = 'abc';
    UPDATE 1
    

All of the policies constructed thus far have been permissive policies,
meaning that when multiple policies are applied they are combined using the
“OR” Boolean operator. While permissive policies can be constructed to only
allow access to rows in the intended cases, it can be simpler to combine
permissive policies with restrictive policies (which the records must pass and
which are combined using the “AND” Boolean operator). Building on the example
above, we add a restrictive policy to require the administrator to be
connected over a local Unix socket to access the records of the `passwd`
table:

    
    
    CREATE POLICY admin_local_only ON passwd AS RESTRICTIVE TO admin
        USING (pg_catalog.inet_client_addr() IS NULL);
    

We can then see that an administrator connecting over a network will not see
any records, due to the restrictive policy:

    
    
    => SELECT current_user;
     current_user
    --------------
     admin
    (1 row)
    
    => select inet_client_addr();
     inet_client_addr
    ------------------
     127.0.0.1
    (1 row)
    
    => TABLE passwd;
     user_name | pwhash | uid | gid | real_name | home_phone | extra_info | home_dir | shell
    -----------+--------+-----+-----+-----------+------------+------------+----------+-------
    (0 rows)
    
    => UPDATE passwd set pwhash = NULL;
    UPDATE 0
    

Referential integrity checks, such as unique or primary key constraints and
foreign key references, always bypass row security to ensure that data
integrity is maintained. Care must be taken when developing schemas and row
level policies to avoid “covert channel” leaks of information through such
referential integrity checks.

In some contexts it is important to be sure that row security is not being
applied. For example, when taking a backup, it could be disastrous if row
security silently caused some rows to be omitted from the backup. In such a
situation, you can set the [row_security](runtime-config-client.html#GUC-ROW-
SECURITY) configuration parameter to `off`. This does not in itself bypass row
security; what it does is throw an error if any query's results would get
filtered by a policy. The reason for the error can then be investigated and
fixed.

In the examples above, the policy expressions consider only the current values
in the row to be accessed or updated. This is the simplest and best-performing
case; when possible, it's best to design row security applications to work
this way. If it is necessary to consult other rows or other tables to make a
policy decision, that can be accomplished using sub-`SELECT`s, or functions
that contain `SELECT`s, in the policy expressions. Be aware however that such
accesses can create race conditions that could allow information leakage if
care is not taken. As an example, consider the following table design:

    
    
    -- definition of privilege groups
    CREATE TABLE groups (group_id int PRIMARY KEY,
                         group_name text NOT NULL);
    
    INSERT INTO groups VALUES
      (1, 'low'),
      (2, 'medium'),
      (5, 'high');
    
    GRANT ALL ON groups TO alice;  -- alice is the administrator
    GRANT SELECT ON groups TO public;
    
    -- definition of users' privilege levels
    CREATE TABLE users (user_name text PRIMARY KEY,
                        group_id int NOT NULL REFERENCES groups);
    
    INSERT INTO users VALUES
      ('alice', 5),
      ('bob', 2),
      ('mallory', 2);
    
    GRANT ALL ON users TO alice;
    GRANT SELECT ON users TO public;
    
    -- table holding the information to be protected
    CREATE TABLE information (info text,
                              group_id int NOT NULL REFERENCES groups);
    
    INSERT INTO information VALUES
      ('barely secret', 1),
      ('slightly secret', 2),
      ('very secret', 5);
    
    ALTER TABLE information ENABLE ROW LEVEL SECURITY;
    
    -- a row should be visible to/updatable by users whose security group_id is
    -- greater than or equal to the row's group_id
    CREATE POLICY fp_s ON information FOR SELECT
      USING (group_id <= (SELECT group_id FROM users WHERE user_name = current_user));
    CREATE POLICY fp_u ON information FOR UPDATE
      USING (group_id <= (SELECT group_id FROM users WHERE user_name = current_user));
    
    -- we rely only on RLS to protect the information table
    GRANT ALL ON information TO public;
    

Now suppose that `alice` wishes to change the “slightly secret” information,
but decides that `mallory` should not be trusted with the new content of that
row, so she does:

    
    
    BEGIN;
    UPDATE users SET group_id = 1 WHERE user_name = 'mallory';
    UPDATE information SET info = 'secret from mallory' WHERE group_id = 2;
    COMMIT;
    

That looks safe; there is no window wherein `mallory` should be able to see
the “secret from mallory” string. However, there is a race condition here. If
`mallory` is concurrently doing, say,

    
    
    SELECT * FROM information WHERE group_id = 2 FOR UPDATE;
    

and her transaction is in `READ COMMITTED` mode, it is possible for her to see
“secret from mallory”. That happens if her transaction reaches the
`information` row just after `alice`'s does. It blocks waiting for `alice`'s
transaction to commit, then fetches the updated row contents thanks to the
`FOR UPDATE` clause. However, it does _not_ fetch an updated row for the
implicit `SELECT` from `users`, because that sub-`SELECT` did not have `FOR
UPDATE`; instead the `users` row is read with the snapshot taken at the start
of the query. Therefore, the policy expression tests the old value of
`mallory`'s privilege level and allows her to see the updated row.

There are several ways around this problem. One simple answer is to use
`SELECT ... FOR SHARE` in sub-`SELECT`s in row security policies. However,
that requires granting `UPDATE` privilege on the referenced table (here
`users`) to the affected users, which might be undesirable. (But another row
security policy could be applied to prevent them from actually exercising that
privilege; or the sub-`SELECT` could be embedded into a security definer
function.) Also, heavy concurrent use of row share locks on the referenced
table could pose a performance problem, especially if updates of it are
frequent. Another solution, practical if updates of the referenced table are
infrequent, is to take an `ACCESS EXCLUSIVE` lock on the referenced table when
updating it, so that no concurrent transactions could be examining old row
values. Or one could just wait for all concurrent transactions to end after
committing an update of the referenced table and before making changes that
rely on the new security situation.

For additional details see [CREATE POLICY](sql-createpolicy.html "CREATE
POLICY") and [ALTER TABLE](sql-altertable.html "ALTER TABLE").

* * *

[Prev](ddl-priv.html "5.7. Privileges")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-schemas.html "5.9. Schemas")  
---|---|---  
5.7. Privileges  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.9. Schemas  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-rowsecurity.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

