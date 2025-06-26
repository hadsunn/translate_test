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

Supported Versions: [Current](/docs/current/passwordcheck.html "PostgreSQL 17
- F.26. passwordcheck — verify password strength")
([17](/docs/17/passwordcheck.html "PostgreSQL 17 - F.26. passwordcheck —
verify password strength")) / [16](/docs/16/passwordcheck.html "PostgreSQL 16
- F.26. passwordcheck — verify password strength") /
[15](/docs/15/passwordcheck.html "PostgreSQL 15 - F.26. passwordcheck — verify
password strength") / [14](/docs/14/passwordcheck.html "PostgreSQL 14 -
F.26. passwordcheck — verify password strength") /
[13](/docs/13/passwordcheck.html "PostgreSQL 13 - F.26. passwordcheck — verify
password strength")

Development Versions: [18](/docs/18/passwordcheck.html "PostgreSQL 18 -
F.26. passwordcheck — verify password strength") /
[devel](/docs/devel/passwordcheck.html "PostgreSQL devel - F.26. passwordcheck
— verify password strength")

Unsupported versions: [12](/docs/12/passwordcheck.html "PostgreSQL 12 -
F.26. passwordcheck — verify password strength") /
[11](/docs/11/passwordcheck.html "PostgreSQL 11 - F.26. passwordcheck — verify
password strength") / [10](/docs/10/passwordcheck.html "PostgreSQL 10 -
F.26. passwordcheck — verify password strength") /
[9.6](/docs/9.6/passwordcheck.html "PostgreSQL 9.6 - F.26. passwordcheck —
verify password strength") / [9.5](/docs/9.5/passwordcheck.html "PostgreSQL
9.5 - F.26. passwordcheck — verify password strength") /
[9.4](/docs/9.4/passwordcheck.html "PostgreSQL 9.4 - F.26. passwordcheck —
verify password strength") / [9.3](/docs/9.3/passwordcheck.html "PostgreSQL
9.3 - F.26. passwordcheck — verify password strength") /
[9.2](/docs/9.2/passwordcheck.html "PostgreSQL 9.2 - F.26. passwordcheck —
verify password strength") / [9.1](/docs/9.1/passwordcheck.html "PostgreSQL
9.1 - F.26. passwordcheck — verify password strength") /
[9.0](/docs/9.0/passwordcheck.html "PostgreSQL 9.0 - F.26. passwordcheck —
verify password strength")

__

F.26. passwordcheck — verify password strength  
---  
[Prev](pageinspect.html "F.25. pageinspect — low-level inspection of database pages")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgbuffercache.html "F.27. pg_buffercache — inspect PostgreSQL  buffer cache state")  
  
* * *

## F.26. passwordcheck — verify password strength #

The `passwordcheck` module checks users' passwords whenever they are set with
[CREATE ROLE](sql-createrole.html "CREATE ROLE") or [ALTER ROLE](sql-
alterrole.html "ALTER ROLE"). If a password is considered too weak, it will be
rejected and the command will terminate with an error.

To enable this module, add `'$libdir/passwordcheck'` to
[shared_preload_libraries](runtime-config-client.html#GUC-SHARED-PRELOAD-
LIBRARIES) in `postgresql.conf`, then restart the server.

You can adapt this module to your needs by changing the source code. For
example, you can use [CrackLib](https://github.com/cracklib/cracklib) to check
passwords — this only requires uncommenting two lines in the `Makefile` and
rebuilding the module. (We cannot include CrackLib by default for license
reasons.) Without CrackLib, the module enforces a few simple rules for
password strength, which you can modify or extend as you see fit.

### Caution

To prevent unencrypted passwords from being sent across the network, written
to the server log or otherwise stolen by a database administrator, PostgreSQL
allows the user to supply pre-encrypted passwords. Many client programs make
use of this functionality and encrypt the password before sending it to the
server.

This limits the usefulness of the `passwordcheck` module, because in that case
it can only try to guess the password. For this reason, `passwordcheck` is not
recommended if your security requirements are high. It is more secure to use
an external authentication method such as GSSAPI (see [Chapter 21](client-
authentication.html "Chapter 21. Client Authentication")) than to rely on
passwords within the database.

Alternatively, you could modify `passwordcheck` to reject pre-encrypted
passwords, but forcing users to set their passwords in clear text carries its
own security risks.

* * *

[Prev](pageinspect.html "F.25. pageinspect — low-level inspection of database pages")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pgbuffercache.html "F.27. pg_buffercache — inspect PostgreSQL  buffer cache state")  
---|---|---  
F.25. pageinspect — low-level inspection of database pages  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.27. pg_buffercache — inspect PostgreSQL buffer cache state  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/passwordcheck.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

