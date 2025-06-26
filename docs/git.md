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

Supported Versions: [Current](/docs/current/git.html "PostgreSQL 17 -
I.1. Getting the Source via Git") ([17](/docs/17/git.html "PostgreSQL 17 -
I.1. Getting the Source via Git")) / [16](/docs/16/git.html "PostgreSQL 16 -
I.1. Getting the Source via Git") / [15](/docs/15/git.html "PostgreSQL 15 -
I.1. Getting the Source via Git") / [14](/docs/14/git.html "PostgreSQL 14 -
I.1. Getting the Source via Git") / [13](/docs/13/git.html "PostgreSQL 13 -
I.1. Getting the Source via Git")

Development Versions: [18](/docs/18/git.html "PostgreSQL 18 - I.1. Getting the
Source via Git") / [devel](/docs/devel/git.html "PostgreSQL devel -
I.1. Getting the Source via Git")

Unsupported versions: [12](/docs/12/git.html "PostgreSQL 12 - I.1. Getting the
Source via Git") / [11](/docs/11/git.html "PostgreSQL 11 - I.1. Getting the
Source via Git") / [10](/docs/10/git.html "PostgreSQL 10 - I.1. Getting the
Source via Git") / [9.6](/docs/9.6/git.html "PostgreSQL 9.6 - I.1. Getting the
Source via Git") / [9.5](/docs/9.5/git.html "PostgreSQL 9.5 - I.1. Getting the
Source via Git") / [9.4](/docs/9.4/git.html "PostgreSQL 9.4 - I.1. Getting the
Source via Git") / [9.3](/docs/9.3/git.html "PostgreSQL 9.3 - I.1. Getting the
Source via Git") / [9.2](/docs/9.2/git.html "PostgreSQL 9.2 - I.1. Getting the
Source via Git") / [9.1](/docs/9.1/git.html "PostgreSQL 9.1 - I.1. Getting the
Source via Git") / [9.0](/docs/9.0/git.html "PostgreSQL 9.0 - I.1. Getting the
Source via Git") / [8.4](/docs/8.4/git.html "PostgreSQL 8.4 - I.1. Getting the
Source via Git") / [8.3](/docs/8.3/git.html "PostgreSQL 8.3 - I.1. Getting the
Source via Git") / [8.2](/docs/8.2/git.html "PostgreSQL 8.2 - I.1. Getting the
Source via Git")

__

I.1. Getting the Source via Git  
---  
[Prev](sourcerepo.html "Appendix I. The Source Code Repository")  | [Up](sourcerepo.html "Appendix I. The Source Code Repository") | Appendix I. The Source Code Repository | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](docguide.html "Appendix J. Documentation")  
  
* * *

## I.1. Getting the Source via Git #

With Git you will make a copy of the entire code repository on your local
machine, so you will have access to all history and branches offline. This is
the fastest and most flexible way to develop or test patches.

**Git**

  1. You will need an installed version of Git, which you can get from <https://git-scm.com>. Many systems already have a recent version of Git installed by default, or available in their package distribution system.

  2. To begin using the Git repository, make a clone of the official mirror:
         
         git clone https://git.postgresql.org/git/postgresql.git
         

This will copy the full repository to your local machine, so it may take a
while to complete, especially if you have a slow Internet connection. The
files will be placed in a new subdirectory `postgresql` of your current
directory.

The Git mirror can also be reached via the Git protocol. Just change the URL
prefix to `git`, as in:

         
         git clone git://git.postgresql.org/git/postgresql.git
         

  3. Whenever you want to get the latest updates in the system, `cd` into the repository, and run:
         
         git fetch
         

Git can do a lot more things than just fetch the source. For more information,
consult the Git man pages, or see the website at <https://git-scm.com>.

* * *

[Prev](sourcerepo.html "Appendix I. The Source Code Repository")  | [Up](sourcerepo.html "Appendix I. The Source Code Repository") |  [Next](docguide.html "Appendix J. Documentation")  
---|---|---  
Appendix I. The Source Code Repository  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix J. Documentation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/git.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

