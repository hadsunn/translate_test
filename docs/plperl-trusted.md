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

Supported Versions: [Current](/docs/current/plperl-trusted.html "PostgreSQL 17
- 45.5. Trusted and Untrusted PL/Perl") ([17](/docs/17/plperl-trusted.html
"PostgreSQL 17 - 45.5. Trusted and Untrusted PL/Perl")) /
[16](/docs/16/plperl-trusted.html "PostgreSQL 16 - 45.5. Trusted and Untrusted
PL/Perl") / [15](/docs/15/plperl-trusted.html "PostgreSQL 15 - 45.5. Trusted
and Untrusted PL/Perl") / [14](/docs/14/plperl-trusted.html "PostgreSQL 14 -
45.5. Trusted and Untrusted PL/Perl") / [13](/docs/13/plperl-trusted.html
"PostgreSQL 13 - 45.5. Trusted and Untrusted PL/Perl")

Development Versions: [18](/docs/18/plperl-trusted.html "PostgreSQL 18 -
45.5. Trusted and Untrusted PL/Perl") / [devel](/docs/devel/plperl-
trusted.html "PostgreSQL devel - 45.5. Trusted and Untrusted PL/Perl")

Unsupported versions: [12](/docs/12/plperl-trusted.html "PostgreSQL 12 -
45.5. Trusted and Untrusted PL/Perl") / [11](/docs/11/plperl-trusted.html
"PostgreSQL 11 - 45.5. Trusted and Untrusted PL/Perl") / [10](/docs/10/plperl-
trusted.html "PostgreSQL 10 - 45.5. Trusted and Untrusted PL/Perl") /
[9.6](/docs/9.6/plperl-trusted.html "PostgreSQL 9.6 - 45.5. Trusted and
Untrusted PL/Perl") / [9.5](/docs/9.5/plperl-trusted.html "PostgreSQL 9.5 -
45.5. Trusted and Untrusted PL/Perl") / [9.4](/docs/9.4/plperl-trusted.html
"PostgreSQL 9.4 - 45.5. Trusted and Untrusted PL/Perl") /
[9.3](/docs/9.3/plperl-trusted.html "PostgreSQL 9.3 - 45.5. Trusted and
Untrusted PL/Perl") / [9.2](/docs/9.2/plperl-trusted.html "PostgreSQL 9.2 -
45.5. Trusted and Untrusted PL/Perl") / [9.1](/docs/9.1/plperl-trusted.html
"PostgreSQL 9.1 - 45.5. Trusted and Untrusted PL/Perl") /
[9.0](/docs/9.0/plperl-trusted.html "PostgreSQL 9.0 - 45.5. Trusted and
Untrusted PL/Perl") / [8.4](/docs/8.4/plperl-trusted.html "PostgreSQL 8.4 -
45.5. Trusted and Untrusted PL/Perl") / [8.3](/docs/8.3/plperl-trusted.html
"PostgreSQL 8.3 - 45.5. Trusted and Untrusted PL/Perl") /
[8.2](/docs/8.2/plperl-trusted.html "PostgreSQL 8.2 - 45.5. Trusted and
Untrusted PL/Perl") / [8.1](/docs/8.1/plperl-trusted.html "PostgreSQL 8.1 -
45.5. Trusted and Untrusted PL/Perl") / [8.0](/docs/8.0/plperl-trusted.html
"PostgreSQL 8.0 - 45.5. Trusted and Untrusted PL/Perl") /
[7.4](/docs/7.4/plperl-trusted.html "PostgreSQL 7.4 - 45.5. Trusted and
Untrusted PL/Perl") / [7.3](/docs/7.3/plperl-trusted.html "PostgreSQL 7.3 -
45.5. Trusted and Untrusted PL/Perl")

__

45.5. Trusted and Untrusted PL/Perl  
---  
[Prev](plperl-global.html "45.4. Global Values in PL/Perl")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") | Chapter 45. PL/Perl — Perl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-triggers.html "45.6. PL/Perl Triggers")  
  
* * *

## 45.5. Trusted and Untrusted PL/Perl #

Normally, PL/Perl is installed as a “trusted” programming language named
`plperl`. In this setup, certain Perl operations are disabled to preserve
security. In general, the operations that are restricted are those that
interact with the environment. This includes file handle operations,
`require`, and `use` (for external modules). There is no way to access
internals of the database server process or to gain OS-level access with the
permissions of the server process, as a C function can do. Thus, any
unprivileged database user can be permitted to use this language.

### Warning

Trusted PL/Perl relies on the Perl `Opcode` module to preserve security. Perl
[documents](https://perldoc.perl.org/Opcode#WARNING) that the module is not
effective for the trusted PL/Perl use case. If your security needs are
incompatible with the uncertainty in that warning, consider executing `REVOKE
USAGE ON LANGUAGE plperl FROM PUBLIC`.

Here is an example of a function that will not work because file system
operations are not allowed for security reasons:

    
    
    CREATE FUNCTION badfunc() RETURNS integer AS $$
        my $tmpfile = "/tmp/badfile";
        open my $fh, '>', $tmpfile
            or elog(ERROR, qq{could not open the file "$tmpfile": $!});
        print $fh "Testing writing to a file\n";
        close $fh or elog(ERROR, qq{could not close the file "$tmpfile": $!});
        return 1;
    $$ LANGUAGE plperl;
    

The creation of this function will fail as its use of a forbidden operation
will be caught by the validator.

Sometimes it is desirable to write Perl functions that are not restricted. For
example, one might want a Perl function that sends mail. To handle these
cases, PL/Perl can also be installed as an “untrusted” language (usually
called PL/PerlU). In this case the full Perl language is available. When
installing the language, the language name `plperlu` will select the untrusted
PL/Perl variant.

The writer of a PL/PerlU function must take care that the function cannot be
used to do anything unwanted, since it will be able to do anything that could
be done by a user logged in as the database administrator. Note that the
database system allows only database superusers to create functions in
untrusted languages.

If the above function was created by a superuser using the language `plperlu`,
execution would succeed.

In the same way, anonymous code blocks written in Perl can use restricted
operations if the language is specified as `plperlu` rather than `plperl`, but
the caller must be a superuser.

### Note

While PL/Perl functions run in a separate Perl interpreter for each SQL role,
all PL/PerlU functions executed in a given session run in a single Perl
interpreter (which is not any of the ones used for PL/Perl functions). This
allows PL/PerlU functions to share data freely, but no communication can occur
between PL/Perl and PL/PerlU functions.

### Note

Perl cannot support multiple interpreters within one process unless it was
built with the appropriate flags, namely either `usemultiplicity` or
`useithreads`. (`usemultiplicity` is preferred unless you actually need to use
threads. For more details, see the perlembed man page.) If PL/Perl is used
with a copy of Perl that was not built this way, then it is only possible to
have one Perl interpreter per session, and so any one session can only execute
either PL/PerlU functions, or PL/Perl functions that are all called by the
same SQL role.

* * *

[Prev](plperl-global.html "45.4. Global Values in PL/Perl")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") |  [Next](plperl-triggers.html "45.6. PL/Perl Triggers")  
---|---|---  
45.4. Global Values in PL/Perl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.6. PL/Perl Triggers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl-trusted.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

