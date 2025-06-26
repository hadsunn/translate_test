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

Supported Versions: [Current](/docs/current/plperl-funcs.html "PostgreSQL 17 -
45.1. PL/Perl Functions and Arguments") ([17](/docs/17/plperl-funcs.html
"PostgreSQL 17 - 45.1. PL/Perl Functions and Arguments")) /
[16](/docs/16/plperl-funcs.html "PostgreSQL 16 - 45.1. PL/Perl Functions and
Arguments") / [15](/docs/15/plperl-funcs.html "PostgreSQL 15 - 45.1. PL/Perl
Functions and Arguments") / [14](/docs/14/plperl-funcs.html "PostgreSQL 14 -
45.1. PL/Perl Functions and Arguments") / [13](/docs/13/plperl-funcs.html
"PostgreSQL 13 - 45.1. PL/Perl Functions and Arguments")

Development Versions: [18](/docs/18/plperl-funcs.html "PostgreSQL 18 -
45.1. PL/Perl Functions and Arguments") / [devel](/docs/devel/plperl-
funcs.html "PostgreSQL devel - 45.1. PL/Perl Functions and Arguments")

Unsupported versions: [12](/docs/12/plperl-funcs.html "PostgreSQL 12 -
45.1. PL/Perl Functions and Arguments") / [11](/docs/11/plperl-funcs.html
"PostgreSQL 11 - 45.1. PL/Perl Functions and Arguments") /
[10](/docs/10/plperl-funcs.html "PostgreSQL 10 - 45.1. PL/Perl Functions and
Arguments") / [9.6](/docs/9.6/plperl-funcs.html "PostgreSQL 9.6 -
45.1. PL/Perl Functions and Arguments") / [9.5](/docs/9.5/plperl-funcs.html
"PostgreSQL 9.5 - 45.1. PL/Perl Functions and Arguments") /
[9.4](/docs/9.4/plperl-funcs.html "PostgreSQL 9.4 - 45.1. PL/Perl Functions
and Arguments") / [9.3](/docs/9.3/plperl-funcs.html "PostgreSQL 9.3 -
45.1. PL/Perl Functions and Arguments") / [9.2](/docs/9.2/plperl-funcs.html
"PostgreSQL 9.2 - 45.1. PL/Perl Functions and Arguments") /
[9.1](/docs/9.1/plperl-funcs.html "PostgreSQL 9.1 - 45.1. PL/Perl Functions
and Arguments") / [9.0](/docs/9.0/plperl-funcs.html "PostgreSQL 9.0 -
45.1. PL/Perl Functions and Arguments") / [8.4](/docs/8.4/plperl-funcs.html
"PostgreSQL 8.4 - 45.1. PL/Perl Functions and Arguments") /
[8.3](/docs/8.3/plperl-funcs.html "PostgreSQL 8.3 - 45.1. PL/Perl Functions
and Arguments") / [8.2](/docs/8.2/plperl-funcs.html "PostgreSQL 8.2 -
45.1. PL/Perl Functions and Arguments")

__

45.1. PL/Perl Functions and Arguments  
---  
[Prev](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") | Chapter 45. PL/Perl — Perl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-data.html "45.2. Data Values in PL/Perl")  
  
* * *

## 45.1. PL/Perl Functions and Arguments #

To create a function in the PL/Perl language, use the standard [CREATE
FUNCTION](sql-createfunction.html "CREATE FUNCTION") syntax:

    
    
    CREATE FUNCTION _funcname_ (_argument-types_)
    RETURNS _return-type_
    -- function attributes can go here
    AS $$
        # PL/Perl function body goes here
    $$ LANGUAGE plperl;
    

The body of the function is ordinary Perl code. In fact, the PL/Perl glue code
wraps it inside a Perl subroutine. A PL/Perl function is called in a scalar
context, so it can't return a list. You can return non-scalar values (arrays,
records, and sets) by returning a reference, as discussed below.

In a PL/Perl procedure, any return value from the Perl code is ignored.

PL/Perl also supports anonymous code blocks called with the [DO](sql-do.html
"DO") statement:

    
    
    DO $$
        # PL/Perl code
    $$ LANGUAGE plperl;
    

An anonymous code block receives no arguments, and whatever value it might
return is discarded. Otherwise it behaves just like a function.

### Note

The use of named nested subroutines is dangerous in Perl, especially if they
refer to lexical variables in the enclosing scope. Because a PL/Perl function
is wrapped in a subroutine, any named subroutine you place inside one will be
nested. In general, it is far safer to create anonymous subroutines which you
call via a coderef. For more information, see the entries for `Variable "%s"
will not stay shared` and `Variable "%s" is not available` in the perldiag man
page, or search the Internet for “perl nested named subroutine”.

The syntax of the `CREATE FUNCTION` command requires the function body to be
written as a string constant. It is usually most convenient to use dollar
quoting (see [Section 4.1.2.4](sql-syntax-lexical.html#SQL-SYNTAX-DOLLAR-
QUOTING "4.1.2.4. Dollar-Quoted String Constants")) for the string constant.
If you choose to use escape string syntax `E''`, you must double any single
quote marks (`'`) and backslashes (`\`) used in the body of the function (see
[Section 4.1.2.1](sql-syntax-lexical.html#SQL-SYNTAX-STRINGS "4.1.2.1. String
Constants")).

Arguments and results are handled as in any other Perl subroutine: arguments
are passed in `@_`, and a result value is returned with `return` or as the
last expression evaluated in the function.

For example, a function returning the greater of two integer values could be
defined as:

    
    
    CREATE FUNCTION perl_max (integer, integer) RETURNS integer AS $$
        if ($_[0] > $_[1]) { return $_[0]; }
        return $_[1];
    $$ LANGUAGE plperl;
    

### Note

Arguments will be converted from the database's encoding to UTF-8 for use
inside PL/Perl, and then converted from UTF-8 back to the database encoding
upon return.

If an SQL null value is passed to a function, the argument value will appear
as “undefined” in Perl. The above function definition will not behave very
nicely with null inputs (in fact, it will act as though they are zeroes). We
could add `STRICT` to the function definition to make PostgreSQL do something
more reasonable: if a null value is passed, the function will not be called at
all, but will just return a null result automatically. Alternatively, we could
check for undefined inputs in the function body. For example, suppose that we
wanted `perl_max` with one null and one nonnull argument to return the nonnull
argument, rather than a null value:

    
    
    CREATE FUNCTION perl_max (integer, integer) RETURNS integer AS $$
        my ($x, $y) = @_;
        if (not defined $x) {
            return undef if not defined $y;
            return $y;
        }
        return $x if not defined $y;
        return $x if $x > $y;
        return $y;
    $$ LANGUAGE plperl;
    

As shown above, to return an SQL null value from a PL/Perl function, return an
undefined value. This can be done whether the function is strict or not.

Anything in a function argument that is not a reference is a string, which is
in the standard PostgreSQL external text representation for the relevant data
type. In the case of ordinary numeric or text types, Perl will just do the
right thing and the programmer will normally not have to worry about it.
However, in other cases the argument will need to be converted into a form
that is more usable in Perl. For example, the `decode_bytea` function can be
used to convert an argument of type `bytea` into unescaped binary.

Similarly, values passed back to PostgreSQL must be in the external text
representation format. For example, the `encode_bytea` function can be used to
escape binary data for a return value of type `bytea`.

One case that is particularly important is boolean values. As just stated, the
default behavior for `bool` values is that they are passed to Perl as text,
thus either `'t'` or `'f'`. This is problematic, since Perl will not treat
`'f'` as false! It is possible to improve matters by using a “transform” (see
[CREATE TRANSFORM](sql-createtransform.html "CREATE TRANSFORM")). Suitable
transforms are provided by the `bool_plperl` extension. To use it, install the
extension:

    
    
    CREATE EXTENSION bool_plperl;  -- or bool_plperlu for PL/PerlU
    

Then use the `TRANSFORM` function attribute for a PL/Perl function that takes
or returns `bool`, for example:

    
    
    CREATE FUNCTION perl_and(bool, bool) RETURNS bool
    TRANSFORM FOR TYPE bool
    AS $$
      my ($a, $b) = @_;
      return $a && $b;
    $$ LANGUAGE plperl;
    

When this transform is applied, `bool` arguments will be seen by Perl as being
`1` or empty, thus properly true or false. If the function result is type
`bool`, it will be true or false according to whether Perl would evaluate the
returned value as true. Similar transformations are also performed for boolean
query arguments and results of SPI queries performed inside the function
([Section 45.3.1](plperl-builtins.html#PLPERL-DATABASE "45.3.1. Database
Access from PL/Perl")).

Perl can return PostgreSQL arrays as references to Perl arrays. Here is an
example:

    
    
    CREATE OR REPLACE function returns_array()
    RETURNS text[][] AS $$
        return [['a"b','c,d'],['e\\f','g']];
    $$ LANGUAGE plperl;
    
    select returns_array();
    

Perl passes PostgreSQL arrays as a blessed `PostgreSQL::InServer::ARRAY`
object. This object may be treated as an array reference or a string, allowing
for backward compatibility with Perl code written for PostgreSQL versions
below 9.1 to run. For example:

    
    
    CREATE OR REPLACE FUNCTION concat_array_elements(text[]) RETURNS TEXT AS $$
        my $arg = shift;
        my $result = "";
        return undef if (!defined $arg);
    
        # as an array reference
        for (@$arg) {
            $result .= $_;
        }
    
        # also works as a string
        $result .= $arg;
    
        return $result;
    $$ LANGUAGE plperl;
    
    SELECT concat_array_elements(ARRAY['PL','/','Perl']);
    

### Note

Multidimensional arrays are represented as references to lower-dimensional
arrays of references in a way common to every Perl programmer.

Composite-type arguments are passed to the function as references to hashes.
The keys of the hash are the attribute names of the composite type. Here is an
example:

    
    
    CREATE TABLE employee (
        name text,
        basesalary integer,
        bonus integer
    );
    
    CREATE FUNCTION empcomp(employee) RETURNS integer AS $$
        my ($emp) = @_;
        return $emp->{basesalary} + $emp->{bonus};
    $$ LANGUAGE plperl;
    
    SELECT name, empcomp(employee.*) FROM employee;
    

A PL/Perl function can return a composite-type result using the same approach:
return a reference to a hash that has the required attributes. For example:

    
    
    CREATE TYPE testrowperl AS (f1 integer, f2 text, f3 text);
    
    CREATE OR REPLACE FUNCTION perl_row() RETURNS testrowperl AS $$
        return {f2 => 'hello', f1 => 1, f3 => 'world'};
    $$ LANGUAGE plperl;
    
    SELECT * FROM perl_row();
    

Any columns in the declared result data type that are not present in the hash
will be returned as null values.

Similarly, output arguments of procedures can be returned as a hash reference:

    
    
    CREATE PROCEDURE perl_triple(INOUT a integer, INOUT b integer) AS $$
        my ($a, $b) = @_;
        return {a => $a * 3, b => $b * 3};
    $$ LANGUAGE plperl;
    
    CALL perl_triple(5, 10);
    

PL/Perl functions can also return sets of either scalar or composite types.
Usually you'll want to return rows one at a time, both to speed up startup
time and to keep from queuing up the entire result set in memory. You can do
this with `return_next` as illustrated below. Note that after the last
`return_next`, you must put either `return` or (better) `return undef`.

    
    
    CREATE OR REPLACE FUNCTION perl_set_int(int)
    RETURNS SETOF INTEGER AS $$
        foreach (0..$_[0]) {
            return_next($_);
        }
        return undef;
    $$ LANGUAGE plperl;
    
    SELECT * FROM perl_set_int(5);
    
    CREATE OR REPLACE FUNCTION perl_set()
    RETURNS SETOF testrowperl AS $$
        return_next({ f1 => 1, f2 => 'Hello', f3 => 'World' });
        return_next({ f1 => 2, f2 => 'Hello', f3 => 'PostgreSQL' });
        return_next({ f1 => 3, f2 => 'Hello', f3 => 'PL/Perl' });
        return undef;
    $$ LANGUAGE plperl;
    

For small result sets, you can return a reference to an array that contains
either scalars, references to arrays, or references to hashes for simple
types, array types, and composite types, respectively. Here are some simple
examples of returning the entire result set as an array reference:

    
    
    CREATE OR REPLACE FUNCTION perl_set_int(int) RETURNS SETOF INTEGER AS $$
        return [0..$_[0]];
    $$ LANGUAGE plperl;
    
    SELECT * FROM perl_set_int(5);
    
    CREATE OR REPLACE FUNCTION perl_set() RETURNS SETOF testrowperl AS $$
        return [
            { f1 => 1, f2 => 'Hello', f3 => 'World' },
            { f1 => 2, f2 => 'Hello', f3 => 'PostgreSQL' },
            { f1 => 3, f2 => 'Hello', f3 => 'PL/Perl' }
        ];
    $$ LANGUAGE plperl;
    
    SELECT * FROM perl_set();
    

If you wish to use the `strict` pragma with your code you have a few options.
For temporary global use you can `SET` `plperl.use_strict` to true. This will
affect subsequent compilations of PL/Perl functions, but not functions already
compiled in the current session. For permanent global use you can set
`plperl.use_strict` to true in the `postgresql.conf` file.

For permanent use in specific functions you can simply put:

    
    
    use strict;
    

at the top of the function body.

The `feature` pragma is also available to `use` if your Perl is version 5.10.0
or higher.

* * *

[Prev](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") |  [Next](plperl-data.html "45.2. Data Values in PL/Perl")  
---|---|---  
Chapter 45. PL/Perl — Perl Procedural Language  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.2. Data Values in PL/Perl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl-funcs.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

