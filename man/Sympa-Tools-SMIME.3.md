---
title: 'Sympa::Tools::SMIME(3)'
release: '6.2.70'
---

# NAME

Sympa::Tools::SMIME - Tools for S/MIME messages and X.509 certificates

# DESCRIPTION

## Functions

- find\_keys ( $that, $operation )

    Find the appropriate S/MIME keys/certs for $operation of $that.

    $operation can be:

    - 'sign'

        return the preferred signing key/cert

    - 'decrypt'

        return a list of possible decryption keys/certs

    - 'encrypt'

        return the preferred encryption key/cert

    Returnss `($certs, $keys)`.
    For 'sign' and 'encrypt', these are strings containing the absolute filename.
    For 'decrypt', these are arrayrefs containing absolute filenames.

- parse\_cert ( `text`&#124;`file` => $content )

    Parses X.509 certificate.

    Options:

    - `file` => $filename
    - `text` => $text

        Specifies PEM-encoded certificate.

    Returns a hashref containing these items:

    - {email}

        hashref with email addresses from cert as keys

    - {emails}

        arrayref with email addresses from cert.
        This was added on Sympa 6.2.67b.

    - {subject}

        distinguished name

    - {purpose}

        hashref containing:

        - {enc}

            true if v3 purpose is encryption

        - {sign}

            true if v3 purpose is signing

    - TBD.

    If parsing failed, returns `undef`.

# HISTORY

TBD.
