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

Supported Versions: [Current](/docs/current/plpgsql-errors-and-messages.html
"PostgreSQL 17 - 43.9. Errors and Messages") ([17](/docs/17/plpgsql-errors-
and-messages.html "PostgreSQL 17 - 43.9. Errors and Messages")) /
[16](/docs/16/plpgsql-errors-and-messages.html "PostgreSQL 16 - 43.9. Errors
and Messages") / [15](/docs/15/plpgsql-errors-and-messages.html "PostgreSQL 15
- 43.9. Errors and Messages") / [14](/docs/14/plpgsql-errors-and-messages.html
"PostgreSQL 14 - 43.9. Errors and Messages") / [13](/docs/13/plpgsql-errors-
and-messages.html "PostgreSQL 13 - 43.9. Errors and Messages")

Development Versions: [18](/docs/18/plpgsql-errors-and-messages.html
"PostgreSQL 18 - 43.9. Errors and Messages") / [devel](/docs/devel/plpgsql-
errors-and-messages.html "PostgreSQL devel - 43.9. Errors and Messages")

Unsupported versions: [12](/docs/12/plpgsql-errors-and-messages.html
"PostgreSQL 12 - 43.9. Errors and Messages") / [11](/docs/11/plpgsql-errors-
and-messages.html "PostgreSQL 11 - 43.9. Errors and Messages") /
[10](/docs/10/plpgsql-errors-and-messages.html "PostgreSQL 10 - 43.9. Errors
and Messages") / [9.6](/docs/9.6/plpgsql-errors-and-messages.html "PostgreSQL
9.6 - 43.9. Errors and Messages") / [9.5](/docs/9.5/plpgsql-errors-and-
messages.html "PostgreSQL 9.5 - 43.9. Errors and Messages") /
[9.4](/docs/9.4/plpgsql-errors-and-messages.html "PostgreSQL 9.4 -
43.9. Errors and Messages") / [9.3](/docs/9.3/plpgsql-errors-and-messages.html
"PostgreSQL 9.3 - 43.9. Errors and Messages") / [9.2](/docs/9.2/plpgsql-
errors-and-messages.html "PostgreSQL 9.2 - 43.9. Errors and Messages") /
[9.1](/docs/9.1/plpgsql-errors-and-messages.html "PostgreSQL 9.1 -
43.9. Errors and Messages") / [9.0](/docs/9.0/plpgsql-errors-and-messages.html
"PostgreSQL 9.0 - 43.9. Errors and Messages") / [8.4](/docs/8.4/plpgsql-
errors-and-messages.html "PostgreSQL 8.4 - 43.9. Errors and Messages") /
[8.3](/docs/8.3/plpgsql-errors-and-messages.html "PostgreSQL 8.3 -
43.9. Errors and Messages") / [8.2](/docs/8.2/plpgsql-errors-and-messages.html
"PostgreSQL 8.2 - 43.9. Errors and Messages") / [8.1](/docs/8.1/plpgsql-
errors-and-messages.html "PostgreSQL 8.1 - 43.9. Errors and Messages") /
[8.0](/docs/8.0/plpgsql-errors-and-messages.html "PostgreSQL 8.0 -
43.9. Errors and Messages") / [7.4](/docs/7.4/plpgsql-errors-and-messages.html
"PostgreSQL 7.4 - 43.9. Errors and Messages") / [7.3](/docs/7.3/plpgsql-
errors-and-messages.html "PostgreSQL 7.3 - 43.9. Errors and Messages") /
[7.2](/docs/7.2/plpgsql-errors-and-messages.html "PostgreSQL 7.2 -
43.9. Errors and Messages")

__

43.9. Errors and Messages  
---  
[Prev](plpgsql-transactions.html "43.8. Transaction Management")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-trigger.html "43.10. Trigger Functions")  
  
* * *

## 43.9. Errors and Messages #

[43.9.1. Reporting Errors and Messages](plpgsql-errors-and-
messages.html#PLPGSQL-STATEMENTS-RAISE)

[43.9.2. Checking Assertions](plpgsql-errors-and-messages.html#PLPGSQL-
STATEMENTS-ASSERT)

### 43.9.1. Reporting Errors and Messages #

Use the `RAISE` statement to report messages and raise errors.

    
    
    RAISE [ _level_ ] '_format_ ' [, _expression_ [, ... ]] [ USING _option_ = _expression_ [, ... ] ];
    RAISE [ _level_ ] _condition_name_ [ USING _option_ = _expression_ [, ... ] ];
    RAISE [ _level_ ] SQLSTATE '_sqlstate_ ' [ USING _option_ = _expression_ [, ... ] ];
    RAISE [ _level_ ] USING _option_ = _expression_ [, ... ];
    RAISE ;
    

The _`level`_ option specifies the error severity. Allowed levels are `DEBUG`,
`LOG`, `INFO`, `NOTICE`, `WARNING`, and `EXCEPTION`, with `EXCEPTION` being
the default. `EXCEPTION` raises an error (which normally aborts the current
transaction); the other levels only generate messages of different priority
levels. Whether messages of a particular priority are reported to the client,
written to the server log, or both is controlled by the
[log_min_messages](runtime-config-logging.html#GUC-LOG-MIN-MESSAGES) and
[client_min_messages](runtime-config-client.html#GUC-CLIENT-MIN-MESSAGES)
configuration variables. See [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") for more information.

After _`level`_ if any, you can specify a _`format`_ string (which must be a
simple string literal, not an expression). The format string specifies the
error message text to be reported. The format string can be followed by
optional argument expressions to be inserted into the message. Inside the
format string, `%` is replaced by the string representation of the next
optional argument's value. Write `%%` to emit a literal `%`. The number of
arguments must match the number of `%` placeholders in the format string, or
an error is raised during the compilation of the function.

In this example, the value of `v_job_id` will replace the `%` in the string:

    
    
    RAISE NOTICE 'Calling cs_create_job(%)', v_job_id;
    

You can attach additional information to the error report by writing `USING`
followed by _`option`_ = _`expression`_ items. Each _`expression`_ can be any
string-valued expression. The allowed _`option`_ key words are:

`MESSAGE` #

    

Sets the error message text. This option can't be used in the form of `RAISE`
that includes a format string before `USING`.

`DETAIL` #

    

Supplies an error detail message.

`HINT` #

    

Supplies a hint message.

`ERRCODE` #

    

Specifies the error code (SQLSTATE) to report, either by condition name, as
shown in [Appendix A](errcodes-appendix.html "Appendix A. PostgreSQL Error
Codes"), or directly as a five-character SQLSTATE code.

`COLUMN`  
`CONSTRAINT`  
`DATATYPE`  
`TABLE`  
`SCHEMA` #

    

Supplies the name of a related object.

This example will abort the transaction with the given error message and hint:

    
    
    RAISE EXCEPTION 'Nonexistent ID --> %', user_id
          USING HINT = 'Please check your user ID';
    

These two examples show equivalent ways of setting the SQLSTATE:

    
    
    RAISE 'Duplicate user ID: %', user_id USING ERRCODE = 'unique_violation';
    RAISE 'Duplicate user ID: %', user_id USING ERRCODE = '23505';
    

There is a second `RAISE` syntax in which the main argument is the condition
name or SQLSTATE to be reported, for example:

    
    
    RAISE division_by_zero;
    RAISE SQLSTATE '22012';
    

In this syntax, `USING` can be used to supply a custom error message, detail,
or hint. Another way to do the earlier example is

    
    
    RAISE unique_violation USING MESSAGE = 'Duplicate user ID: ' || user_id;
    

Still another variant is to write `RAISE USING` or `RAISE _`level`_ USING` and
put everything else into the `USING` list.

The last variant of `RAISE` has no parameters at all. This form can only be
used inside a `BEGIN` block's `EXCEPTION` clause; it causes the error
currently being handled to be re-thrown.

### Note

Before PostgreSQL 9.1, `RAISE` without parameters was interpreted as re-
throwing the error from the block containing the active exception handler.
Thus an `EXCEPTION` clause nested within that handler could not catch it, even
if the `RAISE` was within the nested `EXCEPTION` clause's block. This was
deemed surprising as well as being incompatible with Oracle's PL/SQL.

If no condition name nor SQLSTATE is specified in a `RAISE EXCEPTION` command,
the default is to use `raise_exception` (`P0001`). If no message text is
specified, the default is to use the condition name or SQLSTATE as message
text.

### Note

When specifying an error code by SQLSTATE code, you are not limited to the
predefined error codes, but can select any error code consisting of five
digits and/or upper-case ASCII letters, other than `00000`. It is recommended
that you avoid throwing error codes that end in three zeroes, because these
are category codes and can only be trapped by trapping the whole category.

### 43.9.2. Checking Assertions #

The `ASSERT` statement is a convenient shorthand for inserting debugging
checks into PL/pgSQL functions.

    
    
    ASSERT _condition_ [ , _message_ ];
    

The _`condition`_ is a Boolean expression that is expected to always evaluate
to true; if it does, the `ASSERT` statement does nothing further. If the
result is false or null, then an `ASSERT_FAILURE` exception is raised. (If an
error occurs while evaluating the _`condition`_ , it is reported as a normal
error.)

If the optional _`message`_ is provided, it is an expression whose result (if
not null) replaces the default error message text “assertion failed”, should
the _`condition`_ fail. The _`message`_ expression is not evaluated in the
normal case where the assertion succeeds.

Testing of assertions can be enabled or disabled via the configuration
parameter `plpgsql.check_asserts`, which takes a Boolean value; the default is
`on`. If this parameter is `off` then `ASSERT` statements do nothing.

Note that `ASSERT` is meant for detecting program bugs, not for reporting
ordinary error conditions. Use the `RAISE` statement, described above, for
that.

* * *

[Prev](plpgsql-transactions.html "43.8. Transaction Management")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-trigger.html "43.10. Trigger Functions")  
---|---|---  
43.8. Transaction Management  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.10. Trigger Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-errors-and-
messages.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

