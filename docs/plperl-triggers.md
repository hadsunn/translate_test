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

Supported Versions: [Current](/docs/current/plperl-triggers.html "PostgreSQL
17 - 45.6. PL/Perl Triggers") ([17](/docs/17/plperl-triggers.html "PostgreSQL
17 - 45.6. PL/Perl Triggers")) / [16](/docs/16/plperl-triggers.html
"PostgreSQL 16 - 45.6. PL/Perl Triggers") / [15](/docs/15/plperl-triggers.html
"PostgreSQL 15 - 45.6. PL/Perl Triggers") / [14](/docs/14/plperl-triggers.html
"PostgreSQL 14 - 45.6. PL/Perl Triggers") / [13](/docs/13/plperl-triggers.html
"PostgreSQL 13 - 45.6. PL/Perl Triggers")

Development Versions: [18](/docs/18/plperl-triggers.html "PostgreSQL 18 -
45.6. PL/Perl Triggers") / [devel](/docs/devel/plperl-triggers.html
"PostgreSQL devel - 45.6. PL/Perl Triggers")

Unsupported versions: [12](/docs/12/plperl-triggers.html "PostgreSQL 12 -
45.6. PL/Perl Triggers") / [11](/docs/11/plperl-triggers.html "PostgreSQL 11 -
45.6. PL/Perl Triggers") / [10](/docs/10/plperl-triggers.html "PostgreSQL 10 -
45.6. PL/Perl Triggers") / [9.6](/docs/9.6/plperl-triggers.html "PostgreSQL
9.6 - 45.6. PL/Perl Triggers") / [9.5](/docs/9.5/plperl-triggers.html
"PostgreSQL 9.5 - 45.6. PL/Perl Triggers") / [9.4](/docs/9.4/plperl-
triggers.html "PostgreSQL 9.4 - 45.6. PL/Perl Triggers") /
[9.3](/docs/9.3/plperl-triggers.html "PostgreSQL 9.3 - 45.6. PL/Perl
Triggers") / [9.2](/docs/9.2/plperl-triggers.html "PostgreSQL 9.2 -
45.6. PL/Perl Triggers") / [9.1](/docs/9.1/plperl-triggers.html "PostgreSQL
9.1 - 45.6. PL/Perl Triggers") / [9.0](/docs/9.0/plperl-triggers.html
"PostgreSQL 9.0 - 45.6. PL/Perl Triggers") / [8.4](/docs/8.4/plperl-
triggers.html "PostgreSQL 8.4 - 45.6. PL/Perl Triggers") /
[8.3](/docs/8.3/plperl-triggers.html "PostgreSQL 8.3 - 45.6. PL/Perl
Triggers") / [8.2](/docs/8.2/plperl-triggers.html "PostgreSQL 8.2 -
45.6. PL/Perl Triggers") / [8.1](/docs/8.1/plperl-triggers.html "PostgreSQL
8.1 - 45.6. PL/Perl Triggers") / [8.0](/docs/8.0/plperl-triggers.html
"PostgreSQL 8.0 - 45.6. PL/Perl Triggers")

__

45.6. PL/Perl Triggers  
---  
[Prev](plperl-trusted.html "45.5. Trusted and Untrusted PL/Perl")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") | Chapter 45. PL/Perl — Perl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-event-triggers.html "45.7. PL/Perl Event Triggers")  
  
* * *

## 45.6. PL/Perl Triggers #

PL/Perl can be used to write trigger functions. In a trigger function, the
hash reference `$_TD` contains information about the current trigger event.
`$_TD` is a global variable, which gets a separate local value for each
invocation of the trigger. The fields of the `$_TD` hash reference are:

`$_TD->{new}{foo}`

    

`NEW` value of column `foo`

`$_TD->{old}{foo}`

    

`OLD` value of column `foo`

`$_TD->{name}`

    

Name of the trigger being called

`$_TD->{event}`

    

Trigger event: `INSERT`, `UPDATE`, `DELETE`, `TRUNCATE`, or `UNKNOWN`

`$_TD->{when}`

    

When the trigger was called: `BEFORE`, `AFTER`, `INSTEAD OF`, or `UNKNOWN`

`$_TD->{level}`

    

The trigger level: `ROW`, `STATEMENT`, or `UNKNOWN`

`$_TD->{relid}`

    

OID of the table on which the trigger fired

`$_TD->{table_name}`

    

Name of the table on which the trigger fired

`$_TD->{relname}`

    

Name of the table on which the trigger fired. This has been deprecated, and
could be removed in a future release. Please use $_TD->{table_name} instead.

`$_TD->{table_schema}`

    

Name of the schema in which the table on which the trigger fired, is

`$_TD->{argc}`

    

Number of arguments of the trigger function

`@{$_TD->{args}}`

    

Arguments of the trigger function. Does not exist if `$_TD->{argc}` is 0.

Row-level triggers can return one of the following:

`return;`

    

Execute the operation

`"SKIP"`

    

Don't execute the operation

`"MODIFY"`

    

Indicates that the `NEW` row was modified by the trigger function

Here is an example of a trigger function, illustrating some of the above:

    
    
    CREATE TABLE test (
        i int,
        v varchar
    );
    
    CREATE OR REPLACE FUNCTION valid_id() RETURNS trigger AS $$
        if (($_TD->{new}{i} >= 100) || ($_TD->{new}{i} <= 0)) {
            return "SKIP";    # skip INSERT/UPDATE command
        } elsif ($_TD->{new}{v} ne "immortal") {
            $_TD->{new}{v} .= "(modified by trigger)";
            return "MODIFY";  # modify row and execute INSERT/UPDATE command
        } else {
            return;           # execute INSERT/UPDATE command
        }
    $$ LANGUAGE plperl;
    
    CREATE TRIGGER test_valid_id_trig
        BEFORE INSERT OR UPDATE ON test
        FOR EACH ROW EXECUTE FUNCTION valid_id();
    

* * *

[Prev](plperl-trusted.html "45.5. Trusted and Untrusted PL/Perl")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") |  [Next](plperl-event-triggers.html "45.7. PL/Perl Event Triggers")  
---|---|---  
45.5. Trusted and Untrusted PL/Perl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.7. PL/Perl Event Triggers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl-triggers.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

