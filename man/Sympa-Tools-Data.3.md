---
title: 'Sympa::Tools::Data(3)'
release: '6.2.72'
---

# NAME

Sympa::Tools::Data - Functions related to data structures

# DESCRIPTION

This package provides some functions related to data strucures.

## Functions

- clone\_var (...)

    Duplicates a complex variable (faster than dup\_var()).
    TBD.

    CAUTION:
    This duplicates blessed elements even if they are
    singleton/multiton; this breaks subroutine references.

- decode\_custom\_attribute ($string)

    Creates a custom attribute from an XML description.

    Options:

    - $string

        XML formed data as stored in database

    Returns:

    A hashref storing custom attributes.

- diff\_on\_arrays ( $setA, $setB )

    Makes set operation on arrays (seen as set, with no double) :

    \- deleted : A \\ B

    \- added : B \\ A

    \- intersection : A /\\ B

    \- union : A \\/ B

    Options:

    - $setA, $setB

        Arrayrefs.

    Returns:

    A hashref with keys :
    deleted, added, intersection, union.

- dump\_html\_var (...)

    Dump a variable's content.
    TBD.

- dump\_var (...)

    Dump a variable's content.
    TBD.

- dup\_var (...)

    Duplictate a complex variable.
    TBD.

    See also clone\_var().

- encode\_custom\_attribute ($hashref)

    Create an XML Custom attribute to be stored into data base.

    Options:

    - $hasref

        Hashref storing custom attributes.

    Returns:

    String, XML formed data to be stored in database.

- format\_config (\\@params, \[ \\%curConf, \[ \\%newConf \] \],
\[ _key_ `=>` _val_ ... \] ))

    Outputs formetted configuration.

    Options:

    - \\@params

        Configuration scheme.
        See [Sympa::ConfDef](./Sympa-ConfDef.3.md).

    - \\%curConf

        Hashref including current configuration.

    - \\%newConf

        Hashref including update of configuration, if any.

    - _key_ `=>` _val_ ...

        Following options are possible:

        - `output` `=>` `[`_classes_, ...`]`

            Classes of parameters to output: Any of
            `mandatory`, `omittable`, `optional`,
            `full` (synonym for the former tree), `minimal` (included in minimal set,
            i.e. described in installation instruction) and
            `explicit` (the parameter given an empty value with \\%curConf and \\%newConf).

        - `only_changed` `=>` `1`

            When both \\%curConf and \\%newConf are given and no changes were given,
            returns `undef`.

    Returns:

    Formatted string.

    This was introduced on Sympa 6.2.70.

- get\_array\_from\_splitted\_string ($string)

    Returns an array made on a string splited by ','.
    It removes spaces.

    Options:

    - $string

        string to split

    Returns:

    An arrayref.

- hash\_2\_string (...)

    Converts a hash into a string formatted as var1="value1";var2="value2"; into
    a hash.
    TBD.

- is\_in\_array ( $setA, $value )

    Test if a value is on an array.

    Options:

    - $setA

        An arrayref.

    - $value

        a serached value

    Returns true or false.

- recursive\_transformation (...)

    This applies recursively to a data structure.
    The transformation subroutine is passed as a ref.
    TBD.

- smart\_eq ( $x, $y )

    _Function_.
    Check if two strings are identical.

    Parameters:

    - $x, $y

        Operands.

        If both of them are undefined, they are equal.
        If only one of them is undefined, the are not equal.
        If `$y` is a [Regexp](https://metacpan.org/pod/Regexp) object and it matches to `$x`, they are equal.
        Otherwise, they are compared as strings.

    Returns:

    If arguments matched, true value.  Otherwise false value.

- smart\_lessthan (...)

    Compares two scalars, string/numeric independent.
    TBD.

- sort\_uniq ( \[ \\&comp \], @items )

    Returns sorted array of unique elements in the list.

    Parameters:

    - \\&comp

        Optional subroutine reference to compare each pairs of elements.
        It should take two arguments and return negative, zero or positive result.

    - @items

        Items to be sorted.

    This function was added on Sympa 6.2.16.

- string\_2\_hash (...)

    Converts a string formatted as var1="value1";var2="value2"; into a hash.
    Used when extracting from session table some session properties or when
    extracting users preference from user table.
    Current encoding is NOT compatible with encoding of values with '"'.
    TBD.

# SEE ALSO

TBD.

# HISTORY

TBD.
