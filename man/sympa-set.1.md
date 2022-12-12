---
title: 'sympa-set(1)'
release: '6.2.71b.1'
---

# NAME

sympa-set - Set properties of users of the list

# SYNOPSIS

`sympa set` \[ `--role=`_role_ \] _list_`@`_domain_ _key_`=`_value_ ...

# DESCRIPTION

Set properties of the user(s) in a list. Email addresses of users are read
from standard input.
The data should contain one email address per line.

Option:

- `--role=`_role_

    Traget role: `member`, `editor` or `owner`.
    By default the member is assumed.

Parameters:

_list_`@`_domain_
is mandatory parameter to specify target list.

_key_`=`_value_ ...
is the name and value of each attribute of users.
Following keys are available:

- gecos

    Display name.

- reception

    Reception mode.

- visibility

    Visibility.

- info

    Owner or editor only.  Secrect information.

- profile

    Owner only.
    Privileges of the owner.  `normal` or `privileged`.

With `gecos` or `info`,
empty value may be used to delete attribute.

# HISTORY

This option was added on Sympa 6.2.71b.
