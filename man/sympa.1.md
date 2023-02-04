---
title: 'sympa(1)'
release: '6.2.72'
---

# NAME

sympa, sympa.pl - Command line utility to manage Sympa

# SYNOPSIS

`sympa` _command_ \[ _general options_... \] ...

# DESCRIPTION

**NOTE**:
On overview of Sympa documentation see [sympa\_toc(1)](./sympa_toc.1.md).

`sympa` is invoked from command line then performs various administration
tasks.

# GENERAL OPTIONS

`sympa` may run with following options in general.

- `-d`, `--debug`

    Enable debug mode.

- `-f`, `--config=`_file_

    Force Sympa to use an alternative configuration file instead
    of `/etc/sympa/sympa.conf`.

- `-l`, `--lang=`_lang_

    Set this option to use a language for Sympa. The corresponding
    gettext catalog file must be located in `$LOCALEDIR`
    directory.

- `--log_level=`_level_

    Sets Sympa log level.

- `-m`, `--mail`

    Enable SMTP logging.

- `--noout`

    Skip output to the console except for fatal error messages.

# COMMANDS

Currently following commands are available.
To see detail of each command, run '`sympa help` _command_'.

- ["sympa add"](./sympa-add.1.md)

    Add users to the list

- ["sympa bouncers"](./sympa-bouncers.1.md)

    Manipulate list bounced users

- ["sympa check"](./sympa-check.1.md)

    Check environment

- ["sympa close"](./sympa-close.1.md)

    Close a list or the lists belonging to a family

- ["sympa config"](./sympa-config.1.md)

    Manipulate configuration of Sympa

- ["sympa copy"](./sympa-move.1.md)

    Copy the list

- ["sympa create"](./sympa-create.1.md)

    Create a list

- ["sympa del"](./sympa-del.1.md)

    Delete users from the list

- ["sympa dump"](./sympa-dump.1.md)

    Dump users of the lists

- ["sympa export\_list"](./sympa-export_list.1.md)

    TBD

- ["sympa help"](./sympa-help.1.md)

    Display help information about Sympa CLI

- ["sympa include"](./sympa-include.1.md)

    Update inclusion

- ["sympa instantiate"](./sympa-instantiate.1.md)

    Instantiate the lists in a family

- ["sympa lowercase"](./sympa-lowercase.1.md)

    Lowercase email addresses in database

- ["sympa make\_alias\_file"](./sympa-make_alias_file.1.md)

    Create aliases file

- ["sympa md5\_digest"](./sympa-md5_digest.1.md)

    Output a MD5 digest

- ["sympa move"](./sympa-move.1.md)

    Move or copy the list

- ["sympa open"](./sympa-open.1.md)

    Open the list

- ["sympa rebuildarc"](./sympa-rebuildarc.1.md)

    Rebuild the archives of the list

- ["sympa reload\_list\_config"](./sympa-reload_list_config.1.md)

    Recreate config cache of the lists

- ["sympa restore"](./sympa-restore.1.md)

    Restore users of the lists

- ["sympa review"](./sympa-review.1.md)

    Show subscribers of the list

- ["sympa send\_digest"](./sympa-send_digest.1.md)

    Send digest

- ["sympa set"](https://metacpan.org/pod/sympa-set%29)

    Set properties of the users of the list

- ["sympa show\_pending\_lists"](./sympa-show_pending_lists.1.md)

    Show pending lists

- ["sympa sync\_list\_db"](./sympa-sync_list_db.1.md)

    Synchronize database cache of the lists

- ["sympa test"](./sympa-test.1.md)

    Test the functions of Sympa

- ["sympa update"](./sympa-update.1.md)

    Modify the existing list in the family

- ["sympa upgrade"](./sympa-upgrade.1.md)

    Upgrade Sympa

- ["sympa upgrade\_config\_location"](./sympa-upgrade_config_location.1.md)

    TBD

- ["sympa user"](./sympa-user.1.md)

    Manipulate list users

- ["sympa version"](./sympa-version.1.md)

    Print the version number of Sympa

# DESCRIPTION FOR EARLIER VERSION

**NOTE**:
Description in this section is kept for compatibility to earlier versions.
Run `sympa help` or see [sympa(1)](./sympa.1.md) to see recent conventions.

## Synopsis

`sympa.pl` \[ `-d, --debug` \] \[ `-f, --file`=_another.sympa.conf_ \]
\[ `-l, --lang`=_lang_ \] \[ `-m, --mail` \]
\[ `-h, --help` \] \[ `-v, --version` \]

\[ `--add`=_list_@_domain_ \[--role=_role_\] \[--quiet\] \[--notify\] \[--force\] \]
\[ `--del`=_list_@_domain_ \[--role=_role_\] \[--quiet\] \[--notify\] \[--force\] \]
\[ `--open_list`=_list_\[_@robot_\] \[--notify\] \]
\[ `--close_list`=_list_\[_@robot_\] \]
\[ `--purge_list`=_list_\[_@robot_\] \]
\[ `--lowercase` \] \[ `--make_alias_file` \]
\[ `--dump_users` `--list`=_list_@_domain_&#124;ALL \[ `--role`=_roles_ \] \]
\[ `--restore_users` `--list`=_list_@_domain_&#124;ALL \[ `--role`=_roles_ \] \]
\[ `--show_pending_lists`=_robot_ \]
\[ `--rebuildarc`=_list_\[_@robot_\] \]

## Options

`sympa.pl` may run with following options in general.

- `-d`, `--debug`

    Enable debug mode.

- `-f`, `--config=`_file_

    Force Sympa to use an alternative configuration file instead
    of `/etc/sympa/sympa.conf`.

- `-l`, `--lang=`_lang_

    Set this option to use a language for Sympa. The corresponding
    gettext catalog file must be located in `$LOCALEDIR`
    directory.

- `--log_level=`_level_

    Sets Sympa log level.

With the following options `sympa.pl` will run in batch mode:

- `--add=`_list_@_domain_ \[ `--role`=_role_ \]
\[ `--quiet` \] \[ `--notify` \] \[ `--force` \]

    Add email(s) from the list. Data are read from standard input.
    The data should contain one email address per line.

    Sample:

        ## emails to be added
        john.steward@some.company.com       John Steward
        mary.blacksmith@another.company.com Mary Blacksmith

    Note:
    This option was added on Sympa 6.2.67b.2.

    New command line format:

    - `sympa add` \[ `--role`=_role_ \] \[ `--quiet` \] \[ `--notify` \]
    \[ `--force` \] _list_`@`_domain_

- `--add_list=`_family\_name_ `--robot=`_robot\_name_
`--input_file=`_/path/to/file.xml_

    Add the list described by the file.xml under robot\_name, to the family
    family\_name.

    New command line format:

    - `sympa create` `--input_file=`_/path/to/file.xml_
    _family\_name_`@@`_robot\_name_

- `--change_user_email` `--current_email=`_current_ `--new_email=`_new_

    Changes a user email address in all Sympa  databases (subscriber\_table,
    list config, etc) for all virtual robots.

    New command line format:

    - `sympa user move` _current_ _new_

- `--close_family=`_family\_name_ `--robot=`_robot\_name_

    Close lists of family\_name family under robot\_name.      

    New command line format:

    - `sympa close` _family\_name_`@@`_robot\_name_

- `--close_list=`_list_\[`@`_robot_\]

    Close the list (changing its status to closed), remove aliases and remove
    subscribers from DB (a dump is created in the list directory to allow
    restoring the list)

    New command line format:

    - `sympa close` _list_\[`@`_robot_\]

- `--conf_2_db`

    **Deprecated**.
    Load sympa.conf and each robot.conf into database.

    New command line format:

    None.

- `--copy_list=`_listname_`@`_robot_
`--new_listname=`_newlistname_ `--new_listrobot=`_newrobot_

    Copy a list.

    New command line format:

    - `sympa move --mode=copy`
    _listname_`@`_robot_ _newlistname_`@`_newrobot_
    - `sympa copy`
    _listname_`@`_robot_ _newlistname_`@`_newrobot_

- `--create_list` `--robot=`_robot\_name_
`--input_file=`_/path/to/file.xml_

    Create a list with the XML file under robot robot\_name.

    New command line format:

    - `sympa create` `--input_file=`_/path/to/file.xml_ _robot\_name_

- `--del=`_list_`@`_domain_ \[ `--role`=_role_ \]
\[ `--quiet` \] \[ `--notify` \] \[ `--force` \]

    Delete email(s) from the list. Data are read from standard input.
    The data should contain one email address per line.

    Sample:

        ## emails to be deleted
        john.steward@some.company.com
        mary.blacksmith@another.company.com

    Note:
    This options was added on Sympa 6.2.67b.2.

    New command line format:

    - `sympa del` \[ `--role`=_role_ \] \[ `--quiet` \] \[ `--notify` \]
    \[ `--force` \] _list_`@`_domain_ 

- `--dump=`_list_@_domain_&#124;`ALL`

    Obsoleted option.  Use `--dump_users`.

- `--dump_users` `--list=`_list_@_domain_&#124;`ALL` \[ `--role=`_roles_ \]

    Dumps users of a list or all lists.

    `--role` may specify `member`, `owner`, `editor` or any of them separated
    by comma (`,`). Only `member` is chosen by default.

    Users are dumped in files _role_`.dump` in each list directory.

    Note: On Sympa prior to 6.2.31b.1, subscribers were dumped in
    `subscribers.db.dump` file, and owners and moderators could not be dumped.

    See also `--restore_users`.

    Note: This option replaced `--dump` on Sympa 6.2.34.

    New command line format:

    - `sympa dump` \[ `--roles=`_roles_ \] _list_`@`_domain_ 
    - `sympa dump` \[ `--roles=`_roles_ \] `"*"`

- `--health_check`

    Check if `sympa.conf`, `robot.conf` of virtual robots and database structure
    are correct.  If any errors occur, exits with non-zero status.

    New command line format:

    - `sympa check`

- `--import=`_list_@_dom_

    Deprecated.  Use `--add` instead.

- `--instantiate_family=`_family\_name_ `--robot=`_robot\_name_
`--input_file=`_/path/to/file.xml_ \[ `--close_unknown` \] \[ `--quiet` \]

    Instantiate family\_name lists described in the file.xml under robot\_name.
    The family directory must exist; automatically close undefined lists in a
    new instantiation if --close\_unknown is specified; do not print report if
    `--quiet` is specified.

    New command line format:

    - `sympa instantiate`
    `--input_file=`_/path/to/file.xml_ \[ `--close_unknown` \] \[ `--quiet` \]
    _family\_name_`@@`_robot\_name_

- `--lowercase`

    Lowercases email addresses in database.

    New command line format:

    TBD.

- `--make_alias_file` \[ `--robot` robot \]

    Create an aliases file in /tmp/ with all list aliases. It uses the
    `list_aliases.tt2` template  (useful when list\_aliases.tt2 was changed).

    New command line format:

    TBD.

- `--md5_encode_password`

    Rewrite password in `user_table` of database using MD5 fingerprint.
    YOU CAN'T UNDO unless you save this table first.

    **Note** that this option was obsoleted.
    Use [sympa upgrade password](./symp-upgrade-password.1.md).

- `--modify_list=`_family\_name_ `--robot=`_robot\_name_
`--input_file=`_/path/to/file.xml_

    Modify the existing list installed under the robot robot\_name and that
    belongs to the family family\_name. The new description is in the `file.xml`.

    New command line format:

    - `sympa update` `--input_file=`_/path/to/file.xml_
    _family\_name_`@@`_robot\_name_

- `--open_list=`_list_\[`@`_robot_\] \[ `--notify` \]

    Restore the closed list (changing its status to open), add aliases and restore
    users to DB (dump files in the list directory are imported).

    The `--notify` is optional. If present, the owner(s) of the list will be notified.

    New command line format:

    - `sympa open` \[ `--notify` \] _list_\[`@`_robot_\]

- `--purge_list`=_list_\[`@`_robot_\]

    Remove the list (remove archive, configuration files, users and owners in admin table. Restore is not possible after this operation.

    New command line format:

    - `sympa close` `--mode=purge` _list_\[`@`_robot_\]

- `--show_pending_lists`=_robot_

    Print all pending lists for the robot, with information.

    New command line format:

    TBD.

- `--rebuildarc`=_list_\[_@robot_\]

    Rebuild the archives of the list.

    New command line format:

    TBD.

- `--reload_list_config`
\[ `--list=`_mylist_@_mydom_ \] \[ `--robot=`_mydom_ \]

    Recreates all `config.bin` files or cache in `list_table`.
    You should run this command if you edit authorization scenarios.
    The list and robot parameters are optional.

    New command line format:

    TBD.

- `--rename_list=`_listname_`@`_robot_
`--new_listname=`_newlistname_ `--new_listrobot=`_newrobot_

    Renames a list or move it to another virtual robot.

    New command line format:

    - `sympa move` _listname_`@`_robot_ _newlistname_`@`_newrobot_

- `--send_digest` \[ `--keep_digest` \]

    Send digest right now.
    If `--keep_digest` is specified, stocked digest will not be removed.

    New command line format:

    TBD.

- `--restore_users` `--list=`_list_@_domain_&#124;`ALL` \[ `--role=`_roles_ \]

    Restore users from files dumped by `--dump_users`.

    Note: This option was added on Sympa 6.2.34.

    New command line format:

    - `sympa restore` \[ `--roles=`_roles_ \] _list_`@`_domain_
    - `sympa restore` \[ `--roles=`_roles_ \] `"*"`

- `--sync_include=`_listname_`@`_robot_ \[ `--role=`_role_ \]

    Trigger update of the list users included from data sources.

    New command line format:

    - `sympa include` \[ `--role=`_role_ \] _listname_`@`_robot_ 

- `--sync_list_db` \[ `--list=`_listname_@_robot_ \]

    Syncs filesystem list configs to the database cache of list configs,
    optionally syncs an individual list if specified.

    New command line format:

    TBD.

- `--test_database_message_buffer`

    **Note**:
    This option was deprecated.

    Test the database message buffer size.

- `--upgrade` \[ `--from=`_X_ \] \[ `--to=`_Y_ \]

    Runs Sympa maintenance script to upgrade from version _X_ to version _Y_.

    New command line format:

    - `sympa upgrade` \[ <--from=>_X_ \] \[ `--to=`_Y_ \]

- `--upgrade_shared` \[ `--list=`_X_ \] \[ `--robot=`_Y_ \]

    **Note**:
    This option was deprecated.
    See [sympa upgrade shared](./sympa-upgrade-shared.1.md) command line.

    Rename files in shared.

    New command line format:

    - `sympa upgrade shared` \[ `--fix_qencode` \] listname@robot &#124; "\*"

With following options `sympa.pl` will print some information and exit.

- `-h`, `--help`

    Print this help message.

- `--md5_digest=`_password_

    Output a MD5 digest of a password (useful for SOAP client trusted
    application).

- `-v`, `--version`

    Print the version number.

**End of description for earlier version**.

# FILES

`/etc/sympa/sympa.conf` main configuration file.

# SEE ALSO

[sympa\_toc(1)](./sympa_toc.1.md).

# HISTORY

`sympa.pl` was originally written by:

- Serge Aumont

    Comité Réseau des Universités

- Olivier Salaün

    Comité Réseau des Universités

As of Sympa 6.2b.4, it was split into three programs:
`sympa.pl` command line utility, `sympa_automatic.pl` daemon and
`sympa_msg.pl` daemon.

As of Sympa 6.2.68, `sympa.pl` was renamed to `sympa`
and the new form of command line arguments was introduced.

The `--noout` option was introduced on Sympa 6.2.71b.
