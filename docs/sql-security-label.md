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

Supported Versions: [Current](/docs/current/sql-security-label.html
"PostgreSQL 17 - SECURITY LABEL") ([17](/docs/17/sql-security-label.html
"PostgreSQL 17 - SECURITY LABEL")) / [16](/docs/16/sql-security-label.html
"PostgreSQL 16 - SECURITY LABEL") / [15](/docs/15/sql-security-label.html
"PostgreSQL 15 - SECURITY LABEL") / [14](/docs/14/sql-security-label.html
"PostgreSQL 14 - SECURITY LABEL") / [13](/docs/13/sql-security-label.html
"PostgreSQL 13 - SECURITY LABEL")

Development Versions: [18](/docs/18/sql-security-label.html "PostgreSQL 18 -
SECURITY LABEL") / [devel](/docs/devel/sql-security-label.html "PostgreSQL
devel - SECURITY LABEL")

Unsupported versions: [12](/docs/12/sql-security-label.html "PostgreSQL 12 -
SECURITY LABEL") / [11](/docs/11/sql-security-label.html "PostgreSQL 11 -
SECURITY LABEL") / [10](/docs/10/sql-security-label.html "PostgreSQL 10 -
SECURITY LABEL") / [9.6](/docs/9.6/sql-security-label.html "PostgreSQL 9.6 -
SECURITY LABEL") / [9.5](/docs/9.5/sql-security-label.html "PostgreSQL 9.5 -
SECURITY LABEL") / [9.4](/docs/9.4/sql-security-label.html "PostgreSQL 9.4 -
SECURITY LABEL") / [9.3](/docs/9.3/sql-security-label.html "PostgreSQL 9.3 -
SECURITY LABEL") / [9.2](/docs/9.2/sql-security-label.html "PostgreSQL 9.2 -
SECURITY LABEL") / [9.1](/docs/9.1/sql-security-label.html "PostgreSQL 9.1 -
SECURITY LABEL")

__

SECURITY LABEL  
---  
[Prev](sql-savepoint.html "SAVEPOINT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-select.html "SELECT")  
  
* * *

## SECURITY LABEL

SECURITY LABEL — define or change a security label applied to an object

## Synopsis

    
    
    SECURITY LABEL [ FOR _provider_ ] ON
    {
      TABLE _object_name_ |
      COLUMN _table_name_._column_name_ |
      AGGREGATE _aggregate_name_ ( _aggregate_signature_ ) |
      DATABASE _object_name_ |
      DOMAIN _object_name_ |
      EVENT TRIGGER _object_name_ |
      FOREIGN TABLE _object_name_ |
      FUNCTION _function_name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ] |
      LARGE OBJECT _large_object_oid_ |
      MATERIALIZED VIEW _object_name_ |
      [ PROCEDURAL ] LANGUAGE _object_name_ |
      PROCEDURE _procedure_name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ] |
      PUBLICATION _object_name_ |
      ROLE _object_name_ |
      ROUTINE _routine_name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ] |
      SCHEMA _object_name_ |
      SEQUENCE _object_name_ |
      SUBSCRIPTION _object_name_ |
      TABLESPACE _object_name_ |
      TYPE _object_name_ |
      VIEW _object_name_
    } IS { _string_literal_ | NULL }
    
    where _aggregate_signature_ is:
    
    * |
    [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ] |
    [ [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ] ] ORDER BY [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ]
    

## Description

`SECURITY LABEL` applies a security label to a database object. An arbitrary
number of security labels, one per label provider, can be associated with a
given database object. Label providers are loadable modules which register
themselves by using the function `register_label_provider`.

### Note

`register_label_provider` is not an SQL function; it can only be called from C
code loaded into the backend.

The label provider determines whether a given label is valid and whether it is
permissible to assign that label to a given object. The meaning of a given
label is likewise at the discretion of the label provider. PostgreSQL places
no restrictions on whether or how a label provider must interpret security
labels; it merely provides a mechanism for storing them. In practice, this
facility is intended to allow integration with label-based mandatory access
control (MAC) systems such as SELinux. Such systems make all access control
decisions based on object labels, rather than traditional discretionary access
control (DAC) concepts such as users and groups.

## Parameters

_`object_name`_  
 _`table_name.column_name`_  
 _`aggregate_name`_  
 _`function_name`_  
 _`procedure_name`_  
 _`routine_name`_

    

The name of the object to be labeled. Names of objects that reside in schemas
(tables, functions, etc.) can be schema-qualified.

_`provider`_

    

The name of the provider with which this label is to be associated. The named
provider must be loaded and must consent to the proposed labeling operation.
If exactly one provider is loaded, the provider name may be omitted for
brevity.

_`argmode`_

    

The mode of a function, procedure, or aggregate argument: `IN`, `OUT`,
`INOUT`, or `VARIADIC`. If omitted, the default is `IN`. Note that `SECURITY
LABEL` does not actually pay any attention to `OUT` arguments, since only the
input arguments are needed to determine the function's identity. So it is
sufficient to list the `IN`, `INOUT`, and `VARIADIC` arguments.

_`argname`_

    

The name of a function, procedure, or aggregate argument. Note that `SECURITY
LABEL` does not actually pay any attention to argument names, since only the
argument data types are needed to determine the function's identity.

_`argtype`_

    

The data type of a function, procedure, or aggregate argument.

_`large_object_oid`_

    

The OID of the large object.

`PROCEDURAL`

    

This is a noise word.

_`string_literal`_

    

The new setting of the security label, written as a string literal.

`NULL`

    

Write `NULL` to drop the security label.

## Examples

The following example shows how the security label of a table could be set or
changed:

    
    
    SECURITY LABEL FOR selinux ON TABLE mytable IS 'system_u:object_r:sepgsql_table_t:s0';
    

To remove the label:

    
    
    SECURITY LABEL FOR selinux ON TABLE mytable IS NULL;
    

## Compatibility

There is no `SECURITY LABEL` command in the SQL standard.

## See Also

[sepgsql](sepgsql.html "F.40. sepgsql — SELinux-, label-based mandatory access
control \(MAC\) security module"), `src/test/modules/dummy_seclabel`

* * *

[Prev](sql-savepoint.html "SAVEPOINT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-select.html "SELECT")  
---|---|---  
SAVEPOINT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SELECT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-security-label.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

