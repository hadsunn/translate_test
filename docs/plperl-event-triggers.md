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

Supported Versions: [Current](/docs/current/plperl-event-triggers.html
"PostgreSQL 17 - 45.7. PL/Perl Event Triggers") ([17](/docs/17/plperl-event-
triggers.html "PostgreSQL 17 - 45.7. PL/Perl Event Triggers")) /
[16](/docs/16/plperl-event-triggers.html "PostgreSQL 16 - 45.7. PL/Perl Event
Triggers") / [15](/docs/15/plperl-event-triggers.html "PostgreSQL 15 -
45.7. PL/Perl Event Triggers") / [14](/docs/14/plperl-event-triggers.html
"PostgreSQL 14 - 45.7. PL/Perl Event Triggers") / [13](/docs/13/plperl-event-
triggers.html "PostgreSQL 13 - 45.7. PL/Perl Event Triggers")

Development Versions: [18](/docs/18/plperl-event-triggers.html "PostgreSQL 18
- 45.7. PL/Perl Event Triggers") / [devel](/docs/devel/plperl-event-
triggers.html "PostgreSQL devel - 45.7. PL/Perl Event Triggers")

Unsupported versions: [12](/docs/12/plperl-event-triggers.html "PostgreSQL 12
- 45.7. PL/Perl Event Triggers") / [11](/docs/11/plperl-event-triggers.html
"PostgreSQL 11 - 45.7. PL/Perl Event Triggers") / [10](/docs/10/plperl-event-
triggers.html "PostgreSQL 10 - 45.7. PL/Perl Event Triggers") /
[9.6](/docs/9.6/plperl-event-triggers.html "PostgreSQL 9.6 - 45.7. PL/Perl
Event Triggers") / [9.5](/docs/9.5/plperl-event-triggers.html "PostgreSQL 9.5
- 45.7. PL/Perl Event Triggers") / [9.4](/docs/9.4/plperl-event-triggers.html
"PostgreSQL 9.4 - 45.7. PL/Perl Event Triggers")

__

45.7. PL/Perl Event Triggers  
---  
[Prev](plperl-triggers.html "45.6. PL/Perl Triggers")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") | Chapter 45. PL/Perl — Perl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plperl-under-the-hood.html "45.8. PL/Perl Under the Hood")  
  
* * *

## 45.7. PL/Perl Event Triggers #

PL/Perl can be used to write event trigger functions. In an event trigger
function, the hash reference `$_TD` contains information about the current
trigger event. `$_TD` is a global variable, which gets a separate local value
for each invocation of the trigger. The fields of the `$_TD` hash reference
are:

`$_TD->{event}`

    

The name of the event the trigger is fired for.

`$_TD->{tag}`

    

The command tag for which the trigger is fired.

The return value of the trigger function is ignored.

Here is an example of an event trigger function, illustrating some of the
above:

    
    
    CREATE OR REPLACE FUNCTION perlsnitch() RETURNS event_trigger AS $$
      elog(NOTICE, "perlsnitch: " . $_TD->{event} . " " . $_TD->{tag} . " ");
    $$ LANGUAGE plperl;
    
    CREATE EVENT TRIGGER perl_a_snitch
        ON ddl_command_start
        EXECUTE FUNCTION perlsnitch();
    

* * *

[Prev](plperl-triggers.html "45.6. PL/Perl Triggers")  | [Up](plperl.html "Chapter 45. PL/Perl — Perl Procedural Language") |  [Next](plperl-under-the-hood.html "45.8. PL/Perl Under the Hood")  
---|---|---  
45.6. PL/Perl Triggers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  45.8. PL/Perl Under the Hood  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plperl-event-triggers.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

