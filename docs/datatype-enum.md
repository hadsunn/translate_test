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

Supported Versions: [Current](/docs/current/datatype-enum.html "PostgreSQL 17
- 8.7. Enumerated Types") ([17](/docs/17/datatype-enum.html "PostgreSQL 17 -
8.7. Enumerated Types")) / [16](/docs/16/datatype-enum.html "PostgreSQL 16 -
8.7. Enumerated Types") / [15](/docs/15/datatype-enum.html "PostgreSQL 15 -
8.7. Enumerated Types") / [14](/docs/14/datatype-enum.html "PostgreSQL 14 -
8.7. Enumerated Types") / [13](/docs/13/datatype-enum.html "PostgreSQL 13 -
8.7. Enumerated Types")

Development Versions: [18](/docs/18/datatype-enum.html "PostgreSQL 18 -
8.7. Enumerated Types") / [devel](/docs/devel/datatype-enum.html "PostgreSQL
devel - 8.7. Enumerated Types")

Unsupported versions: [12](/docs/12/datatype-enum.html "PostgreSQL 12 -
8.7. Enumerated Types") / [11](/docs/11/datatype-enum.html "PostgreSQL 11 -
8.7. Enumerated Types") / [10](/docs/10/datatype-enum.html "PostgreSQL 10 -
8.7. Enumerated Types") / [9.6](/docs/9.6/datatype-enum.html "PostgreSQL 9.6 -
8.7. Enumerated Types") / [9.5](/docs/9.5/datatype-enum.html "PostgreSQL 9.5 -
8.7. Enumerated Types") / [9.4](/docs/9.4/datatype-enum.html "PostgreSQL 9.4 -
8.7. Enumerated Types") / [9.3](/docs/9.3/datatype-enum.html "PostgreSQL 9.3 -
8.7. Enumerated Types") / [9.2](/docs/9.2/datatype-enum.html "PostgreSQL 9.2 -
8.7. Enumerated Types") / [9.1](/docs/9.1/datatype-enum.html "PostgreSQL 9.1 -
8.7. Enumerated Types") / [9.0](/docs/9.0/datatype-enum.html "PostgreSQL 9.0 -
8.7. Enumerated Types") / [8.4](/docs/8.4/datatype-enum.html "PostgreSQL 8.4 -
8.7. Enumerated Types") / [8.3](/docs/8.3/datatype-enum.html "PostgreSQL 8.3 -
8.7. Enumerated Types")

__

8.7. Enumerated Types  
---  
[Prev](datatype-boolean.html "8.6. Boolean Type")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-geometric.html "8.8. Geometric Types")  
  
* * *

## 8.7. Enumerated Types #

[8.7.1. Declaration of Enumerated Types](datatype-enum.html#DATATYPE-ENUM-
DECLARATION)

[8.7.2. Ordering](datatype-enum.html#DATATYPE-ENUM-ORDERING)

[8.7.3. Type Safety](datatype-enum.html#DATATYPE-ENUM-TYPE-SAFETY)

[8.7.4. Implementation Details](datatype-enum.html#DATATYPE-ENUM-
IMPLEMENTATION-DETAILS)

Enumerated (enum) types are data types that comprise a static, ordered set of
values. They are equivalent to the `enum` types supported in a number of
programming languages. An example of an enum type might be the days of the
week, or a set of status values for a piece of data.

### 8.7.1. Declaration of Enumerated Types #

Enum types are created using the [CREATE TYPE](sql-createtype.html "CREATE
TYPE") command, for example:

    
    
    CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
    

Once created, the enum type can be used in table and function definitions much
like any other type:

    
    
    CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
    CREATE TABLE person (
        name text,
        current_mood mood
    );
    INSERT INTO person VALUES ('Moe', 'happy');
    SELECT * FROM person WHERE current_mood = 'happy';
     name | current_mood
    ------+--------------
     Moe  | happy
    (1 row)
    

### 8.7.2. Ordering #

The ordering of the values in an enum type is the order in which the values
were listed when the type was created. All standard comparison operators and
related aggregate functions are supported for enums. For example:

    
    
    INSERT INTO person VALUES ('Larry', 'sad');
    INSERT INTO person VALUES ('Curly', 'ok');
    SELECT * FROM person WHERE current_mood > 'sad';
     name  | current_mood
    -------+--------------
     Moe   | happy
     Curly | ok
    (2 rows)
    
    SELECT * FROM person WHERE current_mood > 'sad' ORDER BY current_mood;
     name  | current_mood
    -------+--------------
     Curly | ok
     Moe   | happy
    (2 rows)
    
    SELECT name
    FROM person
    WHERE current_mood = (SELECT MIN(current_mood) FROM person);
     name
    -------
     Larry
    (1 row)
    

### 8.7.3. Type Safety #

Each enumerated data type is separate and cannot be compared with other
enumerated types. See this example:

    
    
    CREATE TYPE happiness AS ENUM ('happy', 'very happy', 'ecstatic');
    CREATE TABLE holidays (
        num_weeks integer,
        happiness happiness
    );
    INSERT INTO holidays(num_weeks,happiness) VALUES (4, 'happy');
    INSERT INTO holidays(num_weeks,happiness) VALUES (6, 'very happy');
    INSERT INTO holidays(num_weeks,happiness) VALUES (8, 'ecstatic');
    INSERT INTO holidays(num_weeks,happiness) VALUES (2, 'sad');
    ERROR:  invalid input value for enum happiness: "sad"
    SELECT person.name, holidays.num_weeks FROM person, holidays
      WHERE person.current_mood = holidays.happiness;
    ERROR:  operator does not exist: mood = happiness
    

If you really need to do something like that, you can either write a custom
operator or add explicit casts to your query:

    
    
    SELECT person.name, holidays.num_weeks FROM person, holidays
      WHERE person.current_mood::text = holidays.happiness::text;
     name | num_weeks
    ------+-----------
     Moe  |         4
    (1 row)
    
    

### 8.7.4. Implementation Details #

Enum labels are case sensitive, so `'happy'` is not the same as `'HAPPY'`.
White space in the labels is significant too.

Although enum types are primarily intended for static sets of values, there is
support for adding new values to an existing enum type, and for renaming
values (see [ALTER TYPE](sql-altertype.html "ALTER TYPE")). Existing values
cannot be removed from an enum type, nor can the sort ordering of such values
be changed, short of dropping and re-creating the enum type.

An enum value occupies four bytes on disk. The length of an enum value's
textual label is limited by the `NAMEDATALEN` setting compiled into
PostgreSQL; in standard builds this means at most 63 bytes.

The translations from internal enum values to textual labels are kept in the
system catalog [`pg_enum`](catalog-pg-enum.html "53.20. pg_enum"). Querying
this catalog directly can be useful.

* * *

[Prev](datatype-boolean.html "8.6. Boolean Type")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-geometric.html "8.8. Geometric Types")  
---|---|---  
8.6. Boolean Type  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.8. Geometric Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-enum.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

