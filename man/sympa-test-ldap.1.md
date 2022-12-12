---
title: 'sympa-test-ldap(1)'
release: '6.2.71b.1'
---

# NAME

sympa-test-ldap - Testing LDAP connection for Sympa

# SYNOPSIS

    sympa test ldap --host=string --suffix=string
    [ --attrs=[ string,...|* ] ]
    [ --bind_dn=string [ --bind_password=string ] ]
    [ --port=string ] [ --scope=base|one|sub ]
    [ --use_tls=starttls|ldaps|none
      [ --ca_file=string ] [ --ca_path=string ]
      [ --ca_verify=none|optional|require ]
      [ --ssl_cert=string ] [ --ssl_ciphers=string ] [ --ssl_key=string ]
      [ --ssl_version=sslv2|sslv3|tlsv1|tlsv1_1|tlsv1_2|tlsv1_3 ] ]
    filter

# DESCRIPTION

`sympa test ldap` tests LDAP connection and search operation using LDAP
driver of Sympa.

# SEE ALSO

[Sympa::DatabaseDriver::LDAP](./Sympa-DatabaseDriver-LDAP.3.md).

# HISTORY

testldap.pl appeared before Sympa 3.0.

It supported LDAP over TLS (ldaps) on Sympa 5.3a.1.

testldap.pl was renamed to sympa\_test\_ldap.pl on Sympa 6.2.

`--use_ssl` and `--use_start_tls` options were obsoleted by Sympa 6.2.15.
`--use_tls` option would be used instead.

This function was moved to `sympa test ldap` command line on Sympa 6.2.70.
