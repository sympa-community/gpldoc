---
title: 'Sympa::Aliases(3)'
release: '6.2.72'
---

# NAME

Sympa::Aliases - Base class for alias management

# SYNOPSIS

    package Sympa::Aliases::FOO;
    
    use base qw(Sympa::Aliases);
    
    sub check { ... }
    sub add { ... }
    sub del { ... }
    
    1;

# DESCRIPTION 

This module is the base class for subclasses to manage list aliases of Sympa.

## Methods

- new ( $type, \[ key => value, ... \] )

    _Constructor_.
    Creates new instance of [Sympa::Aliases](./Sympa-Aliases.3.md).

    Returns one of appropriate subclasses according to $type:

    - `'none'`

        No aliases management.

    - Full path to executable

        Use external program to manage aliases.
        See [Sympa::Aliases::External](./Sympa-Aliases-External.3.md).

    - Name of subclass

        Use a subclass `Sympa::Aliases::_name_` to manage aliases.

    For invalid types returns `undef`.

    Note:
    For compatibility to the earlier versions of Sympa,
    if a string `SBINDIR/alias_manager.pl` was given as $type,
    [Sympa::Aliases::Template](./Sympa-Aliases-Template.3.md) subclass will be used.

    Optional `_key_ => _value_` pairs are included in the instance as
    hash entries.

- check ($listname, $robot\_id)

    _Instance method_, _overridable_.
    Checks if the addresses of requested list exist already.

    Parameters:

    - $listname

        Name of the list.
        Mandatory.

    - $robot\_id

        List's robot.

    Returns:

    True value if one of addresses exists.
    `0` if none found.
    `undef` if something wrong happened.

    By default, this method always returns `0`.

- add ($list)

    _Instance method_, _overridable_.
    Installs aliases for the list $list.

    Parameters:

    - $list

        An instance of [Sympa::List](./Sympa-List.3.md).

    Returns:

    `1` if installation succeeded.
    `0` if there were no aliases to be installed.
    `undef` if not applicable.

    By default, this method always returns `0`.

- del ($list)

    _Instance method_, _overridable_.
    Removes aliases for the list $list.

    Parameters:

    - $list

        An instance of [Sympa::List](./Sympa-List.3.md).

    Returns:

    `1` if removal succeeded.
    `0` if there were no aliases to be removed.
    `undef` if not applicable.

    By default, this method always returns `0`.

## Function

- check\_new\_listname ( $listname, $robot )

    _Function_.
    Checks if a new listname is allowed.

    TBD.

    Parameteres:

    - $listname

        A list name to be checked.

    - $robot

        Robot context.

    Returns:

    If check fails, an array including information of errors.
    If it succeeds, empty array.

    **Note**:
    This should be used to check name of list to be created.
    Names of existing lists may not necessarily pass checks by this function.

    This function was added on Sympa 6.2.37b.2.

# SEE ALSO

[Sympa::Aliases::CheckSMTP](./Sympa-Aliases-CheckSMTP.3.md),
[Sympa::Aliases::External](./Sympa-Aliases-External.3.md),
[Sympa::Aliases::Template](./Sympa-Aliases-Template.3.md).

# HISTORY

`alias_manager.pl` as a program to automate alias management appeared on
Sympa 3.1b.13.

[Sympa::Aliases](./Sympa-Aliases.3.md) module as an OO-based class appeared on Sympa 6.2.23b,
and it obsoleted `alias_manager.pl`.
