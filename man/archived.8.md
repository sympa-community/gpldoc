---
title: 'archived(8)'
release: '6.2.72'
---

# NAME

archived, archived.pl - Mailing List Archiving Daemon for Sympa

# SYNOPSIS

`archived.pl` \[ `--foreground` \] \[ `--debug` \]

# DESCRIPTION

**Archived** is a program which scan permanently the archive spool
and feeds the web archives, converting messages to the HTML format and
linking them. Original mails are also kept (in _arctxt/_ directory> for
later rebuilding of archives.

The HTML conversion is achieved by the means of the **MHonArc** program.

Archives are accessed via **wwsympa.fcgi** and **sympa\_msg.pl**,
which proposes access control;
therefore archives should not be located in a public web directory.

# OPTIONS

These programs follow the usual GNU command line syntax,
with long options starting with two dashes (`--`).  A summary of
options is included below.

- `-F`, `--foreground`

    Do not detach TTY.

- `-f`, `--config=`_file_

    Force archived to use an alternative configuration file instead
    of `/etc/sympa/sympa.conf`.

- `-d`, `--debug`

    Run the program in a debug mode.

- `-h`, `--help`

    Print this help message.

# FILES

`$SPOOLDIR/outgoing/` outgoing Sympa directory.

`$DEFAULTDIR/mhonarc_rc.tt2` template of MHonArc resource file.

- `mhonarc-ressources.tt2` was replaced with `mhonarc_rc.tt2`
on Sympa 6.2.61b.1.

`/etc/sympa/sympa.conf` Sympa configuration file.

`$PIDDIR/archived.pid` this file contains the process ID
of `archived.pl`.

# MORE DOCUMENTATION

The full documentation in HTML format can be found in
[https://www.sympa.community/manual/](https://www.sympa.community/manual/).

The mailing lists (with web archives) can be accessed at
[https://www.sympa.community/community/lists.html](https://www.sympa.community/community/lists.html).

# HISTORY

This program was originally written by:

- Serge Aumont

    Comité Réseau des Universités

- Olivier Salaün

    Comité Réseau des Universités

This manual page was initially written by
Jérôme Marant &lt;jerome.marant@IDEALX.org>
for the Debian GNU/Linux system.

# LICENSE

You may distribute this software under the terms of the GNU General
Public License Version 2.  For more details see `README` file.

Permission is granted to copy, distribute and/or modify this document
under the terms of the GNU Free Documentation License, Version 1.1 or
any later version published by the Free Software Foundation; with no
Invariant Sections, no Front-Cover Texts and no Back-Cover Texts.  A
copy of the license can be found under
[http://www.gnu.org/licenses/fdl.html](http://www.gnu.org/licenses/fdl.html).

# BUGS

Report bugs to Sympa bug tracker.
See [https://github.com/sympa-community/sympa/issues](https://github.com/sympa-community/sympa/issues).

# SEE ALSO

[sympa\_msg(8)](./sympa_msg.8.md), [bounced(8)](./bounced.8.md), [mhonarc(1)](./mhonarc.1.md), [sympa\_config(5)](./sympa_config.5.md).

[Sympa::Spindle::ProcessArchive](./Sympa-Spindle-ProcessArchive.3.md).
