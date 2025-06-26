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

Supported Versions: [Current](/docs/current/domains.html "PostgreSQL 17 -
8.18. Domain Types") ([17](/docs/17/domains.html "PostgreSQL 17 - 8.18. Domain
Types")) / [16](/docs/16/domains.html "PostgreSQL 16 - 8.18. Domain Types") /
[15](/docs/15/domains.html "PostgreSQL 15 - 8.18. Domain Types") /
[14](/docs/14/domains.html "PostgreSQL 14 - 8.18. Domain Types") /
[13](/docs/13/domains.html "PostgreSQL 13 - 8.18. Domain Types")

Development Versions: [18](/docs/18/domains.html "PostgreSQL 18 - 8.18. Domain
Types") / [devel](/docs/devel/domains.html "PostgreSQL devel - 8.18. Domain
Types")

Unsupported versions: [12](/docs/12/domains.html "PostgreSQL 12 - 8.18. Domain
Types") / [11](/docs/11/domains.html "PostgreSQL 11 - 8.18. Domain Types")

__

8.18. Domain Types  
---  
[Prev](rangetypes.html "8.17. Range Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-oid.html "8.19. Object Identifier Types")  
  
* * *

## 8.18. Domain Types #

A _domain_ is a user-defined data type that is based on another _underlying
type_. Optionally, it can have constraints that restrict its valid values to a
subset of what the underlying type would allow. Otherwise it behaves like the
underlying type — for example, any operator or function that can be applied to
the underlying type will work on the domain type. The underlying type can be
any built-in or user-defined base type, enum type, array type, composite type,
range type, or another domain.

For example, we could create a domain over integers that accepts only positive
integers:

    
    
    CREATE DOMAIN posint AS integer CHECK (VALUE > 0);
    CREATE TABLE mytable (id posint);
    INSERT INTO mytable VALUES(1);   -- works
    INSERT INTO mytable VALUES(-1);  -- fails
    

When an operator or function of the underlying type is applied to a domain
value, the domain is automatically down-cast to the underlying type. Thus, for
example, the result of `mytable.id - 1` is considered to be of type `integer`
not `posint`. We could write `(mytable.id - 1)::posint` to cast the result
back to `posint`, causing the domain's constraints to be rechecked. In this
case, that would result in an error if the expression had been applied to an
`id` value of 1. Assigning a value of the underlying type to a field or
variable of the domain type is allowed without writing an explicit cast, but
the domain's constraints will be checked.

For additional information see [CREATE DOMAIN](sql-createdomain.html "CREATE
DOMAIN").

* * *

[Prev](rangetypes.html "8.17. Range Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-oid.html "8.19. Object Identifier Types")  
---|---|---  
8.17. Range Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.19. Object Identifier Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/domains.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

