---
title: 'sympa-move(1)'
release: '6.2.72'
---

# NAME

sympa-move - Move or copy the list

# SYNOPSIS

`sympa move` \[ `--mode=copy` \] _list_`@`_domain_ _new\_list_\[`@`_new\_domain_\]

`sympa copy` _list_`@`_domain_ _new\_list_\[`@`_new\_domain_\]

# DESCRIPTION

Rename a list or move it to another domain.

If `--mode=copy` is specified, original list will be kept.
`sympa copy` is an equivalent alias.
