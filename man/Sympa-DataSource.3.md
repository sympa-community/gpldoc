---
title: 'Sympa::DataSource(3)'
release: '6.2.65b.1'
---

# NAME

Sympa::DataSource - Base class of Sympa data source subclasses

# SYNOPSIS

    # To implemnt Sympa::DataSource::Foo:

    package Sympa::DataSource::Foo;

    use base qw(Sympa::DataSource);
    
    sub _open {
        my $self = shift;
        ...
        return $handle;
    }
    
    sub _next {
        my $self = shift;
        ...
        return [$email, $gecos];
    }
    
    1;
    
    # To use Sympa::DataSource::Foo:
    
    usr Sympa::DataSource;
    
    $ds = Sympa::DataSource->new('Foo', 'member', context => $list,
        key => val, ...);
    if ($ds and $ds->open) {
        while (my $member = $ds->next) {
            ...
        }
        $ds->close;
    }

# DESCRIPTION

TBD.

## Methods

- new ( $type, $role, context => $that, \[ _key_ => _val_, ... \] )

    _Constructor_.
    Creates a new instance of [Sympa::DataSource](./Sympa-DataSource.3.md).

    Parameters:

    - $type

        Type of data source.
        This corresponds to impemented subclasses.

    - $role

        Role of data source.
        `'member'`, `'owner'`, `'editor'` or `'custom_attribute'`.

    - context => $that

        Context. [Sympa::List](./Sympa-List.3.md) instance and so on.

    - _key_ => _val_, ...

        Optional or mandatory parameters.

    Returns:

    A new instance, or `undef` on failure.

- close ( )

    _Instance method_.
    Closes backend and does cleanup.

- is\_external ( )

    _Instance method_.
    Returns true value if the data source is external data source.
    "External" means that it is not `include_sympa_list` (the instance of
    [Sympa::DataSource::List](./Sympa-DataSource-List.3.md)) or not including any lists on local domain.

    Known bug:

    - If a data source is a list included from the other external data source(s),
    this method will treat it as non-external so that some requests not allowed
    for external data sources, such as `move_user` request, on corresponding
    users may be allowed.

- next ( )

    _Instance method_.
    Returns the next entry in data source.
    Data source should have been opened.

- open ( )

    _Instance method_.
    Opens backend and returns handle.

- get\_id ( )

    _Instance method_.
    Gets unique ID of the instance.

- get\_short\_id ( )

    _Instance method_.
    Gets data source ID, a hexadecimal string with 8 columns.

- name ( )

    _Instance method_.
    Gets human-readable name of data source.
    Typically it is value of {name} attribute or result of get\_short\_id().

- role ( )

    _Instance method_.
    Returns $role set by new().

- \_\_dsh ( )

    _Instance method_, _protected_.
    Returns native query handle which [\_open](https://metacpan.org/pod/_open)() returned.
    This may be used only at inside of each subclass.

## Methods subclass should implement

- required\_modules

    _Class or instance method_.
    TBD.

- \_open ( \[ options... \] )

    _Instance mthod_.
    TBD.

- \_next ( \[ options... \] )

    _Instance method_, _mandatory_.
    TBD.

- \_next\_ca ( \[ options... \] )

    _Instance method_, _mandatory_ if the data source supports custom attribute.
    TBD.

- \_close (  )

    _Instance method_.
    TBD.

## Attributes

- {context}

    Context of the data source set by new().

- Others

    The other options set by new() may be accessed as attributes.

# HISTORY

[Sympa::DataSource](./Sympa-DataSource.3.md) appeared on Sympa 6.2.45b.
See also ["HISTORY" in Sympa::Request::Handler::include](./Sympa-Request-Handler-include.3.md#history).
