---
title: 'sympa-del(1)'
release: '6.2.67b.3'
---

# NAME

sympa-del - Delete users from the list

# SYNOPSIS

`sympa del` \[ `--force` \] \[ `--notify` \] \[ `--quiet` \] \[ `role=`_role_ \] _list_`@`_domain_

# DESCRIPTION

Delete email(s) from the list. Data are read from standard input.
The data should contain one email address per line.

Sample:

    # emails to be deleted
    john.steward@some.company.com
    mary.blacksmith@another.company.com

# HISTORY

This option was added on Sympa 6.2.67b.2.
