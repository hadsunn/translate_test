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

Supported Versions: [Current](/docs/current/ddl-depend.html "PostgreSQL 17 -
5.14. Dependency Tracking") ([17](/docs/17/ddl-depend.html "PostgreSQL 17 -
5.14. Dependency Tracking")) / [16](/docs/16/ddl-depend.html "PostgreSQL 16 -
5.14. Dependency Tracking") / [15](/docs/15/ddl-depend.html "PostgreSQL 15 -
5.14. Dependency Tracking") / [14](/docs/14/ddl-depend.html "PostgreSQL 14 -
5.14. Dependency Tracking") / [13](/docs/13/ddl-depend.html "PostgreSQL 13 -
5.14. Dependency Tracking")

Development Versions: [18](/docs/18/ddl-depend.html "PostgreSQL 18 -
5.14. Dependency Tracking") / [devel](/docs/devel/ddl-depend.html "PostgreSQL
devel - 5.14. Dependency Tracking")

Unsupported versions: [12](/docs/12/ddl-depend.html "PostgreSQL 12 -
5.14. Dependency Tracking") / [11](/docs/11/ddl-depend.html "PostgreSQL 11 -
5.14. Dependency Tracking") / [10](/docs/10/ddl-depend.html "PostgreSQL 10 -
5.14. Dependency Tracking") / [9.6](/docs/9.6/ddl-depend.html "PostgreSQL 9.6
- 5.14. Dependency Tracking") / [9.5](/docs/9.5/ddl-depend.html "PostgreSQL
9.5 - 5.14. Dependency Tracking") / [9.4](/docs/9.4/ddl-depend.html
"PostgreSQL 9.4 - 5.14. Dependency Tracking") / [9.3](/docs/9.3/ddl-
depend.html "PostgreSQL 9.3 - 5.14. Dependency Tracking") /
[9.2](/docs/9.2/ddl-depend.html "PostgreSQL 9.2 - 5.14. Dependency Tracking")
/ [9.1](/docs/9.1/ddl-depend.html "PostgreSQL 9.1 - 5.14. Dependency
Tracking") / [9.0](/docs/9.0/ddl-depend.html "PostgreSQL 9.0 -
5.14. Dependency Tracking") / [8.4](/docs/8.4/ddl-depend.html "PostgreSQL 8.4
- 5.14. Dependency Tracking") / [8.3](/docs/8.3/ddl-depend.html "PostgreSQL
8.3 - 5.14. Dependency Tracking") / [8.2](/docs/8.2/ddl-depend.html
"PostgreSQL 8.2 - 5.14. Dependency Tracking") / [8.1](/docs/8.1/ddl-
depend.html "PostgreSQL 8.1 - 5.14. Dependency Tracking") /
[8.0](/docs/8.0/ddl-depend.html "PostgreSQL 8.0 - 5.14. Dependency Tracking")
/ [7.4](/docs/7.4/ddl-depend.html "PostgreSQL 7.4 - 5.14. Dependency
Tracking") / [7.3](/docs/7.3/ddl-depend.html "PostgreSQL 7.3 -
5.14. Dependency Tracking")

__

5.14. Dependency Tracking  
---  
[Prev](ddl-others.html "5.13. Other Database Objects")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](dml.html "Chapter 6. Data Manipulation")  
  
* * *

## 5.14. Dependency Tracking #

When you create complex database structures involving many tables with foreign
key constraints, views, triggers, functions, etc. you implicitly create a net
of dependencies between the objects. For instance, a table with a foreign key
constraint depends on the table it references.

To ensure the integrity of the entire database structure, PostgreSQL makes
sure that you cannot drop objects that other objects still depend on. For
example, attempting to drop the products table we considered in [Section
5.4.5](ddl-constraints.html#DDL-CONSTRAINTS-FK "5.4.5. Foreign Keys"), with
the orders table depending on it, would result in an error message like this:

    
    
    DROP TABLE products;
    
    ERROR:  cannot drop table products because other objects depend on it
    DETAIL:  constraint orders_product_no_fkey on table orders depends on table products
    HINT:  Use DROP ... CASCADE to drop the dependent objects too.
    

The error message contains a useful hint: if you do not want to bother
deleting all the dependent objects individually, you can run:

    
    
    DROP TABLE products CASCADE;
    

and all the dependent objects will be removed, as will any objects that depend
on them, recursively. In this case, it doesn't remove the orders table, it
only removes the foreign key constraint. It stops there because nothing
depends on the foreign key constraint. (If you want to check what `DROP ...
CASCADE` will do, run `DROP` without `CASCADE` and read the `DETAIL` output.)

Almost all `DROP` commands in PostgreSQL support specifying `CASCADE`. Of
course, the nature of the possible dependencies varies with the type of the
object. You can also write `RESTRICT` instead of `CASCADE` to get the default
behavior, which is to prevent dropping objects that any other objects depend
on.

### Note

According to the SQL standard, specifying either `RESTRICT` or `CASCADE` is
required in a `DROP` command. No database system actually enforces that rule,
but whether the default behavior is `RESTRICT` or `CASCADE` varies across
systems.

If a `DROP` command lists multiple objects, `CASCADE` is only required when
there are dependencies outside the specified group. For example, when saying
`DROP TABLE tab1, tab2` the existence of a foreign key referencing `tab1` from
`tab2` would not mean that `CASCADE` is needed to succeed.

For a user-defined function or procedure whose body is defined as a string
literal, PostgreSQL tracks dependencies associated with the function's
externally-visible properties, such as its argument and result types, but
_not_ dependencies that could only be known by examining the function body. As
an example, consider this situation:

    
    
    CREATE TYPE rainbow AS ENUM ('red', 'orange', 'yellow',
                                 'green', 'blue', 'purple');
    
    CREATE TABLE my_colors (color rainbow, note text);
    
    CREATE FUNCTION get_color_note (rainbow) RETURNS text AS
      'SELECT note FROM my_colors WHERE color = $1'
      LANGUAGE SQL;
    

(See [Section 38.5](xfunc-sql.html "38.5. Query Language \(SQL\) Functions")
for an explanation of SQL-language functions.) PostgreSQL will be aware that
the `get_color_note` function depends on the `rainbow` type: dropping the type
would force dropping the function, because its argument type would no longer
be defined. But PostgreSQL will not consider `get_color_note` to depend on the
`my_colors` table, and so will not drop the function if the table is dropped.
While there are disadvantages to this approach, there are also benefits. The
function is still valid in some sense if the table is missing, though
executing it would cause an error; creating a new table of the same name would
allow the function to work again.

On the other hand, for a SQL-language function or procedure whose body is
written in SQL-standard style, the body is parsed at function definition time
and all dependencies recognized by the parser are stored. Thus, if we write
the function above as

    
    
    CREATE FUNCTION get_color_note (rainbow) RETURNS text
    BEGIN ATOMIC
      SELECT note FROM my_colors WHERE color = $1;
    END;
    

then the function's dependency on the `my_colors` table will be known and
enforced by `DROP`.

* * *

[Prev](ddl-others.html "5.13. Other Database Objects")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](dml.html "Chapter 6. Data Manipulation")  
---|---|---  
5.13. Other Database Objects  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 6. Data Manipulation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-depend.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

