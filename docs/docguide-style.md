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

Supported Versions: [Current](/docs/current/docguide-style.html "PostgreSQL 17
- J.6. Style Guide") ([17](/docs/17/docguide-style.html "PostgreSQL 17 -
J.6. Style Guide")) / [16](/docs/16/docguide-style.html "PostgreSQL 16 -
J.6. Style Guide") / [15](/docs/15/docguide-style.html "PostgreSQL 15 -
J.6. Style Guide") / [14](/docs/14/docguide-style.html "PostgreSQL 14 -
J.6. Style Guide") / [13](/docs/13/docguide-style.html "PostgreSQL 13 -
J.6. Style Guide")

Development Versions: [18](/docs/18/docguide-style.html "PostgreSQL 18 -
J.6. Style Guide") / [devel](/docs/devel/docguide-style.html "PostgreSQL devel
- J.6. Style Guide")

Unsupported versions: [12](/docs/12/docguide-style.html "PostgreSQL 12 -
J.6. Style Guide") / [11](/docs/11/docguide-style.html "PostgreSQL 11 -
J.6. Style Guide") / [10](/docs/10/docguide-style.html "PostgreSQL 10 -
J.6. Style Guide") / [9.6](/docs/9.6/docguide-style.html "PostgreSQL 9.6 -
J.6. Style Guide") / [9.5](/docs/9.5/docguide-style.html "PostgreSQL 9.5 -
J.6. Style Guide") / [9.4](/docs/9.4/docguide-style.html "PostgreSQL 9.4 -
J.6. Style Guide") / [9.3](/docs/9.3/docguide-style.html "PostgreSQL 9.3 -
J.6. Style Guide") / [9.2](/docs/9.2/docguide-style.html "PostgreSQL 9.2 -
J.6. Style Guide") / [9.1](/docs/9.1/docguide-style.html "PostgreSQL 9.1 -
J.6. Style Guide") / [9.0](/docs/9.0/docguide-style.html "PostgreSQL 9.0 -
J.6. Style Guide") / [8.4](/docs/8.4/docguide-style.html "PostgreSQL 8.4 -
J.6. Style Guide") / [8.3](/docs/8.3/docguide-style.html "PostgreSQL 8.3 -
J.6. Style Guide") / [8.2](/docs/8.2/docguide-style.html "PostgreSQL 8.2 -
J.6. Style Guide") / [8.1](/docs/8.1/docguide-style.html "PostgreSQL 8.1 -
J.6. Style Guide") / [8.0](/docs/8.0/docguide-style.html "PostgreSQL 8.0 -
J.6. Style Guide") / [7.4](/docs/7.4/docguide-style.html "PostgreSQL 7.4 -
J.6. Style Guide")

__

J.6. Style Guide  
---  
[Prev](docguide-authoring.html "J.5. Documentation Authoring")  | [Up](docguide.html "Appendix J. Documentation") | Appendix J. Documentation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](limits.html "Appendix K. PostgreSQL Limits")  
  
* * *

## J.6. Style Guide #

[J.6.1. Reference Pages](docguide-style.html#DOCGUIDE-STYLE-REF-PAGES)

### J.6.1. Reference Pages #

Reference pages should follow a standard layout. This allows users to find the
desired information more quickly, and it also encourages writers to document
all relevant aspects of a command. Consistency is not only desired among
PostgreSQL reference pages, but also with reference pages provided by the
operating system and other packages. Hence the following guidelines have been
developed. They are for the most part consistent with similar guidelines
established by various operating systems.

Reference pages that describe executable commands should contain the following
sections, in this order. Sections that do not apply can be omitted. Additional
top-level sections should only be used in special circumstances; often that
information belongs in the “Usage” section.

Name #

    

This section is generated automatically. It contains the command name and a
half-sentence summary of its functionality.

Synopsis #

    

This section contains the syntax diagram of the command. The synopsis should
normally not list each command-line option; that is done below. Instead, list
the major components of the command line, such as where input and output files
go.

Description #

    

Several paragraphs explaining what the command does.

Options #

    

A list describing each command-line option. If there are a lot of options,
subsections can be used.

Exit Status #

    

If the program uses 0 for success and non-zero for failure, then you do not
need to document it. If there is a meaning behind the different non-zero exit
codes, list them here.

Usage #

    

Describe any sublanguage or run-time interface of the program. If the program
is not interactive, this section can usually be omitted. Otherwise, this
section is a catch-all for describing run-time features. Use subsections if
appropriate.

Environment #

    

List all environment variables that the program might use. Try to be complete;
even seemingly trivial variables like `SHELL` might be of interest to the
user.

Files #

    

List any files that the program might access implicitly. That is, do not list
input and output files that were specified on the command line, but list
configuration files, etc.

Diagnostics #

    

Explain any unusual output that the program might create. Refrain from listing
every possible error message. This is a lot of work and has little use in
practice. But if, say, the error messages have a standard format that the user
can parse, this would be the place to explain it.

Notes #

    

Anything that doesn't fit elsewhere, but in particular bugs, implementation
flaws, security considerations, compatibility issues.

Examples #

    

Examples

History #

    

If there were some major milestones in the history of the program, they might
be listed here. Usually, this section can be omitted.

Author #

    

Author (only used in the contrib section)

See Also #

    

Cross-references, listed in the following order: other PostgreSQL command
reference pages, PostgreSQL SQL command reference pages, citation of
PostgreSQL manuals, other reference pages (e.g., operating system, other
packages), other documentation. Items in the same group are listed
alphabetically.

Reference pages describing SQL commands should contain the following sections:
Name, Synopsis, Description, Parameters, Outputs, Notes, Examples,
Compatibility, History, See Also. The Parameters section is like the Options
section, but there is more freedom about which clauses of the command can be
listed. The Outputs section is only needed if the command returns something
other than a default command-completion tag. The Compatibility section should
explain to what extent this command conforms to the SQL standard(s), or to
which other database system it is compatible. The See Also section of SQL
commands should list SQL commands before cross-references to programs.

* * *

[Prev](docguide-authoring.html "J.5. Documentation Authoring")  | [Up](docguide.html "Appendix J. Documentation") |  [Next](limits.html "Appendix K. PostgreSQL Limits")  
---|---|---  
J.5. Documentation Authoring  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix K. PostgreSQL Limits  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/docguide-style.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

