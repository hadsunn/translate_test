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

Supported Versions: [Current](/docs/current/sql-createconversion.html
"PostgreSQL 17 - CREATE CONVERSION") ([17](/docs/17/sql-createconversion.html
"PostgreSQL 17 - CREATE CONVERSION")) / [16](/docs/16/sql-
createconversion.html "PostgreSQL 16 - CREATE CONVERSION") /
[15](/docs/15/sql-createconversion.html "PostgreSQL 15 - CREATE CONVERSION") /
[14](/docs/14/sql-createconversion.html "PostgreSQL 14 - CREATE CONVERSION") /
[13](/docs/13/sql-createconversion.html "PostgreSQL 13 - CREATE CONVERSION")

Development Versions: [18](/docs/18/sql-createconversion.html "PostgreSQL 18 -
CREATE CONVERSION") / [devel](/docs/devel/sql-createconversion.html
"PostgreSQL devel - CREATE CONVERSION")

Unsupported versions: [12](/docs/12/sql-createconversion.html "PostgreSQL 12 -
CREATE CONVERSION") / [11](/docs/11/sql-createconversion.html "PostgreSQL 11 -
CREATE CONVERSION") / [10](/docs/10/sql-createconversion.html "PostgreSQL 10 -
CREATE CONVERSION") / [9.6](/docs/9.6/sql-createconversion.html "PostgreSQL
9.6 - CREATE CONVERSION") / [9.5](/docs/9.5/sql-createconversion.html
"PostgreSQL 9.5 - CREATE CONVERSION") / [9.4](/docs/9.4/sql-
createconversion.html "PostgreSQL 9.4 - CREATE CONVERSION") /
[9.3](/docs/9.3/sql-createconversion.html "PostgreSQL 9.3 - CREATE
CONVERSION") / [9.2](/docs/9.2/sql-createconversion.html "PostgreSQL 9.2 -
CREATE CONVERSION") / [9.1](/docs/9.1/sql-createconversion.html "PostgreSQL
9.1 - CREATE CONVERSION") / [9.0](/docs/9.0/sql-createconversion.html
"PostgreSQL 9.0 - CREATE CONVERSION") / [8.4](/docs/8.4/sql-
createconversion.html "PostgreSQL 8.4 - CREATE CONVERSION") /
[8.3](/docs/8.3/sql-createconversion.html "PostgreSQL 8.3 - CREATE
CONVERSION") / [8.2](/docs/8.2/sql-createconversion.html "PostgreSQL 8.2 -
CREATE CONVERSION") / [8.1](/docs/8.1/sql-createconversion.html "PostgreSQL
8.1 - CREATE CONVERSION") / [8.0](/docs/8.0/sql-createconversion.html
"PostgreSQL 8.0 - CREATE CONVERSION") / [7.4](/docs/7.4/sql-
createconversion.html "PostgreSQL 7.4 - CREATE CONVERSION") /
[7.3](/docs/7.3/sql-createconversion.html "PostgreSQL 7.3 - CREATE
CONVERSION")

__

CREATE CONVERSION  
---  
[Prev](sql-createcollation.html "CREATE COLLATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createdatabase.html "CREATE DATABASE")  
  
* * *

## CREATE CONVERSION

CREATE CONVERSION — define a new encoding conversion

## Synopsis

    
    
    CREATE [ DEFAULT ] CONVERSION _name_
        FOR _source_encoding_ TO _dest_encoding_ FROM _function_name_
    

## Description

`CREATE CONVERSION` defines a new conversion between two character set
encodings.

Conversions that are marked `DEFAULT` can be used for automatic encoding
conversion between client and server. To support that usage, two conversions,
from encoding A to B _and_ from encoding B to A, must be defined.

To be able to create a conversion, you must have `EXECUTE` privilege on the
function and `CREATE` privilege on the destination schema.

## Parameters

`DEFAULT`

    

The `DEFAULT` clause indicates that this conversion is the default for this
particular source to destination encoding. There should be only one default
encoding in a schema for the encoding pair.

_`name`_

    

The name of the conversion. The conversion name can be schema-qualified. If it
is not, the conversion is defined in the current schema. The conversion name
must be unique within a schema.

_`source_encoding`_

    

The source encoding name.

_`dest_encoding`_

    

The destination encoding name.

_`function_name`_

    

The function used to perform the conversion. The function name can be schema-
qualified. If it is not, the function will be looked up in the path.

The function must have the following signature:

    
    
    conv_proc(
        integer,  -- source encoding ID
        integer,  -- destination encoding ID
        cstring,  -- source string (null terminated C string)
        internal, -- destination (fill with a null terminated C string)
        integer,  -- source string length
        boolean   -- if true, don't throw an error if conversion fails
    ) RETURNS integer;
    

The return value is the number of source bytes that were successfully
converted. If the last argument is false, the function must throw an error on
invalid input, and the return value is always equal to the source string
length.

## Notes

Neither the source nor the destination encoding can be `SQL_ASCII`, as the
server's behavior for cases involving the `SQL_ASCII` “encoding” is hard-
wired.

Use `DROP CONVERSION` to remove user-defined conversions.

The privileges required to create a conversion might be changed in a future
release.

## Examples

To create a conversion from encoding `UTF8` to `LATIN1` using `myfunc`:

    
    
    CREATE CONVERSION myconv FOR 'UTF8' TO 'LATIN1' FROM myfunc;
    

## Compatibility

`CREATE CONVERSION` is a PostgreSQL extension. There is no `CREATE CONVERSION`
statement in the SQL standard, but a `CREATE TRANSLATION` statement that is
very similar in purpose and syntax.

## See Also

[ALTER CONVERSION](sql-alterconversion.html "ALTER CONVERSION"), [CREATE
FUNCTION](sql-createfunction.html "CREATE FUNCTION"), [DROP CONVERSION](sql-
dropconversion.html "DROP CONVERSION")

* * *

[Prev](sql-createcollation.html "CREATE COLLATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createdatabase.html "CREATE DATABASE")  
---|---|---  
CREATE COLLATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE DATABASE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createconversion.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

