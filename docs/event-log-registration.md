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

Supported Versions: [Current](/docs/current/event-log-registration.html
"PostgreSQL 17 - 19.12. Registering Event Log on Windows")
([17](/docs/17/event-log-registration.html "PostgreSQL 17 - 19.12. Registering
Event Log on Windows")) / [16](/docs/16/event-log-registration.html
"PostgreSQL 16 - 19.12. Registering Event Log on Windows") /
[15](/docs/15/event-log-registration.html "PostgreSQL 15 - 19.12. Registering
Event Log on Windows") / [14](/docs/14/event-log-registration.html "PostgreSQL
14 - 19.12. Registering Event Log on Windows") / [13](/docs/13/event-log-
registration.html "PostgreSQL 13 - 19.12. Registering Event Log on Windows")

Development Versions: [18](/docs/18/event-log-registration.html "PostgreSQL 18
- 19.12. Registering Event Log on Windows") / [devel](/docs/devel/event-log-
registration.html "PostgreSQL devel - 19.12. Registering Event Log on
Windows")

Unsupported versions: [12](/docs/12/event-log-registration.html "PostgreSQL 12
- 19.12. Registering Event Log on Windows") / [11](/docs/11/event-log-
registration.html "PostgreSQL 11 - 19.12. Registering Event Log on Windows") /
[10](/docs/10/event-log-registration.html "PostgreSQL 10 - 19.12. Registering
Event Log on Windows") / [9.6](/docs/9.6/event-log-registration.html
"PostgreSQL 9.6 - 19.12. Registering Event Log on Windows") /
[9.5](/docs/9.5/event-log-registration.html "PostgreSQL 9.5 -
19.12. Registering Event Log on Windows") / [9.4](/docs/9.4/event-log-
registration.html "PostgreSQL 9.4 - 19.12. Registering Event Log on Windows")
/ [9.3](/docs/9.3/event-log-registration.html "PostgreSQL 9.3 -
19.12. Registering Event Log on Windows") / [9.2](/docs/9.2/event-log-
registration.html "PostgreSQL 9.2 - 19.12. Registering Event Log on Windows")

__

19.12. Registering Event Log on Windows  
---  
[Prev](ssh-tunnels.html "19.11. Secure TCP/IP Connections with SSH Tunnels")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config.html "Chapter 20. Server Configuration")  
  
* * *

## 19.12. Registering Event Log on Windows #

To register a Windows event log library with the operating system, issue this
command:

    
    
    **regsvr32 _pgsql_library_directory_ /pgevent.dll**
    

This creates registry entries used by the event viewer, under the default
event source named `PostgreSQL`.

To specify a different event source name (see [event_source](runtime-config-
logging.html#GUC-EVENT-SOURCE)), use the `/n` and `/i` options:

    
    
    **regsvr32 /n /i:_event_source_name_ _pgsql_library_directory_ /pgevent.dll**
    

To unregister the event log library from the operating system, issue this
command:

    
    
    **regsvr32 /u [/i:_event_source_name_] _pgsql_library_directory_ /pgevent.dll**
    

### Note

To enable event logging in the database server, modify
[log_destination](runtime-config-logging.html#GUC-LOG-DESTINATION) to include
`eventlog` in `postgresql.conf`.

* * *

[Prev](ssh-tunnels.html "19.11. Secure TCP/IP Connections with SSH Tunnels")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](runtime-config.html "Chapter 20. Server Configuration")  
---|---|---  
19.11. Secure TCP/IP Connections with SSH Tunnels  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 20. Server Configuration  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-log-registration.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

