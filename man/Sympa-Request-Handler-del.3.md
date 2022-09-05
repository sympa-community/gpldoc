---
title: 'Sympa::Request::Handler::del(3)'
release: '6.2.70'
---

# NAME

Sympa::Request::Handler::del - del request handler

# DESCRIPTION

Removes a user from a list (requested by another user).
Verifies the authorization and sends acknowledgements
unless quiet is specified.

\+**Note**:
The autharization secenario `del.*` is applicable only when the {role}
attribute is `'member'` (default).
In the other cases the scenario processing should be skipped.

## Attributes

See also ["Attributes" in Sympa::Request::Handler](./Sympa-Request-Handler.3.md#attributes).

- {email}

    _Mandatory_.
    E-mail of the user to be deleted.

- {force}

    _Optional_.
    If true value is specified,
    users will be deleted even if the list is closed.

- {role}

    _Optional_.
    Role of the user to be deleted: `'member'`, `'owner'` or `'editor'`.
    Default value is `'member'`.

    This attribute was introduced on Sympa 6.2.67b.2.

- {quiet}

    _Optional_.
    Don't notify addition to the user.

# SEE ALSO

[Sympa::Request::Handler](./Sympa-Request-Handler.3.md).

# HISTORY
