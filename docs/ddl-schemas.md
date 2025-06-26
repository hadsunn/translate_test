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

Supported Versions: [Current](/docs/current/ddl-schemas.html "PostgreSQL 17 -
5.9. Schemas") ([17](/docs/17/ddl-schemas.html "PostgreSQL 17 -
5.9. Schemas")) / [16](/docs/16/ddl-schemas.html "PostgreSQL 16 -
5.9. Schemas") / [15](/docs/15/ddl-schemas.html "PostgreSQL 15 -
5.9. Schemas") / [14](/docs/14/ddl-schemas.html "PostgreSQL 14 -
5.9. Schemas") / [13](/docs/13/ddl-schemas.html "PostgreSQL 13 -
5.9. Schemas")

Development Versions: [18](/docs/18/ddl-schemas.html "PostgreSQL 18 -
5.9. Schemas") / [devel](/docs/devel/ddl-schemas.html "PostgreSQL devel -
5.9. Schemas")

Unsupported versions: [12](/docs/12/ddl-schemas.html "PostgreSQL 12 -
5.9. Schemas") / [11](/docs/11/ddl-schemas.html "PostgreSQL 11 -
5.9. Schemas") / [10](/docs/10/ddl-schemas.html "PostgreSQL 10 -
5.9. Schemas") / [9.6](/docs/9.6/ddl-schemas.html "PostgreSQL 9.6 -
5.9. Schemas") / [9.5](/docs/9.5/ddl-schemas.html "PostgreSQL 9.5 -
5.9. Schemas") / [9.4](/docs/9.4/ddl-schemas.html "PostgreSQL 9.4 -
5.9. Schemas") / [9.3](/docs/9.3/ddl-schemas.html "PostgreSQL 9.3 -
5.9. Schemas") / [9.2](/docs/9.2/ddl-schemas.html "PostgreSQL 9.2 -
5.9. Schemas") / [9.1](/docs/9.1/ddl-schemas.html "PostgreSQL 9.1 -
5.9. Schemas") / [9.0](/docs/9.0/ddl-schemas.html "PostgreSQL 9.0 -
5.9. Schemas") / [8.4](/docs/8.4/ddl-schemas.html "PostgreSQL 8.4 -
5.9. Schemas") / [8.3](/docs/8.3/ddl-schemas.html "PostgreSQL 8.3 -
5.9. Schemas") / [8.2](/docs/8.2/ddl-schemas.html "PostgreSQL 8.2 -
5.9. Schemas") / [8.1](/docs/8.1/ddl-schemas.html "PostgreSQL 8.1 -
5.9. Schemas") / [8.0](/docs/8.0/ddl-schemas.html "PostgreSQL 8.0 -
5.9. Schemas") / [7.4](/docs/7.4/ddl-schemas.html "PostgreSQL 7.4 -
5.9. Schemas") / [7.3](/docs/7.3/ddl-schemas.html "PostgreSQL 7.3 -
5.9. Schemas")

__

5.9. Schemas  
---  
[Prev](ddl-rowsecurity.html "5.8. Row Security Policies")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-inherit.html "5.10. Inheritance")  
  
* * *

## 5.9. Schemas #

[5.9.1. Creating a Schema](ddl-schemas.html#DDL-SCHEMAS-CREATE)

[5.9.2. The Public Schema](ddl-schemas.html#DDL-SCHEMAS-PUBLIC)

[5.9.3. The Schema Search Path](ddl-schemas.html#DDL-SCHEMAS-PATH)

[5.9.4. Schemas and Privileges](ddl-schemas.html#DDL-SCHEMAS-PRIV)

[5.9.5. The System Catalog Schema](ddl-schemas.html#DDL-SCHEMAS-CATALOG)

[5.9.6. Usage Patterns](ddl-schemas.html#DDL-SCHEMAS-PATTERNS)

[5.9.7. Portability](ddl-schemas.html#DDL-SCHEMAS-PORTABILITY)

A PostgreSQL database cluster contains one or more named databases. Roles and
a few other object types are shared across the entire cluster. A client
connection to the server can only access data in a single database, the one
specified in the connection request.

### Note

Users of a cluster do not necessarily have the privilege to access every
database in the cluster. Sharing of role names means that there cannot be
different roles named, say, `joe` in two databases in the same cluster; but
the system can be configured to allow `joe` access to only some of the
databases.

A database contains one or more named _schemas_ , which in turn contain
tables. Schemas also contain other kinds of named objects, including data
types, functions, and operators. The same object name can be used in different
schemas without conflict; for example, both `schema1` and `myschema` can
contain tables named `mytable`. Unlike databases, schemas are not rigidly
separated: a user can access objects in any of the schemas in the database
they are connected to, if they have privileges to do so.

There are several reasons why one might want to use schemas:

  * To allow many users to use one database without interfering with each other.

  * To organize database objects into logical groups to make them more manageable.

  * Third-party applications can be put into separate schemas so they do not collide with the names of other objects.

Schemas are analogous to directories at the operating system level, except
that schemas cannot be nested.

### 5.9.1. Creating a Schema #

To create a schema, use the [CREATE SCHEMA](sql-createschema.html "CREATE
SCHEMA") command. Give the schema a name of your choice. For example:

    
    
    CREATE SCHEMA myschema;
    

To create or access objects in a schema, write a _qualified name_ consisting
of the schema name and table name separated by a dot:

    
    
    _schema_._table_
    

This works anywhere a table name is expected, including the table modification
commands and the data access commands discussed in the following chapters.
(For brevity we will speak of tables only, but the same ideas apply to other
kinds of named objects, such as types and functions.)

Actually, the even more general syntax

    
    
    _database_._schema_._table_
    

can be used too, but at present this is just for pro forma compliance with the
SQL standard. If you write a database name, it must be the same as the
database you are connected to.

So to create a table in the new schema, use:

    
    
    CREATE TABLE myschema.mytable (
     ...
    );
    

To drop a schema if it's empty (all objects in it have been dropped), use:

    
    
    DROP SCHEMA myschema;
    

To drop a schema including all contained objects, use:

    
    
    DROP SCHEMA myschema CASCADE;
    

See [Section 5.14](ddl-depend.html "5.14. Dependency Tracking") for a
description of the general mechanism behind this.

Often you will want to create a schema owned by someone else (since this is
one of the ways to restrict the activities of your users to well-defined
namespaces). The syntax for that is:

    
    
    CREATE SCHEMA _schema_name_ AUTHORIZATION _user_name_ ;
    

You can even omit the schema name, in which case the schema name will be the
same as the user name. See [Section 5.9.6](ddl-schemas.html#DDL-SCHEMAS-
PATTERNS "5.9.6. Usage Patterns") for how this can be useful.

Schema names beginning with `pg_` are reserved for system purposes and cannot
be created by users.

### 5.9.2. The Public Schema #

In the previous sections we created tables without specifying any schema
names. By default such tables (and other objects) are automatically put into a
schema named “public”. Every new database contains such a schema. Thus, the
following are equivalent:

    
    
    CREATE TABLE products ( ... );
    

and:

    
    
    CREATE TABLE public.products ( ... );
    

### 5.9.3. The Schema Search Path #

Qualified names are tedious to write, and it's often best not to wire a
particular schema name into applications anyway. Therefore tables are often
referred to by _unqualified names_ , which consist of just the table name. The
system determines which table is meant by following a _search path_ , which is
a list of schemas to look in. The first matching table in the search path is
taken to be the one wanted. If there is no match in the search path, an error
is reported, even if matching table names exist in other schemas in the
database.

The ability to create like-named objects in different schemas complicates
writing a query that references precisely the same objects every time. It also
opens up the potential for users to change the behavior of other users'
queries, maliciously or accidentally. Due to the prevalence of unqualified
names in queries and their use in PostgreSQL internals, adding a schema to
`search_path` effectively trusts all users having `CREATE` privilege on that
schema. When you run an ordinary query, a malicious user able to create
objects in a schema of your search path can take control and execute arbitrary
SQL functions as though you executed them.

The first schema named in the search path is called the current schema. Aside
from being the first schema searched, it is also the schema in which new
tables will be created if the `CREATE TABLE` command does not specify a schema
name.

To show the current search path, use the following command:

    
    
    SHOW search_path;
    

In the default setup this returns:

    
    
     search_path
    --------------
     "$user", public
    

The first element specifies that a schema with the same name as the current
user is to be searched. If no such schema exists, the entry is ignored. The
second element refers to the public schema that we have seen already.

The first schema in the search path that exists is the default location for
creating new objects. That is the reason that by default objects are created
in the public schema. When objects are referenced in any other context without
schema qualification (table modification, data modification, or query
commands) the search path is traversed until a matching object is found.
Therefore, in the default configuration, any unqualified access again can only
refer to the public schema.

To put our new schema in the path, we use:

    
    
    SET search_path TO myschema,public;
    

(We omit the `$user` here because we have no immediate need for it.) And then
we can access the table without schema qualification:

    
    
    DROP TABLE mytable;
    

Also, since `myschema` is the first element in the path, new objects would by
default be created in it.

We could also have written:

    
    
    SET search_path TO myschema;
    

Then we no longer have access to the public schema without explicit
qualification. There is nothing special about the public schema except that it
exists by default. It can be dropped, too.

See also [Section 9.26](functions-info.html "9.26. System Information
Functions and Operators") for other ways to manipulate the schema search path.

The search path works in the same way for data type names, function names, and
operator names as it does for table names. Data type and function names can be
qualified in exactly the same way as table names. If you need to write a
qualified operator name in an expression, there is a special provision: you
must write

    
    
    OPERATOR(_schema_._operator_)
    

This is needed to avoid syntactic ambiguity. An example is:

    
    
    SELECT 3 OPERATOR(pg_catalog.+) 4;
    

In practice one usually relies on the search path for operators, so as not to
have to write anything so ugly as that.

### 5.9.4. Schemas and Privileges #

By default, users cannot access any objects in schemas they do not own. To
allow that, the owner of the schema must grant the `USAGE` privilege on the
schema. By default, everyone has that privilege on the schema `public`. To
allow users to make use of the objects in a schema, additional privileges
might need to be granted, as appropriate for the object.

A user can also be allowed to create objects in someone else's schema. To
allow that, the `CREATE` privilege on the schema needs to be granted. In
databases upgraded from PostgreSQL 14 or earlier, everyone has that privilege
on the schema `public`. Some [usage patterns](ddl-schemas.html#DDL-SCHEMAS-
PATTERNS "5.9.6. Usage Patterns") call for revoking that privilege:

    
    
    REVOKE CREATE ON SCHEMA public FROM PUBLIC;
    

(The first “public” is the schema, the second “public” means “every user”. In
the first sense it is an identifier, in the second sense it is a key word,
hence the different capitalization; recall the guidelines from [Section
4.1.1](sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS "4.1.1. Identifiers and
Key Words").)

### 5.9.5. The System Catalog Schema #

In addition to `public` and user-created schemas, each database contains a
`pg_catalog` schema, which contains the system tables and all the built-in
data types, functions, and operators. `pg_catalog` is always effectively part
of the search path. If it is not named explicitly in the path then it is
implicitly searched _before_ searching the path's schemas. This ensures that
built-in names will always be findable. However, you can explicitly place
`pg_catalog` at the end of your search path if you prefer to have user-defined
names override built-in names.

Since system table names begin with `pg_`, it is best to avoid such names to
ensure that you won't suffer a conflict if some future version defines a
system table named the same as your table. (With the default search path, an
unqualified reference to your table name would then be resolved as the system
table instead.) System tables will continue to follow the convention of having
names beginning with `pg_`, so that they will not conflict with unqualified
user-table names so long as users avoid the `pg_` prefix.

### 5.9.6. Usage Patterns #

Schemas can be used to organize your data in many ways. A _secure schema usage
pattern_ prevents untrusted users from changing the behavior of other users'
queries. When a database does not use a secure schema usage pattern, users
wishing to securely query that database would take protective action at the
beginning of each session. Specifically, they would begin each session by
setting `search_path` to the empty string or otherwise removing schemas that
are writable by non-superusers from `search_path`. There are a few usage
patterns easily supported by the default configuration:

  * Constrain ordinary users to user-private schemas. To implement this pattern, first ensure that no schemas have public `CREATE` privileges. Then, for every user needing to create non-temporary objects, create a schema with the same name as that user, for example `CREATE SCHEMA alice AUTHORIZATION alice`. (Recall that the default search path starts with `$user`, which resolves to the user name. Therefore, if each user has a separate schema, they access their own schemas by default.) This pattern is a secure schema usage pattern unless an untrusted user is the database owner or has been granted `ADMIN OPTION` on a relevant role, in which case no secure schema usage pattern exists.

In PostgreSQL 15 and later, the default configuration supports this usage
pattern. In prior versions, or when using a database that has been upgraded
from a prior version, you will need to remove the public `CREATE` privilege
from the `public` schema (issue `REVOKE CREATE ON SCHEMA public FROM PUBLIC`).
Then consider auditing the `public` schema for objects named like objects in
schema `pg_catalog`.

  * Remove the public schema from the default search path, by modifying [`postgresql.conf`](config-setting.html#CONFIG-SETTING-CONFIGURATION-FILE "20.1.2. Parameter Interaction via the Configuration File") or by issuing `ALTER ROLE ALL SET search_path = "$user"`. Then, grant privileges to create in the public schema. Only qualified names will choose public schema objects. While qualified table references are fine, calls to functions in the public schema [will be unsafe or unreliable](typeconv-func.html "10.3. Functions"). If you create functions or extensions in the public schema, use the first pattern instead. Otherwise, like the first pattern, this is secure unless an untrusted user is the database owner or has been granted `ADMIN OPTION` on a relevant role.

  * Keep the default search path, and grant privileges to create in the public schema. All users access the public schema implicitly. This simulates the situation where schemas are not available at all, giving a smooth transition from the non-schema-aware world. However, this is never a secure pattern. It is acceptable only when the database has a single user or a few mutually-trusting users. In databases upgraded from PostgreSQL 14 or earlier, this is the default.

For any pattern, to install shared applications (tables to be used by
everyone, additional functions provided by third parties, etc.), put them into
separate schemas. Remember to grant appropriate privileges to allow the other
users to access them. Users can then refer to these additional objects by
qualifying the names with a schema name, or they can put the additional
schemas into their search path, as they choose.

### 5.9.7. Portability #

In the SQL standard, the notion of objects in the same schema being owned by
different users does not exist. Moreover, some implementations do not allow
you to create schemas that have a different name than their owner. In fact,
the concepts of schema and user are nearly equivalent in a database system
that implements only the basic schema support specified in the standard.
Therefore, many users consider qualified names to really consist of
`_`user_name`_._`table_name`_`. This is how PostgreSQL will effectively behave
if you create a per-user schema for every user.

Also, there is no concept of a `public` schema in the SQL standard. For
maximum conformance to the standard, you should not use the `public` schema.

Of course, some SQL database systems might not implement schemas at all, or
provide namespace support by allowing (possibly limited) cross-database
access. If you need to work with those systems, then maximum portability would
be achieved by not using schemas at all.

* * *

[Prev](ddl-rowsecurity.html "5.8. Row Security Policies")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-inherit.html "5.10. Inheritance")  
---|---|---  
5.8. Row Security Policies  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.10. Inheritance  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-schemas.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

