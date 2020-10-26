---
title: 'Sympa::List(3)'
release: '6.2.58'
---

# NAME

Sympa::List - Mailing list

# DESCRIPTION

[Sympa::List](./Sympa-List.3.md) represents the mailing list on Sympa.

## Methods

- new( $name, \[ $domain \[ {options...} \] \] )

    _Constructor_.
    Creates a new object which will be used for a list and
    eventually loads the list if a name is given. Returns
    a List object.

    Parameters

    FIXME @todo doc

- add\_list\_admin ( ROLE, USERS, ... )

    Adds a new admin user to the list. May overwrite existing
    entries.

- add\_list\_header ( $message, $field\_type )

    FIXME @todo doc

- add\_list\_member ( USER, HASHPTR )

    Adds a new user to the list. May overwrite existing
    entries.

- available\_reception\_mode ( )

    _Instance method_.
    FIXME @todo doc

    Note: Since Sympa 6.1.18, this returns an array under array context.

- delete\_list\_admin ( ROLE, ARRAY )

    Delete the indicated admin user with the predefined role from the list.
    ROLE may be `'owner'` or `'editor'`.

- delete\_list\_member ( ARRAY )

    Delete the indicated users from the list.

- delete\_list\_member\_picture ( $email )

    Deletes a member's picture file.

- destroy\_multiton ( )
_Instance method_.
Destroy multiton instance. FIXME
- dump\_users ( ROLE )

    Dump user information in user store into file `_$role_.dump` under
    list directory. ROLE may be `'member'`, `'owner'` or `'editor'`.

- find\_picture\_filenames ( $email )

    Returns the type of a pictures according to the user.

- find\_picture\_paths ( )

    _Instance method_.
    FIXME @todo doc

- find\_picture\_url ( $email )

    Find pictures URL

- get\_admins ( $role, \[ filter => \\@filters \] )

    _Instance method_.
    Gets users of the list with one of following roles.

    - `actual_editor`

        Editors belonging to the list.
        If there are no such users, owners of the list.

    - `editor`

        Editors belonging to the list.

    - `owner`

        Owners of the list.

    - `privileged_owner`

        Owners whose `profile` attribute is `privileged`.

    - `receptive_editor`

        Editors belonging to the list and whose reception mode is `mail`.
        If there are no such users, owners whose reception mode is `mail`.

    - `receptive_owner`

        Owners whose reception mode is `mail`.

    Optional filter may be:

    - \[email => $email\]

        Limit result to the user with their e-mail $email.

    Returns:

    In array context, returns (possiblly empty or single-item) array of users.
    In scalar context, returns reference to it.
    In case of database error, returns empty array or undefined value.

- get\_admins\_email ( $role )

    _Instance method_.
    Gets an array of emails of list admins with role
    `receptive_editor`, `actual_editor`, `receptive_owner` or `owner`.

- get\_archive\_dir ( )

    _Instance method_.
    FIXME @todo doc

- get\_available\_msg\_topic ( )

    _Instance method_.
    FIXME @todo doc

- get\_bounce\_address ( WHO, \[ OPTS, ... \] )

    Return the VERP address of the list for the user WHO.

    FIXME: VERP addresses have the name of originating robot, not mail host.

- get\_bounce\_dir ( )

    _Instance method_.
    FIXME @todo doc

- get\_cert ( )

    _Instance method_.
    FIXME @todo doc

- get\_config\_changes ( )

    _Instance method_.
    FIXME @todo doc

- get\_cookie ()

    Returns the cookie for a list, if available.

- get\_current\_admins ( ... )

    _Instance method_.
    FIXME @todo doc

- get\_default\_user\_options ()

    Returns a default option of the list for subscription.

- get\_first\_list\_member ()

    Returns a hash to the first user on the list.

- get\_id ( )

    Return the list ID, different from the list address (uses the robot name)

- get\_including\_lists ( $role )

    _Instance method_.
    List of lists including specified list and hosted by a whole site.

    Parameter:

    - $role

        Role of included users.
        `'member'`, `'owner'` or `'editor'`.

    Returns:

    Arrayref of <Sympa::List> instances.
    Return `undef` on failure.

- get\_list\_member ( USER )

    Returns a subscriber of the list.

- get\_max\_size ()

    Returns the maximum allowed size for a message.

- get\_members ( $role, \[ offset => $offset \], \[ order => $order \],
\[ limit => $limit \])

    _Instance method_.
    Gets users of the list with one of following roles.

    - `member`

        Members of the list, either subscribed or included.

    - `unconcealed_member`

        Members whose `visibility` property is not `conceal`.

    Optional parameters:

    - limit => $limit
    - offset => $offset
    - order => $order

        TBD.

    Returns:

    In array context, returns (possiblly empty or single-item) array of users.
    In scalar context, returns reference to it.
    In case of database error, returns empty array or undefined value.

- get\_msg\_count ( )

    _Instance method_.
    Returns the number of messages sent to the list.
    FIXME

- get\_next\_bouncing\_list\_member ( )

    _Instance method_.
    Loop for all subsequent bouncing users.
    FIXME

- get\_next\_delivery\_date ( )

    _Instance method_.
    Returns the date epoch for next delivery planned for a list.

    Note: As of 6.2a.41, returns `undef` if parameter is not set or invalid.
    Previously it returned current time.

- get\_next\_list\_member ()

    Returns a hash to the next users, until we reach the end of
    the list.

- get\_param\_value ( $param, \[ $as\_arrayref \] )

    _instance method_.
    Returns the list parameter value.
    the parameter is simple (_name_) or composed (_name_`.`_minor_)
    the value is a scalar or a ref on an array of scalar
    (for parameter digest : only for days).

- get\_picture\_path ( )

    _Instance method_.
    FIXME

- get\_recipients\_per\_mode ( )

    _Instance method_.
    FIXME @todo doc

- get\_reply\_to ()

    Returns an array with the Reply-To values.

- get\_resembling\_members ( $role, $searchkey )

    _instance method_.
    TBD.

- get\_stats ( )

    Returns array of the statistics.

- get\_total ( \[ 'nocache' \] )

    Returns the number of subscribers to the list.

- get\_total\_bouncing ( )

    _Instance method_.
    Gets total number of bouncing subscribers.

- has\_data\_sources ( )

    _Instance method_.
    Checks if a list has data sources.

- has\_included\_users ( $role )

    _Instance method_.
    FIXME @todo doc

- insert\_delete\_exclusion ( $email, `"insert"`&#124;`"delete"` )

    _Instance method_.
    Update the exclusion table.
    FIXME @todo doc

- is\_admin ( $role, $user )

    _Instance method_.
    Returns true if $user has $role
    (`privileged_owner`, `owner`, `actual_editor` or `editor`) on the list.

- is\_archived ()

    Returns true is the list is configured to keep archives of
    its messages.

- is\_archiving\_enabled ( )

    Returns true is the list is configured to keep archives of
    its messages, i.e. process\_archive parameter is set to "on".

- is\_available\_msg\_topic ( $topic )

    _Instance method_.
    Checks for a topic if it is available in the list
    (look for each list parameter `msg_topic.name`).

- is\_available\_reception\_mode ( $mode )

    _Instance method_.
    Is a reception mode in the parameter reception of the available\_user\_options
    section?

- is\_digest ( )

    _Instance method_.
    Does the list support digest mode?

- is\_included ( )

    Returns true value if the list is included in another list(s).

- is\_list\_member ( USER )

    Returns true if the indicated user is member of the list.

- is\_member\_excluded ( $email )

    _Instance method_.
    FIXME @todo doc

- is\_moderated ()

    Returns true if the list is moderated.
    FIXME this may not be useful.

- is\_msg\_topic\_tagging\_required ( )

    _Instance method_.
    Checks for the list parameter msg\_topic\_tagging
    if it is set to 'required'.

- is\_there\_msg\_topic ( )

    _Instance method_.
    Tests if some msg\_topic are defined.

- is\_web\_archived ( )

    _Instance method_.
    Is the list web archived?

    FIXME: Broken. Use scenario or is\_archiving\_enabled().

- load ( )

    Loads the indicated list into the object.

- load\_data\_sources\_list ( $robot )

    _Instance method_.
    Loads all data sources.
    FIXME: Used only in wwsympa.fcgi.

- may\_edit ( $param, $who, \[ options, ... \] )

    _Instance method_.
    May the indicated user edit the indicated list parameter or not?
    FIXME @todo doc

- parse\_list\_member\_bounce ( $user )

    _Instance method_.
    FIXME @todo doc

- restore\_suspended\_subscription ( $email )

    _Instance method_.
    FIXME @todo doc

- restore\_users ( ROLE )

    Import user information into user store from file `_$role_.dump` under
    list directory. ROLE may be `'member'`, `'owner'` or `'editor'`.

- save\_config ( LIST )

    Saves the indicated list object to the disk files.

- search\_list\_among\_robots ( $listname )

    _Instance method_.
    FIXME @todo doc

- select\_list\_members\_for\_topic ( $topic, \\@emails )

    _Instance method_.
    FIXME @todo doc

- send\_notify\_to\_owner ( $operation, $params )

    _Instance method_.
    FIXME @todo doc

- send\_probe\_to\_user ( $type, $who )

    _Instance method_.
    FIXME @todo doc

- set\_status\_error\_config ( $msg, parameters, ... )

    _Instance method_.
    FIXME @todo doc

- suspend\_subscription ( $email, $list, $data, $robot )

    _Function_.
    FIXME This should be a instance method.
    FIXME @todo doc

- sync\_include ( $role, options... )

    _Instance method_.
    FIXME would be obsoleted.
    FIXME @todo doc

- update\_config\_changes ( )

    _Instance method_.
    FIXME @todo doc

- update\_list\_admin ( USER, ROLE, HASHPTR )

    Sets the new values given in the hash for the admin user.

- update\_list\_member ( $email, key => value, ... )

    _Instance method_.
    Sets the new values given in the pairs for the user.

- update\_stats ( count, \[ sent, bytes, sent\_by\_bytes \] )

    Updates the stats, argument is number of bytes, returns list fo the updated
    values.  Returns zeroes if failed.

## Functions

- get\_lists ( \[ $that, \[ options, ... \] \] )

    _Function_.
    List of lists hosted by a family, a robot or whole site.

    - $that

        Robot, Sympa::Family object or site (default).

    - options, ...

        Hash including options passed to Sympa::List->new() (see load()) and any of
        following pairs:

        - `'filter' => [ KEYS => VALS, ... ]`

            Filter with list profiles.  When any of items specified by KEYS
            (separated by `"|"`) have any of values specified by VALS,
            condition by that pair is satisfied.
            KEYS prefixed by `"!"` mean negated condition.
            Only lists satisfying all conditions of query are returned.
            Currently available keys and values are:

            - 'creation' => TIME
            - 'creation<' => TIME
            - 'creation>' => TIME

                Creation date is equal to, earlier than or later than the date (UNIX time).

            - 'member' => EMAIL
            - 'owner' => EMAIL
            - 'editor' => EMAIL

                Specified user is a subscriber, owner or editor of the list.

            - 'name' => STRING
            - 'name%' => STRING
            - '%name%' => STRING

                Exact, prefixed or substring match against list name,
                case-insensitive.

            - 'status' => "STATUS&#124;..."

                Status of list.  One of 'open', 'closed', 'pending',
                'error\_config' and 'family\_closed'.

            - 'subject' => STRING
            - 'subject%' => STRING
            - '%subject%' => STRING

                Exact, prefixed or substring match against list subject,
                case-insensitive (case folding is Unicode-aware).

            - 'topics' => "TOPIC&#124;..."

                Exact match against any of list topics.
                'others' or 'topicsless' means no topics.

            - 'update' => TIME
            - 'update<' => TIME
            - 'update>' => TIME

                Date of last update is equal to, earlier than or later than the date (UNIX time).

        - `'limit' => NUMBER `

            Limit the number of results.
            `0` means no limit (default).
            Note that this option may be applied prior to `'order'` option.

        - `'order' => [ KEY, ... ]`

            Subordinate sort key(s).  The results are sorted primarily by robot names
            then by other key(s).  Keys prefixed by `"-"` mean descendent ordering.
            Available keys are:

            - `'creation'`

                Creation date.

            - `'name'`

                List name, case-insensitive.  It is the default.

            - `'total'`

                Estimated number of subscribers.

            - `'update'`

                Date of last update.

    Returns a ref to an array of List objects.

- get\_robots ( )

    _Function_.
    List of robots hosted by Sympa.

- get\_which ( EMAIL, ROBOT, ROLE )

    _Function_.
    Get a list of lists where EMAIL assumes this ROLE (owner, editor or member) of
    function to any list in ROBOT.

## Obsoleted methods

- add\_admin\_user ( USER, ROLE, HASHPTR )

    DEPRECATED.
    Use add\_list\_admin().

- am\_i ( ROLE, USER )

    DEPRECATED. Use is\_admin().

- archive\_exist ( FILE )

    DEPRECATED.
    Returns true if the indicated file exists.

- archive\_ls ()

    DEPRECATED.
    Returns the list of available files, if any.

- archive\_msg ( MSG )

    DEPRECATED.
    Archives the Mail::Internet message given as argument.

- archive\_send ( WHO, FILE )

    DEPRECATED.
    Send the indicated archive file to the user, if it exists.

- get\_db\_field\_type ( ... )

    _Instance method_.
    Obsoleted.

- get\_first\_list\_admin ( ROLE )

    OBSOLETED.
    Use get\_admins().

- get\_global\_user ( USER )

    DEPRECATED.
    Returns a hash with the information regarding the indicated
    user.

- get\_latest\_distribution\_date ( )

    _Instance method_.
    Gets last date of distribution message .

- get\_list\_address ( \[ TYPE \] )

    OBSOLETED.
    Use ["get\_address" in Sympa](./Sympa.3.md#get_address).

    Return the list email address of type TYPE: posting address (default),
    "owner", "editor" or (non-VERP) "return\_path".

- get\_list\_admin ( ROLE, USER)

    Return an admin user of the list with predefined role

    OBSOLETED.
    Use get\_admins().

- get\_list\_id ( )

    OBSOLETED.
    Use get\_id().

- get\_next\_list\_admin ()

    OBSOLETED.
    Use get\_admins().

- get\_state ( FLAG )

    Deprecated.
    Returns the value for a flag : sig or sub.

- may\_do ( ACTION, USER )

    **Note**:
    This method was obsoleted.

    Chcks is USER may do the ACTION for the list. ACTION can be
    one of following : send, review, index, getm add, del,
    reconfirm, purge.

- move\_message ( $file, $queue )

    DEPRECATED.
    No longer used.

- print\_info ( FDNAME )

    DEPRECATED.
    Print the list information to the given file descriptor, or the
    currently selected descriptor.

- savestats ()

    **Deprecated** on 6.2.23b.

    Saves updates the statistics file on disk.

- send\_confirm\_to\_editor ( $message, $method )

    This method was DEPRECATED.

    Send a [Sympa::Message](./Sympa-Message.3.md) object to the editor (for approval).

    Sends a message to the list editor to ask them for moderation
    (in moderation context : editor or editorkey). The message
    to moderate is set in moderation spool with name containing
    a key (reference send to editor for moderation).
    In context of msg\_topic defined the editor must tag it
    for the moderation (on Web interface).

    Parameters:

    - $message

        Sympa::Message instance - the message to moderate.

    - $method

        'md5' - for "editorkey", 'smtp' - for "editor".

    Returns:

    The moderation key for naming message waiting for moderation in moderation spool, or `undef`.

- send\_confirm\_to\_sender ( $message )

    This method was DEPRECATED.

    Sends an authentication request for a sent message to distribute.
    The message for distribution is copied in the auth
    spool in order to wait for confirmation by its sender.
    This message is named with a key.
    In context of msg\_topic defined, the sender must tag it
    for the confirmation

    Parameter:

    - $message

        [Sympa::Message](./Sympa-Message.3.md) instance.

    Returns:

    The key for naming message waiting for confirmation (or tagging) in auth spool, or `undef`.

## Attributes

FIXME @todo doc

# SEE ALSO

[Sympa](./Sympa.3.md).

# HISTORY

[List](https://metacpan.org/pod/List) module was renamed to [Sympa::List](./Sympa-List.3.md) module on Sympa 6.2.
