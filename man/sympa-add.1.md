---
title: 'sympa-add(1)'
release: '6.2.68'
---

# NAME

sympa-add - Add users to the list

# SYNOPSIS

`sympa add` \[ `--force` \] \[ `--notify` \] \[ `--quiet` \] \[ `role=`_role_ \] _list_`@`_domain_

# DESCRIPTION

Add email(s) from the list. Data are read from standard input.
The data should contain one email address per line.

Sample:

    # emails to be added
    john.steward@some.company.com       John Steward
    mary.blacksmith@another.company.com Mary Blacksmith

# HISTORY

This option was added on Sympa 6.2.67b.2.
