---
title: 'Sympa::DatabaseDriver::LDAP(3)'
release: '6.2.64'
---

# NAME

Sympa::DatabaseDriver::LDAP - Database driver for LDAP search operation

# DESCRIPTION

TBD.

## Methods specific to this module

- canonical\_dn ( $dn )

    **Obsoleted**.

    _Instance method_.
    See ["canonical\_dn" in Net::LDAP::Util](https://metacpan.org/pod/Net%3A%3ALDAP%3A%3AUtil#canonical_dn).

    However, this method try to use RFC 1779 escaping as much as possible.

- escape\_dn\_value ( $string )

    **Obsoleted**.

    _Instance method_.
    See ["escape\_dn\_value" in Net::LDAP::Util](https://metacpan.org/pod/Net%3A%3ALDAP%3A%3AUtil#escape_dn_value).

- escape\_filter\_value ( $string )

    **Obsoleted**.

    _Instance method_.
    See ["escape\_filter\_value" in Net::LDAP::Util](https://metacpan.org/pod/Net%3A%3ALDAP%3A%3AUtil#escape_filter_value).

# SEE ALSO

[Sympa::DatabaseDriver](./Sympa-DatabaseDriver.3.md), [Sympa::Database](./Sympa-Database.3.md).

# HISTORY

[Sympa::DatabaseDriver::LDAP](./Sympa-DatabaseDriver-LDAP.3.md) appeared on Sympa 6.2.

On Sympa 6.2.15, `use_ssl` and `use_start_tls` options were deprecated and
replaced by `use_tls`.
