---
title: 'Sympa::Tools::Domains(3)'
release: '6.2.70'
---

# NAME

Sympa::Tools::Domains - Domains-related functions

# DESCRIPTION

This package provides some email's domains-related functions.

## Functions

- is\_blocklisted ( $email )

    Says if the domain of the given email is blocklisted (`domains_blocklist`
    setting).

    Returns 1 if it's blocklisted, 0 otherwise
