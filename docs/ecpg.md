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

Supported Versions: [Current](/docs/current/ecpg.html "PostgreSQL 17 -
Chapter 36. ECPG — Embedded SQL in C") ([17](/docs/17/ecpg.html "PostgreSQL 17
- Chapter 36. ECPG — Embedded SQL in C")) / [16](/docs/16/ecpg.html
"PostgreSQL 16 - Chapter 36. ECPG — Embedded SQL in C") /
[15](/docs/15/ecpg.html "PostgreSQL 15 - Chapter 36. ECPG — Embedded SQL in
C") / [14](/docs/14/ecpg.html "PostgreSQL 14 - Chapter 36. ECPG — Embedded SQL
in C") / [13](/docs/13/ecpg.html "PostgreSQL 13 - Chapter 36. ECPG — Embedded
SQL in C")

Development Versions: [18](/docs/18/ecpg.html "PostgreSQL 18 -
Chapter 36. ECPG — Embedded SQL in C") / [devel](/docs/devel/ecpg.html
"PostgreSQL devel - Chapter 36. ECPG — Embedded SQL in C")

Unsupported versions: [12](/docs/12/ecpg.html "PostgreSQL 12 -
Chapter 36. ECPG — Embedded SQL in C") / [11](/docs/11/ecpg.html "PostgreSQL
11 - Chapter 36. ECPG — Embedded SQL in C") / [10](/docs/10/ecpg.html
"PostgreSQL 10 - Chapter 36. ECPG — Embedded SQL in C") /
[9.6](/docs/9.6/ecpg.html "PostgreSQL 9.6 - Chapter 36. ECPG — Embedded SQL in
C") / [9.5](/docs/9.5/ecpg.html "PostgreSQL 9.5 - Chapter 36. ECPG — Embedded
SQL in C") / [9.4](/docs/9.4/ecpg.html "PostgreSQL 9.4 - Chapter 36. ECPG —
Embedded SQL in C") / [9.3](/docs/9.3/ecpg.html "PostgreSQL 9.3 -
Chapter 36. ECPG — Embedded SQL in C") / [9.2](/docs/9.2/ecpg.html "PostgreSQL
9.2 - Chapter 36. ECPG — Embedded SQL in C") / [9.1](/docs/9.1/ecpg.html
"PostgreSQL 9.1 - Chapter 36. ECPG — Embedded SQL in C") /
[9.0](/docs/9.0/ecpg.html "PostgreSQL 9.0 - Chapter 36. ECPG — Embedded SQL in
C") / [8.4](/docs/8.4/ecpg.html "PostgreSQL 8.4 - Chapter 36. ECPG — Embedded
SQL in C") / [8.3](/docs/8.3/ecpg.html "PostgreSQL 8.3 - Chapter 36. ECPG —
Embedded SQL in C") / [8.2](/docs/8.2/ecpg.html "PostgreSQL 8.2 -
Chapter 36. ECPG — Embedded SQL in C") / [8.1](/docs/8.1/ecpg.html "PostgreSQL
8.1 - Chapter 36. ECPG — Embedded SQL in C") / [8.0](/docs/8.0/ecpg.html
"PostgreSQL 8.0 - Chapter 36. ECPG — Embedded SQL in C") /
[7.4](/docs/7.4/ecpg.html "PostgreSQL 7.4 - Chapter 36. ECPG — Embedded SQL in
C") / [7.3](/docs/7.3/ecpg.html "PostgreSQL 7.3 - Chapter 36. ECPG — Embedded
SQL in C") / [7.2](/docs/7.2/ecpg.html "PostgreSQL 7.2 - Chapter 36. ECPG —
Embedded SQL in C") / [7.1](/docs/7.1/ecpg.html "PostgreSQL 7.1 -
Chapter 36. ECPG — Embedded SQL in C")

__

Chapter 36. ECPG — Embedded SQL in C  
---  
[Prev](lo-examplesect.html "35.5. Example Program")  | [Up](client-interfaces.html "Part IV. Client Interfaces") | Part IV. Client Interfaces | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-concept.html "36.1. The Concept")  
  
* * *

## Chapter 36. ECPG — Embedded SQL in C

**Table of Contents**

[36.1. The Concept](ecpg-concept.html)

[36.2. Managing Database Connections](ecpg-connect.html)

    

[36.2.1. Connecting to the Database Server](ecpg-connect.html#ECPG-CONNECTING)

[36.2.2. Choosing a Connection](ecpg-connect.html#ECPG-SET-CONNECTION)

[36.2.3. Closing a Connection](ecpg-connect.html#ECPG-DISCONNECT)

[36.3. Running SQL Commands](ecpg-commands.html)

    

[36.3.1. Executing SQL Statements](ecpg-commands.html#ECPG-EXECUTING)

[36.3.2. Using Cursors](ecpg-commands.html#ECPG-CURSORS)

[36.3.3. Managing Transactions](ecpg-commands.html#ECPG-TRANSACTIONS)

[36.3.4. Prepared Statements](ecpg-commands.html#ECPG-PREPARED)

[36.4. Using Host Variables](ecpg-variables.html)

    

[36.4.1. Overview](ecpg-variables.html#ECPG-VARIABLES-OVERVIEW)

[36.4.2. Declare Sections](ecpg-variables.html#ECPG-DECLARE-SECTIONS)

[36.4.3. Retrieving Query Results](ecpg-variables.html#ECPG-RETRIEVING)

[36.4.4. Type Mapping](ecpg-variables.html#ECPG-VARIABLES-TYPE-MAPPING)

[36.4.5. Handling Nonprimitive SQL Data Types](ecpg-variables.html#ECPG-
VARIABLES-NONPRIMITIVE-SQL)

[36.4.6. Indicators](ecpg-variables.html#ECPG-INDICATORS)

[36.5. Dynamic SQL](ecpg-dynamic.html)

    

[36.5.1. Executing Statements without a Result Set](ecpg-dynamic.html#ECPG-
DYNAMIC-WITHOUT-RESULT)

[36.5.2. Executing a Statement with Input Parameters](ecpg-dynamic.html#ECPG-
DYNAMIC-INPUT)

[36.5.3. Executing a Statement with a Result Set](ecpg-dynamic.html#ECPG-
DYNAMIC-WITH-RESULT)

[36.6. pgtypes Library](ecpg-pgtypes.html)

    

[36.6.1. Character Strings](ecpg-pgtypes.html#ECPG-PGTYPES-CSTRINGS)

[36.6.2. The numeric Type](ecpg-pgtypes.html#ECPG-PGTYPES-NUMERIC)

[36.6.3. The date Type](ecpg-pgtypes.html#ECPG-PGTYPES-DATE)

[36.6.4. The timestamp Type](ecpg-pgtypes.html#ECPG-PGTYPES-TIMESTAMP)

[36.6.5. The interval Type](ecpg-pgtypes.html#ECPG-PGTYPES-INTERVAL)

[36.6.6. The decimal Type](ecpg-pgtypes.html#ECPG-PGTYPES-DECIMAL)

[36.6.7. errno Values of pgtypeslib](ecpg-pgtypes.html#ECPG-PGTYPES-ERRNO)

[36.6.8. Special Constants of pgtypeslib](ecpg-pgtypes.html#ECPG-PGTYPES-
CONSTANTS)

[36.7. Using Descriptor Areas](ecpg-descriptors.html)

    

[36.7.1. Named SQL Descriptor Areas](ecpg-descriptors.html#ECPG-NAMED-
DESCRIPTORS)

[36.7.2. SQLDA Descriptor Areas](ecpg-descriptors.html#ECPG-SQLDA-DESCRIPTORS)

[36.8. Error Handling](ecpg-errors.html)

    

[36.8.1. Setting Callbacks](ecpg-errors.html#ECPG-WHENEVER)

[36.8.2. sqlca](ecpg-errors.html#ECPG-SQLCA)

[36.8.3. `SQLSTATE` vs. `SQLCODE`](ecpg-errors.html#ECPG-SQLSTATE-SQLCODE)

[36.9. Preprocessor Directives](ecpg-preproc.html)

    

[36.9.1. Including Files](ecpg-preproc.html#ECPG-INCLUDE)

[36.9.2. The define and undef Directives](ecpg-preproc.html#ECPG-DEFINE)

[36.9.3. ifdef, ifndef, elif, else, and endif Directives](ecpg-
preproc.html#ECPG-IFDEF)

[36.10. Processing Embedded SQL Programs](ecpg-process.html)

[36.11. Library Functions](ecpg-library.html)

[36.12. Large Objects](ecpg-lo.html)

[36.13. C++ Applications](ecpg-cpp.html)

    

[36.13.1. Scope for Host Variables](ecpg-cpp.html#ECPG-CPP-SCOPE)

[36.13.2. C++ Application Development with External C Module](ecpg-
cpp.html#ECPG-CPP-AND-C)

[36.14. Embedded SQL Commands](ecpg-sql-commands.html)

    

[ALLOCATE DESCRIPTOR](ecpg-sql-allocate-descriptor.html) — allocate an SQL
descriptor area

[CONNECT](ecpg-sql-connect.html) — establish a database connection

[DEALLOCATE DESCRIPTOR](ecpg-sql-deallocate-descriptor.html) — deallocate an
SQL descriptor area

[DECLARE](ecpg-sql-declare.html) — define a cursor

[DECLARE STATEMENT](ecpg-sql-declare-statement.html) — declare SQL statement
identifier

[DESCRIBE](ecpg-sql-describe.html) — obtain information about a prepared
statement or result set

[DISCONNECT](ecpg-sql-disconnect.html) — terminate a database connection

[EXECUTE IMMEDIATE](ecpg-sql-execute-immediate.html) — dynamically prepare and
execute a statement

[GET DESCRIPTOR](ecpg-sql-get-descriptor.html) — get information from an SQL
descriptor area

[OPEN](ecpg-sql-open.html) — open a dynamic cursor

[PREPARE](ecpg-sql-prepare.html) — prepare a statement for execution

[SET AUTOCOMMIT](ecpg-sql-set-autocommit.html) — set the autocommit behavior
of the current session

[SET CONNECTION](ecpg-sql-set-connection.html) — select a database connection

[SET DESCRIPTOR](ecpg-sql-set-descriptor.html) — set information in an SQL
descriptor area

[TYPE](ecpg-sql-type.html) — define a new data type

[VAR](ecpg-sql-var.html) — define a variable

[WHENEVER](ecpg-sql-whenever.html) — specify the action to be taken when an
SQL statement causes a specific class condition to be raised

[36.15. Informix Compatibility Mode](ecpg-informix-compat.html)

    

[36.15.1. Additional Types](ecpg-informix-compat.html#ECPG-INFORMIX-TYPES)

[36.15.2. Additional/Missing Embedded SQL Statements](ecpg-informix-
compat.html#ECPG-INFORMIX-STATEMENTS)

[36.15.3. Informix-compatible SQLDA Descriptor Areas](ecpg-informix-
compat.html#ECPG-INFORMIX-SQLDA)

[36.15.4. Additional Functions](ecpg-informix-compat.html#ECPG-INFORMIX-
FUNCTIONS)

[36.15.5. Additional Constants](ecpg-informix-compat.html#ECPG-INFORMIX-
CONSTANTS)

[36.16. Oracle Compatibility Mode](ecpg-oracle-compat.html)

[36.17. Internals](ecpg-develop.html)

This chapter describes the embedded SQL package for PostgreSQL. It was written
by Linus Tolke (`<[linus@epact.se](mailto:linus@epact.se)>`) and Michael
Meskes (`<[meskes@postgresql.org](mailto:meskes@postgresql.org)>`). Originally
it was written to work with C. It also works with C++, but it does not
recognize all C++ constructs yet.

This documentation is quite incomplete. But since this interface is
standardized, additional information can be found in many resources about SQL.

* * *

[Prev](lo-examplesect.html "35.5. Example Program")  | [Up](client-interfaces.html "Part IV. Client Interfaces") |  [Next](ecpg-concept.html "36.1. The Concept")  
---|---|---  
35.5. Example Program  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.1. The Concept  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

