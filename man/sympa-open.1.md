---
title: 'sympa-open(1)'
release: '6.2.68'
---

# NAME

sympa-open - Open the list

# SYNOPSIS

`sympa open` \[ `--notify` \] _list_\[`@`_domain_\]

# DESCRIPTION

Restore the closed list (changing its status to open), add aliases and restore
users to database (dump files in the list directory are imported).

The `--notify` is optional.
If present, the owner(s) of the list will be notified.
