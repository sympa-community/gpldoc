---
title: 'sympa-close(1)'
release: '6.2.67b.3'
---

# NAME

sympa-close - Close a list or the lists belonging to a family

# SYNOPSIS

`sympa close` \[ `--mode=purge` \] _list_\[`@`_domain_\]

`sympa close` _family_`@@`_domain_

# DESCRIPTION

Close list(s).

If a list is specified, close it.
And if `--mode=purge` is specified, remove the list entirely.

If a family is specified, tries to close all the lists belonging to it.
