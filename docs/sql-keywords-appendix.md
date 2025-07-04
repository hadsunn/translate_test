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

Supported Versions: [Current](/docs/current/sql-keywords-appendix.html
"PostgreSQL 17 - Appendix C. SQL Key Words") ([17](/docs/17/sql-keywords-
appendix.html "PostgreSQL 17 - Appendix C. SQL Key Words")) /
[16](/docs/16/sql-keywords-appendix.html "PostgreSQL 16 - Appendix C. SQL Key
Words") / [15](/docs/15/sql-keywords-appendix.html "PostgreSQL 15 -
Appendix C. SQL Key Words") / [14](/docs/14/sql-keywords-appendix.html
"PostgreSQL 14 - Appendix C. SQL Key Words") / [13](/docs/13/sql-keywords-
appendix.html "PostgreSQL 13 - Appendix C. SQL Key Words")

Development Versions: [18](/docs/18/sql-keywords-appendix.html "PostgreSQL 18
- Appendix C. SQL Key Words") / [devel](/docs/devel/sql-keywords-appendix.html
"PostgreSQL devel - Appendix C. SQL Key Words")

Unsupported versions: [12](/docs/12/sql-keywords-appendix.html "PostgreSQL 12
- Appendix C. SQL Key Words") / [11](/docs/11/sql-keywords-appendix.html
"PostgreSQL 11 - Appendix C. SQL Key Words") / [10](/docs/10/sql-keywords-
appendix.html "PostgreSQL 10 - Appendix C. SQL Key Words") /
[9.6](/docs/9.6/sql-keywords-appendix.html "PostgreSQL 9.6 - Appendix C. SQL
Key Words") / [9.5](/docs/9.5/sql-keywords-appendix.html "PostgreSQL 9.5 -
Appendix C. SQL Key Words") / [9.4](/docs/9.4/sql-keywords-appendix.html
"PostgreSQL 9.4 - Appendix C. SQL Key Words") / [9.3](/docs/9.3/sql-keywords-
appendix.html "PostgreSQL 9.3 - Appendix C. SQL Key Words") /
[9.2](/docs/9.2/sql-keywords-appendix.html "PostgreSQL 9.2 - Appendix C. SQL
Key Words") / [9.1](/docs/9.1/sql-keywords-appendix.html "PostgreSQL 9.1 -
Appendix C. SQL Key Words") / [9.0](/docs/9.0/sql-keywords-appendix.html
"PostgreSQL 9.0 - Appendix C. SQL Key Words") / [8.4](/docs/8.4/sql-keywords-
appendix.html "PostgreSQL 8.4 - Appendix C. SQL Key Words") /
[8.3](/docs/8.3/sql-keywords-appendix.html "PostgreSQL 8.3 - Appendix C. SQL
Key Words") / [8.2](/docs/8.2/sql-keywords-appendix.html "PostgreSQL 8.2 -
Appendix C. SQL Key Words") / [8.1](/docs/8.1/sql-keywords-appendix.html
"PostgreSQL 8.1 - Appendix C. SQL Key Words") / [8.0](/docs/8.0/sql-keywords-
appendix.html "PostgreSQL 8.0 - Appendix C. SQL Key Words") /
[7.4](/docs/7.4/sql-keywords-appendix.html "PostgreSQL 7.4 - Appendix C. SQL
Key Words") / [7.3](/docs/7.3/sql-keywords-appendix.html "PostgreSQL 7.3 -
Appendix C. SQL Key Words") / [7.2](/docs/7.2/sql-keywords-appendix.html
"PostgreSQL 7.2 - Appendix C. SQL Key Words") / [7.1](/docs/7.1/sql-keywords-
appendix.html "PostgreSQL 7.1 - Appendix C. SQL Key Words")

__

Appendix C. SQL Key Words  
---  
[Prev](datetime-julian-dates.html "B.7. Julian Dates")  | [Up](appendixes.html "Part VIII. Appendixes") | Part VIII. Appendixes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](features.html "Appendix D. SQL Conformance")  
  
* * *

## Appendix C. SQL Key Words

[Table C.1](sql-keywords-appendix.html#KEYWORDS-TABLE "Table C.1. SQL Key
Words") lists all tokens that are key words in the SQL standard and in
PostgreSQL 16.9. Background information can be found in [Section 4.1.1](sql-
syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS "4.1.1. Identifiers and Key
Words"). (For space reasons, only the latest two versions of the SQL standard,
and SQL-92 for historical comparison, are included. The differences between
those and the other intermediate standard versions are small.)

SQL distinguishes between _reserved_ and _non-reserved_ key words. According
to the standard, reserved key words are the only real key words; they are
never allowed as identifiers. Non-reserved key words only have a special
meaning in particular contexts and can be used as identifiers in other
contexts. Most non-reserved key words are actually the names of built-in
tables and functions specified by SQL. The concept of non-reserved key words
essentially only exists to declare that some predefined meaning is attached to
a word in some contexts.

In the PostgreSQL parser, life is a bit more complicated. There are several
different classes of tokens ranging from those that can never be used as an
identifier to those that have absolutely no special status in the parser, but
are considered ordinary identifiers. (The latter is usually the case for
functions specified by SQL.) Even reserved key words are not completely
reserved in PostgreSQL, but can be used as column labels (for example, `SELECT
55 AS CHECK`, even though `CHECK` is a reserved key word).

In [Table C.1](sql-keywords-appendix.html#KEYWORDS-TABLE "Table C.1. SQL Key
Words") in the column for PostgreSQL we classify as “non-reserved” those key
words that are explicitly known to the parser but are allowed as column or
table names. Some key words that are otherwise non-reserved cannot be used as
function or data type names and are marked accordingly. (Most of these words
represent built-in functions or data types with special syntax. The function
or type is still available but it cannot be redefined by the user.) Labeled
“reserved” are those tokens that are not allowed as column or table names.
Some reserved key words are allowable as names for functions or data types;
this is also shown in the table. If not so marked, a reserved key word is only
allowed as a column label. A blank entry in this column means that the word is
treated as an ordinary identifier by PostgreSQL.

Furthermore, while most key words can be used as “bare” column labels without
writing `AS` before them (as described in [Section 7.3.2](queries-select-
lists.html#QUERIES-COLUMN-LABELS "7.3.2. Column Labels")), there are a few
that require a leading `AS` to avoid ambiguity. These are marked in the table
as “requires `AS`”.

As a general rule, if you get spurious parser errors for commands that use any
of the listed key words as an identifier, you should try quoting the
identifier to see if the problem goes away.

It is important to understand before studying [Table C.1](sql-keywords-
appendix.html#KEYWORDS-TABLE "Table C.1. SQL Key Words") that the fact that a
key word is not reserved in PostgreSQL does not mean that the feature related
to the word is not implemented. Conversely, the presence of a key word does
not indicate the existence of a feature.

**Table  C.1. SQL Key Words**

Key Word | PostgreSQL | SQL:2023 | SQL:2016 | SQL-92  
---|---|---|---|---  
`A` |   | non-reserved | non-reserved |    
`ABORT` | non-reserved |   |   |    
`ABS` |   | reserved | reserved |    
`ABSENT` | non-reserved | reserved | reserved |    
`ABSOLUTE` | non-reserved | non-reserved | non-reserved | reserved  
`ACCESS` | non-reserved |   |   |    
`ACCORDING` |   | non-reserved | non-reserved |    
`ACOS` |   | reserved | reserved |    
`ACTION` | non-reserved | non-reserved | non-reserved | reserved  
`ADA` |   | non-reserved | non-reserved | non-reserved  
`ADD` | non-reserved | non-reserved | non-reserved | reserved  
`ADMIN` | non-reserved | non-reserved | non-reserved |    
`AFTER` | non-reserved | non-reserved | non-reserved |    
`AGGREGATE` | non-reserved |   |   |    
`ALL` | reserved | reserved | reserved | reserved  
`ALLOCATE` |   | reserved | reserved | reserved  
`ALSO` | non-reserved |   |   |    
`ALTER` | non-reserved | reserved | reserved | reserved  
`ALWAYS` | non-reserved | non-reserved | non-reserved |    
`ANALYSE` | reserved |   |   |    
`ANALYZE` | reserved |   |   |    
`AND` | reserved | reserved | reserved | reserved  
`ANY` | reserved | reserved | reserved | reserved  
`ANY_VALUE` |   | reserved |   |    
`ARE` |   | reserved | reserved | reserved  
`ARRAY` | reserved, requires `AS` | reserved | reserved |    
`ARRAY_AGG` |   | reserved | reserved |    
`ARRAY_​MAX_​CARDINALITY` |   | reserved | reserved |    
`AS` | reserved, requires `AS` | reserved | reserved | reserved  
`ASC` | reserved | non-reserved | non-reserved | reserved  
`ASENSITIVE` | non-reserved | reserved | reserved |    
`ASIN` |   | reserved | reserved |    
`ASSERTION` | non-reserved | non-reserved | non-reserved | reserved  
`ASSIGNMENT` | non-reserved | non-reserved | non-reserved |    
`ASYMMETRIC` | reserved | reserved | reserved |    
`AT` | non-reserved | reserved | reserved | reserved  
`ATAN` |   | reserved | reserved |    
`ATOMIC` | non-reserved | reserved | reserved |    
`ATTACH` | non-reserved |   |   |    
`ATTRIBUTE` | non-reserved | non-reserved | non-reserved |    
`ATTRIBUTES` |   | non-reserved | non-reserved |    
`AUTHORIZATION` | reserved (can be function or type) | reserved | reserved | reserved  
`AVG` |   | reserved | reserved | reserved  
`BACKWARD` | non-reserved |   |   |    
`BASE64` |   | non-reserved | non-reserved |    
`BEFORE` | non-reserved | non-reserved | non-reserved |    
`BEGIN` | non-reserved | reserved | reserved | reserved  
`BEGIN_FRAME` |   | reserved | reserved |    
`BEGIN_PARTITION` |   | reserved | reserved |    
`BERNOULLI` |   | non-reserved | non-reserved |    
`BETWEEN` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`BIGINT` | non-reserved (cannot be function or type) | reserved | reserved |    
`BINARY` | reserved (can be function or type) | reserved | reserved |    
`BIT` | non-reserved (cannot be function or type) |   |   | reserved  
`BIT_LENGTH` |   |   |   | reserved  
`BLOB` |   | reserved | reserved |    
`BLOCKED` |   | non-reserved | non-reserved |    
`BOM` |   | non-reserved | non-reserved |    
`BOOLEAN` | non-reserved (cannot be function or type) | reserved | reserved |    
`BOTH` | reserved | reserved | reserved | reserved  
`BREADTH` | non-reserved | non-reserved | non-reserved |    
`BTRIM` |   | reserved |   |    
`BY` | non-reserved | reserved | reserved | reserved  
`C` |   | non-reserved | non-reserved | non-reserved  
`CACHE` | non-reserved |   |   |    
`CALL` | non-reserved | reserved | reserved |    
`CALLED` | non-reserved | reserved | reserved |    
`CARDINALITY` |   | reserved | reserved |    
`CASCADE` | non-reserved | non-reserved | non-reserved | reserved  
`CASCADED` | non-reserved | reserved | reserved | reserved  
`CASE` | reserved | reserved | reserved | reserved  
`CAST` | reserved | reserved | reserved | reserved  
`CATALOG` | non-reserved | non-reserved | non-reserved | reserved  
`CATALOG_NAME` |   | non-reserved | non-reserved | non-reserved  
`CEIL` |   | reserved | reserved |    
`CEILING` |   | reserved | reserved |    
`CHAIN` | non-reserved | non-reserved | non-reserved |    
`CHAINING` |   | non-reserved | non-reserved |    
`CHAR` | non-reserved (cannot be function or type), requires `AS` | reserved | reserved | reserved  
`CHARACTER` | non-reserved (cannot be function or type), requires `AS` | reserved | reserved | reserved  
`CHARACTERISTICS` | non-reserved | non-reserved | non-reserved |    
`CHARACTERS` |   | non-reserved | non-reserved |    
`CHARACTER_LENGTH` |   | reserved | reserved | reserved  
`CHARACTER_​SET_​CATALOG` |   | non-reserved | non-reserved | non-reserved  
`CHARACTER_SET_NAME` |   | non-reserved | non-reserved | non-reserved  
`CHARACTER_SET_SCHEMA` |   | non-reserved | non-reserved | non-reserved  
`CHAR_LENGTH` |   | reserved | reserved | reserved  
`CHECK` | reserved | reserved | reserved | reserved  
`CHECKPOINT` | non-reserved |   |   |    
`CLASS` | non-reserved |   |   |    
`CLASSIFIER` |   | reserved | reserved |    
`CLASS_ORIGIN` |   | non-reserved | non-reserved | non-reserved  
`CLOB` |   | reserved | reserved |    
`CLOSE` | non-reserved | reserved | reserved | reserved  
`CLUSTER` | non-reserved |   |   |    
`COALESCE` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`COBOL` |   | non-reserved | non-reserved | non-reserved  
`COLLATE` | reserved | reserved | reserved | reserved  
`COLLATION` | reserved (can be function or type) | non-reserved | non-reserved | reserved  
`COLLATION_CATALOG` |   | non-reserved | non-reserved | non-reserved  
`COLLATION_NAME` |   | non-reserved | non-reserved | non-reserved  
`COLLATION_SCHEMA` |   | non-reserved | non-reserved | non-reserved  
`COLLECT` |   | reserved | reserved |    
`COLUMN` | reserved | reserved | reserved | reserved  
`COLUMNS` | non-reserved | non-reserved | non-reserved |    
`COLUMN_NAME` |   | non-reserved | non-reserved | non-reserved  
`COMMAND_FUNCTION` |   | non-reserved | non-reserved | non-reserved  
`COMMAND_​FUNCTION_​CODE` |   | non-reserved | non-reserved |    
`COMMENT` | non-reserved |   |   |    
`COMMENTS` | non-reserved |   |   |    
`COMMIT` | non-reserved | reserved | reserved | reserved  
`COMMITTED` | non-reserved | non-reserved | non-reserved | non-reserved  
`COMPRESSION` | non-reserved |   |   |    
`CONCURRENTLY` | reserved (can be function or type) |   |   |    
`CONDITION` |   | reserved | reserved |    
`CONDITIONAL` |   | non-reserved | non-reserved |    
`CONDITION_NUMBER` |   | non-reserved | non-reserved | non-reserved  
`CONFIGURATION` | non-reserved |   |   |    
`CONFLICT` | non-reserved |   |   |    
`CONNECT` |   | reserved | reserved | reserved  
`CONNECTION` | non-reserved | non-reserved | non-reserved | reserved  
`CONNECTION_NAME` |   | non-reserved | non-reserved | non-reserved  
`CONSTRAINT` | reserved | reserved | reserved | reserved  
`CONSTRAINTS` | non-reserved | non-reserved | non-reserved | reserved  
`CONSTRAINT_CATALOG` |   | non-reserved | non-reserved | non-reserved  
`CONSTRAINT_NAME` |   | non-reserved | non-reserved | non-reserved  
`CONSTRAINT_SCHEMA` |   | non-reserved | non-reserved | non-reserved  
`CONSTRUCTOR` |   | non-reserved | non-reserved |    
`CONTAINS` |   | reserved | reserved |    
`CONTENT` | non-reserved | non-reserved | non-reserved |    
`CONTINUE` | non-reserved | non-reserved | non-reserved | reserved  
`CONTROL` |   | non-reserved | non-reserved |    
`CONVERSION` | non-reserved |   |   |    
`CONVERT` |   | reserved | reserved | reserved  
`COPARTITION` |   | non-reserved |   |    
`COPY` | non-reserved | reserved | reserved |    
`CORR` |   | reserved | reserved |    
`CORRESPONDING` |   | reserved | reserved | reserved  
`COS` |   | reserved | reserved |    
`COSH` |   | reserved | reserved |    
`COST` | non-reserved |   |   |    
`COUNT` |   | reserved | reserved | reserved  
`COVAR_POP` |   | reserved | reserved |    
`COVAR_SAMP` |   | reserved | reserved |    
`CREATE` | reserved, requires `AS` | reserved | reserved | reserved  
`CROSS` | reserved (can be function or type) | reserved | reserved | reserved  
`CSV` | non-reserved |   |   |    
`CUBE` | non-reserved | reserved | reserved |    
`CUME_DIST` |   | reserved | reserved |    
`CURRENT` | non-reserved | reserved | reserved | reserved  
`CURRENT_CATALOG` | reserved | reserved | reserved |    
`CURRENT_DATE` | reserved | reserved | reserved | reserved  
`CURRENT_​DEFAULT_​TRANSFORM_​GROUP` |   | reserved | reserved |    
`CURRENT_PATH` |   | reserved | reserved |    
`CURRENT_ROLE` | reserved | reserved | reserved |    
`CURRENT_ROW` |   | reserved | reserved |    
`CURRENT_SCHEMA` | reserved (can be function or type) | reserved | reserved |    
`CURRENT_TIME` | reserved | reserved | reserved | reserved  
`CURRENT_TIMESTAMP` | reserved | reserved | reserved | reserved  
`CURRENT_​TRANSFORM_​GROUP_​FOR_​TYPE` |   | reserved | reserved |    
`CURRENT_USER` | reserved | reserved | reserved | reserved  
`CURSOR` | non-reserved | reserved | reserved | reserved  
`CURSOR_NAME` |   | non-reserved | non-reserved | non-reserved  
`CYCLE` | non-reserved | reserved | reserved |    
`DATA` | non-reserved | non-reserved | non-reserved | non-reserved  
`DATABASE` | non-reserved |   |   |    
`DATALINK` |   | reserved | reserved |    
`DATE` |   | reserved | reserved | reserved  
`DATETIME_​INTERVAL_​CODE` |   | non-reserved | non-reserved | non-reserved  
`DATETIME_​INTERVAL_​PRECISION` |   | non-reserved | non-reserved | non-reserved  
`DAY` | non-reserved, requires `AS` | reserved | reserved | reserved  
`DB` |   | non-reserved | non-reserved |    
`DEALLOCATE` | non-reserved | reserved | reserved | reserved  
`DEC` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`DECFLOAT` |   | reserved | reserved |    
`DECIMAL` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`DECLARE` | non-reserved | reserved | reserved | reserved  
`DEFAULT` | reserved | reserved | reserved | reserved  
`DEFAULTS` | non-reserved | non-reserved | non-reserved |    
`DEFERRABLE` | reserved | non-reserved | non-reserved | reserved  
`DEFERRED` | non-reserved | non-reserved | non-reserved | reserved  
`DEFINE` |   | reserved | reserved |    
`DEFINED` |   | non-reserved | non-reserved |    
`DEFINER` | non-reserved | non-reserved | non-reserved |    
`DEGREE` |   | non-reserved | non-reserved |    
`DELETE` | non-reserved | reserved | reserved | reserved  
`DELIMITER` | non-reserved |   |   |    
`DELIMITERS` | non-reserved |   |   |    
`DENSE_RANK` |   | reserved | reserved |    
`DEPENDS` | non-reserved |   |   |    
`DEPTH` | non-reserved | non-reserved | non-reserved |    
`DEREF` |   | reserved | reserved |    
`DERIVED` |   | non-reserved | non-reserved |    
`DESC` | reserved | non-reserved | non-reserved | reserved  
`DESCRIBE` |   | reserved | reserved | reserved  
`DESCRIPTOR` |   | non-reserved | non-reserved | reserved  
`DETACH` | non-reserved |   |   |    
`DETERMINISTIC` |   | reserved | reserved |    
`DIAGNOSTICS` |   | non-reserved | non-reserved | reserved  
`DICTIONARY` | non-reserved |   |   |    
`DISABLE` | non-reserved |   |   |    
`DISCARD` | non-reserved |   |   |    
`DISCONNECT` |   | reserved | reserved | reserved  
`DISPATCH` |   | non-reserved | non-reserved |    
`DISTINCT` | reserved | reserved | reserved | reserved  
`DLNEWCOPY` |   | reserved | reserved |    
`DLPREVIOUSCOPY` |   | reserved | reserved |    
`DLURLCOMPLETE` |   | reserved | reserved |    
`DLURLCOMPLETEONLY` |   | reserved | reserved |    
`DLURLCOMPLETEWRITE` |   | reserved | reserved |    
`DLURLPATH` |   | reserved | reserved |    
`DLURLPATHONLY` |   | reserved | reserved |    
`DLURLPATHWRITE` |   | reserved | reserved |    
`DLURLSCHEME` |   | reserved | reserved |    
`DLURLSERVER` |   | reserved | reserved |    
`DLVALUE` |   | reserved | reserved |    
`DO` | reserved |   |   |    
`DOCUMENT` | non-reserved | non-reserved | non-reserved |    
`DOMAIN` | non-reserved | non-reserved | non-reserved | reserved  
`DOUBLE` | non-reserved | reserved | reserved | reserved  
`DROP` | non-reserved | reserved | reserved | reserved  
`DYNAMIC` |   | reserved | reserved |    
`DYNAMIC_FUNCTION` |   | non-reserved | non-reserved | non-reserved  
`DYNAMIC_​FUNCTION_​CODE` |   | non-reserved | non-reserved |    
`EACH` | non-reserved | reserved | reserved |    
`ELEMENT` |   | reserved | reserved |    
`ELSE` | reserved | reserved | reserved | reserved  
`EMPTY` |   | reserved | reserved |    
`ENABLE` | non-reserved |   |   |    
`ENCODING` | non-reserved | non-reserved | non-reserved |    
`ENCRYPTED` | non-reserved |   |   |    
`END` | reserved | reserved | reserved | reserved  
`END-EXEC` |   | reserved | reserved | reserved  
`END_FRAME` |   | reserved | reserved |    
`END_PARTITION` |   | reserved | reserved |    
`ENFORCED` |   | non-reserved | non-reserved |    
`ENUM` | non-reserved |   |   |    
`EQUALS` |   | reserved | reserved |    
`ERROR` |   | non-reserved | non-reserved |    
`ESCAPE` | non-reserved | reserved | reserved | reserved  
`EVENT` | non-reserved |   |   |    
`EVERY` |   | reserved | reserved |    
`EXCEPT` | reserved, requires `AS` | reserved | reserved | reserved  
`EXCEPTION` |   |   |   | reserved  
`EXCLUDE` | non-reserved | non-reserved | non-reserved |    
`EXCLUDING` | non-reserved | non-reserved | non-reserved |    
`EXCLUSIVE` | non-reserved |   |   |    
`EXEC` |   | reserved | reserved | reserved  
`EXECUTE` | non-reserved | reserved | reserved | reserved  
`EXISTS` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`EXP` |   | reserved | reserved |    
`EXPLAIN` | non-reserved |   |   |    
`EXPRESSION` | non-reserved | non-reserved | non-reserved |    
`EXTENSION` | non-reserved |   |   |    
`EXTERNAL` | non-reserved | reserved | reserved | reserved  
`EXTRACT` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`FALSE` | reserved | reserved | reserved | reserved  
`FAMILY` | non-reserved |   |   |    
`FETCH` | reserved, requires `AS` | reserved | reserved | reserved  
`FILE` |   | non-reserved | non-reserved |    
`FILTER` | non-reserved, requires `AS` | reserved | reserved |    
`FINAL` |   | non-reserved | non-reserved |    
`FINALIZE` | non-reserved |   |   |    
`FINISH` |   | non-reserved | non-reserved |    
`FIRST` | non-reserved | non-reserved | non-reserved | reserved  
`FIRST_VALUE` |   | reserved | reserved |    
`FLAG` |   | non-reserved | non-reserved |    
`FLOAT` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`FLOOR` |   | reserved | reserved |    
`FOLLOWING` | non-reserved | non-reserved | non-reserved |    
`FOR` | reserved, requires `AS` | reserved | reserved | reserved  
`FORCE` | non-reserved |   |   |    
`FOREIGN` | reserved | reserved | reserved | reserved  
`FORMAT` | non-reserved | non-reserved | non-reserved |    
`FORTRAN` |   | non-reserved | non-reserved | non-reserved  
`FORWARD` | non-reserved |   |   |    
`FOUND` |   | non-reserved | non-reserved | reserved  
`FRAME_ROW` |   | reserved | reserved |    
`FREE` |   | reserved | reserved |    
`FREEZE` | reserved (can be function or type) |   |   |    
`FROM` | reserved, requires `AS` | reserved | reserved | reserved  
`FS` |   | non-reserved | non-reserved |    
`FULFILL` |   | non-reserved | non-reserved |    
`FULL` | reserved (can be function or type) | reserved | reserved | reserved  
`FUNCTION` | non-reserved | reserved | reserved |    
`FUNCTIONS` | non-reserved |   |   |    
`FUSION` |   | reserved | reserved |    
`G` |   | non-reserved | non-reserved |    
`GENERAL` |   | non-reserved | non-reserved |    
`GENERATED` | non-reserved | non-reserved | non-reserved |    
`GET` |   | reserved | reserved | reserved  
`GLOBAL` | non-reserved | reserved | reserved | reserved  
`GO` |   | non-reserved | non-reserved | reserved  
`GOTO` |   | non-reserved | non-reserved | reserved  
`GRANT` | reserved, requires `AS` | reserved | reserved | reserved  
`GRANTED` | non-reserved | non-reserved | non-reserved |    
`GREATEST` | non-reserved (cannot be function or type) | reserved |   |    
`GROUP` | reserved, requires `AS` | reserved | reserved | reserved  
`GROUPING` | non-reserved (cannot be function or type) | reserved | reserved |    
`GROUPS` | non-reserved | reserved | reserved |    
`HANDLER` | non-reserved |   |   |    
`HAVING` | reserved, requires `AS` | reserved | reserved | reserved  
`HEADER` | non-reserved |   |   |    
`HEX` |   | non-reserved | non-reserved |    
`HIERARCHY` |   | non-reserved | non-reserved |    
`HOLD` | non-reserved | reserved | reserved |    
`HOUR` | non-reserved, requires `AS` | reserved | reserved | reserved  
`ID` |   | non-reserved | non-reserved |    
`IDENTITY` | non-reserved | reserved | reserved | reserved  
`IF` | non-reserved |   |   |    
`IGNORE` |   | non-reserved | non-reserved |    
`ILIKE` | reserved (can be function or type) |   |   |    
`IMMEDIATE` | non-reserved | non-reserved | non-reserved | reserved  
`IMMEDIATELY` |   | non-reserved | non-reserved |    
`IMMUTABLE` | non-reserved |   |   |    
`IMPLEMENTATION` |   | non-reserved | non-reserved |    
`IMPLICIT` | non-reserved |   |   |    
`IMPORT` | non-reserved | reserved | reserved |    
`IN` | reserved | reserved | reserved | reserved  
`INCLUDE` | non-reserved |   |   |    
`INCLUDING` | non-reserved | non-reserved | non-reserved |    
`INCREMENT` | non-reserved | non-reserved | non-reserved |    
`INDENT` | non-reserved | non-reserved | non-reserved |    
`INDEX` | non-reserved |   |   |    
`INDEXES` | non-reserved |   |   |    
`INDICATOR` |   | reserved | reserved | reserved  
`INHERIT` | non-reserved |   |   |    
`INHERITS` | non-reserved |   |   |    
`INITIAL` |   | reserved | reserved |    
`INITIALLY` | reserved | non-reserved | non-reserved | reserved  
`INLINE` | non-reserved |   |   |    
`INNER` | reserved (can be function or type) | reserved | reserved | reserved  
`INOUT` | non-reserved (cannot be function or type) | reserved | reserved |    
`INPUT` | non-reserved | non-reserved | non-reserved | reserved  
`INSENSITIVE` | non-reserved | reserved | reserved | reserved  
`INSERT` | non-reserved | reserved | reserved | reserved  
`INSTANCE` |   | non-reserved | non-reserved |    
`INSTANTIABLE` |   | non-reserved | non-reserved |    
`INSTEAD` | non-reserved | non-reserved | non-reserved |    
`INT` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`INTEGER` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`INTEGRITY` |   | non-reserved | non-reserved |    
`INTERSECT` | reserved, requires `AS` | reserved | reserved | reserved  
`INTERSECTION` |   | reserved | reserved |    
`INTERVAL` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`INTO` | reserved, requires `AS` | reserved | reserved | reserved  
`INVOKER` | non-reserved | non-reserved | non-reserved |    
`IS` | reserved (can be function or type) | reserved | reserved | reserved  
`ISNULL` | reserved (can be function or type), requires `AS` |   |   |    
`ISOLATION` | non-reserved | non-reserved | non-reserved | reserved  
`JOIN` | reserved (can be function or type) | reserved | reserved | reserved  
`JSON` | non-reserved | reserved |   |    
`JSON_ARRAY` | non-reserved (cannot be function or type) | reserved | reserved |    
`JSON_ARRAYAGG` | non-reserved (cannot be function or type) | reserved | reserved |    
`JSON_EXISTS` |   | reserved | reserved |    
`JSON_OBJECT` | non-reserved (cannot be function or type) | reserved | reserved |    
`JSON_OBJECTAGG` | non-reserved (cannot be function or type) | reserved | reserved |    
`JSON_QUERY` |   | reserved | reserved |    
`JSON_SCALAR` |   | reserved |   |    
`JSON_SERIALIZE` |   | reserved |   |    
`JSON_TABLE` |   | reserved | reserved |    
`JSON_TABLE_PRIMITIVE` |   | reserved | reserved |    
`JSON_VALUE` |   | reserved | reserved |    
`K` |   | non-reserved | non-reserved |    
`KEEP` |   | non-reserved | non-reserved |    
`KEY` | non-reserved | non-reserved | non-reserved | reserved  
`KEYS` | non-reserved | non-reserved | non-reserved |    
`KEY_MEMBER` |   | non-reserved | non-reserved |    
`KEY_TYPE` |   | non-reserved | non-reserved |    
`LABEL` | non-reserved |   |   |    
`LAG` |   | reserved | reserved |    
`LANGUAGE` | non-reserved | reserved | reserved | reserved  
`LARGE` | non-reserved | reserved | reserved |    
`LAST` | non-reserved | non-reserved | non-reserved | reserved  
`LAST_VALUE` |   | reserved | reserved |    
`LATERAL` | reserved | reserved | reserved |    
`LEAD` |   | reserved | reserved |    
`LEADING` | reserved | reserved | reserved | reserved  
`LEAKPROOF` | non-reserved |   |   |    
`LEAST` | non-reserved (cannot be function or type) | reserved |   |    
`LEFT` | reserved (can be function or type) | reserved | reserved | reserved  
`LENGTH` |   | non-reserved | non-reserved | non-reserved  
`LEVEL` | non-reserved | non-reserved | non-reserved | reserved  
`LIBRARY` |   | non-reserved | non-reserved |    
`LIKE` | reserved (can be function or type) | reserved | reserved | reserved  
`LIKE_REGEX` |   | reserved | reserved |    
`LIMIT` | reserved, requires `AS` | non-reserved | non-reserved |    
`LINK` |   | non-reserved | non-reserved |    
`LISTAGG` |   | reserved | reserved |    
`LISTEN` | non-reserved |   |   |    
`LN` |   | reserved | reserved |    
`LOAD` | non-reserved |   |   |    
`LOCAL` | non-reserved | reserved | reserved | reserved  
`LOCALTIME` | reserved | reserved | reserved |    
`LOCALTIMESTAMP` | reserved | reserved | reserved |    
`LOCATION` | non-reserved | non-reserved | non-reserved |    
`LOCATOR` |   | non-reserved | non-reserved |    
`LOCK` | non-reserved |   |   |    
`LOCKED` | non-reserved |   |   |    
`LOG` |   | reserved | reserved |    
`LOG10` |   | reserved | reserved |    
`LOGGED` | non-reserved |   |   |    
`LOWER` |   | reserved | reserved | reserved  
`LPAD` |   | reserved |   |    
`LTRIM` |   | reserved |   |    
`M` |   | non-reserved | non-reserved |    
`MAP` |   | non-reserved | non-reserved |    
`MAPPING` | non-reserved | non-reserved | non-reserved |    
`MATCH` | non-reserved | reserved | reserved | reserved  
`MATCHED` | non-reserved | non-reserved | non-reserved |    
`MATCHES` |   | reserved | reserved |    
`MATCH_NUMBER` |   | reserved | reserved |    
`MATCH_RECOGNIZE` |   | reserved | reserved |    
`MATERIALIZED` | non-reserved |   |   |    
`MAX` |   | reserved | reserved | reserved  
`MAXVALUE` | non-reserved | non-reserved | non-reserved |    
`MEASURES` |   | non-reserved | non-reserved |    
`MEMBER` |   | reserved | reserved |    
`MERGE` | non-reserved | reserved | reserved |    
`MESSAGE_LENGTH` |   | non-reserved | non-reserved | non-reserved  
`MESSAGE_OCTET_LENGTH` |   | non-reserved | non-reserved | non-reserved  
`MESSAGE_TEXT` |   | non-reserved | non-reserved | non-reserved  
`METHOD` | non-reserved | reserved | reserved |    
`MIN` |   | reserved | reserved | reserved  
`MINUTE` | non-reserved, requires `AS` | reserved | reserved | reserved  
`MINVALUE` | non-reserved | non-reserved | non-reserved |    
`MOD` |   | reserved | reserved |    
`MODE` | non-reserved |   |   |    
`MODIFIES` |   | reserved | reserved |    
`MODULE` |   | reserved | reserved | reserved  
`MONTH` | non-reserved, requires `AS` | reserved | reserved | reserved  
`MORE` |   | non-reserved | non-reserved | non-reserved  
`MOVE` | non-reserved |   |   |    
`MULTISET` |   | reserved | reserved |    
`MUMPS` |   | non-reserved | non-reserved | non-reserved  
`NAME` | non-reserved | non-reserved | non-reserved | non-reserved  
`NAMES` | non-reserved | non-reserved | non-reserved | reserved  
`NAMESPACE` |   | non-reserved | non-reserved |    
`NATIONAL` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`NATURAL` | reserved (can be function or type) | reserved | reserved | reserved  
`NCHAR` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`NCLOB` |   | reserved | reserved |    
`NESTED` |   | non-reserved | non-reserved |    
`NESTING` |   | non-reserved | non-reserved |    
`NEW` | non-reserved | reserved | reserved |    
`NEXT` | non-reserved | non-reserved | non-reserved | reserved  
`NFC` | non-reserved | non-reserved | non-reserved |    
`NFD` | non-reserved | non-reserved | non-reserved |    
`NFKC` | non-reserved | non-reserved | non-reserved |    
`NFKD` | non-reserved | non-reserved | non-reserved |    
`NIL` |   | non-reserved | non-reserved |    
`NO` | non-reserved | reserved | reserved | reserved  
`NONE` | non-reserved (cannot be function or type) | reserved | reserved |    
`NORMALIZE` | non-reserved (cannot be function or type) | reserved | reserved |    
`NORMALIZED` | non-reserved | non-reserved | non-reserved |    
`NOT` | reserved | reserved | reserved | reserved  
`NOTHING` | non-reserved |   |   |    
`NOTIFY` | non-reserved |   |   |    
`NOTNULL` | reserved (can be function or type), requires `AS` |   |   |    
`NOWAIT` | non-reserved |   |   |    
`NTH_VALUE` |   | reserved | reserved |    
`NTILE` |   | reserved | reserved |    
`NULL` | reserved | reserved | reserved | reserved  
`NULLABLE` |   | non-reserved | non-reserved | non-reserved  
`NULLIF` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`NULLS` | non-reserved | non-reserved | non-reserved |    
`NULL_ORDERING` |   | non-reserved | non-reserved |    
`NUMBER` |   | non-reserved | non-reserved | non-reserved  
`NUMERIC` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`OBJECT` | non-reserved | non-reserved | non-reserved |    
`OCCURRENCE` |   | non-reserved | non-reserved |    
`OCCURRENCES_REGEX` |   | reserved | reserved |    
`OCTETS` |   | non-reserved | non-reserved |    
`OCTET_LENGTH` |   | reserved | reserved | reserved  
`OF` | non-reserved | reserved | reserved | reserved  
`OFF` | non-reserved | non-reserved | non-reserved |    
`OFFSET` | reserved, requires `AS` | reserved | reserved |    
`OIDS` | non-reserved |   |   |    
`OLD` | non-reserved | reserved | reserved |    
`OMIT` |   | reserved | reserved |    
`ON` | reserved, requires `AS` | reserved | reserved | reserved  
`ONE` |   | reserved | reserved |    
`ONLY` | reserved | reserved | reserved | reserved  
`OPEN` |   | reserved | reserved | reserved  
`OPERATOR` | non-reserved |   |   |    
`OPTION` | non-reserved | non-reserved | non-reserved | reserved  
`OPTIONS` | non-reserved | non-reserved | non-reserved |    
`OR` | reserved | reserved | reserved | reserved  
`ORDER` | reserved, requires `AS` | reserved | reserved | reserved  
`ORDERING` |   | non-reserved | non-reserved |    
`ORDINALITY` | non-reserved | non-reserved | non-reserved |    
`OTHERS` | non-reserved | non-reserved | non-reserved |    
`OUT` | non-reserved (cannot be function or type) | reserved | reserved |    
`OUTER` | reserved (can be function or type) | reserved | reserved | reserved  
`OUTPUT` |   | non-reserved | non-reserved | reserved  
`OVER` | non-reserved, requires `AS` | reserved | reserved |    
`OVERFLOW` |   | non-reserved | non-reserved |    
`OVERLAPS` | reserved (can be function or type), requires `AS` | reserved | reserved | reserved  
`OVERLAY` | non-reserved (cannot be function or type) | reserved | reserved |    
`OVERRIDING` | non-reserved | non-reserved | non-reserved |    
`OWNED` | non-reserved |   |   |    
`OWNER` | non-reserved |   |   |    
`P` |   | non-reserved | non-reserved |    
`PAD` |   | non-reserved | non-reserved | reserved  
`PARALLEL` | non-reserved |   |   |    
`PARAMETER` | non-reserved | reserved | reserved |    
`PARAMETER_MODE` |   | non-reserved | non-reserved |    
`PARAMETER_NAME` |   | non-reserved | non-reserved |    
`PARAMETER_​ORDINAL_​POSITION` |   | non-reserved | non-reserved |    
`PARAMETER_​SPECIFIC_​CATALOG` |   | non-reserved | non-reserved |    
`PARAMETER_​SPECIFIC_​NAME` |   | non-reserved | non-reserved |    
`PARAMETER_​SPECIFIC_​SCHEMA` |   | non-reserved | non-reserved |    
`PARSER` | non-reserved |   |   |    
`PARTIAL` | non-reserved | non-reserved | non-reserved | reserved  
`PARTITION` | non-reserved | reserved | reserved |    
`PASCAL` |   | non-reserved | non-reserved | non-reserved  
`PASS` |   | non-reserved | non-reserved |    
`PASSING` | non-reserved | non-reserved | non-reserved |    
`PASSTHROUGH` |   | non-reserved | non-reserved |    
`PASSWORD` | non-reserved |   |   |    
`PAST` |   | non-reserved | non-reserved |    
`PATH` |   | non-reserved | non-reserved |    
`PATTERN` |   | reserved | reserved |    
`PER` |   | reserved | reserved |    
`PERCENT` |   | reserved | reserved |    
`PERCENTILE_CONT` |   | reserved | reserved |    
`PERCENTILE_DISC` |   | reserved | reserved |    
`PERCENT_RANK` |   | reserved | reserved |    
`PERIOD` |   | reserved | reserved |    
`PERMISSION` |   | non-reserved | non-reserved |    
`PERMUTE` |   | non-reserved | non-reserved |    
`PIPE` |   | non-reserved | non-reserved |    
`PLACING` | reserved | non-reserved | non-reserved |    
`PLAN` |   | non-reserved | non-reserved |    
`PLANS` | non-reserved |   |   |    
`PLI` |   | non-reserved | non-reserved | non-reserved  
`POLICY` | non-reserved |   |   |    
`PORTION` |   | reserved | reserved |    
`POSITION` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`POSITION_REGEX` |   | reserved | reserved |    
`POWER` |   | reserved | reserved |    
`PRECEDES` |   | reserved | reserved |    
`PRECEDING` | non-reserved | non-reserved | non-reserved |    
`PRECISION` | non-reserved (cannot be function or type), requires `AS` | reserved | reserved | reserved  
`PREPARE` | non-reserved | reserved | reserved | reserved  
`PREPARED` | non-reserved |   |   |    
`PRESERVE` | non-reserved | non-reserved | non-reserved | reserved  
`PREV` |   | non-reserved | non-reserved |    
`PRIMARY` | reserved | reserved | reserved | reserved  
`PRIOR` | non-reserved | non-reserved | non-reserved | reserved  
`PRIVATE` |   | non-reserved | non-reserved |    
`PRIVILEGES` | non-reserved | non-reserved | non-reserved | reserved  
`PROCEDURAL` | non-reserved |   |   |    
`PROCEDURE` | non-reserved | reserved | reserved | reserved  
`PROCEDURES` | non-reserved |   |   |    
`PROGRAM` | non-reserved |   |   |    
`PRUNE` |   | non-reserved | non-reserved |    
`PTF` |   | reserved | reserved |    
`PUBLIC` |   | non-reserved | non-reserved | reserved  
`PUBLICATION` | non-reserved |   |   |    
`QUOTE` | non-reserved |   |   |    
`QUOTES` |   | non-reserved | non-reserved |    
`RANGE` | non-reserved | reserved | reserved |    
`RANK` |   | reserved | reserved |    
`READ` | non-reserved | non-reserved | non-reserved | reserved  
`READS` |   | reserved | reserved |    
`REAL` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`REASSIGN` | non-reserved |   |   |    
`RECHECK` | non-reserved |   |   |    
`RECOVERY` |   | non-reserved | non-reserved |    
`RECURSIVE` | non-reserved | reserved | reserved |    
`REF` | non-reserved | reserved | reserved |    
`REFERENCES` | reserved | reserved | reserved | reserved  
`REFERENCING` | non-reserved | reserved | reserved |    
`REFRESH` | non-reserved |   |   |    
`REGR_AVGX` |   | reserved | reserved |    
`REGR_AVGY` |   | reserved | reserved |    
`REGR_COUNT` |   | reserved | reserved |    
`REGR_INTERCEPT` |   | reserved | reserved |    
`REGR_R2` |   | reserved | reserved |    
`REGR_SLOPE` |   | reserved | reserved |    
`REGR_SXX` |   | reserved | reserved |    
`REGR_SXY` |   | reserved | reserved |    
`REGR_SYY` |   | reserved | reserved |    
`REINDEX` | non-reserved |   |   |    
`RELATIVE` | non-reserved | non-reserved | non-reserved | reserved  
`RELEASE` | non-reserved | reserved | reserved |    
`RENAME` | non-reserved |   |   |    
`REPEATABLE` | non-reserved | non-reserved | non-reserved | non-reserved  
`REPLACE` | non-reserved |   |   |    
`REPLICA` | non-reserved |   |   |    
`REQUIRING` |   | non-reserved | non-reserved |    
`RESET` | non-reserved |   |   |    
`RESPECT` |   | non-reserved | non-reserved |    
`RESTART` | non-reserved | non-reserved | non-reserved |    
`RESTORE` |   | non-reserved | non-reserved |    
`RESTRICT` | non-reserved | non-reserved | non-reserved | reserved  
`RESULT` |   | reserved | reserved |    
`RETURN` | non-reserved | reserved | reserved |    
`RETURNED_CARDINALITY` |   | non-reserved | non-reserved |    
`RETURNED_LENGTH` |   | non-reserved | non-reserved | non-reserved  
`RETURNED_​OCTET_​LENGTH` |   | non-reserved | non-reserved | non-reserved  
`RETURNED_SQLSTATE` |   | non-reserved | non-reserved | non-reserved  
`RETURNING` | reserved, requires `AS` | non-reserved | non-reserved |    
`RETURNS` | non-reserved | reserved | reserved |    
`REVOKE` | non-reserved | reserved | reserved | reserved  
`RIGHT` | reserved (can be function or type) | reserved | reserved | reserved  
`ROLE` | non-reserved | non-reserved | non-reserved |    
`ROLLBACK` | non-reserved | reserved | reserved | reserved  
`ROLLUP` | non-reserved | reserved | reserved |    
`ROUTINE` | non-reserved | non-reserved | non-reserved |    
`ROUTINES` | non-reserved |   |   |    
`ROUTINE_CATALOG` |   | non-reserved | non-reserved |    
`ROUTINE_NAME` |   | non-reserved | non-reserved |    
`ROUTINE_SCHEMA` |   | non-reserved | non-reserved |    
`ROW` | non-reserved (cannot be function or type) | reserved | reserved |    
`ROWS` | non-reserved | reserved | reserved | reserved  
`ROW_COUNT` |   | non-reserved | non-reserved | non-reserved  
`ROW_NUMBER` |   | reserved | reserved |    
`RPAD` |   | reserved |   |    
`RTRIM` |   | reserved |   |    
`RULE` | non-reserved |   |   |    
`RUNNING` |   | reserved | reserved |    
`SAVEPOINT` | non-reserved | reserved | reserved |    
`SCALAR` | non-reserved | non-reserved | non-reserved |    
`SCALE` |   | non-reserved | non-reserved | non-reserved  
`SCHEMA` | non-reserved | non-reserved | non-reserved | reserved  
`SCHEMAS` | non-reserved |   |   |    
`SCHEMA_NAME` |   | non-reserved | non-reserved | non-reserved  
`SCOPE` |   | reserved | reserved |    
`SCOPE_CATALOG` |   | non-reserved | non-reserved |    
`SCOPE_NAME` |   | non-reserved | non-reserved |    
`SCOPE_SCHEMA` |   | non-reserved | non-reserved |    
`SCROLL` | non-reserved | reserved | reserved | reserved  
`SEARCH` | non-reserved | reserved | reserved |    
`SECOND` | non-reserved, requires `AS` | reserved | reserved | reserved  
`SECTION` |   | non-reserved | non-reserved | reserved  
`SECURITY` | non-reserved | non-reserved | non-reserved |    
`SEEK` |   | reserved | reserved |    
`SELECT` | reserved | reserved | reserved | reserved  
`SELECTIVE` |   | non-reserved | non-reserved |    
`SELF` |   | non-reserved | non-reserved |    
`SEMANTICS` |   | non-reserved | non-reserved |    
`SENSITIVE` |   | reserved | reserved |    
`SEQUENCE` | non-reserved | non-reserved | non-reserved |    
`SEQUENCES` | non-reserved |   |   |    
`SERIALIZABLE` | non-reserved | non-reserved | non-reserved | non-reserved  
`SERVER` | non-reserved | non-reserved | non-reserved |    
`SERVER_NAME` |   | non-reserved | non-reserved | non-reserved  
`SESSION` | non-reserved | non-reserved | non-reserved | reserved  
`SESSION_USER` | reserved | reserved | reserved | reserved  
`SET` | non-reserved | reserved | reserved | reserved  
`SETOF` | non-reserved (cannot be function or type) |   |   |    
`SETS` | non-reserved | non-reserved | non-reserved |    
`SHARE` | non-reserved |   |   |    
`SHOW` | non-reserved | reserved | reserved |    
`SIMILAR` | reserved (can be function or type) | reserved | reserved |    
`SIMPLE` | non-reserved | non-reserved | non-reserved |    
`SIN` |   | reserved | reserved |    
`SINH` |   | reserved | reserved |    
`SIZE` |   | non-reserved | non-reserved | reserved  
`SKIP` | non-reserved | reserved | reserved |    
`SMALLINT` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`SNAPSHOT` | non-reserved |   |   |    
`SOME` | reserved | reserved | reserved | reserved  
`SORT_DIRECTION` |   | non-reserved | non-reserved |    
`SOURCE` |   | non-reserved | non-reserved |    
`SPACE` |   | non-reserved | non-reserved | reserved  
`SPECIFIC` |   | reserved | reserved |    
`SPECIFICTYPE` |   | reserved | reserved |    
`SPECIFIC_NAME` |   | non-reserved | non-reserved |    
`SQL` | non-reserved | reserved | reserved | reserved  
`SQLCODE` |   |   |   | reserved  
`SQLERROR` |   |   |   | reserved  
`SQLEXCEPTION` |   | reserved | reserved |    
`SQLSTATE` |   | reserved | reserved | reserved  
`SQLWARNING` |   | reserved | reserved |    
`SQRT` |   | reserved | reserved |    
`STABLE` | non-reserved |   |   |    
`STANDALONE` | non-reserved | non-reserved | non-reserved |    
`START` | non-reserved | reserved | reserved |    
`STATE` |   | non-reserved | non-reserved |    
`STATEMENT` | non-reserved | non-reserved | non-reserved |    
`STATIC` |   | reserved | reserved |    
`STATISTICS` | non-reserved |   |   |    
`STDDEV_POP` |   | reserved | reserved |    
`STDDEV_SAMP` |   | reserved | reserved |    
`STDIN` | non-reserved |   |   |    
`STDOUT` | non-reserved |   |   |    
`STORAGE` | non-reserved |   |   |    
`STORED` | non-reserved |   |   |    
`STRICT` | non-reserved |   |   |    
`STRING` |   | non-reserved | non-reserved |    
`STRIP` | non-reserved | non-reserved | non-reserved |    
`STRUCTURE` |   | non-reserved | non-reserved |    
`STYLE` |   | non-reserved | non-reserved |    
`SUBCLASS_ORIGIN` |   | non-reserved | non-reserved | non-reserved  
`SUBMULTISET` |   | reserved | reserved |    
`SUBSCRIPTION` | non-reserved |   |   |    
`SUBSET` |   | reserved | reserved |    
`SUBSTRING` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`SUBSTRING_REGEX` |   | reserved | reserved |    
`SUCCEEDS` |   | reserved | reserved |    
`SUM` |   | reserved | reserved | reserved  
`SUPPORT` | non-reserved |   |   |    
`SYMMETRIC` | reserved | reserved | reserved |    
`SYSID` | non-reserved |   |   |    
`SYSTEM` | non-reserved | reserved | reserved |    
`SYSTEM_TIME` |   | reserved | reserved |    
`SYSTEM_USER` | reserved | reserved | reserved | reserved  
`T` |   | non-reserved | non-reserved |    
`TABLE` | reserved | reserved | reserved | reserved  
`TABLES` | non-reserved |   |   |    
`TABLESAMPLE` | reserved (can be function or type) | reserved | reserved |    
`TABLESPACE` | non-reserved |   |   |    
`TABLE_NAME` |   | non-reserved | non-reserved | non-reserved  
`TAN` |   | reserved | reserved |    
`TANH` |   | reserved | reserved |    
`TEMP` | non-reserved |   |   |    
`TEMPLATE` | non-reserved |   |   |    
`TEMPORARY` | non-reserved | non-reserved | non-reserved | reserved  
`TEXT` | non-reserved |   |   |    
`THEN` | reserved | reserved | reserved | reserved  
`THROUGH` |   | non-reserved | non-reserved |    
`TIES` | non-reserved | non-reserved | non-reserved |    
`TIME` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`TIMESTAMP` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`TIMEZONE_HOUR` |   | reserved | reserved | reserved  
`TIMEZONE_MINUTE` |   | reserved | reserved | reserved  
`TO` | reserved, requires `AS` | reserved | reserved | reserved  
`TOKEN` |   | non-reserved | non-reserved |    
`TOP_LEVEL_COUNT` |   | non-reserved | non-reserved |    
`TRAILING` | reserved | reserved | reserved | reserved  
`TRANSACTION` | non-reserved | non-reserved | non-reserved | reserved  
`TRANSACTIONS_​COMMITTED` |   | non-reserved | non-reserved |    
`TRANSACTIONS_​ROLLED_​BACK` |   | non-reserved | non-reserved |    
`TRANSACTION_ACTIVE` |   | non-reserved | non-reserved |    
`TRANSFORM` | non-reserved | non-reserved | non-reserved |    
`TRANSFORMS` |   | non-reserved | non-reserved |    
`TRANSLATE` |   | reserved | reserved | reserved  
`TRANSLATE_REGEX` |   | reserved | reserved |    
`TRANSLATION` |   | reserved | reserved | reserved  
`TREAT` | non-reserved (cannot be function or type) | reserved | reserved |    
`TRIGGER` | non-reserved | reserved | reserved |    
`TRIGGER_CATALOG` |   | non-reserved | non-reserved |    
`TRIGGER_NAME` |   | non-reserved | non-reserved |    
`TRIGGER_SCHEMA` |   | non-reserved | non-reserved |    
`TRIM` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`TRIM_ARRAY` |   | reserved | reserved |    
`TRUE` | reserved | reserved | reserved | reserved  
`TRUNCATE` | non-reserved | reserved | reserved |    
`TRUSTED` | non-reserved |   |   |    
`TYPE` | non-reserved | non-reserved | non-reserved | non-reserved  
`TYPES` | non-reserved |   |   |    
`UESCAPE` | non-reserved | reserved | reserved |    
`UNBOUNDED` | non-reserved | non-reserved | non-reserved |    
`UNCOMMITTED` | non-reserved | non-reserved | non-reserved | non-reserved  
`UNCONDITIONAL` |   | non-reserved | non-reserved |    
`UNDER` |   | non-reserved | non-reserved |    
`UNENCRYPTED` | non-reserved |   |   |    
`UNION` | reserved, requires `AS` | reserved | reserved | reserved  
`UNIQUE` | reserved | reserved | reserved | reserved  
`UNKNOWN` | non-reserved | reserved | reserved | reserved  
`UNLINK` |   | non-reserved | non-reserved |    
`UNLISTEN` | non-reserved |   |   |    
`UNLOGGED` | non-reserved |   |   |    
`UNMATCHED` |   | non-reserved | non-reserved |    
`UNNAMED` |   | non-reserved | non-reserved | non-reserved  
`UNNEST` |   | reserved | reserved |    
`UNTIL` | non-reserved |   |   |    
`UNTYPED` |   | non-reserved | non-reserved |    
`UPDATE` | non-reserved | reserved | reserved | reserved  
`UPPER` |   | reserved | reserved | reserved  
`URI` |   | non-reserved | non-reserved |    
`USAGE` |   | non-reserved | non-reserved | reserved  
`USER` | reserved | reserved | reserved | reserved  
`USER_​DEFINED_​TYPE_​CATALOG` |   | non-reserved | non-reserved |    
`USER_​DEFINED_​TYPE_​CODE` |   | non-reserved | non-reserved |    
`USER_​DEFINED_​TYPE_​NAME` |   | non-reserved | non-reserved |    
`USER_​DEFINED_​TYPE_​SCHEMA` |   | non-reserved | non-reserved |    
`USING` | reserved | reserved | reserved | reserved  
`UTF16` |   | non-reserved | non-reserved |    
`UTF32` |   | non-reserved | non-reserved |    
`UTF8` |   | non-reserved | non-reserved |    
`VACUUM` | non-reserved |   |   |    
`VALID` | non-reserved | non-reserved | non-reserved |    
`VALIDATE` | non-reserved |   |   |    
`VALIDATOR` | non-reserved |   |   |    
`VALUE` | non-reserved | reserved | reserved | reserved  
`VALUES` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`VALUE_OF` |   | reserved | reserved |    
`VARBINARY` |   | reserved | reserved |    
`VARCHAR` | non-reserved (cannot be function or type) | reserved | reserved | reserved  
`VARIADIC` | reserved |   |   |    
`VARYING` | non-reserved, requires `AS` | reserved | reserved | reserved  
`VAR_POP` |   | reserved | reserved |    
`VAR_SAMP` |   | reserved | reserved |    
`VERBOSE` | reserved (can be function or type) |   |   |    
`VERSION` | non-reserved | non-reserved | non-reserved |    
`VERSIONING` |   | reserved | reserved |    
`VIEW` | non-reserved | non-reserved | non-reserved | reserved  
`VIEWS` | non-reserved |   |   |    
`VOLATILE` | non-reserved |   |   |    
`WHEN` | reserved | reserved | reserved | reserved  
`WHENEVER` |   | reserved | reserved | reserved  
`WHERE` | reserved, requires `AS` | reserved | reserved | reserved  
`WHITESPACE` | non-reserved | non-reserved | non-reserved |    
`WIDTH_BUCKET` |   | reserved | reserved |    
`WINDOW` | reserved, requires `AS` | reserved | reserved |    
`WITH` | reserved, requires `AS` | reserved | reserved | reserved  
`WITHIN` | non-reserved, requires `AS` | reserved | reserved |    
`WITHOUT` | non-reserved, requires `AS` | reserved | reserved |    
`WORK` | non-reserved | non-reserved | non-reserved | reserved  
`WRAPPER` | non-reserved | non-reserved | non-reserved |    
`WRITE` | non-reserved | non-reserved | non-reserved | reserved  
`XML` | non-reserved | reserved | reserved |    
`XMLAGG` |   | reserved | reserved |    
`XMLATTRIBUTES` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLBINARY` |   | reserved | reserved |    
`XMLCAST` |   | reserved | reserved |    
`XMLCOMMENT` |   | reserved | reserved |    
`XMLCONCAT` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLDECLARATION` |   | non-reserved | non-reserved |    
`XMLDOCUMENT` |   | reserved | reserved |    
`XMLELEMENT` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLEXISTS` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLFOREST` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLITERATE` |   | reserved | reserved |    
`XMLNAMESPACES` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLPARSE` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLPI` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLQUERY` |   | reserved | reserved |    
`XMLROOT` | non-reserved (cannot be function or type) |   |   |    
`XMLSCHEMA` |   | non-reserved | non-reserved |    
`XMLSERIALIZE` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLTABLE` | non-reserved (cannot be function or type) | reserved | reserved |    
`XMLTEXT` |   | reserved | reserved |    
`XMLVALIDATE` |   | reserved | reserved |    
`YEAR` | non-reserved, requires `AS` | reserved | reserved | reserved  
`YES` | non-reserved | non-reserved | non-reserved |    
`ZONE` | non-reserved | non-reserved | non-reserved | reserved  
  
  

* * *

[Prev](datetime-julian-dates.html "B.7. Julian Dates")  | [Up](appendixes.html "Part VIII. Appendixes") |  [Next](features.html "Appendix D. SQL Conformance")  
---|---|---  
B.7. Julian Dates  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix D. SQL Conformance  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-keywords-appendix.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

