---
title: 'Sympa::ListDef(3)'
release: '6.2.72'
---

# NAME

Sympa::ListDef - Definition of list configuration parameters

# DESCRIPTION

This module keeps definition of configuration parameters for each list.

## Global variable

- %alias

    Deprecated by Sympa 6.2.16.

- %pinfo

    This hash COMPLETELY defines ALL list parameters.
    It is then used to load, save, view, edit list config files.
    See [Sympa::Config::Schema](./Sympa-Config-Schema.3.md) for details about the content.

- %user\_info

    TBD.

# SEE ALSO

[list\_config(5)](./list_config.5.md),
[Sympa::List::Config](./Sympa-List-Config.3.md),
[Sympa::ListOpt](./Sympa-ListOpt.3.md).

# HISTORY

[Sympa::ListDef](./Sympa-ListDef.3.md) was separated from [List](https://metacpan.org/pod/List) module on Sympa 6.2.
On Sympa 6.2.57b, its content was moved to [Sympa::Config::Schema](./Sympa-Config-Schema.3.md).
