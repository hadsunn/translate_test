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

Supported Versions: [Current](/docs/current/auth-username-maps.html
"PostgreSQL 17 - 21.2. User Name Maps") ([17](/docs/17/auth-username-maps.html
"PostgreSQL 17 - 21.2. User Name Maps")) / [16](/docs/16/auth-username-
maps.html "PostgreSQL 16 - 21.2. User Name Maps") / [15](/docs/15/auth-
username-maps.html "PostgreSQL 15 - 21.2. User Name Maps") /
[14](/docs/14/auth-username-maps.html "PostgreSQL 14 - 21.2. User Name Maps")
/ [13](/docs/13/auth-username-maps.html "PostgreSQL 13 - 21.2. User Name
Maps")

Development Versions: [18](/docs/18/auth-username-maps.html "PostgreSQL 18 -
21.2. User Name Maps") / [devel](/docs/devel/auth-username-maps.html
"PostgreSQL devel - 21.2. User Name Maps")

Unsupported versions: [12](/docs/12/auth-username-maps.html "PostgreSQL 12 -
21.2. User Name Maps") / [11](/docs/11/auth-username-maps.html "PostgreSQL 11
- 21.2. User Name Maps") / [10](/docs/10/auth-username-maps.html "PostgreSQL
10 - 21.2. User Name Maps") / [9.6](/docs/9.6/auth-username-maps.html
"PostgreSQL 9.6 - 21.2. User Name Maps") / [9.5](/docs/9.5/auth-username-
maps.html "PostgreSQL 9.5 - 21.2. User Name Maps") / [9.4](/docs/9.4/auth-
username-maps.html "PostgreSQL 9.4 - 21.2. User Name Maps") /
[9.3](/docs/9.3/auth-username-maps.html "PostgreSQL 9.3 - 21.2. User Name
Maps") / [9.2](/docs/9.2/auth-username-maps.html "PostgreSQL 9.2 - 21.2. User
Name Maps") / [9.1](/docs/9.1/auth-username-maps.html "PostgreSQL 9.1 -
21.2. User Name Maps") / [9.0](/docs/9.0/auth-username-maps.html "PostgreSQL
9.0 - 21.2. User Name Maps") / [8.4](/docs/8.4/auth-username-maps.html
"PostgreSQL 8.4 - 21.2. User Name Maps")

__

21.2. User Name Maps  
---  
[Prev](auth-pg-hba-conf.html "21.1. The pg_hba.conf File")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-methods.html "21.3. Authentication Methods")  
  
* * *

## 21.2. User Name Maps #

When using an external authentication system such as Ident or GSSAPI, the name
of the operating system user that initiated the connection might not be the
same as the database user (role) that is to be used. In this case, a user name
map can be applied to map the operating system user name to a database user.
To use user name mapping, specify `map`=_`map-name`_ in the options field in
`pg_hba.conf`. This option is supported for all authentication methods that
receive external user names. Since different mappings might be needed for
different connections, the name of the map to be used is specified in the
_`map-name`_ parameter in `pg_hba.conf` to indicate which map to use for each
individual connection.

User name maps are defined in the ident map file, which by default is named
`pg_ident.conf` and is stored in the cluster's data directory. (It is possible
to place the map file elsewhere, however; see the [ident_file](runtime-config-
file-locations.html#GUC-IDENT-FILE) configuration parameter.) The ident map
file contains lines of the general forms:

    
    
    _map-name_ _system-username_ _database-username_
    _include_ _file_
    _include_if_exists_ _file_
    _include_dir_ _directory_
    

Comments, whitespace and line continuations are handled in the same way as in
`pg_hba.conf`. The _`map-name`_ is an arbitrary name that will be used to
refer to this mapping in `pg_hba.conf`. The other two fields specify an
operating system user name and a matching database user name. The same _`map-
name`_ can be used repeatedly to specify multiple user-mappings within a
single map.

As for `pg_hba.conf`, the lines in this file can be include directives,
following the same rules.

There is no restriction regarding how many database users a given operating
system user can correspond to, nor vice versa. Thus, entries in a map should
be thought of as meaning “this operating system user is allowed to connect as
this database user”, rather than implying that they are equivalent. The
connection will be allowed if there is any map entry that pairs the user name
obtained from the external authentication system with the database user name
that the user has requested to connect as. The value `all` can be used as the
_`database-username`_ to specify that if the _`system-username`_ matches, then
this user is allowed to log in as any of the existing database users. Quoting
`all` makes the keyword lose its special meaning.

If the _`database-username`_ begins with a `+` character, then the operating
system user can login as any user belonging to that role, similarly to how
user names beginning with `+` are treated in `pg_hba.conf`. Thus, a `+` mark
means “match any of the roles that are directly or indirectly members of this
role”, while a name without a `+` mark matches only that specific role.
Quoting a username starting with a `+` makes the `+` lose its special meaning.

If the _`system-username`_ field starts with a slash (`/`), the remainder of
the field is treated as a regular expression. (See [Section
9.7.3.1](functions-matching.html#POSIX-SYNTAX-DETAILS "9.7.3.1. Regular
Expression Details") for details of PostgreSQL's regular expression syntax.)
The regular expression can include a single capture, or parenthesized
subexpression, which can then be referenced in the _`database-username`_ field
as `\1` (backslash-one). This allows the mapping of multiple user names in a
single line, which is particularly useful for simple syntax substitutions. For
example, these entries

    
    
    mymap   /^(.*)@mydomain\.com$      \1
    mymap   /^(.*)@otherdomain\.com$   guest
    

will remove the domain part for users with system user names that end with
`@mydomain.com`, and allow any user whose system name ends with
`@otherdomain.com` to log in as `guest`. Quoting a _`database-username`_
containing `\1` _does not_ make `\1` lose its special meaning.

If the _`database-username`_ field starts with a slash (`/`), the remainder of
the field is treated as a regular expression (see [Section 9.7.3.1](functions-
matching.html#POSIX-SYNTAX-DETAILS "9.7.3.1. Regular Expression Details") for
details of PostgreSQL's regular expression syntax). It is not possible to use
`\1` to use a capture from regular expression on _`system-username`_ for a
regular expression on _`database-username`_.

### Tip

Keep in mind that by default, a regular expression can match just part of a
string. It's usually wise to use `^` and `$`, as shown in the above example,
to force the match to be to the entire system user name.

The `pg_ident.conf` file is read on start-up and when the main server process
receives a SIGHUP signal. If you edit the file on an active system, you will
need to signal the postmaster (using `pg_ctl reload`, calling the SQL function
`pg_reload_conf()`, or using `kill -HUP`) to make it re-read the file.

The system view [`pg_ident_file_mappings`](view-pg-ident-file-mappings.html
"54.10. pg_ident_file_mappings") can be helpful for pre-testing changes to the
`pg_ident.conf` file, or for diagnosing problems if loading of the file did
not have the desired effects. Rows in the view with non-null `error` fields
indicate problems in the corresponding lines of the file.

A `pg_ident.conf` file that could be used in conjunction with the
`pg_hba.conf` file in [Example 21.1](auth-pg-hba-conf.html#EXAMPLE-PG-HBA.CONF
"Example 21.1. Example pg_hba.conf Entries") is shown in [Example 21.2](auth-
username-maps.html#EXAMPLE-PG-IDENT.CONF "Example 21.2. An Example
pg_ident.conf File"). In this example, anyone logged in to a machine on the
192.168 network that does not have the operating system user name `bryanh`,
`ann`, or `robert` would not be granted access. Unix user `robert` would only
be allowed access when he tries to connect as PostgreSQL user `bob`, not as
`robert` or anyone else. `ann` would only be allowed to connect as `ann`. User
`bryanh` would be allowed to connect as either `bryanh` or as `guest1`.

**Example  21.2. An Example `pg_ident.conf` File**

    
    
    # MAPNAME       SYSTEM-USERNAME         PG-USERNAME
    
    omicron         bryanh                  bryanh
    omicron         ann                     ann
    # bob has user name robert on these machines
    omicron         robert                  bob
    # bryanh can also connect as guest1
    omicron         bryanh                  guest1
    

  

* * *

[Prev](auth-pg-hba-conf.html "21.1. The pg_hba.conf File")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-methods.html "21.3. Authentication Methods")  
---|---|---  
21.1. The `pg_hba.conf` File  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.3. Authentication Methods  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-username-maps.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

