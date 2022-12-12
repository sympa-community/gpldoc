---
title: 'Sympa::CLI(3)'
release: '6.2.71b.1'
---

# NAME

Sympa::CLI - Base class of Sympa CLI modules

# SYNOPSIS

    package Sympa::CLI::mycommand;
    use parent qw(Sympa::CLI);
    
    use constant _options   => qw(...);
    use constant _args      => qw(...);
    use constant _need_priv => 0;
    
    sub _run {
        my $class   = shift;
        my $options = shift;
        my @argv    = @_;
    
        #... Do the job...
        exit 0;
    }

This will implement the function of `sympa mycommand`.

# DESCRIPTION

[Sympa::CLI](./Sympa-CLI.3.md) is the base class of the classes which defines particular
command of command line utility.
TBD.

## Methods subclass should implement

- \_options ( )

    _Class method_, _overridable_.
    Returns an array to define command line options.
    About the format see ["Summary of Option Specifications" in Getopt::Long](https://metacpan.org/pod/Getopt%3A%3ALong#Summary-of-Option-Specifications).

    By default general options are defined and they always take precedence over
    the definition in subclass.

- \_args ( )

    _Class method_, _overridable_.
    Returns an array to define mandatory arguments.
    TBD.

    By default no mandatory arguments are defined.

- \_need\_priv ( )

    _Class method_, _overridable_.
    If this returns true value (the default), the program tries getting privileges
    of Sympa user, prepare database connection, loading main configuration
    and then setting language according to configuration.
    Otherwise, it sets language according to locale setting of console.

- \_log\_to\_stderr ( )

    _Class method_, _overridable_.
    If this returns true value, output by logging facility will be redirected
    to standard error output (stderr).

    By default redirection is disabled.

- \_run ( \\$options, @argv )

    _Class method_, _mandatory_.
    If the program is invoked, command line options are parsed as \_options()
    defines, arguments are checked as \_args() defines and this method is called.

## Subcommands

To implement a subcommand, simply create a submodule inheriting the module
for parent command:

    package Sympa::CLI::mycommand::subcommand;
    use parent qw(Sympa::CLI::mycommand);
    ...

Then this will implement the function of `sympa mycommand subcommand`.

# SEE ALSO

[sympa(1)](./sympa.1.md).

# HISTORY

[Sympa::CLI](./Sympa-CLI.3.md) appeared on Sympa 6.2.68.
