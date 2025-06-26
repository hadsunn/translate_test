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

Supported Versions: [Current](/docs/current/pltcl-dbaccess.html "PostgreSQL 17
- 44.5. Database Access from PL/Tcl") ([17](/docs/17/pltcl-dbaccess.html
"PostgreSQL 17 - 44.5. Database Access from PL/Tcl")) / [16](/docs/16/pltcl-
dbaccess.html "PostgreSQL 16 - 44.5. Database Access from PL/Tcl") /
[15](/docs/15/pltcl-dbaccess.html "PostgreSQL 15 - 44.5. Database Access from
PL/Tcl") / [14](/docs/14/pltcl-dbaccess.html "PostgreSQL 14 - 44.5. Database
Access from PL/Tcl") / [13](/docs/13/pltcl-dbaccess.html "PostgreSQL 13 -
44.5. Database Access from PL/Tcl")

Development Versions: [18](/docs/18/pltcl-dbaccess.html "PostgreSQL 18 -
44.5. Database Access from PL/Tcl") / [devel](/docs/devel/pltcl-dbaccess.html
"PostgreSQL devel - 44.5. Database Access from PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-dbaccess.html "PostgreSQL 12 -
44.5. Database Access from PL/Tcl") / [11](/docs/11/pltcl-dbaccess.html
"PostgreSQL 11 - 44.5. Database Access from PL/Tcl") / [10](/docs/10/pltcl-
dbaccess.html "PostgreSQL 10 - 44.5. Database Access from PL/Tcl") /
[9.6](/docs/9.6/pltcl-dbaccess.html "PostgreSQL 9.6 - 44.5. Database Access
from PL/Tcl") / [9.5](/docs/9.5/pltcl-dbaccess.html "PostgreSQL 9.5 -
44.5. Database Access from PL/Tcl") / [9.4](/docs/9.4/pltcl-dbaccess.html
"PostgreSQL 9.4 - 44.5. Database Access from PL/Tcl") / [9.3](/docs/9.3/pltcl-
dbaccess.html "PostgreSQL 9.3 - 44.5. Database Access from PL/Tcl") /
[9.2](/docs/9.2/pltcl-dbaccess.html "PostgreSQL 9.2 - 44.5. Database Access
from PL/Tcl") / [9.1](/docs/9.1/pltcl-dbaccess.html "PostgreSQL 9.1 -
44.5. Database Access from PL/Tcl") / [9.0](/docs/9.0/pltcl-dbaccess.html
"PostgreSQL 9.0 - 44.5. Database Access from PL/Tcl") / [8.4](/docs/8.4/pltcl-
dbaccess.html "PostgreSQL 8.4 - 44.5. Database Access from PL/Tcl") /
[8.3](/docs/8.3/pltcl-dbaccess.html "PostgreSQL 8.3 - 44.5. Database Access
from PL/Tcl") / [8.2](/docs/8.2/pltcl-dbaccess.html "PostgreSQL 8.2 -
44.5. Database Access from PL/Tcl") / [8.1](/docs/8.1/pltcl-dbaccess.html
"PostgreSQL 8.1 - 44.5. Database Access from PL/Tcl") / [8.0](/docs/8.0/pltcl-
dbaccess.html "PostgreSQL 8.0 - 44.5. Database Access from PL/Tcl") /
[7.4](/docs/7.4/pltcl-dbaccess.html "PostgreSQL 7.4 - 44.5. Database Access
from PL/Tcl")

__

44.5. Database Access from PL/Tcl  
---  
[Prev](pltcl-global.html "44.4. Global Data in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-trigger.html "44.6. Trigger Functions in PL/Tcl")  
  
* * *

## 44.5. Database Access from PL/Tcl #

In this section, we follow the usual Tcl convention of using question marks,
rather than brackets, to indicate an optional element in a syntax synopsis.
The following commands are available to access the database from the body of a
PL/Tcl function:

``spi_exec` ?-count _`n`_? ?-array _`name`_? _`command`_ ?_`loop-body`_?`

    

Executes an SQL command given as a string. An error in the command causes an
error to be raised. Otherwise, the return value of `spi_exec` is the number of
rows processed (selected, inserted, updated, or deleted) by the command, or
zero if the command is a utility statement. In addition, if the command is a
`SELECT` statement, the values of the selected columns are placed in Tcl
variables as described below.

The optional `-count` value tells `spi_exec` to stop once _`n`_ rows have been
retrieved, much as if the query included a `LIMIT` clause. If _`n`_ is zero,
the query is run to completion, the same as when `-count` is omitted.

If the command is a `SELECT` statement, the values of the result columns are
placed into Tcl variables named after the columns. If the `-array` option is
given, the column values are instead stored into elements of the named
associative array, with the column names used as array indexes. In addition,
the current row number within the result (counting from zero) is stored into
the array element named “`.tupno`”, unless that name is in use as a column
name in the result.

If the command is a `SELECT` statement and no _`loop-body`_ script is given,
then only the first row of results are stored into Tcl variables or array
elements; remaining rows, if any, are ignored. No storing occurs if the query
returns no rows. (This case can be detected by checking the result of
`spi_exec`.) For example:

    
    
    spi_exec "SELECT count(*) AS cnt FROM pg_proc"
    

will set the Tcl variable `$cnt` to the number of rows in the `pg_proc` system
catalog.

If the optional _`loop-body`_ argument is given, it is a piece of Tcl script
that is executed once for each row in the query result. (_`loop-body`_ is
ignored if the given command is not a `SELECT`.) The values of the current
row's columns are stored into Tcl variables or array elements before each
iteration. For example:

    
    
    spi_exec -array C "SELECT * FROM pg_class" {
        elog DEBUG "have table $C(relname)"
    }
    

will print a log message for every row of `pg_class`. This feature works
similarly to other Tcl looping constructs; in particular `continue` and
`break` work in the usual way inside the loop body.

If a column of a query result is null, the target variable for it is “unset”
rather than being set.

`spi_prepare` _`query`_ _`typelist`_

    

Prepares and saves a query plan for later execution. The saved plan will be
retained for the life of the current session.

The query can use parameters, that is, placeholders for values to be supplied
whenever the plan is actually executed. In the query string, refer to
parameters by the symbols `$1` ... `$_`n`_`. If the query uses parameters, the
names of the parameter types must be given as a Tcl list. (Write an empty list
for _`typelist`_ if no parameters are used.)

The return value from `spi_prepare` is a query ID to be used in subsequent
calls to `spi_execp`. See `spi_execp` for an example.

``spi_execp` ?-count _`n`_? ?-array _`name`_? ?-nulls _`string`_? _`queryid`_
?_`value-list`_? ?_`loop-body`_?`

    

Executes a query previously prepared with `spi_prepare`. _`queryid`_ is the ID
returned by `spi_prepare`. If the query references parameters, a _`value-
list`_ must be supplied. This is a Tcl list of actual values for the
parameters. The list must be the same length as the parameter type list
previously given to `spi_prepare`. Omit _`value-list`_ if the query has no
parameters.

The optional value for `-nulls` is a string of spaces and `'n'` characters
telling `spi_execp` which of the parameters are null values. If given, it must
have exactly the same length as the _`value-list`_. If it is not given, all
the parameter values are nonnull.

Except for the way in which the query and its parameters are specified,
`spi_execp` works just like `spi_exec`. The `-count`, `-array`, and _`loop-
body`_ options are the same, and so is the result value.

Here's an example of a PL/Tcl function using a prepared plan:

    
    
    CREATE FUNCTION t1_count(integer, integer) RETURNS integer AS $$
        if {![ info exists GD(plan) ]} {
            # prepare the saved plan on the first call
            set GD(plan) [ spi_prepare \
                    "SELECT count(*) AS cnt FROM t1 WHERE num >= \$1 AND num <= \$2" \
                    [ list int4 int4 ] ]
        }
        spi_execp -count 1 $GD(plan) [ list $1 $2 ]
        return $cnt
    $$ LANGUAGE pltcl;
    

We need backslashes inside the query string given to `spi_prepare` to ensure
that the `$_`n`_` markers will be passed through to `spi_prepare` as-is, and
not replaced by Tcl variable substitution.

`subtransaction` _`command`_

    

The Tcl script contained in _`command`_ is executed within an SQL
subtransaction. If the script returns an error, that entire subtransaction is
rolled back before returning the error out to the surrounding Tcl code. See
[Section 44.9](pltcl-subtransactions.html "44.9. Explicit Subtransactions in
PL/Tcl") for more details and an example.

`quote` _`string`_

    

Doubles all occurrences of single quote and backslash characters in the given
string. This can be used to safely quote strings that are to be inserted into
SQL commands given to `spi_exec` or `spi_prepare`. For example, think about an
SQL command string like:

    
    
    "SELECT '$val' AS ret"
    

where the Tcl variable `val` actually contains `doesn't`. This would result in
the final command string:

    
    
    SELECT 'doesn't' AS ret
    

which would cause a parse error during `spi_exec` or `spi_prepare`. To work
properly, the submitted command should contain:

    
    
    SELECT 'doesn''t' AS ret
    

which can be formed in PL/Tcl using:

    
    
    "SELECT '[ quote $val ]' AS ret"
    

One advantage of `spi_execp` is that you don't have to quote parameter values
like this, since the parameters are never parsed as part of an SQL command
string.

`elog` _`level`_ _`msg`_

    

Emits a log or error message. Possible levels are `DEBUG`, `LOG`, `INFO`,
`NOTICE`, `WARNING`, `ERROR`, and `FATAL`. `ERROR` raises an error condition;
if this is not trapped by the surrounding Tcl code, the error propagates out
to the calling query, causing the current transaction or subtransaction to be
aborted. This is effectively the same as the Tcl `error` command. `FATAL`
aborts the transaction and causes the current session to shut down. (There is
probably no good reason to use this error level in PL/Tcl functions, but it's
provided for completeness.) The other levels only generate messages of
different priority levels. Whether messages of a particular priority are
reported to the client, written to the server log, or both is controlled by
the [log_min_messages](runtime-config-logging.html#GUC-LOG-MIN-MESSAGES) and
[client_min_messages](runtime-config-client.html#GUC-CLIENT-MIN-MESSAGES)
configuration variables. See [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") and [Section 44.8](pltcl-error-
handling.html "44.8. Error Handling in PL/Tcl") for more information.

* * *

[Prev](pltcl-global.html "44.4. Global Data in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-trigger.html "44.6. Trigger Functions in PL/Tcl")  
---|---|---  
44.4. Global Data in PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.6. Trigger Functions in PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-dbaccess.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

