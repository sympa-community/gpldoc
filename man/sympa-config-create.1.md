---
title: 'sympa-config-create(1)'
release: '6.2.70'
---

# NAME

sympa-config-create - Create configuration file

# SYNOPSIS

`sympa config create` \[ `--config=`_/path/to/new/sympa.conf_ \]
\[ `-o`, `--output=`_set_ ... \]

# DESCRIPTION

Creates a new `sympa.conf` configuration file.

Options:

- `--config`, `-f=`_/path/to/new/sympa.conf_

    Use an alternative configuration file.

- `-o`, `--output=`_set_ ...

    Specify set(s) of parameters to be output.
    _set_ may be either `omittable`, `optional`, `mandatory`,
    `full` (synonym of the former three) or `minimal`.
    This option can be specified more than once.

    By default only `minimal` set of parameters, i.e. those described in the
    installation manual, are written in the configuration file.
