---
title: 'Sympa::ConfDef(3)'
release: '6.2.70'
---

# NAME

Sympa::ConfDef - Definition of site and robot configuration parameters

# DESCRIPTION

This module keeps definition of configuration parameters for site default
and each robot.

## Global variable

- @params

    Includes items in order parameters are shown.
    It is then used to load, save, view, edit config files.
    See [Sympa::Config::Schema](./Sympa-Config-Schema.3.md) for details about the content.

# SEE ALSO

[sympa.conf(5)](./sympa.conf.5.md), [robot.conf(5)](./robot.conf.5.md).

# HISTORY

[confdef](https://metacpan.org/pod/confdef) was separated from [Conf](https://metacpan.org/pod/Conf) on Sympa 6.0a,
and renamed to [Sympa::ConfDef](./Sympa-ConfDef.3.md) on 6.2a.39.
On Sympa 6.2.57b, its content was moved to [Sympa::Config::Schema](./Sympa-Config-Schema.3.md).
