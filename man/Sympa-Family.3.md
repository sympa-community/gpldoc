---
title: 'Sympa::Family(3)'
release: '6.2.49b.1'
---

# NAME

Sympa::Family - List families

# DESCRIPTION

Sympa allows lists creation and management by sets. These are the families,
sets of lists sharing common properties.
This module gathers all the family-specific operations.

## Functions

- get\_families ( $robot )

    _Function_.
    Returns the list of existing families in the Sympa installation.

    Arguments

    - $robot

        The robot the family list of which we want to get.

    Returns

    An arrayref containing all the robot's family names.

- get\_available\_families ( $robot )

    _Function_.
    **Obsoleted**.
    Use `get_families()`.

## Methods

- new (STRING $name, STRING $robot)

    _Constructor_.
    Creates a new Sympa::Family object of name $name, belonging to the robot $robot.

    Arguments

    - $name

        A character string containing the family name,

    - $robot

        A character string containing the name of the robot which the family is/will
        be installed in.

    Returns

    The [Sympa::Family](./Sympa-Family.3.md) object.

- check\_param\_constraint (LIST $list)

    _Instance method_.
    Checks the parameter constraints taken from param\_constraint.conf file for
    the [Sympa::List](./Sympa-List.3.md) object $list.

    Arguments

    - $list

        A List object corresponding to the list to chek.

    Returns

    - _1_ if everything goes well,
    - _undef_ if something goes wrong,
    - _\\@error_, a ref on an array containing parameters conflicting with constraints.

- get\_constraints ()

    _Instance method_.
    Returns a hash containing the values found in the param\_constraint.conf file.

    Arguments

    None.

    Returns

    `$self->{'param_constraint_conf'}`,
    a hash containing the values found in the param\_constraint.conf file.

- check\_values (SCALAR $param\_value, SCALAR $constraint\_value)

    _Instance method_.
    Returns 0 if all the value(s) found in $param\_value appear also in
    $constraint\_value.
    Otherwise the function returns an array containing the unmatching values.

    Arguments

    - $param\_value

        A scalar or a ref to a list (which is also a scalar after all)

    - $constraint\_value

        A scalar or a ref to a list

    Returns

    _\\@error_, a ref to an array containing the values in $param\_value
    which don't match those in $constraint\_value.

- get\_param\_constraint (STRING $param)

    _Instance method_.
    Gets the constraints on parameter $param from the 'param\_constraint.conf' file.

    Arguments

    - $param

        A character string corresponding to the name of the parameter
        for which we want to gather constraints.

    Returns

    - _0_ if there are no constraints on the parameter,
    - _a scalar_ containing the allowed value if the parameter has a fixed value,
    - _a ref to a hash_ containing the allowed values if the parameter is controlled,
    - _undef_ if something went wrong.

- get\_uncompellable\_param ()

    _Instance method_.
    Returns a reference to hash whose keys are the uncompellable parameters.

    Arguments

    None.

    Returns

    `\%list_of_param`, a ref to a hash the keys of which are the
    uncompellable parameters names.

- insert\_delete\_exclusion ( $email, $action )

    _Instance method_.
    Handle exclusion table for family.
    TBD.

- get\_id ( )

    _Instance method_.
    Gets unique identifier of instance.

## Attributes

- {name}

    The name of family.

- {robot}

    The robot the family belongs to.

- {dir}

    Base dire4ctory of the family.

- {state}

    Obsoleted.
    TBD.

# SEE ALSO

[Sympa::List](./Sympa-List.3.md),
[Sympa::Request::Handler::close\_list](./Sympa-Request-Handler-close_list.3.md),
[Sympa::Request::Handler::create\_automatic\_list](./Sympa-Request-Handler-create_automatic_list.3.md),
[Sympa::Request::Handler::update\_automatic\_list](./Sympa-Request-Handler-update_automatic_list.3.md).

[sympa\_automatic(8)](./sympa_automatic.8.md).

[List families](https://sympa-community.github.io/manual/customize/basics-families.html), _Sympa Administration Manual_.

# HISTORY

[Family](https://metacpan.org/pod/Family) module was initially written by:

- Serge Aumont &lt;sa AT cru.fr>
- Olivier Salaun &lt;os AT cru.fr>

Renamed [Sympa::Family](./Sympa-Family.3.md) appeared on Sympa 6.2a.39.
Afterward, it has been gradually rewritten,
therefore [Sympa::Request::Handler::close\_list](./Sympa-Request-Handler-close_list.3.md),
[Sympa::Request::Handler::create\_automatic\_list](./Sympa-Request-Handler-create_automatic_list.3.md) and
[Sympa::Request::Handler::update\_automatic\_list](./Sympa-Request-Handler-update_automatic_list.3.md) were separated
up till Sympa 6.2.49b.
