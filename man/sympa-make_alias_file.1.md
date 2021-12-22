---
title: 'sympa-make_alias_file(1)'
release: '6.2.67b.3'
---

# NAME

sympa-make\_alias\_file - Create aliases file

# SYNOPSIS

`sympa make_alias_file` _domain_&#124;`"*"` \[ _domain_ ... \]

# DESCRIPTION

Create an aliases file in the temporary directory
(specified by `tmpdir` parameter) with all list aliases. It uses the
`list_aliases.tt2` template  (useful when `list_aliases.tt2` was changed).
