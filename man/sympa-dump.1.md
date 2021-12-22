---
title: 'sympa-dump(1)'
release: '6.2.67b.3'
---

# NAME

sympa-dump\_ - Dump users of the lists

# SYNOPSIS

`sympa dump` `--roles=`_role_\[`,`_role_...\] _list_`@`_domain_&#124;`"*"`

# DESCRIPTION

Dumps users of a list or all lists.

`--roles` may specify `member` (subscribers), `owner` (owners),
`editor` (moderators) or any of them separated by comma (`,`).
Only `member` is chosen by default.

Users are dumped in files _role_`.dump` in each list directory.

Note: On Sympa prior to 6.2.31b.1, subscribers were dumped in
`subscribers.db.dump` file, and owners and moderators could not be dumped.

See also ["sympa restore"](https://metacpan.org/pod/sympa-restore).
