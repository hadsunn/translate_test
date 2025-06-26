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

Supported Versions: [Current](/docs/current/catalog-pg-authid.html "PostgreSQL
17 - 53.8. pg_authid") ([17](/docs/17/catalog-pg-authid.html "PostgreSQL 17 -
53.8. pg_authid")) / [16](/docs/16/catalog-pg-authid.html "PostgreSQL 16 -
53.8. pg_authid") / [15](/docs/15/catalog-pg-authid.html "PostgreSQL 15 -
53.8. pg_authid") / [14](/docs/14/catalog-pg-authid.html "PostgreSQL 14 -
53.8. pg_authid") / [13](/docs/13/catalog-pg-authid.html "PostgreSQL 13 -
53.8. pg_authid")

Development Versions: [18](/docs/18/catalog-pg-authid.html "PostgreSQL 18 -
53.8. pg_authid") / [devel](/docs/devel/catalog-pg-authid.html "PostgreSQL
devel - 53.8. pg_authid")

Unsupported versions: [12](/docs/12/catalog-pg-authid.html "PostgreSQL 12 -
53.8. pg_authid") / [11](/docs/11/catalog-pg-authid.html "PostgreSQL 11 -
53.8. pg_authid") / [10](/docs/10/catalog-pg-authid.html "PostgreSQL 10 -
53.8. pg_authid") / [9.6](/docs/9.6/catalog-pg-authid.html "PostgreSQL 9.6 -
53.8. pg_authid") / [9.5](/docs/9.5/catalog-pg-authid.html "PostgreSQL 9.5 -
53.8. pg_authid") / [9.4](/docs/9.4/catalog-pg-authid.html "PostgreSQL 9.4 -
53.8. pg_authid") / [9.3](/docs/9.3/catalog-pg-authid.html "PostgreSQL 9.3 -
53.8. pg_authid") / [9.2](/docs/9.2/catalog-pg-authid.html "PostgreSQL 9.2 -
53.8. pg_authid") / [9.1](/docs/9.1/catalog-pg-authid.html "PostgreSQL 9.1 -
53.8. pg_authid") / [9.0](/docs/9.0/catalog-pg-authid.html "PostgreSQL 9.0 -
53.8. pg_authid") / [8.4](/docs/8.4/catalog-pg-authid.html "PostgreSQL 8.4 -
53.8. pg_authid") / [8.3](/docs/8.3/catalog-pg-authid.html "PostgreSQL 8.3 -
53.8. pg_authid") / [8.2](/docs/8.2/catalog-pg-authid.html "PostgreSQL 8.2 -
53.8. pg_authid") / [8.1](/docs/8.1/catalog-pg-authid.html "PostgreSQL 8.1 -
53.8. pg_authid")

__

53.8. `pg_authid`  
---  
[Prev](catalog-pg-attribute.html "53.7. pg_attribute")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-auth-members.html "53.9. pg_auth_members")  
  
* * *

## 53.8. `pg_authid` #

The catalog `pg_authid` contains information about database authorization
identifiers (roles). A role subsumes the concepts of “users” and “groups”. A
user is essentially just a role with the `rolcanlogin` flag set. Any role
(with or without `rolcanlogin`) can have other roles as members; see
[`pg_auth_members`](catalog-pg-auth-members.html "53.9. pg_auth_members").

Since this catalog contains passwords, it must not be publicly readable.
[`pg_roles`](view-pg-roles.html "54.20. pg_roles") is a publicly readable view
on `pg_authid` that blanks out the password field.

[Chapter 22](user-manag.html "Chapter 22. Database Roles") contains detailed
information about user and privilege management.

Because user identities are cluster-wide, `pg_authid` is shared across all
databases of a cluster: there is only one copy of `pg_authid` per cluster, not
one per database.

**Table  53.8. `pg_authid` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`rolname` `name` Role name  
`rolsuper` `bool` Role has superuser privileges  
`rolinherit` `bool` Role automatically inherits privileges of roles it is a
member of  
`rolcreaterole` `bool` Role can create more roles  
`rolcreatedb` `bool` Role can create databases  
`rolcanlogin` `bool` Role can log in. That is, this role can be given as the
initial session authorization identifier.  
`rolreplication` `bool` Role is a replication role. A replication role can
initiate replication connections and create and drop replication slots.  
`rolbypassrls` `bool` Role bypasses every row-level security policy, see
[Section 5.8](ddl-rowsecurity.html "5.8. Row Security Policies") for more
information.  
`rolconnlimit` `int4` For roles that can log in, this sets maximum number of
concurrent connections this role can make. -1 means no limit.  
`rolpassword` `text` Password (possibly encrypted); null if none. The format
depends on the form of encryption used.  
`rolvaliduntil` `timestamptz` Password expiry time (only used for password
authentication); null if no expiration  
  
  

For an MD5 encrypted password, `rolpassword` column will begin with the string
`md5` followed by a 32-character hexadecimal MD5 hash. The MD5 hash will be of
the user's password concatenated to their user name. For example, if user
`joe` has password `xyzzy`, PostgreSQL will store the md5 hash of `xyzzyjoe`.

If the password is encrypted with SCRAM-SHA-256, it has the format:

    
    
    SCRAM-SHA-256$_<iteration count>_:_<salt>_$_<StoredKey>_:_<ServerKey>_
    

where _`salt`_ , _`StoredKey`_ and _`ServerKey`_ are in Base64 encoded format.
This format is the same as that specified by [RFC
5803](https://datatracker.ietf.org/doc/html/rfc5803).

A password that does not follow either of those formats is assumed to be
unencrypted.

* * *

[Prev](catalog-pg-attribute.html "53.7. pg_attribute")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-auth-members.html "53.9. pg_auth_members")  
---|---|---  
53.7. `pg_attribute`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.9. `pg_auth_members`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-authid.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

