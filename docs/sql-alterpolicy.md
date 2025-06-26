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

Supported Versions: [Current](/docs/current/sql-alterpolicy.html "PostgreSQL
17 - ALTER POLICY") ([17](/docs/17/sql-alterpolicy.html "PostgreSQL 17 - ALTER
POLICY")) / [16](/docs/16/sql-alterpolicy.html "PostgreSQL 16 - ALTER POLICY")
/ [15](/docs/15/sql-alterpolicy.html "PostgreSQL 15 - ALTER POLICY") /
[14](/docs/14/sql-alterpolicy.html "PostgreSQL 14 - ALTER POLICY") /
[13](/docs/13/sql-alterpolicy.html "PostgreSQL 13 - ALTER POLICY")

Development Versions: [18](/docs/18/sql-alterpolicy.html "PostgreSQL 18 -
ALTER POLICY") / [devel](/docs/devel/sql-alterpolicy.html "PostgreSQL devel -
ALTER POLICY")

Unsupported versions: [12](/docs/12/sql-alterpolicy.html "PostgreSQL 12 -
ALTER POLICY") / [11](/docs/11/sql-alterpolicy.html "PostgreSQL 11 - ALTER
POLICY") / [10](/docs/10/sql-alterpolicy.html "PostgreSQL 10 - ALTER POLICY")
/ [9.6](/docs/9.6/sql-alterpolicy.html "PostgreSQL 9.6 - ALTER POLICY") /
[9.5](/docs/9.5/sql-alterpolicy.html "PostgreSQL 9.5 - ALTER POLICY")

__

ALTER POLICY  
---  
[Prev](sql-alteropfamily.html "ALTER OPERATOR FAMILY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterprocedure.html "ALTER PROCEDURE")  
  
* * *

## ALTER POLICY

ALTER POLICY — change the definition of a row-level security policy

## Synopsis

    
    
    ALTER POLICY _name_ ON _table_name_ RENAME TO _new_name_
    
    ALTER POLICY _name_ ON _table_name_
        [ TO { _role_name_ | PUBLIC | CURRENT_ROLE | CURRENT_USER | SESSION_USER } [, ...] ]
        [ USING ( _using_expression_ ) ]
        [ WITH CHECK ( _check_expression_ ) ]
    

## Description

`ALTER POLICY` changes the definition of an existing row-level security
policy. Note that `ALTER POLICY` only allows the set of roles to which the
policy applies and the `USING` and `WITH CHECK` expressions to be modified. To
change other properties of a policy, such as the command to which it applies
or whether it is permissive or restrictive, the policy must be dropped and
recreated.

To use `ALTER POLICY`, you must own the table that the policy applies to.

In the second form of `ALTER POLICY`, the role list, _`using_expression`_ ,
and _`check_expression`_ are replaced independently if specified. When one of
those clauses is omitted, the corresponding part of the policy is unchanged.

## Parameters

_`name`_

    

The name of an existing policy to alter.

_`table_name`_

    

The name (optionally schema-qualified) of the table that the policy is on.

_`new_name`_

    

The new name for the policy.

_`role_name`_

    

The role(s) to which the policy applies. Multiple roles can be specified at
one time. To apply the policy to all roles, use `PUBLIC`.

_`using_expression`_

    

The `USING` expression for the policy. See [CREATE POLICY](sql-
createpolicy.html "CREATE POLICY") for details.

_`check_expression`_

    

The `WITH CHECK` expression for the policy. See [CREATE POLICY](sql-
createpolicy.html "CREATE POLICY") for details.

## Compatibility

`ALTER POLICY` is a PostgreSQL extension.

## See Also

[CREATE POLICY](sql-createpolicy.html "CREATE POLICY"), [DROP POLICY](sql-
droppolicy.html "DROP POLICY")

* * *

[Prev](sql-alteropfamily.html "ALTER OPERATOR FAMILY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterprocedure.html "ALTER PROCEDURE")  
---|---|---  
ALTER OPERATOR FAMILY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER PROCEDURE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterpolicy.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

