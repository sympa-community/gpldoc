---
title: 'sympa-upgrade-outgoing(1)'
release: '6.2.71b.1'
---

# NAME

sympa-upgrade-outgoing - Migrating messages in bulk tables

# SYNOPSIS

    sympa upgrade outgoing [ --dry_run ]

# DESCRIPTION

On Sympa earlier than 6.2, messages for bulk sending were stored into
bulk spool based on database tables.
Recent release of Sympa stores outbound messages into the spool based on
filesystem or sends them by Mailer directly.
This program migrates messages with old format in appropriate spool.

# OPTIONS

- --dry\_run

    Shows what will be done but won't really perform upgrade process.

# RETURN VALUE

This program exits with status 0 if processing succeeded.
Otherwise exits with non-zero status.

# CONFIGURATION OPTIONS

Following site configuration parameters in `--CONFIG--` or
robot configuration parameters in `robot.conf` are referred.

- db\_type, db\_name etc.
- queuebulk
- sympa\_packet\_priority
- umask

# SEE ALSO

[sympa.conf(5)](./sympa.conf.5.md),
[Sympa::Message](./Sympa-Message.3.md),
[Sympa::Spool::Outgoing](./Sympa-Spool-Outgoing.3.md).

# HISTORY

`upgrade_bulk_spool.pl` appeared on Sympa 6.2.

Its function was moved to `sympa upgrade outgoing` command line
on Sympa 6.2.70.

Its function was moved to `sympa upgrade outgoing` command line
on Sympa 6.2.70.