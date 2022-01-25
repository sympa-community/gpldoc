---
title: 'Sympa::Request::Handler::include(3)'
release: '6.2.68'
---

# NAME

Sympa::Request::Hander::include - include request handler

# DESCRIPTION

Includes users from data sources to a list.

Opens data sources, include or update list users with each of them and closes.
TBD.

# SEE ALSO

[Sympa::DataSource](./Sympa-DataSource.3.md), [Sympa::List](./Sympa-List.3.md).

["admin\_table"](./sympa_database.5.md#admin_table),
["exclusion\_table"](./sympa_database.5.md#exclusion_table),
["inclusion\_table"](./sympa_database.5.md#inclusion_table) and
["subscriber\_table"](./sympa_database.5.md#subscriber_table)
in [sympa\_database(5)](./sympa_database.5.md).

# HISTORY

The feature to include subscribers from data sources was introduced on
Sympa 3.3.6b.4.
Inclusion of owners and moderators was introduced on Sympa 4.2b.5.

[Datasource](https://metacpan.org/pod/Datasource) module appeared on Sympa 5.3a.9.
Entirely rewritten and renamed [Sympa::DataSource](./Sympa-DataSource.3.md) module and
[Sympa::Request::Hander::include](./Sympa-Request-Hander-include.3.md) module appeared on Sympa 6.2.45b.
