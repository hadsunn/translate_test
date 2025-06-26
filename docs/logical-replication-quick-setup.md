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

Supported Versions: [Current](/docs/current/logical-replication-quick-
setup.html "PostgreSQL 17 - 31.11. Quick Setup") ([17](/docs/17/logical-
replication-quick-setup.html "PostgreSQL 17 - 31.11. Quick Setup")) /
[16](/docs/16/logical-replication-quick-setup.html "PostgreSQL 16 -
31.11. Quick Setup") / [15](/docs/15/logical-replication-quick-setup.html
"PostgreSQL 15 - 31.11. Quick Setup") / [14](/docs/14/logical-replication-
quick-setup.html "PostgreSQL 14 - 31.11. Quick Setup") /
[13](/docs/13/logical-replication-quick-setup.html "PostgreSQL 13 -
31.11. Quick Setup")

Development Versions: [18](/docs/18/logical-replication-quick-setup.html
"PostgreSQL 18 - 31.11. Quick Setup") / [devel](/docs/devel/logical-
replication-quick-setup.html "PostgreSQL devel - 31.11. Quick Setup")

Unsupported versions: [12](/docs/12/logical-replication-quick-setup.html
"PostgreSQL 12 - 31.11. Quick Setup") / [11](/docs/11/logical-replication-
quick-setup.html "PostgreSQL 11 - 31.11. Quick Setup") /
[10](/docs/10/logical-replication-quick-setup.html "PostgreSQL 10 -
31.11. Quick Setup")

__

31.11. Quick Setup  
---  
[Prev](logical-replication-config.html "31.10. Configuration Settings")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)")  
  
* * *

## 31.11. Quick Setup #

First set the configuration options in `postgresql.conf`:

    
    
    wal_level = logical
    

The other required settings have default values that are sufficient for a
basic setup.

`pg_hba.conf` needs to be adjusted to allow replication (the values here
depend on your actual network configuration and user you want to use for
connecting):

    
    
    host     all     repuser     0.0.0.0/0     md5
    

Then on the publisher database:

    
    
    CREATE PUBLICATION mypub FOR TABLE users, departments;
    

And on the subscriber database:

    
    
    CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;
    

The above will start the replication process, which synchronizes the initial
table contents of the tables `users` and `departments` and then starts
replicating incremental changes to those tables.

* * *

[Prev](logical-replication-config.html "31.10. Configuration Settings")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)")  
---|---|---  
31.10. Configuration Settings  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 32. Just-in-Time Compilation (JIT)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-quick-
setup.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

