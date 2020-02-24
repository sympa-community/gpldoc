---
title: 'Sympa::Tools::Domains(3)'
release: '6.2.54'
---

# NAME

Sympa::Tools::Domains - Domains-related functions

# DESCRIPTION

This package provides some email's domains-related functions.

## Functions

- is\_blacklisted ( $email )

    Says if the domain of the given email is blacklisted (`domains_blacklist`
    setting).

    Returns 1 if it's blacklisted, 0 otherwise
