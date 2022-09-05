---
title: 'sympa-config(1)'
release: '6.2.70'
---

# NAME

sympa-config - Manipulate configuration of Sympa

# SYNOPSIS

`sympa config` _name_=_value_ ...

`sympa config` _sub-command_ \[ _options_ ... \]

# DESCRIPTION

- `sympa` `config` _name_`=`_value_ ...

    Edit configuration file in batch mode.
    Arguments would include pairs of parameter name and value.

    If no explicit changes given, configuration file won't be rewritten.

    Options:

    - `-o`, `--output=`_set_ ...

        Specify set(s) of parameters to be output.
        _set_ may be either `omittable`, `optional`, `mandatory`,
        `full` (synonym for the former three), `explicit` or `minimal`.
        This option can be specified more than once.

        With this command, `explicit` and `mandatory` sets,
        i.e. those defined in the configuration file explicitly,
        specified in command line arguments or defined as mandatory,
        are always included.

## SUB-COMMANDS

Currently following sub-commands are available.
To see detail of each sub-command,
run '`sympa help config` _sub-command_'.

- [`sympa config create` ...](./sympa-config-create.1.md)

    Create configuration file.

- [`sympa config show` ...](./sympa-config-show.1.md)

    Show the content of configuration file.

# HISTORY

[sympa\_wizard.pl](https://metacpan.org/pod/sympa_wizard.pl) appeared on Sympa 3.3.4b.9.
It was originally written by:

- Serge Aumont <sa@cru.fr>
- Olivier Salaün <os@cru.fr>

`--batch` and `--display` options are added on Sympa 6.1.25 and 6.2.15.

On Sympa 6.2.69b, the most of functions provided by this program was
reorganized and was integrated into `sympa config` command line,
therefore sympa\_wizard.pl was deprecated.
