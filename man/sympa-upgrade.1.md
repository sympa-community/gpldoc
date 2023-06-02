---
title: 'sympa-upgrade(1)'
release: '6.2.72'
---

# NAME

sympa-upgrade - Upgrade Sympa

# SYNOPSIS

`sympa upgrade` \[ `--from=`_version\_X_ \] \[ `--to=`_version\_Y_ \]

`sympa upgrade` _sub-command_ ...

# DESCRIPTION

If any sub-command are not specified,
runs Sympa maintenance script to upgrade from version _X_ to version _Y_.

About available sub-commands see below.

# SUB-COMMANDS

Currently following sub-commands are available.
To see detail of each sub-command,
run '`sympal.pl help upgrade` _sub-command_'.

- ["sympa upgrade incoming ..."](./sympa-upgrade-incoming.1.md)

    Upgrade messages in incoming spool

- ["sympa upgrade outgoing ..."](./sympa-upgrade-outgoing.1.md)

    Migrating messages in bulk tables

- ["sympa upgrade password ...](./sympa-upgrade-password.1.md)

    Upgrading password in database

- ["sympa upgrade shared ..."](./sympa-upgrade-shared.1.md)

    Encode file names in shared repositories.

- ["sympa upgrade webfont"](./sympa-upgrade-webfont.1.md)

    Upgrading font in web templates.
