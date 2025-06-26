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

Supported Versions: [Current](/docs/current/auth-delay.html "PostgreSQL 17 -
F.3. auth_delay — pause on authentication failure") ([17](/docs/17/auth-
delay.html "PostgreSQL 17 - F.3. auth_delay — pause on authentication
failure")) / [16](/docs/16/auth-delay.html "PostgreSQL 16 - F.3. auth_delay —
pause on authentication failure") / [15](/docs/15/auth-delay.html "PostgreSQL
15 - F.3. auth_delay — pause on authentication failure") / [14](/docs/14/auth-
delay.html "PostgreSQL 14 - F.3. auth_delay — pause on authentication
failure") / [13](/docs/13/auth-delay.html "PostgreSQL 13 - F.3. auth_delay —
pause on authentication failure")

Development Versions: [18](/docs/18/auth-delay.html "PostgreSQL 18 -
F.3. auth_delay — pause on authentication failure") /
[devel](/docs/devel/auth-delay.html "PostgreSQL devel - F.3. auth_delay —
pause on authentication failure")

Unsupported versions: [12](/docs/12/auth-delay.html "PostgreSQL 12 -
F.3. auth_delay — pause on authentication failure") / [11](/docs/11/auth-
delay.html "PostgreSQL 11 - F.3. auth_delay — pause on authentication
failure") / [10](/docs/10/auth-delay.html "PostgreSQL 10 - F.3. auth_delay —
pause on authentication failure") / [9.6](/docs/9.6/auth-delay.html
"PostgreSQL 9.6 - F.3. auth_delay — pause on authentication failure") /
[9.5](/docs/9.5/auth-delay.html "PostgreSQL 9.5 - F.3. auth_delay — pause on
authentication failure") / [9.4](/docs/9.4/auth-delay.html "PostgreSQL 9.4 -
F.3. auth_delay — pause on authentication failure") / [9.3](/docs/9.3/auth-
delay.html "PostgreSQL 9.3 - F.3. auth_delay — pause on authentication
failure") / [9.2](/docs/9.2/auth-delay.html "PostgreSQL 9.2 - F.3. auth_delay
— pause on authentication failure") / [9.1](/docs/9.1/auth-delay.html
"PostgreSQL 9.1 - F.3. auth_delay — pause on authentication failure")

__

F.3. auth_delay — pause on authentication failure  
---  
[Prev](amcheck.html "F.2. amcheck — tools to verify table and index consistency")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auto-explain.html "F.4. auto_explain — log execution plans of slow queries")  
  
* * *

## F.3. auth_delay — pause on authentication failure #

[F.3.1. Configuration Parameters](auth-delay.html#AUTH-DELAY-CONFIGURATION-
PARAMETERS)

[F.3.2. Author](auth-delay.html#AUTH-DELAY-AUTHOR)

`auth_delay` causes the server to pause briefly before reporting
authentication failure, to make brute-force attacks on database passwords more
difficult. Note that it does nothing to prevent denial-of-service attacks, and
may even exacerbate them, since processes that are waiting before reporting
authentication failure will still consume connection slots.

In order to function, this module must be loaded via
[shared_preload_libraries](runtime-config-client.html#GUC-SHARED-PRELOAD-
LIBRARIES) in `postgresql.conf`.

### F.3.1. Configuration Parameters #

`auth_delay.milliseconds` (`integer`)

    

The number of milliseconds to wait before reporting an authentication failure.
The default is 0.

These parameters must be set in `postgresql.conf`. Typical usage might be:

    
    
    # postgresql.conf
    shared_preload_libraries = 'auth_delay'
    
    auth_delay.milliseconds = '500'
    

### F.3.2. Author #

KaiGai Kohei `<[kaigai@ak.jp.nec.com](mailto:kaigai@ak.jp.nec.com)>`

* * *

[Prev](amcheck.html "F.2. amcheck — tools to verify table and index consistency")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](auto-explain.html "F.4. auto_explain — log execution plans of slow queries")  
---|---|---  
F.2. amcheck — tools to verify table and index consistency  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.4. auto_explain — log execution plans of slow queries  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-delay.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

