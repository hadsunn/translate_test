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

Supported Versions: [Current](/docs/current/manage-ag-config.html "PostgreSQL
17 - 23.4. Database Configuration") ([17](/docs/17/manage-ag-config.html
"PostgreSQL 17 - 23.4. Database Configuration")) / [16](/docs/16/manage-ag-
config.html "PostgreSQL 16 - 23.4. Database Configuration") /
[15](/docs/15/manage-ag-config.html "PostgreSQL 15 - 23.4. Database
Configuration") / [14](/docs/14/manage-ag-config.html "PostgreSQL 14 -
23.4. Database Configuration") / [13](/docs/13/manage-ag-config.html
"PostgreSQL 13 - 23.4. Database Configuration")

Development Versions: [18](/docs/18/manage-ag-config.html "PostgreSQL 18 -
23.4. Database Configuration") / [devel](/docs/devel/manage-ag-config.html
"PostgreSQL devel - 23.4. Database Configuration")

Unsupported versions: [12](/docs/12/manage-ag-config.html "PostgreSQL 12 -
23.4. Database Configuration") / [11](/docs/11/manage-ag-config.html
"PostgreSQL 11 - 23.4. Database Configuration") / [10](/docs/10/manage-ag-
config.html "PostgreSQL 10 - 23.4. Database Configuration") /
[9.6](/docs/9.6/manage-ag-config.html "PostgreSQL 9.6 - 23.4. Database
Configuration") / [9.5](/docs/9.5/manage-ag-config.html "PostgreSQL 9.5 -
23.4. Database Configuration") / [9.4](/docs/9.4/manage-ag-config.html
"PostgreSQL 9.4 - 23.4. Database Configuration") / [9.3](/docs/9.3/manage-ag-
config.html "PostgreSQL 9.3 - 23.4. Database Configuration") /
[9.2](/docs/9.2/manage-ag-config.html "PostgreSQL 9.2 - 23.4. Database
Configuration") / [9.1](/docs/9.1/manage-ag-config.html "PostgreSQL 9.1 -
23.4. Database Configuration") / [9.0](/docs/9.0/manage-ag-config.html
"PostgreSQL 9.0 - 23.4. Database Configuration") / [8.4](/docs/8.4/manage-ag-
config.html "PostgreSQL 8.4 - 23.4. Database Configuration") /
[8.3](/docs/8.3/manage-ag-config.html "PostgreSQL 8.3 - 23.4. Database
Configuration") / [8.2](/docs/8.2/manage-ag-config.html "PostgreSQL 8.2 -
23.4. Database Configuration") / [8.1](/docs/8.1/manage-ag-config.html
"PostgreSQL 8.1 - 23.4. Database Configuration") / [8.0](/docs/8.0/manage-ag-
config.html "PostgreSQL 8.0 - 23.4. Database Configuration") /
[7.4](/docs/7.4/manage-ag-config.html "PostgreSQL 7.4 - 23.4. Database
Configuration") / [7.3](/docs/7.3/manage-ag-config.html "PostgreSQL 7.3 -
23.4. Database Configuration")

__

23.4. Database Configuration  
---  
[Prev](manage-ag-templatedbs.html "23.3. Template Databases")  | [Up](managing-databases.html "Chapter 23. Managing Databases") | Chapter 23. Managing Databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](manage-ag-dropdb.html "23.5. Destroying a Database")  
  
* * *

## 23.4. Database Configuration #

Recall from [Chapter 20](runtime-config.html "Chapter 20. Server
Configuration") that the PostgreSQL server provides a large number of run-time
configuration variables. You can set database-specific default values for many
of these settings.

For example, if for some reason you want to disable the GEQO optimizer for a
given database, you'd ordinarily have to either disable it for all databases
or make sure that every connecting client is careful to issue `SET geqo TO
off`. To make this setting the default within a particular database, you can
execute the command:

    
    
    ALTER DATABASE mydb SET geqo TO off;
    

This will save the setting (but not set it immediately). In subsequent
connections to this database it will appear as though `SET geqo TO off;` had
been executed just before the session started. Note that users can still alter
this setting during their sessions; it will only be the default. To undo any
such setting, use `ALTER DATABASE _`dbname`_ RESET _`varname`_`.

* * *

[Prev](manage-ag-templatedbs.html "23.3. Template Databases")  | [Up](managing-databases.html "Chapter 23. Managing Databases") |  [Next](manage-ag-dropdb.html "23.5. Destroying a Database")  
---|---|---  
23.3. Template Databases  | [Home](index.html "PostgreSQL 16.9 Documentation") |  23.5. Destroying a Database  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/manage-ag-config.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

