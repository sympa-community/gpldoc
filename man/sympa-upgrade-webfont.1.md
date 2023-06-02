---
title: 'sympa-upgrade-webfont(1)'
release: '6.2.72'
---

# NAME

sympa-upgrade-webfont - Upgrading font in web templates

# SYNOPSIS

    sympa upgrade webfont [--dry_run|-n]

# OPTIONS

- --dry\_run&#124;-n

    Shows what will be done but won't really perform the upgrade process.

# DESCRIPTION

Versions 6.2.72 or later uses Font Awesome Free which is not compatible to
Font Awesome 4.x or earlier.
To solve this problem, this command upgrades customized web templates.

# HISTORY

This command appeared on Sympa 6.2.72.
