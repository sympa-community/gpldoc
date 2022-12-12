---
title: 'sympa-upgrade-shared(1)'
release: '6.2.71b.1'
---

# NAME

sympa-upgrade-shared -
Migrating shared repository created by earlier versions

# SYNOPSIS

    sympa upgrade shared LISTNAME@DOMAIN [ --fix_qencode ]

    sympa upgrade shared * [ --fix_qencode ]

# DESCRIPTION

` sympa upgrade shared` renames file names in shared repositories
that may be incorrectly encoded because of previous Sympa versions.

- As of Sympa 5.3a.8, file names in shared repository are Q-encoded,
therefore made easier to store on any filesystem with any encoding.
- As of Sympa 6.1b.5, 
Encoding of shared documents was not consistent with recent
version of MIME::EncWords module:
MIME::EncWords::encode\_mimewords() used to encode characters `-!*+/`.
Now these characters are preserved, according to RFC 2047 section 5.
We had to change encoding of shared documents according to new algorithm.

# OPTIONS

- LISTNAME@DOMAIN &#124; `"*"`

    Specifies target list(s).

- --fix\_qencode

    If specified, fixes Q-encoding changed on Sympa 6.1b.5.
    Otherwise, applies Q-encoding introduced by Sympa 5.3a.8.

# HISTORY

upgrade\_shared\_repository.pl appeared as separate executable on Sympa 6.2.17.

Its function was moved to `sympa upgrade shared` on Sympa 6.2.70.
