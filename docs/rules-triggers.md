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

Supported Versions: [Current](/docs/current/rules-triggers.html "PostgreSQL 17
- 41.7. Rules Versus Triggers") ([17](/docs/17/rules-triggers.html "PostgreSQL
17 - 41.7. Rules Versus Triggers")) / [16](/docs/16/rules-triggers.html
"PostgreSQL 16 - 41.7. Rules Versus Triggers") / [15](/docs/15/rules-
triggers.html "PostgreSQL 15 - 41.7. Rules Versus Triggers") /
[14](/docs/14/rules-triggers.html "PostgreSQL 14 - 41.7. Rules Versus
Triggers") / [13](/docs/13/rules-triggers.html "PostgreSQL 13 - 41.7. Rules
Versus Triggers")

Development Versions: [18](/docs/18/rules-triggers.html "PostgreSQL 18 -
41.7. Rules Versus Triggers") / [devel](/docs/devel/rules-triggers.html
"PostgreSQL devel - 41.7. Rules Versus Triggers")

Unsupported versions: [12](/docs/12/rules-triggers.html "PostgreSQL 12 -
41.7. Rules Versus Triggers") / [11](/docs/11/rules-triggers.html "PostgreSQL
11 - 41.7. Rules Versus Triggers") / [10](/docs/10/rules-triggers.html
"PostgreSQL 10 - 41.7. Rules Versus Triggers") / [9.6](/docs/9.6/rules-
triggers.html "PostgreSQL 9.6 - 41.7. Rules Versus Triggers") /
[9.5](/docs/9.5/rules-triggers.html "PostgreSQL 9.5 - 41.7. Rules Versus
Triggers") / [9.4](/docs/9.4/rules-triggers.html "PostgreSQL 9.4 - 41.7. Rules
Versus Triggers") / [9.3](/docs/9.3/rules-triggers.html "PostgreSQL 9.3 -
41.7. Rules Versus Triggers") / [9.2](/docs/9.2/rules-triggers.html
"PostgreSQL 9.2 - 41.7. Rules Versus Triggers") / [9.1](/docs/9.1/rules-
triggers.html "PostgreSQL 9.1 - 41.7. Rules Versus Triggers") /
[9.0](/docs/9.0/rules-triggers.html "PostgreSQL 9.0 - 41.7. Rules Versus
Triggers") / [8.4](/docs/8.4/rules-triggers.html "PostgreSQL 8.4 - 41.7. Rules
Versus Triggers") / [8.3](/docs/8.3/rules-triggers.html "PostgreSQL 8.3 -
41.7. Rules Versus Triggers") / [8.2](/docs/8.2/rules-triggers.html
"PostgreSQL 8.2 - 41.7. Rules Versus Triggers") / [8.1](/docs/8.1/rules-
triggers.html "PostgreSQL 8.1 - 41.7. Rules Versus Triggers") /
[8.0](/docs/8.0/rules-triggers.html "PostgreSQL 8.0 - 41.7. Rules Versus
Triggers") / [7.4](/docs/7.4/rules-triggers.html "PostgreSQL 7.4 - 41.7. Rules
Versus Triggers") / [7.3](/docs/7.3/rules-triggers.html "PostgreSQL 7.3 -
41.7. Rules Versus Triggers") / [7.2](/docs/7.2/rules-triggers.html
"PostgreSQL 7.2 - 41.7. Rules Versus Triggers") / [7.1](/docs/7.1/rules-
triggers.html "PostgreSQL 7.1 - 41.7. Rules Versus Triggers")

__

41.7. Rules Versus Triggers  
---  
[Prev](rules-status.html "41.6. Rules and Command Status")  | [Up](rules.html "Chapter 41. The Rule System") | Chapter 41. The Rule System | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xplang.html "Chapter 42. Procedural Languages")  
  
* * *

## 41.7. Rules Versus Triggers #

Many things that can be done using triggers can also be implemented using the
PostgreSQL rule system. One of the things that cannot be implemented by rules
are some kinds of constraints, especially foreign keys. It is possible to
place a qualified rule that rewrites a command to `NOTHING` if the value of a
column does not appear in another table. But then the data is silently thrown
away and that's not a good idea. If checks for valid values are required, and
in the case of an invalid value an error message should be generated, it must
be done by a trigger.

In this chapter, we focused on using rules to update views. All of the update
rule examples in this chapter can also be implemented using `INSTEAD OF`
triggers on the views. Writing such triggers is often easier than writing
rules, particularly if complex logic is required to perform the update.

For the things that can be implemented by both, which is best depends on the
usage of the database. A trigger is fired once for each affected row. A rule
modifies the query or generates an additional query. So if many rows are
affected in one statement, a rule issuing one extra command is likely to be
faster than a trigger that is called for every single row and must re-
determine what to do many times. However, the trigger approach is conceptually
far simpler than the rule approach, and is easier for novices to get right.

Here we show an example of how the choice of rules versus triggers plays out
in one situation. There are two tables:

    
    
    CREATE TABLE computer (
        hostname        text,    -- indexed
        manufacturer    text     -- indexed
    );
    
    CREATE TABLE software (
        software        text,    -- indexed
        hostname        text     -- indexed
    );
    

Both tables have many thousands of rows and the indexes on `hostname` are
unique. The rule or trigger should implement a constraint that deletes rows
from `software` that reference a deleted computer. The trigger would use this
command:

    
    
    DELETE FROM software WHERE hostname = $1;
    

Since the trigger is called for each individual row deleted from `computer`,
it can prepare and save the plan for this command and pass the `hostname`
value in the parameter. The rule would be written as:

    
    
    CREATE RULE computer_del AS ON DELETE TO computer
        DO DELETE FROM software WHERE hostname = OLD.hostname;
    

Now we look at different types of deletes. In the case of a:

    
    
    DELETE FROM computer WHERE hostname = 'mypc.local.net';
    

the table `computer` is scanned by index (fast), and the command issued by the
trigger would also use an index scan (also fast). The extra command from the
rule would be:

    
    
    DELETE FROM software WHERE computer.hostname = 'mypc.local.net'
                           AND software.hostname = computer.hostname;
    

Since there are appropriate indexes set up, the planner will create a plan of

    
    
    Nestloop
      ->  Index Scan using comp_hostidx on computer
      ->  Index Scan using soft_hostidx on software
    

So there would be not that much difference in speed between the trigger and
the rule implementation.

With the next delete we want to get rid of all the 2000 computers where the
`hostname` starts with `old`. There are two possible commands to do that. One
is:

    
    
    DELETE FROM computer WHERE hostname >= 'old'
                           AND hostname <  'ole'
    

The command added by the rule will be:

    
    
    DELETE FROM software WHERE computer.hostname >= 'old' AND computer.hostname < 'ole'
                           AND software.hostname = computer.hostname;
    

with the plan

    
    
    Hash Join
      ->  Seq Scan on software
      ->  Hash
        ->  Index Scan using comp_hostidx on computer
    

The other possible command is:

    
    
    DELETE FROM computer WHERE hostname ~ '^old';
    

which results in the following executing plan for the command added by the
rule:

    
    
    Nestloop
      ->  Index Scan using comp_hostidx on computer
      ->  Index Scan using soft_hostidx on software
    

This shows, that the planner does not realize that the qualification for
`hostname` in `computer` could also be used for an index scan on `software`
when there are multiple qualification expressions combined with `AND`, which
is what it does in the regular-expression version of the command. The trigger
will get invoked once for each of the 2000 old computers that have to be
deleted, and that will result in one index scan over `computer` and 2000 index
scans over `software`. The rule implementation will do it with two commands
that use indexes. And it depends on the overall size of the table `software`
whether the rule will still be faster in the sequential scan situation. 2000
command executions from the trigger over the SPI manager take some time, even
if all the index blocks will soon be in the cache.

The last command we look at is:

    
    
    DELETE FROM computer WHERE manufacturer = 'bim';
    

Again this could result in many rows to be deleted from `computer`. So the
trigger will again run many commands through the executor. The command
generated by the rule will be:

    
    
    DELETE FROM software WHERE computer.manufacturer = 'bim'
                           AND software.hostname = computer.hostname;
    

The plan for that command will again be the nested loop over two index scans,
only using a different index on `computer`:

    
    
    Nestloop
      ->  Index Scan using comp_manufidx on computer
      ->  Index Scan using soft_hostidx on software
    

In any of these cases, the extra commands from the rule system will be more or
less independent from the number of affected rows in a command.

The summary is, rules will only be significantly slower than triggers if their
actions result in large and badly qualified joins, a situation where the
planner fails.

* * *

[Prev](rules-status.html "41.6. Rules and Command Status")  | [Up](rules.html "Chapter 41. The Rule System") |  [Next](xplang.html "Chapter 42. Procedural Languages")  
---|---|---  
41.6. Rules and Command Status  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 42. Procedural Languages  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/rules-triggers.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

