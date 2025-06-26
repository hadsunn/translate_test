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

Supported Versions: [Current](/docs/current/plperl-global.html "PostgreSQL 17
- 45.4. Global Values in PL/Perl") ([17](/docs/17/plperl-global.html
"PostgreSQL 17 - 45.4. Global Values in PL/Perl")) / [16](/docs/16/plperl-
global.html "PostgreSQL 16 - 45.4. Global Values in PL/Perl") /
[15](/docs/15/plperl-global.html "PostgreSQL 15 - 45.4. Global Values in
PL/Perl") / [14](/docs/14/plperl-global.html "PostgreSQL 14 - 45.4. Global
Values in PL/Perl") / [13](/docs/13/plperl-global.html "PostgreSQL 13 -
45.4. Global Values in PL/Perl")

Development Versions: [18](/docs/18/plperl-global.html "PostgreSQL 18 -
45.4. Global Values in PL/Perl") / [devel](/docs/devel/plperl-global.html
"PostgreSQL devel - 45.4. Global Values in PL/Perl")

Unsupported versions: [12](/docs/12/plperl-global.html "PostgreSQL 12 -
45.4. Global Values in PL/Perl") / [11](/docs/11/plperl-global.html
"PostgreSQL 11 - 45.4. Global Values in PL/Perl") / [10](/docs/10/plperl-
global.html "PostgreSQL 10 - 45.4. Global Values in PL/Perl") /
[9.6](/docs/9.6/plperl-global.html "PostgreSQL 9.6 - 45.4. Global Values in
PL/Perl") / [9.5](/docs/9.5/plperl-global.html "PostgreSQL 9.5 - 45.4. Global
Values in PL/Perl") / [9.4](/docs/9.4/plperl-global.html "PostgreSQL 9.4 -
45.4. Global Values in PL/Perl") / [9.3](/docs/9.3/plperl-global.html
"PostgreSQL 9.3 - 45.4. Global Values in PL/Perl") / [9.2](/docs/9.2/plperl-
global.html "PostgreSQL 9.2 - 45.4. Global Values in PL/Perl") /
[9.1](/docs/9.1/plperl-global.html "PostgreSQL 9.1 - 45.4. Global Values in
PL/Perl") / [9.0](/docs/9.0/plperl-global.html "PostgreSQL 9.0 - 45.4. Global
Values in PL/Perl") / [8.4](/docs/8.4/plperl-global.html "PostgreSQL 8.4 -
45.4. Global Values in PL/Perl") / [8.3](/docs/8.3/plperl-global.html
"PostgreSQL 8.3 - 45.4. Global Values in PL/Perl") / [8.2](/docs/8.2/plperl-
global.html "PostgreSQL 8.2 - 45.4. Global Values in PL/Perl") /
[8.1](/docs/8.1/plperl-global.html "PostgreSQL 8.1 - 45.4. Global Values in
PL/Perl") / [8.0](/docs/8.0/plperl-global.html "PostgreSQL 8.0 - 45.4. Global
Values in PL/Perl")

__

45.4. Global Values in PL/Perl  
---  
[Prev](plperl-builtins.html "45.3. Built-in Functions")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") | Chapter 45. PL/Perl — Perl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-trusted.html "45.5. Trusted and Untrusted PL/Perl")  
  
* * *

## 45.4. Global Values in PL/Perl #

You can use the global hash `%_SHARED` to store data, including code
references, between function calls for the lifetime of the current session.

Here is a simple example for shared data:

    
    
    CREATE OR REPLACE FUNCTION set_var(name text, val text) RETURNS text AS $$
        if ($_SHARED{$_[0]} = $_[1]) {
            return 'ok';
        } else {
            return "cannot set shared variable $_[0] to $_[1]";
        }
    $$ LANGUAGE plperl;
    
    CREATE OR REPLACE FUNCTION get_var(name text) RETURNS text AS $$
        return $_SHARED{$_[0]};
    $$ LANGUAGE plperl;
    
    SELECT set_var('sample', 'Hello, PL/Perl!  How''s tricks?');
    SELECT get_var('sample');
    

Here is a slightly more complicated example using a code reference:

    
    
    CREATE OR REPLACE FUNCTION myfuncs() RETURNS void AS $$
        $_SHARED{myquote} = sub {
            my $arg = shift;
            $arg =~ s/(['\\])/\\$1/g;
            return "'$arg'";
        };
    $$ LANGUAGE plperl;
    
    SELECT myfuncs(); /* initializes the function */
    
    /* Set up a function that uses the quote function */
    
    CREATE OR REPLACE FUNCTION use_quote(TEXT) RETURNS text AS $$
        my $text_to_quote = shift;
        my $qfunc = $_SHARED{myquote};
        return &$qfunc($text_to_quote);
    $$ LANGUAGE plperl;
    

(You could have replaced the above with the one-liner `return
$_SHARED{myquote}->($_[0]);` at the expense of readability.)

For security reasons, PL/Perl executes functions called by any one SQL role in
a separate Perl interpreter for that role. This prevents accidental or
malicious interference by one user with the behavior of another user's PL/Perl
functions. Each such interpreter has its own value of the `%_SHARED` variable
and other global state. Thus, two PL/Perl functions will share the same value
of `%_SHARED` if and only if they are executed by the same SQL role. In an
application wherein a single session executes code under multiple SQL roles
(via `SECURITY DEFINER` functions, use of `SET ROLE`, etc.) you may need to
take explicit steps to ensure that PL/Perl functions can share data via
`%_SHARED`. To do that, make sure that functions that should communicate are
owned by the same user, and mark them `SECURITY DEFINER`. You must of course
take care that such functions can't be used to do anything unintended.

* * *

[Prev](plperl-builtins.html "45.3. Built-in Functions")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") |  [Next](plperl-trusted.html "45.5. Trusted and Untrusted PL/Perl")  
---|---|---  
45.3. Built-in Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.5. Trusted and Untrusted PL/Perl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl-global.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

