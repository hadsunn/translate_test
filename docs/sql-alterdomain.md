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

Supported Versions: [Current](/docs/current/sql-alterdomain.html "PostgreSQL
17 - ALTER DOMAIN") ([17](/docs/17/sql-alterdomain.html "PostgreSQL 17 - ALTER
DOMAIN")) / [16](/docs/16/sql-alterdomain.html "PostgreSQL 16 - ALTER DOMAIN")
/ [15](/docs/15/sql-alterdomain.html "PostgreSQL 15 - ALTER DOMAIN") /
[14](/docs/14/sql-alterdomain.html "PostgreSQL 14 - ALTER DOMAIN") /
[13](/docs/13/sql-alterdomain.html "PostgreSQL 13 - ALTER DOMAIN")

Development Versions: [18](/docs/18/sql-alterdomain.html "PostgreSQL 18 -
ALTER DOMAIN") / [devel](/docs/devel/sql-alterdomain.html "PostgreSQL devel -
ALTER DOMAIN")

Unsupported versions: [12](/docs/12/sql-alterdomain.html "PostgreSQL 12 -
ALTER DOMAIN") / [11](/docs/11/sql-alterdomain.html "PostgreSQL 11 - ALTER
DOMAIN") / [10](/docs/10/sql-alterdomain.html "PostgreSQL 10 - ALTER DOMAIN")
/ [9.6](/docs/9.6/sql-alterdomain.html "PostgreSQL 9.6 - ALTER DOMAIN") /
[9.5](/docs/9.5/sql-alterdomain.html "PostgreSQL 9.5 - ALTER DOMAIN") /
[9.4](/docs/9.4/sql-alterdomain.html "PostgreSQL 9.4 - ALTER DOMAIN") /
[9.3](/docs/9.3/sql-alterdomain.html "PostgreSQL 9.3 - ALTER DOMAIN") /
[9.2](/docs/9.2/sql-alterdomain.html "PostgreSQL 9.2 - ALTER DOMAIN") /
[9.1](/docs/9.1/sql-alterdomain.html "PostgreSQL 9.1 - ALTER DOMAIN") /
[9.0](/docs/9.0/sql-alterdomain.html "PostgreSQL 9.0 - ALTER DOMAIN") /
[8.4](/docs/8.4/sql-alterdomain.html "PostgreSQL 8.4 - ALTER DOMAIN") /
[8.3](/docs/8.3/sql-alterdomain.html "PostgreSQL 8.3 - ALTER DOMAIN") /
[8.2](/docs/8.2/sql-alterdomain.html "PostgreSQL 8.2 - ALTER DOMAIN") /
[8.1](/docs/8.1/sql-alterdomain.html "PostgreSQL 8.1 - ALTER DOMAIN") /
[8.0](/docs/8.0/sql-alterdomain.html "PostgreSQL 8.0 - ALTER DOMAIN") /
[7.4](/docs/7.4/sql-alterdomain.html "PostgreSQL 7.4 - ALTER DOMAIN")

__

ALTER DOMAIN  
---  
[Prev](sql-alterdefaultprivileges.html "ALTER DEFAULT PRIVILEGES")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altereventtrigger.html "ALTER EVENT TRIGGER")  
  
* * *

## ALTER DOMAIN

ALTER DOMAIN — change the definition of a domain

## Synopsis

    
    
    ALTER DOMAIN _name_
        { SET DEFAULT _expression_ | DROP DEFAULT }
    ALTER DOMAIN _name_
        { SET | DROP } NOT NULL
    ALTER DOMAIN _name_
        ADD _domain_constraint_ [ NOT VALID ]
    ALTER DOMAIN _name_
        DROP CONSTRAINT [ IF EXISTS ] _constraint_name_ [ RESTRICT | CASCADE ]
    ALTER DOMAIN _name_
         RENAME CONSTRAINT _constraint_name_ TO _new_constraint_name_
    ALTER DOMAIN _name_
        VALIDATE CONSTRAINT _constraint_name_
    ALTER DOMAIN _name_
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER DOMAIN _name_
        RENAME TO _new_name_
    ALTER DOMAIN _name_
        SET SCHEMA _new_schema_
    
    where _domain_constraint_ is:
    
    [ CONSTRAINT _constraint_name_ ]
    { NOT NULL | CHECK (_expression_) }
    

## Description

`ALTER DOMAIN` changes the definition of an existing domain. There are several
sub-forms:

`SET`/`DROP DEFAULT`

    

These forms set or remove the default value for a domain. Note that defaults
only apply to subsequent `INSERT` commands; they do not affect rows already in
a table using the domain.

`SET`/`DROP NOT NULL`

    

These forms change whether a domain is marked to allow NULL values or to
reject NULL values. You can only `SET NOT NULL` when the columns using the
domain contain no null values.

`ADD _`domain_constraint`_ [ NOT VALID ]`

    

This form adds a new constraint to a domain. When a new constraint is added to
a domain, all columns using that domain will be checked against the newly
added constraint. These checks can be suppressed by adding the new constraint
using the `NOT VALID` option; the constraint can later be made valid using
`ALTER DOMAIN ... VALIDATE CONSTRAINT`. Newly inserted or updated rows are
always checked against all constraints, even those marked `NOT VALID`. `NOT
VALID` is only accepted for `CHECK` constraints.

`DROP CONSTRAINT [ IF EXISTS ]`

    

This form drops constraints on a domain. If `IF EXISTS` is specified and the
constraint does not exist, no error is thrown. In this case a notice is issued
instead.

`RENAME CONSTRAINT`

    

This form changes the name of a constraint on a domain.

`VALIDATE CONSTRAINT`

    

This form validates a constraint previously added as `NOT VALID`, that is, it
verifies that all values in table columns of the domain type satisfy the
specified constraint.

`OWNER`

    

This form changes the owner of the domain to the specified user.

`RENAME`

    

This form changes the name of the domain.

`SET SCHEMA`

    

This form changes the schema of the domain. Any constraints associated with
the domain are moved into the new schema as well.

You must own the domain to use `ALTER DOMAIN`. To change the schema of a
domain, you must also have `CREATE` privilege on the new schema. To alter the
owner, you must be able to `SET ROLE` to the new owning role, and that role
must have `CREATE` privilege on the domain's schema. (These restrictions
enforce that altering the owner doesn't do anything you couldn't do by
dropping and recreating the domain. However, a superuser can alter ownership
of any domain anyway.)

## Parameters

_`name`_

    

The name (possibly schema-qualified) of an existing domain to alter.

_`domain_constraint`_

    

New domain constraint for the domain.

_`constraint_name`_

    

Name of an existing constraint to drop or rename.

`NOT VALID`

    

Do not verify existing stored data for constraint validity.

`CASCADE`

    

Automatically drop objects that depend on the constraint, and in turn all
objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the constraint if there are any dependent objects. This is the
default behavior.

_`new_name`_

    

The new name for the domain.

_`new_constraint_name`_

    

The new name for the constraint.

_`new_owner`_

    

The user name of the new owner of the domain.

_`new_schema`_

    

The new schema for the domain.

## Notes

Although `ALTER DOMAIN ADD CONSTRAINT` attempts to verify that existing stored
data satisfies the new constraint, this check is not bulletproof, because the
command cannot “see” table rows that are newly inserted or updated and not yet
committed. If there is a hazard that concurrent operations might insert bad
data, the way to proceed is to add the constraint using the `NOT VALID`
option, commit that command, wait until all transactions started before that
commit have finished, and then issue `ALTER DOMAIN VALIDATE CONSTRAINT` to
search for data violating the constraint. This method is reliable because once
the constraint is committed, all new transactions are guaranteed to enforce it
against new values of the domain type.

Currently, `ALTER DOMAIN ADD CONSTRAINT`, `ALTER DOMAIN VALIDATE CONSTRAINT`,
and `ALTER DOMAIN SET NOT NULL` will fail if the named domain or any derived
domain is used within a container-type column (a composite, array, or range
column) in any table in the database. They should eventually be improved to be
able to verify the new constraint for such nested values.

## Examples

To add a `NOT NULL` constraint to a domain:

    
    
    ALTER DOMAIN zipcode SET NOT NULL;
    

To remove a `NOT NULL` constraint from a domain:

    
    
    ALTER DOMAIN zipcode DROP NOT NULL;
    

To add a check constraint to a domain:

    
    
    ALTER DOMAIN zipcode ADD CONSTRAINT zipchk CHECK (char_length(VALUE) = 5);
    

To remove a check constraint from a domain:

    
    
    ALTER DOMAIN zipcode DROP CONSTRAINT zipchk;
    

To rename a check constraint on a domain:

    
    
    ALTER DOMAIN zipcode RENAME CONSTRAINT zipchk TO zip_check;
    

To move the domain into a different schema:

    
    
    ALTER DOMAIN zipcode SET SCHEMA customers;
    

## Compatibility

`ALTER DOMAIN` conforms to the SQL standard, except for the `OWNER`, `RENAME`,
`SET SCHEMA`, and `VALIDATE CONSTRAINT` variants, which are PostgreSQL
extensions. The `NOT VALID` clause of the `ADD CONSTRAINT` variant is also a
PostgreSQL extension.

## See Also

[CREATE DOMAIN](sql-createdomain.html "CREATE DOMAIN"), [DROP DOMAIN](sql-
dropdomain.html "DROP DOMAIN")

* * *

[Prev](sql-alterdefaultprivileges.html "ALTER DEFAULT PRIVILEGES")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altereventtrigger.html "ALTER EVENT TRIGGER")  
---|---|---  
ALTER DEFAULT PRIVILEGES  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER EVENT TRIGGER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterdomain.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

