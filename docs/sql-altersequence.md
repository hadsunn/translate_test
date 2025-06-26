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

Supported Versions: [Current](/docs/current/sql-altersequence.html "PostgreSQL
17 - ALTER SEQUENCE") ([17](/docs/17/sql-altersequence.html "PostgreSQL 17 -
ALTER SEQUENCE")) / [16](/docs/16/sql-altersequence.html "PostgreSQL 16 -
ALTER SEQUENCE") / [15](/docs/15/sql-altersequence.html "PostgreSQL 15 - ALTER
SEQUENCE") / [14](/docs/14/sql-altersequence.html "PostgreSQL 14 - ALTER
SEQUENCE") / [13](/docs/13/sql-altersequence.html "PostgreSQL 13 - ALTER
SEQUENCE")

Development Versions: [18](/docs/18/sql-altersequence.html "PostgreSQL 18 -
ALTER SEQUENCE") / [devel](/docs/devel/sql-altersequence.html "PostgreSQL
devel - ALTER SEQUENCE")

Unsupported versions: [12](/docs/12/sql-altersequence.html "PostgreSQL 12 -
ALTER SEQUENCE") / [11](/docs/11/sql-altersequence.html "PostgreSQL 11 - ALTER
SEQUENCE") / [10](/docs/10/sql-altersequence.html "PostgreSQL 10 - ALTER
SEQUENCE") / [9.6](/docs/9.6/sql-altersequence.html "PostgreSQL 9.6 - ALTER
SEQUENCE") / [9.5](/docs/9.5/sql-altersequence.html "PostgreSQL 9.5 - ALTER
SEQUENCE") / [9.4](/docs/9.4/sql-altersequence.html "PostgreSQL 9.4 - ALTER
SEQUENCE") / [9.3](/docs/9.3/sql-altersequence.html "PostgreSQL 9.3 - ALTER
SEQUENCE") / [9.2](/docs/9.2/sql-altersequence.html "PostgreSQL 9.2 - ALTER
SEQUENCE") / [9.1](/docs/9.1/sql-altersequence.html "PostgreSQL 9.1 - ALTER
SEQUENCE") / [9.0](/docs/9.0/sql-altersequence.html "PostgreSQL 9.0 - ALTER
SEQUENCE") / [8.4](/docs/8.4/sql-altersequence.html "PostgreSQL 8.4 - ALTER
SEQUENCE") / [8.3](/docs/8.3/sql-altersequence.html "PostgreSQL 8.3 - ALTER
SEQUENCE") / [8.2](/docs/8.2/sql-altersequence.html "PostgreSQL 8.2 - ALTER
SEQUENCE") / [8.1](/docs/8.1/sql-altersequence.html "PostgreSQL 8.1 - ALTER
SEQUENCE") / [8.0](/docs/8.0/sql-altersequence.html "PostgreSQL 8.0 - ALTER
SEQUENCE") / [7.4](/docs/7.4/sql-altersequence.html "PostgreSQL 7.4 - ALTER
SEQUENCE")

__

ALTER SEQUENCE  
---  
[Prev](sql-alterschema.html "ALTER SCHEMA")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterserver.html "ALTER SERVER")  
  
* * *

## ALTER SEQUENCE

ALTER SEQUENCE — change the definition of a sequence generator

## Synopsis

    
    
    ALTER SEQUENCE [ IF EXISTS ] _name_
        [ AS _data_type_ ]
        [ INCREMENT [ BY ] _increment_ ]
        [ MINVALUE _minvalue_ | NO MINVALUE ] [ MAXVALUE _maxvalue_ | NO MAXVALUE ]
        [ START [ WITH ] _start_ ]
        [ RESTART [ [ WITH ] _restart_ ] ]
        [ CACHE _cache_ ] [ [ NO ] CYCLE ]
        [ OWNED BY { _table_name_._column_name_ | NONE } ]
    ALTER SEQUENCE [ IF EXISTS ] _name_ SET { LOGGED | UNLOGGED }
    ALTER SEQUENCE [ IF EXISTS ] _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER SEQUENCE [ IF EXISTS ] _name_ RENAME TO _new_name_
    ALTER SEQUENCE [ IF EXISTS ] _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER SEQUENCE` changes the parameters of an existing sequence generator. Any
parameters not specifically set in the `ALTER SEQUENCE` command retain their
prior settings.

You must own the sequence to use `ALTER SEQUENCE`. To change a sequence's
schema, you must also have `CREATE` privilege on the new schema. To alter the
owner, you must be able to `SET ROLE` to the new owning role, and that role
must have `CREATE` privilege on the sequence's schema. (These restrictions
enforce that altering the owner doesn't do anything you couldn't do by
dropping and recreating the sequence. However, a superuser can alter ownership
of any sequence anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of a sequence to be altered.

`IF EXISTS`

    

Do not throw an error if the sequence does not exist. A notice is issued in
this case.

_`data_type`_

    

The optional clause `AS _`data_type`_` changes the data type of the sequence.
Valid types are `smallint`, `integer`, and `bigint`.

Changing the data type automatically changes the minimum and maximum values of
the sequence if and only if the previous minimum and maximum values were the
minimum or maximum value of the old data type (in other words, if the sequence
had been created using `NO MINVALUE` or `NO MAXVALUE`, implicitly or
explicitly). Otherwise, the minimum and maximum values are preserved, unless
new values are given as part of the same command. If the minimum and maximum
values do not fit into the new data type, an error will be generated.

_`increment`_

    

The clause `INCREMENT BY _`increment`_` is optional. A positive value will
make an ascending sequence, a negative one a descending sequence. If
unspecified, the old increment value will be maintained.

_`minvalue`_  
`NO MINVALUE`

    

The optional clause `MINVALUE _`minvalue`_` determines the minimum value a
sequence can generate. If `NO MINVALUE` is specified, the defaults of 1 and
the minimum value of the data type for ascending and descending sequences,
respectively, will be used. If neither option is specified, the current
minimum value will be maintained.

_`maxvalue`_  
`NO MAXVALUE`

    

The optional clause `MAXVALUE _`maxvalue`_` determines the maximum value for
the sequence. If `NO MAXVALUE` is specified, the defaults of the maximum value
of the data type and -1 for ascending and descending sequences, respectively,
will be used. If neither option is specified, the current maximum value will
be maintained.

_`start`_

    

The optional clause `START WITH _`start`_` changes the recorded start value of
the sequence. This has no effect on the _current_ sequence value; it simply
sets the value that future `ALTER SEQUENCE RESTART` commands will use.

_`restart`_

    

The optional clause `RESTART [ WITH _`restart`_ ]` changes the current value
of the sequence. This is similar to calling the `setval` function with
`is_called` = `false`: the specified value will be returned by the _next_ call
of `nextval`. Writing `RESTART` with no _`restart`_ value is equivalent to
supplying the start value that was recorded by `CREATE SEQUENCE` or last set
by `ALTER SEQUENCE START WITH`.

In contrast to a `setval` call, a `RESTART` operation on a sequence is
transactional and blocks concurrent transactions from obtaining numbers from
the same sequence. If that's not the desired mode of operation, `setval`
should be used.

_`cache`_

    

The clause `CACHE _`cache`_` enables sequence numbers to be preallocated and
stored in memory for faster access. The minimum value is 1 (only one value can
be generated at a time, i.e., no cache). If unspecified, the old cache value
will be maintained.

`CYCLE`

    

The optional `CYCLE` key word can be used to enable the sequence to wrap
around when the _`maxvalue`_ or _`minvalue`_ has been reached by an ascending
or descending sequence respectively. If the limit is reached, the next number
generated will be the _`minvalue`_ or _`maxvalue`_ , respectively.

`NO CYCLE`

    

If the optional `NO CYCLE` key word is specified, any calls to `nextval` after
the sequence has reached its maximum value will return an error. If neither
`CYCLE` or `NO CYCLE` are specified, the old cycle behavior will be
maintained.

`SET { LOGGED | UNLOGGED }`
    

This form changes the sequence from unlogged to logged or vice-versa (see
[CREATE SEQUENCE](sql-createsequence.html "CREATE SEQUENCE")). It cannot be
applied to a temporary sequence.

`OWNED BY` _`table_name`_._`column_name`_  
`OWNED BY NONE`

    

The `OWNED BY` option causes the sequence to be associated with a specific
table column, such that if that column (or its whole table) is dropped, the
sequence will be automatically dropped as well. If specified, this association
replaces any previously specified association for the sequence. The specified
table must have the same owner and be in the same schema as the sequence.
Specifying `OWNED BY NONE` removes any existing association, making the
sequence “free-standing”.

_`new_owner`_

    

The user name of the new owner of the sequence.

_`new_name`_

    

The new name for the sequence.

_`new_schema`_

    

The new schema for the sequence.

## Notes

`ALTER SEQUENCE` will not immediately affect `nextval` results in backends,
other than the current one, that have preallocated (cached) sequence values.
They will use up all cached values prior to noticing the changed sequence
generation parameters. The current backend will be affected immediately.

`ALTER SEQUENCE` does not affect the `currval` status for the sequence.
(Before PostgreSQL 8.3, it sometimes did.)

`ALTER SEQUENCE` blocks concurrent `nextval`, `currval`, `lastval`, and
`setval` calls.

For historical reasons, `ALTER TABLE` can be used with sequences too; but the
only variants of `ALTER TABLE` that are allowed with sequences are equivalent
to the forms shown above.

## Examples

Restart a sequence called `serial`, at 105:

    
    
    ALTER SEQUENCE serial RESTART WITH 105;
    

## Compatibility

`ALTER SEQUENCE` conforms to the SQL standard, except for the `AS`, `START
WITH`, `OWNED BY`, `OWNER TO`, `RENAME TO`, and `SET SCHEMA` clauses, which
are PostgreSQL extensions.

## See Also

[CREATE SEQUENCE](sql-createsequence.html "CREATE SEQUENCE"), [DROP
SEQUENCE](sql-dropsequence.html "DROP SEQUENCE")

* * *

[Prev](sql-alterschema.html "ALTER SCHEMA")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterserver.html "ALTER SERVER")  
---|---|---  
ALTER SCHEMA  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER SERVER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altersequence.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

