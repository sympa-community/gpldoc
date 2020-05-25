---
title: 'Sympa::Spool::Outgoing(3)'
release: '6.2.56'
---

# NAME

Sympa::Spool::Outgoing - Spool for outgoing messages

# SYNOPSIS

    use Sympa::Spool::Outgoing;
    my $bulk = Sympa::Spool::Outgoing->new;

    $bulk->store($message, ['user@dom.ain', 'user@other.dom.ain']);

    my ($message, $handle) = $bulk->next;

# DESCRIPTION

[Sympa::Spool::Outgoing](./Sympa-Spool-Outgoing.3.md) implements the spool for outgoing messages.

## Methods

- new ( )

    _Constructor_.
    Creates new instance of [Sympa::Spool::Outgoing](./Sympa-Spool-Outgoing.3.md).

- next ( \[ no\_filter => 1 \] )

    _Instance method_.
    Gets next packet to process, order is controlled by message priority, then by
    packet priority, then by delivery date, then by reception date.
    Packets with future delivery date are ignored
    (if `no_filter` option is _not_ set).
    Packet will be locked to prevent multiple processing of a single packet.

    Parameters:

    None.

    Returns:

    Two-elements list of [Sympa::Message](./Sympa-Message.3.md) instance and filehandle locking
    a packet.

- quarantine ( $handle )

    _Instance method_.
    Quarantines a packet.
    Packet will be moved into bad/ subdirectory of the spool.

    Parameter:

    - $handle

        Filehandle, [Sympa::LockedFile](./Sympa-LockedFile.3.md) instance, locking packet.

    Returns:

    True value if packet could be quarantined.
    Otherwise false value.

- remove ( $handle )

    _Instance method_.
    Removes a packet.
    If the packet is the last one of bulk sending,
    corresponding message will also be removed from spool.

    Parameter:

    - $handle

        Filehandle, [Sympa::LockedFile](./Sympa-LockedFile.3.md) instance, locking packet.

    Returns:

    True value if packet could be removed.
    Otherwise false value.

- store ( $message, $rcpt, \[ original => $original \],
\[ tag => $tag \] )

    _Instance method_.
    Stores the message into message spool.
    Recipients will be split into multiple packets and
    stored into packet spool.

    Parameters:

    - $message

        Message to be stored.  Following attributes and metadata are referred:

        - {envelope\_sender}

            SMTP "MAIL FROM:" field.

        - {priority}

            Message priority.

        - {packet\_priority}

            Packet priority, assigned as `sympa_packet_priority` parameter by each robot.

        - {date}

            Unix time when the message would be delivered.

        - {time}

            Unix time in floating point number when the message was stored.

    - $rcpt

        Scalar, scalarref or arrayref, for SMTP "RCPT TO:" field(s).

    - original => $original

        If the message was decrypted, stores original encrypted form.

    - tag => $tag

        TBD.

    Returns:

    If storing succeeded, marshalled metadata (file name) of the message.
    Otherwise `undef`.

- too\_much\_remaining\_packets ( )

    _Instance method_.
    Returns true value if the number of remaining packets exceeds
    the value of the `bulk_fork_threshold` config parameter.

# CONFIGURATION PARAMETERS

Following site configuration parameters in sympa.conf will be referred.

- queuebulk

    Directory path of outgoing spool.

    Note:
    Named such by historical reason.
    Don't confuse with `queueoutgoing` for archive spool
    (see [Sympa::Spool::Archive](./Sympa-Spool-Archive.3.md)).

- umask

    The umask to make directory.

# CAVEAT

[Sympa::Spool::Outgoing](./Sympa-Spool-Outgoing.3.md) is not a real subsclass of [Sympa::Spool](./Sympa-Spool.3.md).

# SEE ALSO

[bulk(8)](./bulk.8.md), [Sympa::Mailer](./Sympa-Mailer.3.md), [Sympa::Message](./Sympa-Message.3.md).

# HISTORY

[Bulk](https://metacpan.org/pod/Bulk) module initially written by Serge Aumont appeared on Sympa 6.0.
It used database tables to store and fetch packets and messages.

Support for DKIM signing was added on Sympa 6.1.

Rewritten [Sympa::Bulk](./Sympa-Bulk.3.md) appeared on Sympa 6.2, using spools based on
filesystem.
It was renamed to [Sympa::Spool::Outgoing](./Sympa-Spool-Outgoing.3.md) on Sympa 6.2.45b.3.
