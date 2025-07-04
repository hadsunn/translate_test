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

Supported Versions: [Current](/docs/current/ecpg-variables.html "PostgreSQL 17
- 36.4. Using Host Variables") ([17](/docs/17/ecpg-variables.html "PostgreSQL
17 - 36.4. Using Host Variables")) / [16](/docs/16/ecpg-variables.html
"PostgreSQL 16 - 36.4. Using Host Variables") / [15](/docs/15/ecpg-
variables.html "PostgreSQL 15 - 36.4. Using Host Variables") /
[14](/docs/14/ecpg-variables.html "PostgreSQL 14 - 36.4. Using Host
Variables") / [13](/docs/13/ecpg-variables.html "PostgreSQL 13 - 36.4. Using
Host Variables")

Development Versions: [18](/docs/18/ecpg-variables.html "PostgreSQL 18 -
36.4. Using Host Variables") / [devel](/docs/devel/ecpg-variables.html
"PostgreSQL devel - 36.4. Using Host Variables")

Unsupported versions: [12](/docs/12/ecpg-variables.html "PostgreSQL 12 -
36.4. Using Host Variables") / [11](/docs/11/ecpg-variables.html "PostgreSQL
11 - 36.4. Using Host Variables") / [10](/docs/10/ecpg-variables.html
"PostgreSQL 10 - 36.4. Using Host Variables") / [9.6](/docs/9.6/ecpg-
variables.html "PostgreSQL 9.6 - 36.4. Using Host Variables") /
[9.5](/docs/9.5/ecpg-variables.html "PostgreSQL 9.5 - 36.4. Using Host
Variables") / [9.4](/docs/9.4/ecpg-variables.html "PostgreSQL 9.4 -
36.4. Using Host Variables") / [9.3](/docs/9.3/ecpg-variables.html "PostgreSQL
9.3 - 36.4. Using Host Variables") / [9.2](/docs/9.2/ecpg-variables.html
"PostgreSQL 9.2 - 36.4. Using Host Variables") / [9.1](/docs/9.1/ecpg-
variables.html "PostgreSQL 9.1 - 36.4. Using Host Variables") /
[9.0](/docs/9.0/ecpg-variables.html "PostgreSQL 9.0 - 36.4. Using Host
Variables") / [8.4](/docs/8.4/ecpg-variables.html "PostgreSQL 8.4 -
36.4. Using Host Variables") / [8.3](/docs/8.3/ecpg-variables.html "PostgreSQL
8.3 - 36.4. Using Host Variables") / [8.2](/docs/8.2/ecpg-variables.html
"PostgreSQL 8.2 - 36.4. Using Host Variables") / [8.1](/docs/8.1/ecpg-
variables.html "PostgreSQL 8.1 - 36.4. Using Host Variables") /
[8.0](/docs/8.0/ecpg-variables.html "PostgreSQL 8.0 - 36.4. Using Host
Variables") / [7.4](/docs/7.4/ecpg-variables.html "PostgreSQL 7.4 -
36.4. Using Host Variables") / [7.3](/docs/7.3/ecpg-variables.html "PostgreSQL
7.3 - 36.4. Using Host Variables")

__

36.4. Using Host Variables  
---  
[Prev](ecpg-commands.html "36.3. Running SQL Commands")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-dynamic.html "36.5. Dynamic SQL")  
  
* * *

## 36.4. Using Host Variables #

[36.4.1. Overview](ecpg-variables.html#ECPG-VARIABLES-OVERVIEW)

[36.4.2. Declare Sections](ecpg-variables.html#ECPG-DECLARE-SECTIONS)

[36.4.3. Retrieving Query Results](ecpg-variables.html#ECPG-RETRIEVING)

[36.4.4. Type Mapping](ecpg-variables.html#ECPG-VARIABLES-TYPE-MAPPING)

[36.4.5. Handling Nonprimitive SQL Data Types](ecpg-variables.html#ECPG-
VARIABLES-NONPRIMITIVE-SQL)

[36.4.6. Indicators](ecpg-variables.html#ECPG-INDICATORS)

In [Section 36.3](ecpg-commands.html "36.3. Running SQL Commands") you saw how
you can execute SQL statements from an embedded SQL program. Some of those
statements only used fixed values and did not provide a way to insert user-
supplied values into statements or have the program process the values
returned by the query. Those kinds of statements are not really useful in real
applications. This section explains in detail how you can pass data between
your C program and the embedded SQL statements using a simple mechanism called
_host variables_. In an embedded SQL program we consider the SQL statements to
be _guests_ in the C program code which is the _host language_. Therefore the
variables of the C program are called _host variables_.

Another way to exchange values between PostgreSQL backends and ECPG
applications is the use of SQL descriptors, described in [Section 36.7](ecpg-
descriptors.html "36.7. Using Descriptor Areas").

### 36.4.1. Overview #

Passing data between the C program and the SQL statements is particularly
simple in embedded SQL. Instead of having the program paste the data into the
statement, which entails various complications, such as properly quoting the
value, you can simply write the name of a C variable into the SQL statement,
prefixed by a colon. For example:

    
    
    EXEC SQL INSERT INTO sometable VALUES (:v1, 'foo', :v2);
    

This statement refers to two C variables named `v1` and `v2` and also uses a
regular SQL string literal, to illustrate that you are not restricted to use
one kind of data or the other.

This style of inserting C variables in SQL statements works anywhere a value
expression is expected in an SQL statement.

### 36.4.2. Declare Sections #

To pass data from the program to the database, for example as parameters in a
query, or to pass data from the database back to the program, the C variables
that are intended to contain this data need to be declared in specially marked
sections, so the embedded SQL preprocessor is made aware of them.

This section starts with:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    

and ends with:

    
    
    EXEC SQL END DECLARE SECTION;
    

Between those lines, there must be normal C variable declarations, such as:

    
    
    int   x = 4;
    char  foo[16], bar[16];
    

As you can see, you can optionally assign an initial value to the variable.
The variable's scope is determined by the location of its declaring section
within the program. You can also declare variables with the following syntax
which implicitly creates a declare section:

    
    
    EXEC SQL int i = 4;
    

You can have as many declare sections in a program as you like.

The declarations are also echoed to the output file as normal C variables, so
there's no need to declare them again. Variables that are not intended to be
used in SQL commands can be declared normally outside these special sections.

The definition of a structure or union also must be listed inside a `DECLARE`
section. Otherwise the preprocessor cannot handle these types since it does
not know the definition.

### 36.4.3. Retrieving Query Results #

Now you should be able to pass data generated by your program into an SQL
command. But how do you retrieve the results of a query? For that purpose,
embedded SQL provides special variants of the usual commands `SELECT` and
`FETCH`. These commands have a special `INTO` clause that specifies which host
variables the retrieved values are to be stored in. `SELECT` is used for a
query that returns only single row, and `FETCH` is used for a query that
returns multiple rows, using a cursor.

Here is an example:

    
    
    /*
     * assume this table:
     * CREATE TABLE test1 (a int, b varchar(50));
     */
    
    EXEC SQL BEGIN DECLARE SECTION;
    int v1;
    VARCHAR v2;
    EXEC SQL END DECLARE SECTION;
    
     ...
    
    EXEC SQL SELECT a, b INTO :v1, :v2 FROM test;
    

So the `INTO` clause appears between the select list and the `FROM` clause.
The number of elements in the select list and the list after `INTO` (also
called the target list) must be equal.

Here is an example using the command `FETCH`:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    int v1;
    VARCHAR v2;
    EXEC SQL END DECLARE SECTION;
    
     ...
    
    EXEC SQL DECLARE foo CURSOR FOR SELECT a, b FROM test;
    
     ...
    
    do
    {
        ...
        EXEC SQL FETCH NEXT FROM foo INTO :v1, :v2;
        ...
    } while (...);
    

Here the `INTO` clause appears after all the normal clauses.

### 36.4.4. Type Mapping #

When ECPG applications exchange values between the PostgreSQL server and the C
application, such as when retrieving query results from the server or
executing SQL statements with input parameters, the values need to be
converted between PostgreSQL data types and host language variable types (C
language data types, concretely). One of the main points of ECPG is that it
takes care of this automatically in most cases.

In this respect, there are two kinds of data types: Some simple PostgreSQL
data types, such as `integer` and `text`, can be read and written by the
application directly. Other PostgreSQL data types, such as `timestamp` and
`numeric` can only be accessed through special library functions; see [Section
36.4.4.2](ecpg-variables.html#ECPG-SPECIAL-TYPES "36.4.4.2. Accessing Special
Data Types").

[Table 36.1](ecpg-variables.html#ECPG-DATATYPE-HOSTVARS-TABLE
"Table 36.1. Mapping Between PostgreSQL Data Types and C Variable Types")
shows which PostgreSQL data types correspond to which C data types. When you
wish to send or receive a value of a given PostgreSQL data type, you should
declare a C variable of the corresponding C data type in the declare section.

**Table  36.1. Mapping Between PostgreSQL Data Types and C Variable Types**

PostgreSQL data type | Host variable type  
---|---  
`smallint` | `short`  
`integer` | `int`  
`bigint` | `long long int`  
`decimal` | `decimal`[a]  
`numeric` | `numeric`[[a]](ecpg-variables.html#ftn.ECPG-DATATYPE-TABLE-FN)  
`real` | `float`  
`double precision` | `double`  
`smallserial` | `short`  
`serial` | `int`  
`bigserial` | `long long int`  
`oid` | `unsigned int`  
`character(_`n`_)`, `varchar(_`n`_)`, `text` | `char[_`n`_ +1]`, `VARCHAR[_`n`_ +1]`  
`name` | `char[NAMEDATALEN]`  
`timestamp` | `timestamp`[[a]](ecpg-variables.html#ftn.ECPG-DATATYPE-TABLE-FN)  
`interval` | `interval`[[a]](ecpg-variables.html#ftn.ECPG-DATATYPE-TABLE-FN)  
`date` | `date`[[a]](ecpg-variables.html#ftn.ECPG-DATATYPE-TABLE-FN)  
`boolean` | `bool`[b]  
`bytea` | `char *`, `bytea[_`n`_]`  
[a] This type can only be accessed through special library functions; see
[Section 36.4.4.2](ecpg-variables.html#ECPG-SPECIAL-TYPES "36.4.4.2. Accessing
Special Data Types"). [b] declared in `ecpglib.h` if not native  
  
  

#### 36.4.4.1. Handling Character Strings #

To handle SQL character string data types, such as `varchar` and `text`, there
are two possible ways to declare the host variables.

One way is using `char[]`, an array of `char`, which is the most common way to
handle character data in C.

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        char str[50];
    EXEC SQL END DECLARE SECTION;
    

Note that you have to take care of the length yourself. If you use this host
variable as the target variable of a query which returns a string with more
than 49 characters, a buffer overflow occurs.

The other way is using the `VARCHAR` type, which is a special type provided by
ECPG. The definition on an array of type `VARCHAR` is converted into a named
`struct` for every variable. A declaration like:

    
    
    VARCHAR var[180];
    

is converted into:

    
    
    struct varchar_var { int len; char arr[180]; } var;
    

The member `arr` hosts the string including a terminating zero byte. Thus, to
store a string in a `VARCHAR` host variable, the host variable has to be
declared with the length including the zero byte terminator. The member `len`
holds the length of the string stored in the `arr` without the terminating
zero byte. When a host variable is used as input for a query, if `strlen(arr)`
and `len` are different, the shorter one is used.

`VARCHAR` can be written in upper or lower case, but not in mixed case.

`char` and `VARCHAR` host variables can also hold values of other SQL types,
which will be stored in their string forms.

#### 36.4.4.2. Accessing Special Data Types #

ECPG contains some special types that help you to interact easily with some
special data types from the PostgreSQL server. In particular, it has
implemented support for the `numeric`, `decimal`, `date`, `timestamp`, and
`interval` types. These data types cannot usefully be mapped to primitive host
variable types (such as `int`, `long long int`, or `char[]`), because they
have a complex internal structure. Applications deal with these types by
declaring host variables in special types and accessing them using functions
in the pgtypes library. The pgtypes library, described in detail in [Section
36.6](ecpg-pgtypes.html "36.6. pgtypes Library") contains basic functions to
deal with those types, such that you do not need to send a query to the SQL
server just for adding an interval to a time stamp for example.

The follow subsections describe these special data types. For more details
about pgtypes library functions, see [Section 36.6](ecpg-pgtypes.html
"36.6. pgtypes Library").

##### 36.4.4.2.1. timestamp, date #

Here is a pattern for handling `timestamp` variables in the ECPG host
application.

First, the program has to include the header file for the `timestamp` type:

    
    
    #include <pgtypes_timestamp.h>
    

Next, declare a host variable as type `timestamp` in the declare section:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    timestamp ts;
    EXEC SQL END DECLARE SECTION;
    

And after reading a value into the host variable, process it using pgtypes
library functions. In following example, the `timestamp` value is converted
into text (ASCII) form with the `PGTYPEStimestamp_to_asc()` function:

    
    
    EXEC SQL SELECT now()::timestamp INTO :ts;
    
    printf("ts = %s\n", PGTYPEStimestamp_to_asc(ts));
    

This example will show some result like following:

    
    
    ts = 2010-06-27 18:03:56.949343
    

In addition, the DATE type can be handled in the same way. The program has to
include `pgtypes_date.h`, declare a host variable as the date type and convert
a DATE value into a text form using `PGTYPESdate_to_asc()` function. For more
details about the pgtypes library functions, see [Section 36.6](ecpg-
pgtypes.html "36.6. pgtypes Library").

##### 36.4.4.2.2. interval #

The handling of the `interval` type is also similar to the `timestamp` and
`date` types. It is required, however, to allocate memory for an `interval`
type value explicitly. In other words, the memory space for the variable has
to be allocated in the heap memory, not in the stack memory.

Here is an example program:

    
    
    #include <stdio.h>
    #include <stdlib.h>
    #include <pgtypes_interval.h>
    
    int
    main(void)
    {
    EXEC SQL BEGIN DECLARE SECTION;
        interval *in;
    EXEC SQL END DECLARE SECTION;
    
        EXEC SQL CONNECT TO testdb;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    
        in = PGTYPESinterval_new();
        EXEC SQL SELECT '1 min'::interval INTO :in;
        printf("interval = %s\n", PGTYPESinterval_to_asc(in));
        PGTYPESinterval_free(in);
    
        EXEC SQL COMMIT;
        EXEC SQL DISCONNECT ALL;
        return 0;
    }
    

##### 36.4.4.2.3. numeric, decimal #

The handling of the `numeric` and `decimal` types is similar to the `interval`
type: It requires defining a pointer, allocating some memory space on the
heap, and accessing the variable using the pgtypes library functions. For more
details about the pgtypes library functions, see [Section 36.6](ecpg-
pgtypes.html "36.6. pgtypes Library").

No functions are provided specifically for the `decimal` type. An application
has to convert it to a `numeric` variable using a pgtypes library function to
do further processing.

Here is an example program handling `numeric` and `decimal` type variables.

    
    
    #include <stdio.h>
    #include <stdlib.h>
    #include <pgtypes_numeric.h>
    
    EXEC SQL WHENEVER SQLERROR STOP;
    
    int
    main(void)
    {
    EXEC SQL BEGIN DECLARE SECTION;
        numeric *num;
        numeric *num2;
        decimal *dec;
    EXEC SQL END DECLARE SECTION;
    
        EXEC SQL CONNECT TO testdb;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    
        num = PGTYPESnumeric_new();
        dec = PGTYPESdecimal_new();
    
        EXEC SQL SELECT 12.345::numeric(4,2), 23.456::decimal(4,2) INTO :num, :dec;
    
        printf("numeric = %s\n", PGTYPESnumeric_to_asc(num, 0));
        printf("numeric = %s\n", PGTYPESnumeric_to_asc(num, 1));
        printf("numeric = %s\n", PGTYPESnumeric_to_asc(num, 2));
    
        /* Convert decimal to numeric to show a decimal value. */
        num2 = PGTYPESnumeric_new();
        PGTYPESnumeric_from_decimal(dec, num2);
    
        printf("decimal = %s\n", PGTYPESnumeric_to_asc(num2, 0));
        printf("decimal = %s\n", PGTYPESnumeric_to_asc(num2, 1));
        printf("decimal = %s\n", PGTYPESnumeric_to_asc(num2, 2));
    
        PGTYPESnumeric_free(num2);
        PGTYPESdecimal_free(dec);
        PGTYPESnumeric_free(num);
    
        EXEC SQL COMMIT;
        EXEC SQL DISCONNECT ALL;
        return 0;
    }
    

##### 36.4.4.2.4. bytea #

The handling of the `bytea` type is similar to that of `VARCHAR`. The
definition on an array of type `bytea` is converted into a named struct for
every variable. A declaration like:

    
    
    bytea var[180];
    

is converted into:

    
    
    struct bytea_var { int len; char arr[180]; } var;
    

The member `arr` hosts binary format data. It can also handle `'\0'` as part
of data, unlike `VARCHAR`. The data is converted from/to hex format and
sent/received by ecpglib.

### Note

`bytea` variable can be used only when [bytea_output](runtime-config-
client.html#GUC-BYTEA-OUTPUT) is set to `hex`.

#### 36.4.4.3. Host Variables with Nonprimitive Types #

As a host variable you can also use arrays, typedefs, structs, and pointers.

##### 36.4.4.3.1. Arrays #

There are two use cases for arrays as host variables. The first is a way to
store some text string in `char[]` or `VARCHAR[]`, as explained in [Section
36.4.4.1](ecpg-variables.html#ECPG-CHAR "36.4.4.1. Handling Character
Strings"). The second use case is to retrieve multiple rows from a query
result without using a cursor. Without an array, to process a query result
consisting of multiple rows, it is required to use a cursor and the `FETCH`
command. But with array host variables, multiple rows can be received at once.
The length of the array has to be defined to be able to accommodate all rows,
otherwise a buffer overflow will likely occur.

Following example scans the `pg_database` system table and shows all OIDs and
names of the available databases:

    
    
    int
    main(void)
    {
    EXEC SQL BEGIN DECLARE SECTION;
        int dbid[8];
        char dbname[8][16];
        int i;
    EXEC SQL END DECLARE SECTION;
    
        memset(dbname, 0, sizeof(char)* 16 * 8);
        memset(dbid, 0, sizeof(int) * 8);
    
        EXEC SQL CONNECT TO testdb;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    
        /* Retrieve multiple rows into arrays at once. */
        EXEC SQL SELECT oid,datname INTO :dbid, :dbname FROM pg_database;
    
        for (i = 0; i < 8; i++)
            printf("oid=%d, dbname=%s\n", dbid[i], dbname[i]);
    
        EXEC SQL COMMIT;
        EXEC SQL DISCONNECT ALL;
        return 0;
    }
    

This example shows following result. (The exact values depend on local
circumstances.)

    
    
    oid=1, dbname=template1
    oid=11510, dbname=template0
    oid=11511, dbname=postgres
    oid=313780, dbname=testdb
    oid=0, dbname=
    oid=0, dbname=
    oid=0, dbname=
    

##### 36.4.4.3.2. Structures #

A structure whose member names match the column names of a query result, can
be used to retrieve multiple columns at once. The structure enables handling
multiple column values in a single host variable.

The following example retrieves OIDs, names, and sizes of the available
databases from the `pg_database` system table and using the
`pg_database_size()` function. In this example, a structure variable
`dbinfo_t` with members whose names match each column in the `SELECT` result
is used to retrieve one result row without putting multiple host variables in
the `FETCH` statement.

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        typedef struct
        {
           int oid;
           char datname[65];
           long long int size;
        } dbinfo_t;
    
        dbinfo_t dbval;
    EXEC SQL END DECLARE SECTION;
    
        memset(&dbval, 0, sizeof(dbinfo_t));
    
        EXEC SQL DECLARE cur1 CURSOR FOR SELECT oid, datname, pg_database_size(oid) AS size FROM pg_database;
        EXEC SQL OPEN cur1;
    
        /* when end of result set reached, break out of while loop */
        EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
        while (1)
        {
            /* Fetch multiple columns into one structure. */
            EXEC SQL FETCH FROM cur1 INTO :dbval;
    
            /* Print members of the structure. */
            printf("oid=%d, datname=%s, size=%lld\n", dbval.oid, dbval.datname, dbval.size);
        }
    
        EXEC SQL CLOSE cur1;
    

This example shows following result. (The exact values depend on local
circumstances.)

    
    
    oid=1, datname=template1, size=4324580
    oid=11510, datname=template0, size=4243460
    oid=11511, datname=postgres, size=4324580
    oid=313780, datname=testdb, size=8183012
    

Structure host variables “absorb” as many columns as the structure as fields.
Additional columns can be assigned to other host variables. For example, the
above program could also be restructured like this, with the `size` variable
outside the structure:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        typedef struct
        {
           int oid;
           char datname[65];
        } dbinfo_t;
    
        dbinfo_t dbval;
        long long int size;
    EXEC SQL END DECLARE SECTION;
    
        memset(&dbval, 0, sizeof(dbinfo_t));
    
        EXEC SQL DECLARE cur1 CURSOR FOR SELECT oid, datname, pg_database_size(oid) AS size FROM pg_database;
        EXEC SQL OPEN cur1;
    
        /* when end of result set reached, break out of while loop */
        EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
        while (1)
        {
            /* Fetch multiple columns into one structure. */
            EXEC SQL FETCH FROM cur1 INTO :dbval, :size;
    
            /* Print members of the structure. */
            printf("oid=%d, datname=%s, size=%lld\n", dbval.oid, dbval.datname, size);
        }
    
        EXEC SQL CLOSE cur1;
    

##### 36.4.4.3.3. Typedefs #

Use the `typedef` keyword to map new types to already existing types.

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        typedef char mychartype[40];
        typedef long serial_t;
    EXEC SQL END DECLARE SECTION;
    

Note that you could also use:

    
    
    EXEC SQL TYPE serial_t IS long;
    

This declaration does not need to be part of a declare section; that is, you
can also write typedefs as normal C statements.

Any word you declare as a typedef cannot be used as an SQL keyword in `EXEC
SQL` commands later in the same program. For example, this won't work:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        typedef int start;
    EXEC SQL END DECLARE SECTION;
    ...
    EXEC SQL START TRANSACTION;
    

ECPG will report a syntax error for `START TRANSACTION`, because it no longer
recognizes `START` as an SQL keyword, only as a typedef. (If you have such a
conflict, and renaming the typedef seems impractical, you could write the SQL
command using [dynamic SQL](ecpg-dynamic.html "36.5. Dynamic SQL").)

### Note

In PostgreSQL releases before v16, use of SQL keywords as typedef names was
likely to result in syntax errors associated with use of the typedef itself,
rather than use of the name as an SQL keyword. The new behavior is less likely
to cause problems when an existing ECPG application is recompiled in a new
PostgreSQL release with new keywords.

##### 36.4.4.3.4. Pointers #

You can declare pointers to the most common types. Note however that you
cannot use pointers as target variables of queries without auto-allocation.
See [Section 36.7](ecpg-descriptors.html "36.7. Using Descriptor Areas") for
more information on auto-allocation.

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        int   *intp;
        char **charp;
    EXEC SQL END DECLARE SECTION;
    

### 36.4.5. Handling Nonprimitive SQL Data Types #

This section contains information on how to handle nonscalar and user-defined
SQL-level data types in ECPG applications. Note that this is distinct from the
handling of host variables of nonprimitive types, described in the previous
section.

#### 36.4.5.1. Arrays #

Multi-dimensional SQL-level arrays are not directly supported in ECPG. One-
dimensional SQL-level arrays can be mapped into C array host variables and
vice-versa. However, when creating a statement ecpg does not know the types of
the columns, so that it cannot check if a C array is input into a
corresponding SQL-level array. When processing the output of an SQL statement,
ecpg has the necessary information and thus checks if both are arrays.

If a query accesses _elements_ of an array separately, then this avoids the
use of arrays in ECPG. Then, a host variable with a type that can be mapped to
the element type should be used. For example, if a column type is array of
`integer`, a host variable of type `int` can be used. Also if the element type
is `varchar` or `text`, a host variable of type `char[]` or `VARCHAR[]` can be
used.

Here is an example. Assume the following table:

    
    
    CREATE TABLE t3 (
        ii integer[]
    );
    
    testdb=> SELECT * FROM t3;
         ii
    -------------
     {1,2,3,4,5}
    (1 row)
    

The following example program retrieves the 4th element of the array and
stores it into a host variable of type `int`:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    int ii;
    EXEC SQL END DECLARE SECTION;
    
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT ii[4] FROM t3;
    EXEC SQL OPEN cur1;
    
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    while (1)
    {
        EXEC SQL FETCH FROM cur1 INTO :ii ;
        printf("ii=%d\n", ii);
    }
    
    EXEC SQL CLOSE cur1;
    

This example shows the following result:

    
    
    ii=4
    

To map multiple array elements to the multiple elements in an array type host
variables each element of array column and each element of the host variable
array have to be managed separately, for example:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    int ii_a[8];
    EXEC SQL END DECLARE SECTION;
    
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT ii[1], ii[2], ii[3], ii[4] FROM t3;
    EXEC SQL OPEN cur1;
    
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    while (1)
    {
        EXEC SQL FETCH FROM cur1 INTO :ii_a[0], :ii_a[1], :ii_a[2], :ii_a[3];
        ...
    }
    

Note again that

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    int ii_a[8];
    EXEC SQL END DECLARE SECTION;
    
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT ii FROM t3;
    EXEC SQL OPEN cur1;
    
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    while (1)
    {
        /* WRONG */
        EXEC SQL FETCH FROM cur1 INTO :ii_a;
        ...
    }
    

would not work correctly in this case, because you cannot map an array type
column to an array host variable directly.

Another workaround is to store arrays in their external string representation
in host variables of type `char[]` or `VARCHAR[]`. For more details about this
representation, see [Section 8.15.2](arrays.html#ARRAYS-INPUT "8.15.2. Array
Value Input"). Note that this means that the array cannot be accessed
naturally as an array in the host program (without further processing that
parses the text representation).

#### 36.4.5.2. Composite Types #

Composite types are not directly supported in ECPG, but an easy workaround is
possible. The available workarounds are similar to the ones described for
arrays above: Either access each attribute separately or use the external
string representation.

For the following examples, assume the following type and table:

    
    
    CREATE TYPE comp_t AS (intval integer, textval varchar(32));
    CREATE TABLE t4 (compval comp_t);
    INSERT INTO t4 VALUES ( (256, 'PostgreSQL') );
    

The most obvious solution is to access each attribute separately. The
following program retrieves data from the example table by selecting each
attribute of the type `comp_t` separately:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    int intval;
    varchar textval[33];
    EXEC SQL END DECLARE SECTION;
    
    /* Put each element of the composite type column in the SELECT list. */
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT (compval).intval, (compval).textval FROM t4;
    EXEC SQL OPEN cur1;
    
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    while (1)
    {
        /* Fetch each element of the composite type column into host variables. */
        EXEC SQL FETCH FROM cur1 INTO :intval, :textval;
    
        printf("intval=%d, textval=%s\n", intval, textval.arr);
    }
    
    EXEC SQL CLOSE cur1;
    

To enhance this example, the host variables to store values in the `FETCH`
command can be gathered into one structure. For more details about the host
variable in the structure form, see [Section 36.4.4.3.2](ecpg-
variables.html#ECPG-VARIABLES-STRUCT "36.4.4.3.2. Structures"). To switch to
the structure, the example can be modified as below. The two host variables,
`intval` and `textval`, become members of the `comp_t` structure, and the
structure is specified on the `FETCH` command.

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    typedef struct
    {
        int intval;
        varchar textval[33];
    } comp_t;
    
    comp_t compval;
    EXEC SQL END DECLARE SECTION;
    
    /* Put each element of the composite type column in the SELECT list. */
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT (compval).intval, (compval).textval FROM t4;
    EXEC SQL OPEN cur1;
    
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    while (1)
    {
        /* Put all values in the SELECT list into one structure. */
        EXEC SQL FETCH FROM cur1 INTO :compval;
    
        printf("intval=%d, textval=%s\n", compval.intval, compval.textval.arr);
    }
    
    EXEC SQL CLOSE cur1;
    

Although a structure is used in the `FETCH` command, the attribute names in
the `SELECT` clause are specified one by one. This can be enhanced by using a
`*` to ask for all attributes of the composite type value.

    
    
    ...
    EXEC SQL DECLARE cur1 CURSOR FOR SELECT (compval).* FROM t4;
    EXEC SQL OPEN cur1;
    
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    while (1)
    {
        /* Put all values in the SELECT list into one structure. */
        EXEC SQL FETCH FROM cur1 INTO :compval;
    
        printf("intval=%d, textval=%s\n", compval.intval, compval.textval.arr);
    }
    ...
    

This way, composite types can be mapped into structures almost seamlessly,
even though ECPG does not understand the composite type itself.

Finally, it is also possible to store composite type values in their external
string representation in host variables of type `char[]` or `VARCHAR[]`. But
that way, it is not easily possible to access the fields of the value from the
host program.

#### 36.4.5.3. User-Defined Base Types #

New user-defined base types are not directly supported by ECPG. You can use
the external string representation and host variables of type `char[]` or
`VARCHAR[]`, and this solution is indeed appropriate and sufficient for many
types.

Here is an example using the data type `complex` from the example in [Section
38.13](xtypes.html "38.13. User-Defined Types"). The external string
representation of that type is `(%f,%f)`, which is defined in the functions
`complex_in()` and `complex_out()` functions in [Section 38.13](xtypes.html
"38.13. User-Defined Types"). The following example inserts the complex type
values `(1,1)` and `(3,3)` into the columns `a` and `b`, and select them from
the table after that.

    
    
    EXEC SQL BEGIN DECLARE SECTION;
        varchar a[64];
        varchar b[64];
    EXEC SQL END DECLARE SECTION;
    
        EXEC SQL INSERT INTO test_complex VALUES ('(1,1)', '(3,3)');
    
        EXEC SQL DECLARE cur1 CURSOR FOR SELECT a, b FROM test_complex;
        EXEC SQL OPEN cur1;
    
        EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
        while (1)
        {
            EXEC SQL FETCH FROM cur1 INTO :a, :b;
            printf("a=%s, b=%s\n", a.arr, b.arr);
        }
    
        EXEC SQL CLOSE cur1;
    

This example shows following result:

    
    
    a=(1,1), b=(3,3)
    

Another workaround is avoiding the direct use of the user-defined types in
ECPG and instead create a function or cast that converts between the user-
defined type and a primitive type that ECPG can handle. Note, however, that
type casts, especially implicit ones, should be introduced into the type
system very carefully.

For example,

    
    
    CREATE FUNCTION create_complex(r double, i double) RETURNS complex
    LANGUAGE SQL
    IMMUTABLE
    AS $$ SELECT $1 * complex '(1,0')' + $2 * complex '(0,1)' $$;
    

After this definition, the following

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    double a, b, c, d;
    EXEC SQL END DECLARE SECTION;
    
    a = 1;
    b = 2;
    c = 3;
    d = 4;
    
    EXEC SQL INSERT INTO test_complex VALUES (create_complex(:a, :b), create_complex(:c, :d));
    

has the same effect as

    
    
    EXEC SQL INSERT INTO test_complex VALUES ('(1,2)', '(3,4)');
    

### 36.4.6. Indicators #

The examples above do not handle null values. In fact, the retrieval examples
will raise an error if they fetch a null value from the database. To be able
to pass null values to the database or retrieve null values from the database,
you need to append a second host variable specification to each host variable
that contains data. This second host variable is called the _indicator_ and
contains a flag that tells whether the datum is null, in which case the value
of the real host variable is ignored. Here is an example that handles the
retrieval of null values correctly:

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR val;
    int val_ind;
    EXEC SQL END DECLARE SECTION:
    
     ...
    
    EXEC SQL SELECT b INTO :val :val_ind FROM test1;
    

The indicator variable `val_ind` will be zero if the value was not null, and
it will be negative if the value was null. (See [Section 36.16](ecpg-oracle-
compat.html "36.16. Oracle Compatibility Mode") to enable Oracle-specific
behavior.)

The indicator has another function: if the indicator value is positive, it
means that the value is not null, but it was truncated when it was stored in
the host variable.

If the argument `-r no_indicator` is passed to the preprocessor `ecpg`, it
works in “no-indicator” mode. In no-indicator mode, if no indicator variable
is specified, null values are signaled (on input and output) for character
string types as empty string and for integer types as the lowest possible
value for type (for example, `INT_MIN` for `int`).

* * *

[Prev](ecpg-commands.html "36.3. Running SQL Commands")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-dynamic.html "36.5. Dynamic SQL")  
---|---|---  
36.3. Running SQL Commands  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.5. Dynamic SQL  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-variables.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

