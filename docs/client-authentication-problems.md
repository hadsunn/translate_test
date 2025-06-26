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

Supported Versions: [Current](/docs/current/client-authentication-
problems.html "PostgreSQL 17 - 21.15. Authentication Problems")
([17](/docs/17/client-authentication-problems.html "PostgreSQL 17 -
21.15. Authentication Problems")) / [16](/docs/16/client-authentication-
problems.html "PostgreSQL 16 - 21.15. Authentication Problems") /
[15](/docs/15/client-authentication-problems.html "PostgreSQL 15 -
21.15. Authentication Problems") / [14](/docs/14/client-authentication-
problems.html "PostgreSQL 14 - 21.15. Authentication Problems") /
[13](/docs/13/client-authentication-problems.html "PostgreSQL 13 -
21.15. Authentication Problems")

Development Versions: [18](/docs/18/client-authentication-problems.html
"PostgreSQL 18 - 21.15. Authentication Problems") /
[devel](/docs/devel/client-authentication-problems.html "PostgreSQL devel -
21.15. Authentication Problems")

Unsupported versions: [12](/docs/12/client-authentication-problems.html
"PostgreSQL 12 - 21.15. Authentication Problems") / [11](/docs/11/client-
authentication-problems.html "PostgreSQL 11 - 21.15. Authentication Problems")
/ [10](/docs/10/client-authentication-problems.html "PostgreSQL 10 -
21.15. Authentication Problems") / [9.6](/docs/9.6/client-authentication-
problems.html "PostgreSQL 9.6 - 21.15. Authentication Problems") /
[9.5](/docs/9.5/client-authentication-problems.html "PostgreSQL 9.5 -
21.15. Authentication Problems") / [9.4](/docs/9.4/client-authentication-
problems.html "PostgreSQL 9.4 - 21.15. Authentication Problems") /
[9.3](/docs/9.3/client-authentication-problems.html "PostgreSQL 9.3 -
21.15. Authentication Problems") / [9.2](/docs/9.2/client-authentication-
problems.html "PostgreSQL 9.2 - 21.15. Authentication Problems") /
[9.1](/docs/9.1/client-authentication-problems.html "PostgreSQL 9.1 -
21.15. Authentication Problems") / [9.0](/docs/9.0/client-authentication-
problems.html "PostgreSQL 9.0 - 21.15. Authentication Problems") /
[8.4](/docs/8.4/client-authentication-problems.html "PostgreSQL 8.4 -
21.15. Authentication Problems") / [8.3](/docs/8.3/client-authentication-
problems.html "PostgreSQL 8.3 - 21.15. Authentication Problems") /
[8.2](/docs/8.2/client-authentication-problems.html "PostgreSQL 8.2 -
21.15. Authentication Problems") / [8.1](/docs/8.1/client-authentication-
problems.html "PostgreSQL 8.1 - 21.15. Authentication Problems") /
[8.0](/docs/8.0/client-authentication-problems.html "PostgreSQL 8.0 -
21.15. Authentication Problems") / [7.4](/docs/7.4/client-authentication-
problems.html "PostgreSQL 7.4 - 21.15. Authentication Problems") /
[7.3](/docs/7.3/client-authentication-problems.html "PostgreSQL 7.3 -
21.15. Authentication Problems") / [7.2](/docs/7.2/client-authentication-
problems.html "PostgreSQL 7.2 - 21.15. Authentication Problems") /
[7.1](/docs/7.1/client-authentication-problems.html "PostgreSQL 7.1 -
21.15. Authentication Problems")

__

21.15. Authentication Problems  
---  
[Prev](auth-bsd.html "21.14. BSD Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](user-manag.html "Chapter 22. Database Roles")  
  
* * *

## 21.15. Authentication Problems #

Authentication failures and related problems generally manifest themselves
through error messages like the following:

    
    
    FATAL:  no pg_hba.conf entry for host "123.123.123.123", user "andym", database "testdb"
    

This is what you are most likely to get if you succeed in contacting the
server, but it does not want to talk to you. As the message suggests, the
server refused the connection request because it found no matching entry in
its `pg_hba.conf` configuration file.

    
    
    FATAL:  password authentication failed for user "andym"
    

Messages like this indicate that you contacted the server, and it is willing
to talk to you, but not until you pass the authorization method specified in
the `pg_hba.conf` file. Check the password you are providing, or check your
Kerberos or ident software if the complaint mentions one of those
authentication types.

    
    
    FATAL:  user "andym" does not exist
    

The indicated database user name was not found.

    
    
    FATAL:  database "testdb" does not exist
    

The database you are trying to connect to does not exist. Note that if you do
not specify a database name, it defaults to the database user name.

### Tip

The server log might contain more information about an authentication failure
than is reported to the client. If you are confused about the reason for a
failure, check the server log.

* * *

[Prev](auth-bsd.html "21.14. BSD Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](user-manag.html "Chapter 22. Database Roles")  
---|---|---  
21.14. BSD Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 22. Database Roles  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/client-authentication-
problems.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

