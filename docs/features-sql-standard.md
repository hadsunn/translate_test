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

Supported Versions: [Current](/docs/current/features-sql-standard.html
"PostgreSQL 17 - D.1. Supported Features") ([17](/docs/17/features-sql-
standard.html "PostgreSQL 17 - D.1. Supported Features")) /
[16](/docs/16/features-sql-standard.html "PostgreSQL 16 - D.1. Supported
Features") / [15](/docs/15/features-sql-standard.html "PostgreSQL 15 -
D.1. Supported Features") / [14](/docs/14/features-sql-standard.html
"PostgreSQL 14 - D.1. Supported Features") / [13](/docs/13/features-sql-
standard.html "PostgreSQL 13 - D.1. Supported Features")

Development Versions: [18](/docs/18/features-sql-standard.html "PostgreSQL 18
- D.1. Supported Features") / [devel](/docs/devel/features-sql-standard.html
"PostgreSQL devel - D.1. Supported Features")

Unsupported versions: [12](/docs/12/features-sql-standard.html "PostgreSQL 12
- D.1. Supported Features") / [11](/docs/11/features-sql-standard.html
"PostgreSQL 11 - D.1. Supported Features") / [10](/docs/10/features-sql-
standard.html "PostgreSQL 10 - D.1. Supported Features") /
[9.6](/docs/9.6/features-sql-standard.html "PostgreSQL 9.6 - D.1. Supported
Features") / [9.5](/docs/9.5/features-sql-standard.html "PostgreSQL 9.5 -
D.1. Supported Features") / [9.4](/docs/9.4/features-sql-standard.html
"PostgreSQL 9.4 - D.1. Supported Features") / [9.3](/docs/9.3/features-sql-
standard.html "PostgreSQL 9.3 - D.1. Supported Features") /
[9.2](/docs/9.2/features-sql-standard.html "PostgreSQL 9.2 - D.1. Supported
Features") / [9.1](/docs/9.1/features-sql-standard.html "PostgreSQL 9.1 -
D.1. Supported Features") / [9.0](/docs/9.0/features-sql-standard.html
"PostgreSQL 9.0 - D.1. Supported Features") / [8.4](/docs/8.4/features-sql-
standard.html "PostgreSQL 8.4 - D.1. Supported Features") /
[8.3](/docs/8.3/features-sql-standard.html "PostgreSQL 8.3 - D.1. Supported
Features") / [8.2](/docs/8.2/features-sql-standard.html "PostgreSQL 8.2 -
D.1. Supported Features")

__

D.1. Supported Features  
---  
[Prev](features.html "Appendix D. SQL Conformance")  | [Up](features.html "Appendix D. SQL Conformance") | Appendix D. SQL Conformance | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](unsupported-features-sql-standard.html "D.2. Unsupported Features")  
  
* * *

## D.1. Supported Features #

Identifier | Core? | Description | Comment  
---|---|---|---  
B012 |   | Embedded C |    
B021 |   | Direct SQL |    
B128 |   | Routine language SQL |    
E011 | Core | Numeric data types |    
E011-01 | Core | INTEGER and SMALLINT data types |    
E011-02 | Core | REAL, DOUBLE PRECISION, and FLOAT data types |    
E011-03 | Core | DECIMAL and NUMERIC data types |    
E011-04 | Core | Arithmetic operators |    
E011-05 | Core | Numeric comparison |    
E011-06 | Core | Implicit casting among the numeric data types |    
E021 | Core | Character data types |    
E021-01 | Core | CHARACTER data type |    
E021-02 | Core | CHARACTER VARYING data type |    
E021-03 | Core | Character literals |    
E021-04 | Core | CHARACTER_LENGTH function | trims trailing spaces from CHARACTER values before counting  
E021-05 | Core | OCTET_LENGTH function |    
E021-06 | Core | SUBSTRING function |    
E021-07 | Core | Character concatenation |    
E021-08 | Core | UPPER and LOWER functions |    
E021-09 | Core | TRIM function |    
E021-10 | Core | Implicit casting among the character string types |    
E021-11 | Core | POSITION function |    
E021-12 | Core | Character comparison |    
E031 | Core | Identifiers |    
E031-01 | Core | Delimited identifiers |    
E031-02 | Core | Lower case identifiers |    
E031-03 | Core | Trailing underscore |    
E051 | Core | Basic query specification |    
E051-01 | Core | SELECT DISTINCT |    
E051-02 | Core | GROUP BY clause |    
E051-04 | Core | GROUP BY can contain columns not in <select list> |    
E051-05 | Core | Select list items can be renamed |    
E051-06 | Core | HAVING clause |    
E051-07 | Core | Qualified * in select list |    
E051-08 | Core | Correlation names in the FROM clause |    
E051-09 | Core | Rename columns in the FROM clause |    
E061 | Core | Basic predicates and search conditions |    
E061-01 | Core | Comparison predicate |    
E061-02 | Core | BETWEEN predicate |    
E061-03 | Core | IN predicate with list of values |    
E061-04 | Core | LIKE predicate |    
E061-05 | Core | LIKE predicate ESCAPE clause |    
E061-06 | Core | NULL predicate |    
E061-07 | Core | Quantified comparison predicate |    
E061-08 | Core | EXISTS predicate |    
E061-09 | Core | Subqueries in comparison predicate |    
E061-11 | Core | Subqueries in IN predicate |    
E061-12 | Core | Subqueries in quantified comparison predicate |    
E061-13 | Core | Correlated subqueries |    
E061-14 | Core | Search condition |    
E071 | Core | Basic query expressions |    
E071-01 | Core | UNION DISTINCT table operator |    
E071-02 | Core | UNION ALL table operator |    
E071-03 | Core | EXCEPT DISTINCT table operator |    
E071-05 | Core | Columns combined via table operators need not have exactly the same data type |    
E071-06 | Core | Table operators in subqueries |    
E081 | Core | Basic Privileges |    
E081-01 | Core | SELECT privilege |    
E081-02 | Core | DELETE privilege |    
E081-03 | Core | INSERT privilege at the table level |    
E081-04 | Core | UPDATE privilege at the table level |    
E081-05 | Core | UPDATE privilege at the column level |    
E081-06 | Core | REFERENCES privilege at the table level |    
E081-07 | Core | REFERENCES privilege at the column level |    
E081-08 | Core | WITH GRANT OPTION |    
E081-09 | Core | USAGE privilege |    
E081-10 | Core | EXECUTE privilege |    
E091 | Core | Set functions |    
E091-01 | Core | AVG |    
E091-02 | Core | COUNT |    
E091-03 | Core | MAX |    
E091-04 | Core | MIN |    
E091-05 | Core | SUM |    
E091-06 | Core | ALL quantifier |    
E091-07 | Core | DISTINCT quantifier |    
E101 | Core | Basic data manipulation |    
E101-01 | Core | INSERT statement |    
E101-03 | Core | Searched UPDATE statement |    
E101-04 | Core | Searched DELETE statement |    
E111 | Core | Single row SELECT statement |    
E121 | Core | Basic cursor support |    
E121-01 | Core | DECLARE CURSOR |    
E121-02 | Core | ORDER BY columns need not be in select list |    
E121-03 | Core | Value expressions in ORDER BY clause |    
E121-04 | Core | OPEN statement |    
E121-06 | Core | Positioned UPDATE statement |    
E121-07 | Core | Positioned DELETE statement |    
E121-08 | Core | CLOSE statement |    
E121-10 | Core | FETCH statement implicit NEXT |    
E121-17 | Core | WITH HOLD cursors |    
E131 | Core | Null value support (nulls in lieu of values) |    
E141 | Core | Basic integrity constraints |    
E141-01 | Core | NOT NULL constraints |    
E141-02 | Core | UNIQUE constraints of NOT NULL columns |    
E141-03 | Core | PRIMARY KEY constraints |    
E141-04 | Core | Basic FOREIGN KEY constraint with the NO ACTION default for both referential delete action and referential update action |    
E141-06 | Core | CHECK constraints |    
E141-07 | Core | Column defaults |    
E141-08 | Core | NOT NULL inferred on PRIMARY KEY |    
E141-10 | Core | Names in a foreign key can be specified in any order |    
E151 | Core | Transaction support |    
E151-01 | Core | COMMIT statement |    
E151-02 | Core | ROLLBACK statement |    
E152 | Core | Basic SET TRANSACTION statement |    
E152-01 | Core | SET TRANSACTION statement: ISOLATION LEVEL SERIALIZABLE clause |    
E152-02 | Core | SET TRANSACTION statement: READ ONLY and READ WRITE clauses |    
E153 | Core | Updatable queries with subqueries |    
E161 | Core | SQL comments using leading double minus |    
E171 | Core | SQLSTATE support |    
E182 | Core | Host language binding |    
F021 | Core | Basic information schema |    
F021-01 | Core | COLUMNS view |    
F021-02 | Core | TABLES view |    
F021-03 | Core | VIEWS view |    
F021-04 | Core | TABLE_CONSTRAINTS view |    
F021-05 | Core | REFERENTIAL_CONSTRAINTS view |    
F021-06 | Core | CHECK_CONSTRAINTS view |    
F031 | Core | Basic schema manipulation |    
F031-01 | Core | CREATE TABLE statement to create persistent base tables |    
F031-02 | Core | CREATE VIEW statement |    
F031-03 | Core | GRANT statement |    
F031-04 | Core | ALTER TABLE statement: ADD COLUMN clause |    
F031-13 | Core | DROP TABLE statement: RESTRICT clause |    
F031-16 | Core | DROP VIEW statement: RESTRICT clause |    
F031-19 | Core | REVOKE statement: RESTRICT clause |    
F032 |   | CASCADE drop behavior |    
F033 |   | ALTER TABLE statement: DROP COLUMN clause |    
F034 |   | Extended REVOKE statement |    
F035 |   | REVOKE with CASCADE |    
F036 |   | REVOKE statement performed by non-owner |    
F037 |   | REVOKE statement: GRANT OPTION FOR clause |    
F038 |   | REVOKE of a WITH GRANT OPTION privilege |    
F041 | Core | Basic joined table |    
F041-01 | Core | Inner join (but not necessarily the INNER keyword) |    
F041-02 | Core | INNER keyword |    
F041-03 | Core | LEFT OUTER JOIN |    
F041-04 | Core | RIGHT OUTER JOIN |    
F041-05 | Core | Outer joins can be nested |    
F041-07 | Core | The inner table in a left or right outer join can also be used in an inner join |    
F041-08 | Core | All comparison operators are supported (rather than just =) |    
F051 | Core | Basic date and time |    
F051-01 | Core | DATE data type (including support of DATE literal) |    
F051-02 | Core | TIME data type (including support of TIME literal) with fractional seconds precision of at least 0 |    
F051-03 | Core | TIMESTAMP data type (including support of TIMESTAMP literal) with fractional seconds precision of at least 0 and 6 |    
F051-04 | Core | Comparison predicate on DATE, TIME, and TIMESTAMP data types |    
F051-05 | Core | Explicit CAST between datetime types and character string types |    
F051-06 | Core | CURRENT_DATE |    
F051-07 | Core | LOCALTIME |    
F051-08 | Core | LOCALTIMESTAMP |    
F052 |   | Intervals and datetime arithmetic |    
F053 |   | OVERLAPS predicate |    
F081 | Core | UNION and EXCEPT in views |    
F111 |   | Isolation levels other than SERIALIZABLE |    
F112 |   | Isolation level READ UNCOMMITTED |    
F113 |   | Isolation level READ COMMITTED |    
F114 |   | Isolation level REPEATABLE READ |    
F131 | Core | Grouped operations |    
F131-01 | Core | WHERE, GROUP BY, and HAVING clauses supported in queries with grouped views |    
F131-02 | Core | Multiple tables supported in queries with grouped views |    
F131-03 | Core | Set functions supported in queries with grouped views |    
F131-04 | Core | Subqueries with GROUP BY and HAVING clauses and grouped views |    
F131-05 | Core | Single row SELECT with GROUP BY and HAVING clauses and grouped views |    
F171 |   | Multiple schemas per user |    
F181 | Core | Multiple module support |    
F191 |   | Referential delete actions |    
F200 |   | TRUNCATE TABLE statement |    
F201 | Core | CAST function |    
F202 |   | TRUNCATE TABLE: identity column restart option |    
F221 | Core | Explicit defaults |    
F222 |   | INSERT statement: DEFAULT VALUES clause |    
F231 |   | Privilege tables |    
F251 |   | Domain support |    
F261 | Core | CASE expression |    
F261-01 | Core | Simple CASE |    
F261-02 | Core | Searched CASE |    
F261-03 | Core | NULLIF |    
F261-04 | Core | COALESCE |    
F262 |   | Extended CASE expression |    
F271 |   | Compound character literals |    
F281 |   | LIKE enhancements |    
F292 |   | UNIQUE null treatment |    
F302 |   | INTERSECT table operator |    
F303 |   | INTERSECT DISTINCT table operator |    
F304 |   | EXCEPT ALL table operator |    
F305 |   | INTERSECT ALL table operator |    
F311 | Core | Schema definition statement |    
F311-01 | Core | CREATE SCHEMA |    
F311-02 | Core | CREATE TABLE for persistent base tables |    
F311-03 | Core | CREATE VIEW |    
F311-04 | Core | CREATE VIEW: WITH CHECK OPTION |    
F311-05 | Core | GRANT statement |    
F312 |   | MERGE statement |    
F313 |   | Enhanced MERGE statement |    
F314 |   | MERGE statement with DELETE branch |    
F321 |   | User authorization |    
F341 |   | Usage tables |    
F361 |   | Subprogram support |    
F381 |   | Extended schema manipulation |    
F382 |   | Alter column data type |    
F383 |   | Set column not null clause |    
F384 |   | Drop identity property clause |    
F385 |   | Drop column generation expression clause |    
F386 |   | Set identity column generation clause |    
F387 |   | ALTER TABLE statement: ALTER COLUMN clause |    
F388 |   | ALTER TABLE statement: ADD/DROP CONSTRAINT clause |    
F391 |   | Long identifiers |    
F392 |   | Unicode escapes in identifiers |    
F393 |   | Unicode escapes in literals |    
F394 |   | Optional normal form specification |    
F401 |   | Extended joined table |    
F402 |   | Named column joins for LOBs, arrays, and multisets |    
F404 |   | Range variable for common column names |    
F405 |   | NATURAL JOIN |    
F406 |   | FULL OUTER JOIN |    
F407 |   | CROSS JOIN |    
F411 |   | Time zone specification | differences regarding literal interpretation  
F421 |   | National character |    
F431 |   | Read-only scrollable cursors |    
F432 |   | FETCH with explicit NEXT |    
F433 |   | FETCH FIRST |    
F434 |   | FETCH LAST |    
F435 |   | FETCH PRIOR |    
F436 |   | FETCH ABSOLUTE |    
F437 |   | FETCH RELATIVE |    
F438 |   | Scrollable cursors |    
F441 |   | Extended set function support |    
F442 |   | Mixed column references in set functions |    
F471 | Core | Scalar subquery values |    
F481 | Core | Expanded NULL predicate |    
F491 |   | Constraint management |    
F501 | Core | Features and conformance views |    
F501-01 | Core | SQL_FEATURES view |    
F501-02 | Core | SQL_SIZING view |    
F502 |   | Enhanced documentation tables |    
F531 |   | Temporary tables |    
F555 |   | Enhanced seconds precision |    
F561 |   | Full value expressions |    
F571 |   | Truth value tests |    
F591 |   | Derived tables |    
F611 |   | Indicator data types |    
F641 |   | Row and table constructors |    
F651 |   | Catalog name qualifiers |    
F661 |   | Simple tables |    
F672 |   | Retrospective CHECK constraints |    
F690 |   | Collation support |    
F692 |   | Extended collation support |    
F701 |   | Referential update actions |    
F711 |   | ALTER domain |    
F731 |   | INSERT column privileges |    
F751 |   | View CHECK enhancements |    
F761 |   | Session management |    
F762 |   | CURRENT_CATALOG |    
F763 |   | CURRENT_SCHEMA |    
F771 |   | Connection management |    
F781 |   | Self-referencing operations |    
F791 |   | Insensitive cursors |    
F801 |   | Full set function |    
F850 |   | Top-level ORDER BY in query expression |    
F851 |   | ORDER BY in subqueries |    
F852 |   | Top-level ORDER BY in views |    
F855 |   | Nested ORDER BY in query expression |    
F856 |   | Nested FETCH FIRST in query expression |    
F857 |   | Top-level FETCH FIRST in query expression |    
F858 |   | FETCH FIRST in subqueries |    
F859 |   | Top-level FETCH FIRST in views |    
F860 |   | Dynamic FETCH FIRST row count |    
F861 |   | Top-level OFFSET in query expression |    
F862 |   | OFFSET in subqueries |    
F863 |   | Nested OFFSET in query expression |    
F864 |   | Top-level OFFSET in views |    
F865 |   | Dynamic offset row count in OFFSET |    
F867 |   | FETCH FIRST clause: WITH TIES option |    
F868 |   | ORDER BY in grouped table |    
F869 |   | SQL implementation info population |    
S071 |   | SQL paths in function and type name resolution |    
S090 |   | Minimal array support |    
S092 |   | Arrays of user-defined types |    
S095 |   | Array constructors by query |    
S096 |   | Optional array bounds |    
S098 |   | ARRAY_AGG |    
S099 |   | Array expressions |    
S111 |   | ONLY in query expressions |    
S201 |   | SQL-invoked routines on arrays |    
S203 |   | Array parameters |    
S204 |   | Array as result type of functions |    
S211 |   | User-defined cast functions |    
S301 |   | Enhanced UNNEST |    
S404 |   | TRIM_ARRAY |    
T031 |   | BOOLEAN data type |    
T054 |   | GREATEST and LEAST | different null handling  
T055 |   | String padding functions |    
T056 |   | Multi-character TRIM functions |    
T061 |   | UCS support |    
T071 |   | BIGINT data type |    
T081 |   | Optional string types maximum length |    
T121 |   | WITH (excluding RECURSIVE) in query expression |    
T122 |   | WITH (excluding RECURSIVE) in subquery |    
T131 |   | Recursive query |    
T132 |   | Recursive query in subquery |    
T133 |   | Enhanced cycle mark values |    
T141 |   | SIMILAR predicate |    
T151 |   | DISTINCT predicate |    
T152 |   | DISTINCT predicate with negation |    
T171 |   | LIKE clause in table definition |    
T172 |   | AS subquery clause in table definition |    
T173 |   | Extended LIKE clause in table definition |    
T174 |   | Identity columns |    
T177 |   | Sequence generator support: simple restart option |    
T178 |   | Identity columns: simple restart option |    
T191 |   | Referential action RESTRICT |    
T201 |   | Comparable data types for referential constraints |    
T212 |   | Enhanced trigger capability |    
T213 |   | INSTEAD OF triggers |    
T214 |   | BEFORE triggers |    
T215 |   | AFTER triggers |    
T216 |   | Ability to require true search condition before trigger is invoked |    
T217 |   | TRIGGER privilege |    
T241 |   | START TRANSACTION statement |    
T261 |   | Chained transactions |    
T271 |   | Savepoints |    
T281 |   | SELECT privilege with column granularity |    
T285 |   | Enhanced derived column names |    
T312 |   | OVERLAY function |    
T321-01 | Core | User-defined functions with no overloading |    
T321-02 | Core | User-defined stored procedures with no overloading |    
T321-03 | Core | Function invocation |    
T321-04 | Core | CALL statement |    
T321-05 | Core | RETURN statement |    
T321-06 | Core | ROUTINES view |    
T321-07 | Core | PARAMETERS view |    
T323 |   | Explicit security for external routines |    
T325 |   | Qualified SQL parameter references |    
T331 |   | Basic roles |    
T332 |   | Extended roles |    
T341 |   | Overloading of SQL-invoked functions and SQL-invoked procedures |    
T351 |   | Bracketed comments |    
T431 |   | Extended grouping capabilities |    
T432 |   | Nested and concatenated GROUPING SETS |    
T433 |   | Multi-argument GROUPING function |    
T434 |   | GROUP BY DISTINCT |    
T441 |   | ABS and MOD functions |    
T461 |   | Symmetric BETWEEN predicate |    
T491 |   | LATERAL derived table |    
T501 |   | Enhanced EXISTS predicate |    
T521 |   | Named arguments in CALL statement |    
T523 |   | Default values for INOUT parameters of SQL-invoked procedures |    
T524 |   | Named arguments in routine invocations other than a CALL statement |    
T525 |   | Default values for parameters of SQL-invoked functions |    
T551 |   | Optional key words for default syntax |    
T581 |   | Regular expression substring function |    
T591 |   | UNIQUE constraints of possibly null columns |    
T611 |   | Elementary OLAP operations |    
T612 |   | Advanced OLAP operations |    
T613 |   | Sampling |    
T614 |   | NTILE function |    
T615 |   | LEAD and LAG functions |    
T617 |   | FIRST_VALUE and LAST_VALUE functions |    
T620 |   | WINDOW clause: GROUPS option |    
T621 |   | Enhanced numeric functions |    
T622 |   | Trigonometric functions |    
T623 |   | General logarithm functions |    
T624 |   | Common logarithm functions |    
T626 |   | ANY_VALUE |    
T627 |   | Window framed COUNT DISTINCT |    
T631 | Core | IN predicate with one list element |    
T651 |   | SQL-schema statements in SQL routines |    
T653 |   | SQL-schema statements in external routines |    
T655 |   | Cyclically dependent routines |    
T661 |   | Non-decimal integer literals |    
T662 |   | Underscores in numeric literals |    
T670 |   | Schema and data statement mixing |    
T803 |   | String-based JSON |    
T811 |   | Basic SQL/JSON constructor functions |    
T812 |   | SQL/JSON: JSON_OBJECTAGG |    
T813 |   | SQL/JSON: JSON_ARRAYAGG with ORDER BY |    
T814 |   | Colon in JSON_OBJECT or JSON_OBJECTAGG |    
T822 |   | SQL/JSON: IS JSON WITH UNIQUE KEYS predicate |    
T830 |   | Enforcing unique keys in SQL/JSON constructor functions |    
T831 |   | SQL/JSON path language: strict mode |    
T832 |   | SQL/JSON path language: item method |    
T833 |   | SQL/JSON path language: multiple subscripts |    
T834 |   | SQL/JSON path language: wildcard member accessor |    
T835 |   | SQL/JSON path language: filter expressions |    
T836 |   | SQL/JSON path language: starts with predicate |    
T837 |   | SQL/JSON path language: regex_like predicate |    
T840 |   | Hex integer literals in SQL/JSON path language |    
T851 |   | SQL/JSON: optional keywords for default syntax |    
T879 |   | JSON in equality operations | with jsonb  
T880 |   | JSON in grouping operations | with jsonb  
X010 |   | XML type |    
X011 |   | Arrays of XML type |    
X014 |   | Attributes of XML type |    
X016 |   | Persistent XML values |    
X020 |   | XMLConcat |    
X031 |   | XMLElement |    
X032 |   | XMLForest |    
X034 |   | XMLAgg |    
X035 |   | XMLAgg: ORDER BY option |    
X036 |   | XMLComment |    
X037 |   | XMLPI |    
X040 |   | Basic table mapping |    
X041 |   | Basic table mapping: null absent |    
X042 |   | Basic table mapping: null as nil |    
X043 |   | Basic table mapping: table as forest |    
X044 |   | Basic table mapping: table as element |    
X045 |   | Basic table mapping: with target namespace |    
X046 |   | Basic table mapping: data mapping |    
X047 |   | Basic table mapping: metadata mapping |    
X048 |   | Basic table mapping: base64 encoding of binary strings |    
X049 |   | Basic table mapping: hex encoding of binary strings |    
X050 |   | Advanced table mapping |    
X051 |   | Advanced table mapping: null absent |    
X052 |   | Advanced table mapping: null as nil |    
X053 |   | Advanced table mapping: table as forest |    
X054 |   | Advanced table mapping: table as element |    
X055 |   | Advanced table mapping: with target namespace |    
X056 |   | Advanced table mapping: data mapping |    
X057 |   | Advanced table mapping: metadata mapping |    
X058 |   | Advanced table mapping: base64 encoding of binary strings |    
X059 |   | Advanced table mapping: hex encoding of binary strings |    
X060 |   | XMLParse: character string input and CONTENT option |    
X061 |   | XMLParse: character string input and DOCUMENT option |    
X069 |   | XMLSerialize: INDENT |    
X070 |   | XMLSerialize: character string serialization and CONTENT option |    
X071 |   | XMLSerialize: character string serialization and DOCUMENT option |    
X072 |   | XMLSerialize: character string serialization |    
X090 |   | XML document predicate |    
X120 |   | XML parameters in SQL routines |    
X121 |   | XML parameters in external routines |    
X221 |   | XML passing mechanism BY VALUE |    
X301 |   | XMLTable: derived column list option |    
X302 |   | XMLTable: ordinality column option |    
X303 |   | XMLTable: column default option |    
X304 |   | XMLTable: passing a context item | must be XML DOCUMENT  
X400 |   | Name and identifier mapping |    
X410 |   | Alter column data type: XML type |    
  
* * *

[Prev](features.html "Appendix D. SQL Conformance")  | [Up](features.html "Appendix D. SQL Conformance") |  [Next](unsupported-features-sql-standard.html "D.2. Unsupported Features")  
---|---|---  
Appendix D. SQL Conformance  | [Home](index.html "PostgreSQL 16.9 Documentation") |  D.2. Unsupported Features  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/features-sql-standard.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

