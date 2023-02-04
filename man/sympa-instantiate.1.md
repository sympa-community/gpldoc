---
title: 'sympa-instantiate(1)'
release: '6.2.72'
---

# NAME

sympa-instantiate - Instantiate the lists in a family

# SYNOPSIS

`sympa instantiate` `--input-file=`_/path/to/file.xml_ \[ `--close-unknown` \] \[ `--quiet` \] _family_`@@`_domain_

# DESCRIPTION

Instantiate the lists described in the file.xml in specified family.
The family directory must exist; automatically close undefined lists in a
new instantiation if `--close_unknown` is specified; do not print report if
`--quiet` is specified.
