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

Supported Versions: [Current](/docs/current/libpq-ldap.html "PostgreSQL 17 -
34.18. LDAP Lookup of Connection Parameters") ([17](/docs/17/libpq-ldap.html
"PostgreSQL 17 - 34.18. LDAP Lookup of Connection Parameters")) /
[16](/docs/16/libpq-ldap.html "PostgreSQL 16 - 34.18. LDAP Lookup of
Connection Parameters") / [15](/docs/15/libpq-ldap.html "PostgreSQL 15 -
34.18. LDAP Lookup of Connection Parameters") / [14](/docs/14/libpq-ldap.html
"PostgreSQL 14 - 34.18. LDAP Lookup of Connection Parameters") /
[13](/docs/13/libpq-ldap.html "PostgreSQL 13 - 34.18. LDAP Lookup of
Connection Parameters")

Development Versions: [18](/docs/18/libpq-ldap.html "PostgreSQL 18 -
34.18. LDAP Lookup of Connection Parameters") / [devel](/docs/devel/libpq-
ldap.html "PostgreSQL devel - 34.18. LDAP Lookup of Connection Parameters")

Unsupported versions: [12](/docs/12/libpq-ldap.html "PostgreSQL 12 -
34.18. LDAP Lookup of Connection Parameters") / [11](/docs/11/libpq-ldap.html
"PostgreSQL 11 - 34.18. LDAP Lookup of Connection Parameters") /
[10](/docs/10/libpq-ldap.html "PostgreSQL 10 - 34.18. LDAP Lookup of
Connection Parameters") / [9.6](/docs/9.6/libpq-ldap.html "PostgreSQL 9.6 -
34.18. LDAP Lookup of Connection Parameters") / [9.5](/docs/9.5/libpq-
ldap.html "PostgreSQL 9.5 - 34.18. LDAP Lookup of Connection Parameters") /
[9.4](/docs/9.4/libpq-ldap.html "PostgreSQL 9.4 - 34.18. LDAP Lookup of
Connection Parameters") / [9.3](/docs/9.3/libpq-ldap.html "PostgreSQL 9.3 -
34.18. LDAP Lookup of Connection Parameters") / [9.2](/docs/9.2/libpq-
ldap.html "PostgreSQL 9.2 - 34.18. LDAP Lookup of Connection Parameters") /
[9.1](/docs/9.1/libpq-ldap.html "PostgreSQL 9.1 - 34.18. LDAP Lookup of
Connection Parameters") / [9.0](/docs/9.0/libpq-ldap.html "PostgreSQL 9.0 -
34.18. LDAP Lookup of Connection Parameters") / [8.4](/docs/8.4/libpq-
ldap.html "PostgreSQL 8.4 - 34.18. LDAP Lookup of Connection Parameters") /
[8.3](/docs/8.3/libpq-ldap.html "PostgreSQL 8.3 - 34.18. LDAP Lookup of
Connection Parameters") / [8.2](/docs/8.2/libpq-ldap.html "PostgreSQL 8.2 -
34.18. LDAP Lookup of Connection Parameters")

__

34.18. LDAP Lookup of Connection Parameters  
---  
[Prev](libpq-pgservice.html "34.17. The Connection Service File")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-ssl.html "34.19. SSL Support")  
  
* * *

## 34.18. LDAP Lookup of Connection Parameters #

If libpq has been compiled with LDAP support (option ``\--with-ldap`` for
`configure`) it is possible to retrieve connection options like `host` or
`dbname` via LDAP from a central server. The advantage is that if the
connection parameters for a database change, the connection information
doesn't have to be updated on all client machines.

LDAP connection parameter lookup uses the connection service file
`pg_service.conf` (see [Section 34.17](libpq-pgservice.html "34.17. The
Connection Service File")). A line in a `pg_service.conf` stanza that starts
with `ldap://` will be recognized as an LDAP URL and an LDAP query will be
performed. The result must be a list of `keyword = value` pairs which will be
used to set connection options. The URL must conform to [RFC
1959](https://datatracker.ietf.org/doc/html/rfc1959) and be of the form

    
    
    ldap://[_hostname_[:_port_]]/_search_base_?_attribute_?_search_scope_?_filter_
    

where _`hostname`_ defaults to `localhost` and _`port`_ defaults to 389.

Processing of `pg_service.conf` is terminated after a successful LDAP lookup,
but is continued if the LDAP server cannot be contacted. This is to provide a
fallback with further LDAP URL lines that point to different LDAP servers,
classical `keyword = value` pairs, or default connection options. If you would
rather get an error message in this case, add a syntactically incorrect line
after the LDAP URL.

A sample LDAP entry that has been created with the LDIF file

    
    
    version:1
    dn:cn=mydatabase,dc=mycompany,dc=com
    changetype:add
    objectclass:top
    objectclass:device
    cn:mydatabase
    description:host=dbserver.mycompany.com
    description:port=5439
    description:dbname=mydb
    description:user=mydb_user
    description:sslmode=require
    

might be queried with the following LDAP URL:

    
    
    ldap://ldap.mycompany.com/dc=mycompany,dc=com?description?one?(cn=mydatabase)
    

You can also mix regular service file entries with LDAP lookups. A complete
example for a stanza in `pg_service.conf` would be:

    
    
    # only host and port are stored in LDAP, specify dbname and user explicitly
    [customerdb]
    dbname=customer
    user=appuser
    ldap://ldap.acme.com/cn=dbserver,cn=hosts?pgconnectinfo?base?(objectclass=*)
    

* * *

[Prev](libpq-pgservice.html "34.17. The Connection Service File")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-ssl.html "34.19. SSL Support")  
---|---|---  
34.17. The Connection Service File  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.19. SSL Support  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-ldap.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

