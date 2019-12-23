---
title: 'Sympa::Spool::Listmaster(3)'
release: '6.2.50'
---

# NAME

Sympa::Spool::Listmaster - Spool on memory for listmaster notification

# SYNOPSIS

    use Sympa::Spool::Listmaster;
    my $alarm = Sympa::Spool::Listmaster->instance;

    $alarm->store($message, $rcpt, $operation);

    $alarm->flush();
    $alarm->flush(purge => 1);

# DESCRIPTION

[Sympa::Spool::Listmaster](./Sympa-Spool-Listmaster.3.md) implements on-memory spool for
listmaster notification.

## Methods

- instance ( )

    _Constructor_.
    Creates a singleton instance of [Sympa::Spool::Listmaster](./Sympa-Spool-Listmaster.3.md) object.

    _Note_:
    Unlike the other spool classes, the instance of this class is singleton.

    Returns:

    A new [Sympa::Spool::Listmaster](./Sympa-Spool-Listmaster.3.md) instance, or undef for failure.

- store ( $message, $rcpt, operation => $operation )

    _Instance method_.
    Stores a message of a operation to spool.

    Parameters:

    - $message

        [Sympa::Message](./Sympa-Message.3.md) object to be stored.

    - $rcpt

        Arrayref or scalar.  Recipient of notification.

    - operation => $operation

        A string specifies tag of the message.

    Returns:

    True value if succeed, otherwise `undef`.

- flush ( \[ purge => $purge \] )

    _Instance method_.
    Sends compiled messages in spool.

    If true value is given as optional argument, all messages in spool will be
    sent.

## Attribute

The instance of [Sympa::Spool::Listmaster](./Sympa-Spool-Listmaster.3.md) has following attribute.

- {use\_bulk}

    If set to be true, messages to be sent will be stored into spool
    instead of being stored to sendmail.

    Default is false.

# CAVEAT

[Sympa::Spool::Listmaster](./Sympa-Spool-Listmaster.3.md) is not a real subsclass of [Sympa::Spool](./Sympa-Spool.3.md).

# HISTORY

Feature to compile notification to listmaster in group appeared on Sympa 6.2.

[Sympa::Alarm](./Sympa-Alarm.3.md) appeared on Sympa 6.2.
It was renamed to [Sympa::Spool::Listmaster](./Sympa-Spool-Listmaster.3.md) on Sympa 6.2.45b.3.
