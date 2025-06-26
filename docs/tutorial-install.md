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

Supported Versions: [Current](/docs/current/tutorial-install.html "PostgreSQL
17 - 1.1. Installation") ([17](/docs/17/tutorial-install.html "PostgreSQL 17 -
1.1. Installation")) / [16](/docs/16/tutorial-install.html "PostgreSQL 16 -
1.1. Installation") / [15](/docs/15/tutorial-install.html "PostgreSQL 15 -
1.1. Installation") / [14](/docs/14/tutorial-install.html "PostgreSQL 14 -
1.1. Installation") / [13](/docs/13/tutorial-install.html "PostgreSQL 13 -
1.1. Installation")

Development Versions: [18](/docs/18/tutorial-install.html "PostgreSQL 18 -
1.1. Installation") / [devel](/docs/devel/tutorial-install.html "PostgreSQL
devel - 1.1. Installation")

Unsupported versions: [12](/docs/12/tutorial-install.html "PostgreSQL 12 -
1.1. Installation") / [11](/docs/11/tutorial-install.html "PostgreSQL 11 -
1.1. Installation") / [10](/docs/10/tutorial-install.html "PostgreSQL 10 -
1.1. Installation") / [9.6](/docs/9.6/tutorial-install.html "PostgreSQL 9.6 -
1.1. Installation") / [9.5](/docs/9.5/tutorial-install.html "PostgreSQL 9.5 -
1.1. Installation") / [9.4](/docs/9.4/tutorial-install.html "PostgreSQL 9.4 -
1.1. Installation") / [9.3](/docs/9.3/tutorial-install.html "PostgreSQL 9.3 -
1.1. Installation") / [9.2](/docs/9.2/tutorial-install.html "PostgreSQL 9.2 -
1.1. Installation") / [9.1](/docs/9.1/tutorial-install.html "PostgreSQL 9.1 -
1.1. Installation") / [9.0](/docs/9.0/tutorial-install.html "PostgreSQL 9.0 -
1.1. Installation") / [8.4](/docs/8.4/tutorial-install.html "PostgreSQL 8.4 -
1.1. Installation") / [8.3](/docs/8.3/tutorial-install.html "PostgreSQL 8.3 -
1.1. Installation") / [8.2](/docs/8.2/tutorial-install.html "PostgreSQL 8.2 -
1.1. Installation")

__

1.1. Installation  
---  
[Prev](tutorial-start.html "Chapter 1. Getting Started")  | [Up](tutorial-start.html "Chapter 1. Getting Started") | Chapter 1. Getting Started | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-arch.html "1.2. Architectural Fundamentals")  
  
* * *

## 1.1. Installation #

Before you can use PostgreSQL you need to install it, of course. It is
possible that PostgreSQL is already installed at your site, either because it
was included in your operating system distribution or because the system
administrator already installed it. If that is the case, you should obtain
information from the operating system documentation or your system
administrator about how to access PostgreSQL.

If you are not sure whether PostgreSQL is already available or whether you can
use it for your experimentation then you can install it yourself. Doing so is
not hard and it can be a good exercise. PostgreSQL can be installed by any
unprivileged user; no superuser (root) access is required.

If you are installing PostgreSQL yourself, then refer to [Chapter
17](installation.html "Chapter 17. Installation from Source Code") for
instructions on installation, and return to this guide when the installation
is complete. Be sure to follow closely the section about setting up the
appropriate environment variables.

If your site administrator has not set things up in the default way, you might
have some more work to do. For example, if the database server machine is a
remote machine, you will need to set the `PGHOST` environment variable to the
name of the database server machine. The environment variable `PGPORT` might
also have to be set. The bottom line is this: if you try to start an
application program and it complains that it cannot connect to the database,
you should consult your site administrator or, if that is you, the
documentation to make sure that your environment is properly set up. If you
did not understand the preceding paragraph then read the next section.

* * *

[Prev](tutorial-start.html "Chapter 1. Getting Started")  | [Up](tutorial-start.html "Chapter 1. Getting Started") |  [Next](tutorial-arch.html "1.2. Architectural Fundamentals")  
---|---|---  
Chapter 1. Getting Started  | [Home](index.html "PostgreSQL 16.9 Documentation") |  1.2. Architectural Fundamentals  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-install.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

