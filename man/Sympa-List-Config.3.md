---
title: 'Sympa::List::Config(3)'
release: '6.2.50'
---

# NAME

Sympa::List::Config - List configuration

# SYNOPSIS

     use Sympa::List::Config;
     my $config = Sympa::List::Config->new($list, {...});
    
     my $errors = []; 
     my $validity = $config->submit({...}, $user, $errors);
     $config->commit($errors);
     
     my ($value) = $config->get('owner.0.gecos');
     my @keys  = $config->keys('owner');

# DESCRIPTION

## Methods

- new ( $list, \[ config => $initial\_config \], \[ copy => 1 \],
\[ no\_family => 1 \] )

    _Constructor_.
    Creates new instance of [Sympa::List::Config](./Sympa-List-Config.3.md) object.

    Parameters:

    See also ["new" in Sympa::Config](./Sympa-Config.3.md#new).

    - $list

        Context.  An instance of [Sympa::List](./Sympa-List.3.md) class.

    - no\_family => 1

        Won't apply family constraint.
        By default, the constraint will be applied if the list is belonging to
        family.
        See also ["Family constraint"](#family-constraint).

- get\_schema ( \[ $user \] )

    _Instance method_.
    Get configuration schema as hashref.
    See [Sympa::ListDef](./Sympa-ListDef.3.md) about structure of schema.

    Parameter:

    - $user

        Email address of a user.
        If specified, adds `'privilege'` attribute taken from [edit\_list.conf(5)](./edit_list.conf.5.md)
        for the user.

## Attribute

See ["Attribute" in Sympa::Config](./Sympa-Config.3.md#attribute).

## Family constraint

The family (see [Sympa::Family](./Sympa-Family.3.md)) adds additional constraint to schema.

- restricts options for particular scalar parameters to the set of values
or single value,
- makes occurrence of them be required (`'1'` or `'1-n'`), and
- if the occurrence became `'1'`,
makes their privilege be unwritable (`'read'` if it was not `'hidden'`).

## Filters

TBD.

## Validations

TBD.

# SEE ALSO

[Sympa::Config](./Sympa-Config.3.md),
[Sympa::List](./Sympa-List.3.md),
[Sympa::ListDef](./Sympa-ListDef.3.md).

# HISTORY

[Sympa::List::Config](./Sympa-List-Config.3.md) appeared on Sympa 6.2.17.
