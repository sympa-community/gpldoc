---
title: 'sympa_config(5)'
release: '6.2.58'
---

# NAME

sympa\_config - Configuration files for Sympa mailing list manager

# DESCRIPTION

There are three levels in Sympa's main configuration:
site global, mail domain and list.

## `sympa.conf`: Configuration file for global settings

`/etc/sympa/sympa.conf` is main configuration file of Sympa.
Several parameters defined in this file may be overridden by `robot.conf`
configuration file for each virtual domain, or by `config` configuration file
for each mailing list.

Format of `sympa.conf` and `robot.conf` is as following:

- Lines beginning with `#` and containing only spaces are ignored.
- Each line has the form "_parameter_ _value_".
_value_ may contain spaces but may not contain newlines.

    There are simple parameters and compound parameters.

    The name of compound parameter consist of a paragraph name and
    a sub-parameter name separated by period (`.`).
    However some compound parameters have simple synonym names to keep
    compatibility to earlier versions (See ["Obsoleted sympa.conf parameters"](#obsoleted-sympaconf-parameters)).

    Example:

        process_archive on
        archive.web_access open
        archive.mail_access closed

## `robot.conf`: Optional configuration file for the mail domain

`robot.conf` is the optional configuration file for each mail domain.

Format of `robot.conf` is the same as `sympa.conf` above.

## `config`: Configuration file for the mailing list

`config` is main configuration file of each mailing list.

Format of `config` is as following:

- Lines beginning with `#` and containing only spaces are ignored.
- There are simple parameters and compound parameters:
    - A cimple parameter is expressed by single line by each.
    The line has the form "_parameter_ _value_".
    _value_ may contain spaces but may not contain newlines.

        Several parameters may have multiple values.
        If it's the case, values may be separated by comma (`,`)
        or parameter lines may be repeated.
        Some of parameters must have one or more of limited values.

        Example:

            subject This is subject of my list
            
            remove_headers User-Agent,Importance
            
            custom_headers X-List: mylist
            custom_headers X-Face: %`-W7!?^]Sg'I-K>P<cdn&k:~A^{x>(]Gc{V...
            
            rfc2369_header_fields post,owner 

    - A compound parameter is expressed by multiple lines, so-called "paragraph",
    that consists of
    the first line specifying paragraph name and subsequent one or more
    sub-parameter lines.  Paragraph must be separated by one or more empty lines
    from the other parameters.

        Several multiple line parameters may occur multiple times.

# PARAMETERS

Below is entire list of configuration parameters.

- Sub-parameters in paragraph are listed as _paragraph_`.`_sub-parameter_
by each.
- "Default" is built-in default value if any.

## Service description

### `**domain**`

Primary mail domain name

- Format:

    /`[-\w]+(?:[.][-\w]+)+`/

- Default:

    None, _mandatory_.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Example:

    domain mail.example.org

### `**listmaster**`

Email addresses of listmasters

- Format:

    Multiple values allowed, separated by `,`.

    /`$addrspec`/

- Default:

    None, _mandatory_.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Email addresses of the listmasters (users authorized to perform global server commands). Some error reports may also be sent to these addresses. Listmasters can be defined for each virtual host, however, the default listmasters will have privileges to manage all virtual hosts.

Example:

    listmaster your_email_address@domain.tld

### `**supported_lang**`

Supported languages

- Format:

    /`\w+(\-\w+)*`/

- Default:

    `ca,cs,de,el,en-US,es,et,eu,fi,fr,gl,hu,it,ja,ko,nb,nl,oc,pl,pt-BR,ru,sv,tr,vi,zh-CN,zh-TW`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

All supported languages for the user interface. Languages proper locale information not installed are ignored.

### `**title**`

Title of service

- Format:

    /`.+`/

- Default:

    `Mailing lists service`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

The name of your mailing list service. It will appear in the header of web interface and subjects of several service messages.

### `**gecos**`

Display name of Sympa

- Format:

    /`.+`/

- Default:

    `SYMPA`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

This parameter is used for display name in the "From:" header field for the messages sent by Sympa itself.

### `**legacy_character_support_feature**`

Support of legacy character set

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    site (`sympa.conf`)

If set to "on", enables support of legacy character set according to charset.conf(5) configuration file.

In some language environments, legacy encoding (character set) can be preferred for e-mail messages: for example iso-2022-jp in Japanese language.

## Database related

### `**update_db_field_types**`

Update database structure

- Format:
    - `auto` - automatic
    - `off` - disabled
- Default:

    `auto`

- Context:

    site (`sympa.conf`)

auto: Updates database table structures automatically.

However, since version 5.3b.5, Sympa will not shorten field size if it already have been longer than the size defined in database definition.

### `**db_type**`

Type of the database

- Format:

    /`\w+`/

- Default:

    `mysql`

- Context:

    site (`sympa.conf`)

Possible types are "MySQL", "PostgreSQL", "Oracle" and "SQLite".

### `**db_host**`

Hostname of the database server

- Format:

    /`$host`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

With PostgreSQL, you can also use the path to Unix Socket Directory, e.g. "/var/run/postgresql" for connection with Unix domain socket.

Example:

    db_host localhost

### `**db_port**`

Port of the database server

- Format:

    /`[-/\w]+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

### `**db_name**`

Name of the database

- Format:

    /`.+`/

- Default:

    `sympa`

- Context:

    site (`sympa.conf`)

With SQLite, this must be the full path to database file.

With Oracle Database, this must be SID, net service name or easy connection identifier (to use net service name, db\_host should be set to "none" and HOST, PORT and SERVICE\_NAME should be defined in tnsnames.ora file).

### `**db_user**`

User for the database connection

- Format:

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

Example:

    db_user sympa

### `**db_passwd**`

Password for the database connection

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    site (`sympa.conf`)

What ever you use a password or not, you must protect the SQL server (is it not a public internet service ?)

Example:

    db_passwd your_passwd

### `**db_options**`

Database options

- Format:

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

If these options are defined, they will be appended to data source name (DSN) fed to database driver. Check the related DBD documentation to learn about the available options.

Example:

    db_options mysql_read_default_file=/home/joe/my.cnf;mysql_socket=tmp/mysql.sock-test

### `**db_env**`

Environment variables setting for database

- Format:

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

With Oracle Database, this is useful for defining ORACLE\_HOME and NLS\_LANG.

Example:

    db_env NLS_LANG=American_America.AL32UTF8;ORACLE_HOME=/u01/app/oracle/product/11.2.0/server

### `**db_timeout**`

Database processing timeout

- Format:

    /`\d+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

Currently, this parameter may be used for SQLite only.

### `**db_additional_subscriber_fields**`

Database private extension to subscriber table

- Format:

    Multiple values allowed, separated by `,`.

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

Adds more fields to "subscriber\_table" table. Sympa recognizes fields defined with this parameter. You will then be able to use them from within templates and scenarios:

\* for scenarios: \[subscriber->field\]

\* for templates: \[% subscriber.field %\]

These fields will also appear in the list members review page and will be editable by the list owner. This parameter is a comma-separated list.

You need to extend the database format with these fields

Example:

    db_additional_subscriber_fields billing_delay,subscription_expiration

### `**db_additional_user_fields**`

Database private extension to user table

- Format:

    Multiple values allowed, separated by `,`.

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

Adds more fields to "user\_table" table. Sympa recognizes fields defined with this parameter. You will then be able to use them from within templates: \[% subscriber.field %\]

This parameter is a comma-separated list.

You need to extend the database format with these fields

Example:

    db_additional_user_fields age,address

## System log

### `**syslog**`

System log facility for Sympa

- Format:

    /`\S+`/

- Default:

    `LOCAL1`

- Context:

    site (`sympa.conf`)

Do not forget to configure syslog server.

### `**log_socket_type**`

Communication mode with syslog server

- Format:

    /`\w+`/

- Default:

    `unix`

- Context:

    site (`sympa.conf`)

### `**log_level**`

Log verbosity

- Format:

    /`\d+`/

- Default:

    `0`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Sets the verbosity of logs.

0: Only main operations are logged

3: Almost everything is logged.

Example:

    log_level 2

## Mail server

### `**sendmail**`

Path to sendmail

- Format:

    /`.+`/

- Default:

    `/usr/sbin/sendmail`

- Context:

    site (`sympa.conf`)

Absolute path to sendmail command line utility (e.g.: a binary named "sendmail" is distributed with Postfix).

Sympa expects this binary to be sendmail compatible (exim, Postfix, qmail and so on provide it).

### `**sendmail_args**`

Command line parameters passed to sendmail

- Format:

    /`.+`/

- Default:

    `-oi -odi -oem`

- Context:

    site (`sympa.conf`)

Note that "-f", "-N" and "-V" options and recipient addresses should not be included, because they will be included by Sympa.

### `**sendmail_aliases**`

Path of the file that contains all list related aliases

- Format:

    /`.+`/

- Default:

    `/etc/mail/sympa_aliases`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

It is recommended to create a specific alias file so that Sympa never overwrites the standard alias file, but only a dedicated file.

Set this parameter to "none" if you want to disable alias management in Sympa.

### `**aliases_program**`

Program used to update alias database

- Format:

    /`makemap|newaliases|postalias|postmap|/.+`/

- Default:

    `newaliases`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

This may be "makemap", "newaliases", "postalias", "postmap" or full path to custom program.

### `**aliases_db_type**`

Type of alias database

- Format:

    /`\w[-\w]*`/

- Default:

    `hash`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

"btree", "dbm", "hash" and so on.  Available when aliases\_program is "makemap", "postalias" or "postmap"

### `**alias_manager**`

Path to alias manager

- Format:

    /`.+`/

- Default:

    `/home/sympa/sbin/alias_manager.pl`

- Context:

    site (`sympa.conf`)

The absolute path to the script that will add/remove mail aliases

Example:

    alias_manager /usr/local/libexec/ldap_alias_manager.pl

## List definition

### `**subject**`

Subject of the list

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

This parameter indicates the subject of the list, which is sent in response to the LISTS mail command. The subject is a free form text limited to one line.

### `**visibility**`

Visibility of the list

- Format:

    Name of `visibility` scenario:

    - `conceal` - conceal except for subscribers
    - `noconceal` - no conceal
    - `secret` - conceal even for subscribers

- Default:

    `conceal`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter indicates whether the list should feature in the output generated in response to a LISTS command or should be shown in the list overview of the web-interface.

### `**topics**`

Topics for the list

- Format:

    Multiple values allowed, separated by `,`.

    List topic.

- Default:

    None.

- Context:

    list (`config`)

This parameter allows the classification of lists. You may define multiple topics as well as hierarchical ones. WWSympa's list of public lists uses this parameter.

### `**lang**`

Language of the list

- Format:

    Language tag.

- Default:

    `en-US`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter defines the language used for the list. It is used to initialize a user's language preference; Sympa command reports are extracted from the associated message catalog.

### `**family_name**`

Family name

- Format:

    /`$family_name`/

- Default:

    None.

- Context:

    list (`config`)

### `**max_list_members**`

Maximum number of list members

- Format:

    Number of list members.

- Default:

    `0` (list members)

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

limit for the number of subscribers. 0 means no limit.

### `**priority**`

Priority

- Format:
    - `0` - 0 - highest priority
    - `1` - 1
    - `2` - 2
    - `3` - 3
    - `4` - 4
    - `5` - 5
    - `6` - 6
    - `7` - 7
    - `8` - 8
    - `9` - 9 - lowest priority
    - `z` - queue messages only
- Default:

    `5`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The priority with which Sympa will process messages for this list. This level of priority is applied while the message is going through the spool. The z priority will freeze the message in the spool.

## Receiving

### `**sender_headers**`

Header field name(s) used to determine sender of the messages

- Format:
- Default:

    `From`

- Context:

    site (`sympa.conf`)

"Return-Path" means envelope sender (a.k.a. "UNIX From") which will be alternative to sender of messages without "From" field.  "Resent-From" may also be inserted before "From", because some mailers add it into redirected messages and keep original "From" field intact.  In particular cases, "Return-Path" can not give right sender: several mail gateway products rewrite envelope sender and add original one as non-standard field such as "X-Envelope-From".  If that is the case, you might want to insert it in place of "Return-Path".

Example:

    sender_headers Resent-From,From,Return-Path

### `**misaddressed_commands**`

Reject misaddressed commands

- Format:
- Default:

    `reject`

- Context:

    site (`sympa.conf`)

When a mail command is sent to a list, by default Sympa rejects this message. This feature can be turned off setting this parameter to "ignore".

### `**misaddressed_commands_regexp**`

Regular expression matching with misaddressed commands

- Format:
- Default:

    `((subscribe\s+(\S+)|unsubscribe\s+(\S+)|signoff\s+(\S+)|set\s+(\S+)\s+(mail|nomail|digest))\s*)`

- Context:

    site (`sympa.conf`)

Perl regular expression applied on messages subject and body to detect misaddressed commands.

### `**sympa_priority**`

Priority for command messages

- Format:
    - `0` - 0 - highest priority
    - `1` - 1
    - `2` - 2
    - `3` - 3
    - `4` - 4
    - `5` - 5
    - `6` - 6
    - `7` - 7
    - `8` - 8
    - `9` - 9 - lowest priority
    - `z` - queue messages only
- Default:

    `1`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Priority applied to messages sent to Sympa command address.

### `**request_priority**`

Priority for messages bound for list owners

- Format:
    - `0` - 0 - highest priority
    - `1` - 1
    - `2` - 2
    - `3` - 3
    - `4` - 4
    - `5` - 5
    - `6` - 6
    - `7` - 7
    - `8` - 8
    - `9` - 9 - lowest priority
    - `z` - queue messages only
- Default:

    `0`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Priority for processing of messages bound for "LIST-request" address, i.e. owners of the list

### `**owner_priority**`

Priority for non-VERP bounces

- Format:
    - `0` - 0 - highest priority
    - `1` - 1
    - `2` - 2
    - `3` - 3
    - `4` - 4
    - `5` - 5
    - `6` - 6
    - `7` - 7
    - `8` - 8
    - `9` - 9 - lowest priority
    - `z` - queue messages only
- Default:

    `9`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Priority for processing of messages bound for "LIST-owner" address, i.e. non-delivery reports (bounces).

### `**incoming_max_count**`

Max number of sympa.pl workers

- Format:

    /`\d+`/

- Default:

    `1`

- Context:

    site (`sympa.conf`)

Max number of workers of sympa.pl daemon processing incoming spool.

### `**sleep**`

Interval between scanning incoming message spool

- Format:

    Number of seconds.

- Default:

    `5` (seconds)

- Context:

    site (`sympa.conf`)

Must not be 0.

## Sending/receiving setup

### `**send**`

Who can send messages

- Format:

    Name of `send` scenario:

    - `closed` - closed
    - `confidential` - restricted to subscribers, messages from others are discarded
    - `editordkim` - Moderated, no authentication needed if DKIM signature from moderator is OK
    - `editorkey` - Moderated
    - `editorkeyonly` - Moderated, even for moderators
    - `editorkeyonlyauth` - Moderated, need authentication from moderator
    - `newsletter` - Newsletter, restricted to moderators
    - `newsletterkeyonly` - Newsletter, restricted to moderators after confirmation
    - `owner` - Restricted to list owners only
    - `ownerauth` - Restricted to list owners with previous MD5 authentication
    - `private` - restricted to subscribers
    - `private_smime` - restricted to subscribers and checked smime signature
    - `privateandeditorkey` - Moderated, restricted to subscribers
    - `privateandnomultipartoreditorkey` - Moderated, for non subscribers sending multipart messages
    - `privatekey` - restricted to subscribers with previous md5 authentication
    - `privatekeyandeditorkeyonly` - Moderated, for subscribers and even moderators themself
    - `privateoreditorkey` - Private, moderated for non subscribers
    - `privateorpublickey` - Private, confirmation for non subscribers
    - `public` - public list
    - `public_nobcc` - public list, Bcc rejected (anti-spam)
    - `publickey` - anyone no authentication if DKIM signature is OK
    - `publicnoattachment` - public list multipart/mixed messages are forwarded to moderator
    - `publicnomultipart` - public list multipart messages are rejected

- Default:

    `private`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter specifies who can send messages to the list.

### `**delivery_time**`

Delivery time (hh:mm)

- Format:

    /`[0-2]?\d\:[0-6]\d`/

- Default:

    None.

- Context:

    list (`config`)

If this parameter is present, non-digest messages will be delivered to subscribers at this time: When this time has been past, delivery is postponed to the same time in next day.

### `**digest**`

(Paragraph)
Digest frequency

- Single occurrence

Definition of digest mode. If this parameter is present, subscribers can select the option of receiving messages in multipart/digest MIME format, or as a plain text digest. Messages are then grouped together, and compiled messages are sent to subscribers according to the frequency selected with this parameter.

#### `digest.days`

days

- Format:

    Multiple occurrences allowed.

    Day of week, `0` - `6`.

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `digest.hour`

hour

- Format:

    /`\d+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `digest.minute`

minute

- Format:

    /`\d+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

### `**digest_max_size**`

Digest maximum number of messages

- Format:

    Number of messages.

- Default:

    `25` (messages)

- Context:

    list (`config`)

### `**available_user_options**`

(Paragraph)
Available subscription options

- Single occurrence

#### `available_user_options.reception`

reception mode

- Format:

    Multiple values allowed, separated by `,`.

    Reception mode of list member.

- Default:

    `mail,notice,digest,digestplain,summary,nomail,txt,urlize,not_me`

- Context:

    list (`config`)

Only these modes will be allowed for the subscribers of this list. If a subscriber has a reception mode not in the list, Sympa uses the mode specified in the default\_user\_options paragraph.

### `**default_user_options**`

(Paragraph)
Subscription profile

- Single occurrence

Default profile for the subscribers of the list.

#### `default_user_options.reception`

reception mode

- Format:

    Reception mode of list member.

- Default:

    `mail`

- Context:

    list (`config`)

Mail reception mode.

#### `default_user_options.visibility`

visibility

- Format:

    Visibility mode of list memeber.

- Default:

    `noconceal`

- Context:

    list (`config`)

Visibility of the subscriber.

### `**msg_topic**`

(Paragraph)
Topics for message categorization

- Multiple occurrences allowed

This paragraph defines a topic used to tag a message of a list, named by msg\_topic.name ("other" is a reserved word), its title is msg\_topic.title. The msg\_topic.keywords entry is optional and allows automatic tagging. This should be a list of keywords, separated by ','.

#### `msg_topic.name`

Message topic name

- Format:

    /`[\-\w]+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `msg_topic.keywords`

Message topic keywords

- Format:

    /`[^,\n]+(,[^,\n]+)*`/

- Default:

    None.

- Context:

    list (`config`)

#### `msg_topic.title`

Message topic title

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

### `**msg_topic_keywords_apply_on**`

Defines to which part of messages topic keywords are applied

- Format:
    - `subject` - subject field
    - `body` - message body
    - `subject_and_body` - subject and body
- Default:

    `subject`

- Context:

    list (`config`)

This parameter indicates which part of the message is used to perform automatic tagging.

### `**msg_topic_tagging**`

Message tagging

- Format:
    - `required_sender` - required to post message
    - `required_moderator` - required to distribute message
    - `optional` - optional
- Default:

    `optional`

- Context:

    list (`config`)

This parameter indicates if the tagging is optional or required for a list.

### `**reply_to_header**`

(Paragraph)
Reply address

- Single occurrence

This defines what Sympa will place in the Reply-To: SMTP header field of the messages it distributes.

#### `reply_to_header.value`

value

- Format:
    - `sender` - sender
    - `list` - list
    - `all` - all
    - `other_email` - other email address
- Default:

    `sender`

- Context:

    list (`config`)

This parameter indicates whether the Reply-To: field should indicate the sender of the message (sender), the list itself (list), both list and sender (all) or an arbitrary e-mail address (defined by the other\_email parameter).

Note: it is inadvisable to change this parameter, and particularly inadvisable to set it to list. Experience has shown it to be almost inevitable that users, mistakenly believing that they are replying only to the sender, will send private messages to a list. This can lead, at the very least, to embarrassment, and sometimes to more serious consequences.

#### `reply_to_header.other_email`

other email address

- Format:

    /`$email`/

- Default:

    None.

- Context:

    list (`config`)

If value was set to other\_email, this parameter defines the e-mail address used.

#### `reply_to_header.apply`

respect of existing header field

- Format:
    - `forced` - overwrite Reply-To: header field
    - `respect` - preserve existing header field
- Default:

    `respect`

- Context:

    list (`config`)

The default is to respect (preserve) the existing Reply-To: SMTP header field in incoming messages. If set to forced, Reply-To: SMTP header field will be overwritten.

### `**anonymous_sender**`

Anonymous sender

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

To hide the sender's email address before distributing the message. It is replaced by the provided email address.

### `**anonymous_header_fields**`

Header fields removed when a mailing list is setup in anonymous mode

- Format:
- Default:

    `Authentication-Results,Disposition-Notification-To,DKIM-Signature,Injection-Info,Organisation,Organization,Original-Recipient,Originator,Path,Received,Received-SPF,Reply-To,Resent-Reply-To,Return-Receipt-To,X-Envelope-From,X-Envelope-To,X-Sender,X-X-Sender`

- Context:

    site (`sympa.conf`)

See "anonymous\_sender" list parameter.

Default value prior to Sympa 6.1.19 is:

    Sender,X-Sender,Received,Message-id,From,X-Envelope-To,Resent-From,Reply-To,Organization,Disposition-Notification-To,X-Envelope-From,X-X-Sender

### `**custom_header**`

Custom header field

- Format:

    Multiple occurrences allowed.

    /`\S+:\s+.*`/

- Default:

    None.

- Context:

    list (`config`)

This parameter is optional. The headers specified will be added to the headers of messages distributed via the list. As of release 1.2.2 of Sympa, it is possible to put several custom header lines in the configuration file at the same time.

### `**custom_subject**`

Subject tagging

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

This parameter is optional. It specifies a string which is added to the subject of distributed messages (intended to help users who do not use automatic tools to sort incoming messages). This string will be surrounded by \[\] characters.

### `**footer_type**`

Attachment type

- Format:
    - `mime` - add a new MIME part
    - `append` - append to message body
- Default:

    `mime`

- Context:

    list (`config`)

List owners may decide to add message headers or footers to messages sent via the list. This parameter defines the way a footer/header is added to a message.

mime: 

The default value. Sympa will add the footer/header as a new MIME part.

append: 

Sympa will not create new MIME parts, but will try to append the header/footer to the body of the message. Predefined message-footers will be ignored. Headers/footers may be appended to text/plain messages only.

### `**max_size**`

Maximum message size

- Format:

    Number of bytes.

- Default:

    `5242880` (bytes)

- Context:

    list (`config`), domain (`robot.conf`), host

Maximum size of a message in 8-bit bytes.

Example:

    max_size 2097152

### `**merge_feature**`

Allow message personalization

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`), site (`sympa.conf`)

### `**message_hook**`

(Paragraph)
Hook modules for message processing

- Single occurrence

#### `message_hook.pre_distribute`

A hook on the messages before distribution

- Format:

    /`(::|\w)+`/

- Default:

    None.

- Context:

    list (`config`)

#### `message_hook.post_archive`

A hook on the messages just after archiving

- Format:

    /`(::|\w)+`/

- Default:

    None.

- Context:

    list (`config`)

### `**reject_mail_from_automates_feature**`

Reject mail from automatic processes (crontab, etc)?

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `on`

- Context:

    list (`config`), site (`sympa.conf`)

Rejects messages that seem to be from automated services, based on a few header fields ("Content-Identifier:", "Auto-Submitted:").

Sympa also can be configured to reject messages based on the "From:" header field value (see "loop\_prevention\_regex").

### `**remove_headers**`

Header fields to be removed from incoming messages

- Format:

    Multiple values allowed, separated by `,`.

    /`\S+`/

- Default:

    `X-Sympa-To,X-Family-To,Return-Receipt-To,Precedence,X-Sequence,Disposition-Notification-To,Sender`

- Context:

    list (`config`), site (`sympa.conf`)

Use it, for example, to ensure some privacy for your users in case that "anonymous\_sender" mode is inappropriate.

The removal of these header fields is applied before Sympa adds its own header fields ("rfc2369\_header\_fields" and "custom\_header").

Example:

    remove_headers Resent-Date,Resent-From,Resent-To,Resent-Message-Id,Sender,Delivered-To

### `**remove_outgoing_headers**`

Header fields to be removed before message distribution

- Format:

    Multiple values allowed, separated by `,`.

    /`\S+`/

- Default:

    `none`

- Context:

    list (`config`), site (`sympa.conf`)

The removal happens after Sympa's own header fields are added; therefore, it is a convenient way to remove Sympa's own header fields (like "X-Loop:" or "X-no-archive:") if you wish.

Example:

    remove_outgoing_headers X-no-archive

### `**rfc2369_header_fields**`

RFC 2369 header fields

- Format:

    Multiple values allowed, separated by `,`.

    - `help` - help
    - `subscribe` - subscription
    - `unsubscribe` - unsubscription
    - `post` - posting address
    - `owner` - owner
    - `archive` - list archive

- Default:

    `help,subscribe,unsubscribe,post,owner,archive`

- Context:

    list (`config`), site (`sympa.conf`)

Specify which RFC 2369 mailing list header fields to be added.

"List-Id:" header field defined in RFC 2919 is always added. Sympa also adds "Archived-At:" header field defined in RFC 5064.

## Distribution

### `**urlize_min_size**`

Minimum size to be urlized

- Format:

    Number of bytes.

- Default:

    `10240` (bytes)

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

When a subscriber chose "urlize" reception mode, attachments not smaller than this size will be urlized.

### `**allowed_external_origin**`

Allowed external links in sanitized HTML

- Format:

    /`[-\w*]+(?:[.][-\w*]+)+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

When the HTML content of a message must be sanitized, links ("href" or "src" attributes) with the hosts listed in this parameter will not be scrubbed. If "\*" character is included, it matches any subdomains. Single "\*" allows any hosts.

Example:

    allowed_external_origin *.example.org,www.example.com

### `**sympa_packet_priority**`

Default priority for a packet

- Format:
    - `0` - 0 - highest priority
    - `1` - 1
    - `2` - 2
    - `3` - 3
    - `4` - 4
    - `5` - 5
    - `6` - 6
    - `7` - 7
    - `8` - 8
    - `9` - 9 - lowest priority
    - `z` - queue messages only
- Default:

    `5`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

The default priority set to a packet to be sent by the bulk.

### `**bulk_fork_threshold**`

Fork threshold of bulk daemon

- Format:

    /`\d+`/

- Default:

    `1`

- Context:

    site (`sympa.conf`)

The minimum number of packets before bulk daemon forks a new worker to increase sending rate.

### `**bulk_max_count**`

Maximum number of bulk workers

- Format:

    /`\d+`/

- Default:

    `3`

- Context:

    site (`sympa.conf`)

### `**bulk_lazytime**`

Idle timeout of bulk workers

- Format:

    Number of seconds.

- Default:

    `600` (seconds)

- Context:

    site (`sympa.conf`)

The number of seconds a bulk worker will remain running without processing a message before it spontaneously exits.

### `**bulk_sleep**`

Sleep time of bulk workers

- Format:

    Number of seconds.

- Default:

    `1` (seconds)

- Context:

    site (`sympa.conf`)

The number of seconds a bulk worker sleeps between starting a new loop if it didn't find a message to send.

Keep it small if you want your server to be reactive.

### `**bulk_wait_to_fork**`

Interval between checks of packet numbers

- Format:

    Number of seconds.

- Default:

    `10` (seconds)

- Context:

    site (`sympa.conf`)

Number of seconds a master bulk daemon waits between two packets number checks.

Keep it small if you expect brutal increases in the message sending load.

### `**log_smtp**`

Log invocation of sendmail

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

This can be overwritten by "-m" option for sympa.pl.

### `**maxsmtp**`

Maximum number of sendmail processes

- Format:

    /`\d+`/

- Default:

    `40`

- Context:

    site (`sympa.conf`)

Maximum number of simultaneous child processes spawned by Sympa. This is the main load control parameter. 

Proposed value is quite low, but you can rise it up to 100, 200 or even 300 with powerful systems.

Example:

    maxsmtp 500

### `**nrcpt**`

Maximum number of recipients per call to sendmail

- Format:

    /`\d+`/

- Default:

    `25`

- Context:

    site (`sympa.conf`)

This grouping factor makes it possible for the sendmail processes to optimize the number of SMTP sessions for message distribution. If needed, you can limit the number of recipients for a particular domain. Check the "nrcpt\_by\_domain.conf" configuration file.

### `**avg**`

Maximum number of different mail domains per call to sendmail

- Format:

    /`\d+`/

- Default:

    `10`

- Context:

    site (`sympa.conf`)

## Privileges

### `**create_list**`

Who is able to create lists

- Format:

    Name of `create_list` scenario:

    - `listmaster` - restricted to listmaster
    - `public_listmaster` - anybody by validation by listmaster required

- Default:

    `public_listmaster`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Defines who can create lists (or request list creation) by creating new lists or by renaming or copying existing lists.

Example:

    create_list intranet

### `**allow_subscribe_if_pending**`

Allow adding subscribers to a list not open

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `on`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If set to "off", adding subscribers to, or removing subscribers from a list with status other than "open" is forbidden.

### `**global_remind**`

Who is able to send remind messages over all lists

- Format:

    Name of `global_remind` scenario:

    - `listmaster` - only for listmaster

- Default:

    `listmaster`

- Context:

    site (`sympa.conf`)

### `**move_user**`

Who is able to change user's email

- Format:

    Name of `move_user` scenario:

    - `auth` - need authentication
    - `closed` - impossible
    - `listmaster` - listmaster only

- Default:

    `auth`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**use_blacklist**`

Use blacklist

- Format:

    /`[-.\w]+`/

- Default:

    `send,create_list`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

List of operations separated by comma for which blacklist filter is applied.  Setting this parameter to "none" will hide the blacklist feature.

### `**info**`

Who can view list information

- Format:

    Name of `info` scenario:

    - `conceal` - restricted to subscribers - Silent rejection otherwise.
    - `open` - for anyone
    - `private` - restricted to subscribers

- Default:

    `open`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

### `**subscribe**`

Who can subscribe to the list

- Format:

    Name of `subscribe` scenario:

    - `auth` - subscription request confirmed
    - `auth_notify` - need authentication (notification is sent to owners)
    - `auth_notifydkim` - need authentication unless DKIM signature is OK (notification is sent to owners)
    - `auth_owner` - requires authentication then owner approval
    - `auth_ownerdkim` - requires authentication unless DKIM signature is OK, then owner approval
    - `authdkim` - subscription request confirmed
    - `closed` - subscription is impossible
    - `open` - for anyone without authentication
    - `open_notify` - anyone, notification is sent to list owner
    - `open_quiet` - anyone, no welcome message
    - `owner` - owners approval
    - `smime` - requires S/MIME signed
    - `smimeorowner` - requires S/MIME signed or owner approval

- Default:

    `open`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The subscribe parameter defines the rules for subscribing to the list.

### `**add**`

Who can add subscribers

- Format:

    Name of `add` scenario:

    - `auth` - restricted to owner with authentication
    - `authdkim` - restricted to owner without authentication if DKIM signature is OK.
    - `closed` - add impossible
    - `owner` - add performed by list owner does not need authentication
    - `owner_notify` - add performed by owner does not need authentication (notification)
    - `ownerdkim` - add performed by list owner does not need authentication if DKIM signature OK

- Default:

    `owner`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Privilege for adding (ADD command) a subscriber to the list

### `**unsubscribe**`

Who can unsubscribe

- Format:

    Name of `unsubscribe` scenario:

    - `auth` - need authentication
    - `auth_notify` - authentication requested, notification sent to owner
    - `auth_notifydkim` - authentication requested unless DKIM signature is OK, notification sent to owner
    - `authdkim` - need authentication unless DKIM signature is OK
    - `closed` - impossible
    - `open` - open
    - `open_notify` - open with mail confirmation, owner is notified
    - `owner` - owners approval

- Default:

    `open`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter specifies the unsubscription method for the list. Use open\_notify or auth\_notify to allow owner notification of each unsubscribe command.

### `**del**`

Who can delete subscribers

- Format:

    Name of `del` scenario:

    - `auth` - deletion performed only by list owners, need authentication
    - `authdkim` - deletion performed only by list owners, need authentication unless DKIM signature is OK
    - `closed` - remove subscriber impossible
    - `owner` - by owner without authentication
    - `owner_notify` - list owners, authentication not needed (notification)
    - `ownerdkim` - by owner without authentication if DKIM signature OK

- Default:

    `owner`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

### `**invite**`

Who can invite people

- Format:

    Name of `invite` scenario:

    - `closed` - closed
    - `owner` - invite perform by list owner do not need authentication
    - `private` - restricted to subscribers
    - `public` - public

- Default:

    `private`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

### `**remind**`

Who can start a remind process

- Format:

    Name of `remind` scenario:

    - `listmaster` - listmaster only
    - `listmasterdkim` - listmaster only (do not require authentication if DKIM siganture is OK) 
    - `owner` - restricted to list owners
    - `ownerdkim` - restricted to list owners (authentication is not required if a DKIM signature is OK)

- Default:

    `owner`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter specifies who is authorized to use the remind command.

### `**review**`

Who can review subscribers

- Format:

    Name of `review` scenario:

    - `closed` - no one can review
    - `listmaster` - listmaster only
    - `owner` - only owner (and listmaster)
    - `private` - restricted to subscribers
    - `public` - anyone can do it!

- Default:

    `owner`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter specifies who can access the list of members. Since subscriber addresses can be abused by spammers, it is strongly recommended that you only authorize owners or subscribers to access the subscriber list. 

### `**owner_domain**`

Required domains for list owners

- Format:

    /`$host( +$host)*`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Restrict list ownership to addresses in the specified domains. This can be used to reserve list ownership to a group of trusted users from a set of domains associated with an organization, while allowing moderators and subscribers from the Internet at large.

### `**owner_domain_min**`

Minimum owners in required domains

- Format:

    /`\d+`/

- Default:

    `0`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Minimum number of owners for each list must satisfy the owner\_domain restriction. The default of zero (0) means \*all\* list owners must match. Setting to 1 requires only one list owner to match owner\_domain; all other owners can be from any domain. This setting can be used to ensure that there is always at least one known contact point for any mailing list.

### `**shared_doc**`

(Paragraph)
Shared documents

- Single occurrence

This paragraph defines read and edit access to the shared document repository.

#### `shared_doc.d_read`

Who can view

- Format:

    Name of `d_read` scenario:

    - `owner` - restricted to list owners
    - `private` - restricted to subscribers
    - `private-https` - restricted to subscribers authenticated with user cert
    - `public` - public documents

- Default:

    `private`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

#### `shared_doc.d_edit`

Who can edit

- Format:

    Name of `d_edit` scenario:

    - `editor` - moderated for subscribers
    - `owner` - restricted to list owners
    - `private` - restricted to subscribers
    - `private-https` - restricted to subscribers authenticated with user cert
    - `public` - public documents

- Default:

    `owner`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

#### `shared_doc.quota`

quota

- Format:

    Number of Kbytes.

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

## Archives

### `**ignore_x_no_archive_header_feature**`

Ignore "X-no-archive:" header field

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    site (`sympa.conf`)

Sympa's default behavior is to skip archiving of incoming messages that have an "X-no-archive:" header field set. This parameter allows one to change this behavior.

Example:

    ignore_x_no_archive_header_feature on

### `**custom_archiver**`

Custom archiver

- Format:

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

Activates a custom archiver to use instead of MHonArc. The value of this parameter is the absolute path to the executable file.

Sympa invokes this file with these two arguments:

\--list

The address of the list including domain part.

\--file

Absolute path to the message to be archived.

### `**process_archive**`

Store distributed messages into archive

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

If enabled, distributed messages via lists will be archived. Otherwise archiving is disabled.

Note that even if setting this parameter disabled, past archives will not be removed and will be accessible according to access settings by each list.

### `**archive**`

(Paragraph)
Archives

- Single occurrence

Privilege for reading mail archives and frequency of archiving.

Defines who can access the list's web archive.

#### `archive.period`

Deprecated.

#### `archive.access`

Deprecated.

#### `archive.web_access`

access right

- Format:

    Name of `archive_web_access` scenario:

    - `closed` - closed
    - `listmaster` - listmaster
    - `owner` - by owner
    - `private` - subscribers only
    - `public` - public

- Default:

    `closed`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

#### `archive.mail_access`

access right by mail commands

- Format:

    Name of `archive_mail_access` scenario:

    - `closed` - closed
    - `owner` - by owner
    - `private` - subscribers only
    - `public` - public

- Default:

    `closed`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

#### `archive.quota`

quota

- Format:

    Number of Kbytes.

- Default:

    None.

- Context:

    list (`config`), site (`sympa.conf`)

#### `archive.max_month`

Maximum number of month archived

- Format:

    Number of months.

- Default:

    None.

- Context:

    list (`config`)

### `**archive_crypted_msg**`

Archive encrypted mails as cleartext

- Format:
    - `original` - original messages
    - `decrypted` - decrypted messages
- Default:

    `original`

- Context:

    list (`config`)

### `**web_archive_spam_protection**`

Protect web archive against spam harvesters

- Format:
    - `cookie` - use HTTP cookie
    - `javascript` - use JavaScript
    - `at` - replace @ characters
    - `gecos` - only show gecos
    - `none` - do nothing
- Default:

    `cookie`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Idem spam\_protection is provided but it can be used only for web archives. Access requires a cookie, and users must submit a small form in order to receive a cookie before browsing the archives. This blocks all robot, even google and co.

## Bounces

### `**bounce**`

(Paragraph)
Bounces management

- Single occurrence

#### `bounce.warn_rate`

warn rate

- Format:

    Number of %.

- Default:

    `30` (%)

- Context:

    list (`config`), site (`sympa.conf`)

The list owner receives a warning whenever a message is distributed and the number (percentage) of bounces exceeds this value.

#### `bounce.halt_rate`

Deprecated.

### `**bouncers_level1**`

(Paragraph)
Management of bouncers, 1st level

- Single occurrence

Level 1 is the lower level of bouncing users

#### `bouncers_level1.rate`

threshold

- Format:

    Number of points.

- Default:

    `45` (points)

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Each bouncing user have a score (from 0 to 100).

This parameter defines a lower limit for each category of bouncing users.For example, level 1 begins from 45 to level\_2\_treshold.

#### `bouncers_level1.action`

action for this population

- Format:
    - `remove_bouncers` - remove bouncing users
    - `notify_bouncers` - send notify to bouncing users
    - `none` - do nothing
- Default:

    `notify_bouncers`

- Context:

    list (`config`)

This parameter defines which task is automatically applied on level 1 bouncers.

#### `bouncers_level1.notification`

notification

- Format:
    - `none` - do nothing
    - `owner` - owner
    - `listmaster` - listmaster
- Default:

    `owner`

- Context:

    list (`config`)

When automatic task is executed on level 1 bouncers, a notification email can be send to listowner or listmaster.

### `**bouncers_level2**`

(Paragraph)
Management of bouncers, 2nd level

- Single occurrence

Level 2 is the highest level of bouncing users

#### `bouncers_level2.rate`

threshold

- Format:

    Number of points.

- Default:

    `75` (points)

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Each bouncing user have a score (from 0 to 100).

This parameter defines the score range defining each category of bouncing users.For example, level 2 is for users with a score between 80 and 100.

#### `bouncers_level2.action`

action for this population

- Format:
    - `remove_bouncers` - remove bouncing users
    - `notify_bouncers` - send notify to bouncing users
    - `none` - do nothing
- Default:

    `remove_bouncers`

- Context:

    list (`config`)

This parameter defines which task is automatically applied on level 2 bouncers.

#### `bouncers_level2.notification`

notification

- Format:
    - `none` - do nothing
    - `owner` - owner
    - `listmaster` - listmaster
- Default:

    `owner`

- Context:

    list (`config`)

When automatic task is executed on level 2 bouncers, a notification email can be send to listowner or listmaster.

### `**verp_rate**`

percentage of list members in VERP mode

- Format:
    - `100%` - 100% - always
    - `50%` - 50%
    - `33%` - 33%
    - `25%` - 25%
    - `20%` - 20%
    - `10%` - 10%
    - `5%` - 5%
    - `2%` - 2%
    - `0%` - 0% - never
- Default:

    `0%`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Uses variable envelope return path (VERP) to detect bouncing subscriber addresses.

0%: VERP is never used.

100%: VERP is always in use.

VERP requires address with extension to be supported by MTA. If tracking is enabled for a list or a message, VERP is applied for 100% of subscribers.

### `**tracking**`

(Paragraph)
Message tracking feature

- Single occurrence

#### `tracking.delivery_status_notification`

tracking message by delivery status notification

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`), site (`sympa.conf`)

#### `tracking.message_disposition_notification`

tracking message by message disposition notification

- Format:
    - `on` - enabled
    - `on_demand` - on demand
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`), site (`sympa.conf`)

#### `tracking.tracking`

who can view message tracking

- Format:

    Name of `tracking` scenario:

    - `owner` - only owner (and listmaster)
    - `private` - restricted to subscribers

- Default:

    `owner`

- Context:

    list (`config`), site (`sympa.conf`)

#### `tracking.retention_period`

Tracking datas are removed after this number of days

- Format:

    Number of days.

- Default:

    `90` (days)

- Context:

    list (`config`), site (`sympa.conf`)

### `**welcome_return_path**`

Welcome return-path

- Format:
    - `unique` - bounce management
    - `owner` - owner
- Default:

    `owner`

- Context:

    list (`config`), site (`sympa.conf`)

If set to unique, the welcome message is sent using a unique return path in order to remove the subscriber immediately in the case of a bounce.

### `**remind_return_path**`

Return-path of the REMIND command

- Format:
    - `unique` - bounce management
    - `owner` - owner
- Default:

    `owner`

- Context:

    list (`config`), site (`sympa.conf`)

Same as welcome\_return\_path, but applied to remind messages.

### `**expire_bounce_task**`

Task for expiration of old bounces

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

This task resets bouncing information for addresses not bouncing in the last 10 days after the latest message distribution.

### `**purge_orphan_bounces_task**`

Task for cleaning invalidated bounces

- Format:

    /`\w+`/

- Default:

    `monthly`

- Context:

    site (`sympa.conf`)

This task deletes bounce information for unsubscribed users.

### `**eval_bouncers_task**`

Task for updating bounce scores

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

This task scans all bouncing users for all lists, and updates "bounce\_score\_subscriber" field in "subscriber\_table" table. The scores may be used for management of bouncers.

### `**process_bouncers_task**`

Task for management of bouncers

- Format:

    /`\w+`/

- Default:

    `weekly`

- Context:

    site (`sympa.conf`)

This task executes actions on bouncing users configured by each list, according to their scores.

### `**purge_tables_task**`

Task for cleaning tables

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

This task cleans old tracking information from "notification\_table" table.

### `**minimum_bouncing_count**`

Minimum number of bounces

- Format:

    /`\d+`/

- Default:

    `10`

- Context:

    site (`sympa.conf`)

The minimum number of bounces received to update bounce score of a user.

### `**minimum_bouncing_period**`

Minimum bouncing period

- Format:

    Number of days.

- Default:

    `10` (days)

- Context:

    site (`sympa.conf`)

The minimum period for which bouncing lasted to update bounce score of a user.

### `**bounce_delay**`

Delay of bounces

- Format:

    Number of days.

- Default:

    `0` (days)

- Context:

    site (`sympa.conf`)

Average time for a bounce sent back to mailing list server after a post was sent to a list. Usually bounces are sent back on the same day as the original message.

### `**bounce_email_prefix**`

Prefix of VERP return address

- Format:

    /`\S+`/

- Default:

    `bounce`

- Context:

    site (`sympa.conf`)

The prefix to consist the return-path of probe messages used for bounce management, when variable envelope return path (VERP) is enabled. VERP requires address with extension to be supported by MTA.

If you change the default value, you must modify the mail aliases too.

### `**return_path_suffix**`

Suffix of list return address

- Format:

    /`\S+`/

- Default:

    `-owner`

- Context:

    site (`sympa.conf`)

The suffix appended to the list name to form the return-path of messages distributed through the list. This address will receive all non-delivery reports (also called bounces).

## Loop prevention

### `**loop_command_max**`

Maximum number of responses to command message

- Format:

    /`\d+`/

- Default:

    `200`

- Context:

    site (`sympa.conf`)

The maximum number of command reports sent to an email address. Messages are stored in "bad" subdirectory of incoming message spool, and reports are not longer sent.

### `**loop_command_sampling_delay**`

Delay before counting responses to command message

- Format:

    Number of seconds.

- Default:

    `3600` (seconds)

- Context:

    site (`sympa.conf`)

This parameter defines the delay in seconds before decrementing the counter of reports sent to an email address.

### `**loop_command_decrease_factor**`

Decrementing factor of responses to command message

- Format:

    /`[.\d]+`/

- Default:

    `0.5`

- Context:

    site (`sympa.conf`)

The decrementation factor (from 0 to 1), used to determine the new report counter after expiration of the delay.

### `**msgid_table_cleanup_ttl**`

Expiration period of message ID table

- Format:

    Number of seconds.

- Default:

    `86400` (seconds)

- Context:

    site (`sympa.conf`)

Expiration period of entries in the table maintained by sympa\_msg.pl daemon to prevent delivery of duplicate messages caused by loop.

### `**msgid_table_cleanup_frequency**`

Cleanup interval of message ID table

- Format:

    Number of seconds.

- Default:

    `3600` (seconds)

- Context:

    site (`sympa.conf`)

Interval between cleanups of the table maintained by sympa\_msg.pl daemon to prevent delivery of duplicate messages caused by loop.

## Automatic lists

### `**automatic_list_feature**`

Automatic list

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**automatic_list_removal**`

Remove empty automatic list

- Format:
    - `none` - do nothing
    - `if_empty` - if\_empty
- Default:

    `none`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If set to "if\_empty", then Sympa will remove automatically created mailing lists just after their creation, if they contain no list member.

Example:

    automatic_list_removal if_empty

### `**automatic_list_creation**`

Who is able to create automatic list

- Format:

    Name of `automatic_list_creation` scenario:

    - `family_owner` - Restricted to people subscribed to the list of family owners.
    - `listmaster` - restricted to listmaster
    - `public` - anybody. Be sure you know what you are doing

- Default:

    `public`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**automatic_list_families**`

Definition of automatic list families

- Format:

    /`.+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Defines the families the automatic lists are based on. It is a character string structured as follows:

\* each family is separated from the other by a semicolon (;)

\* inside a family definition, each field is separated from the other by a colon (:)

\* each field has the structure: "&lt;field name>=&lt;field value>"

Basically, each time Sympa uses the automatic lists families, the values defined in this parameter will be available in the family object.

\* for scenarios: \[family->name\]

\* for templates: \[% family.name %\]

Example:

    automatic_list_families name=family_one:prefix=f1:display=My automatic lists:prefix_separator=+:classes separator=-:family_owners_list=alist@domain.tld;name=family_two:prefix=f2:display=My other automatic lists:prefix_separator=+:classes separator=-:family_owners_list=anotherlist@domain.tld;

### `**parsed_family_files**`

Parsed files for families

- Format:

    /`[-.\w]+`/

- Default:

    `message_header,message_header.mime,message_footer,message_footer.mime,info`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

comma-separated list of files that will be parsed by Sympa when instantiating a family (no space allowed in file names)

### `**family_signoff**`

Global unsubscription

- Format:

    Name of `family_signoff` scenario:

    - `auth` - need authentication
    - `closed` - impossible

- Default:

    `auth`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

## Tag based spam filtering

### `**antispam_feature**`

Tag based spam filtering

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**antispam_tag_header_name**`

Header field to tag spams

- Format:

    /`\S+`/

- Default:

    `X-Spam-Status`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If a spam filter (like spamassassin or j-chkmail) add a header field to tag spams, name of this header field (example X-Spam-Status)

### `**antispam_tag_header_spam_regexp**`

Regular expression to check header field to tag spams

- Format:

    /`.+`/

- Default:

    `^\s*Yes`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Regular expression applied on this header to verify message is a spam (example Yes)

### `**antispam_tag_header_ham_regexp**`

Regular expression to determine spam or ham.

- Format:

    /`.+`/

- Default:

    `^\s*No`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Regular expression applied on this header field to verify message is NOT a spam (example No)

### `**spam_status**`

Name of header field to inform

- Format:

    Name of `spam_status` scenario:

    - `x-spam-status` - test x-spam-status  header

- Default:

    `x-spam-status`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Messages are supposed to be filtered by an spam filter that adds them one or more headers. This parameter is used to select a special scenario in order to decide the message's spam status: ham, spam or unsure. This parameter replaces antispam\_tag\_header\_name, antispam\_tag\_header\_spam\_regexp and antispam\_tag\_header\_ham\_regexp.

## Directories

### `**home**`

List home

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/lib/sympa/list_data`

- Context:

    site (`sympa.conf`)

Base directory of list configurations.

### `**etc**`

Directory for configuration files

- Format:

    /`.+`/

- Default:

    `/home/sympa/etc`

- Context:

    site (`sympa.conf`)

Base directory of global configuration (except "sympa.conf").

### `**spool**`

Base directory of spools

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa`

- Context:

    site (`sympa.conf`)

Base directory of all spools which are created at runtime. This directory must be writable by Sympa user.

### `**queue**`

Directory for message incoming spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/msg`

- Context:

    site (`sympa.conf`)

This spool is used both by "queue" program and "sympa\_msg.pl" daemon.

### `**queuemod**`

Directory for moderation spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/moderation`

- Context:

    site (`sympa.conf`)

### `**queuedigest**`

Directory for digest spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/digest`

- Context:

    site (`sympa.conf`)

### `**queueauth**`

Directory for held message spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/auth`

- Context:

    site (`sympa.conf`)

This parameter is named such by historical reason.

### `**queueoutgoing**`

Directory for archive spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/outgoing`

- Context:

    site (`sympa.conf`)

This parameter is named such by historical reason.

### `**queuesubscribe**`

Directory for held request spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/subscribe`

- Context:

    site (`sympa.conf`)

This parameter is named such by historical reason.

### `**queuetopic**`

Directory for topic spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/topic`

- Context:

    site (`sympa.conf`)

### `**queuebounce**`

Directory for bounce incoming spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/bounce`

- Context:

    site (`sympa.conf`)

This spool is used both by "bouncequeue" program and "bounced.pl" daemon.

### `**queuetask**`

Directory for task spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/task`

- Context:

    site (`sympa.conf`)

### `**queueautomatic**`

Directory for automatic list creation spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/automatic`

- Context:

    site (`sympa.conf`)

This spool is used both by "familyqueue" program and "sympa\_automatic.pl" daemon.

### `**queuebulk**`

Directory for message outgoing spool

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/bulk`

- Context:

    site (`sympa.conf`)

This parameter is named such by historical reason.

### `**tmpdir**`

Temporary directory used by external programs such as virus scanner. Also, outputs to daemons' standard error are redirected to the files under this directory.

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/tmp`

- Context:

    site (`sympa.conf`)

### `**viewmail_dir**`

Directory to cache formatted messages

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/spool/sympa/viewmail`

- Context:

    site (`sympa.conf`)

Base directory path of directories where HTML view of messages are cached.

### `**bounce_path**`

Directory for storing bounces

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/lib/sympa/bounce`

- Context:

    site (`sympa.conf`)

The directory where bounced.pl daemon will store the last bouncing message for each user. A message is stored in the file: &lt;bounce\_path>/&lt;list name>@&lt;mail domain name>/&lt;email address>, or, if tracking is enabled: &lt;bounce\_path>/&lt;list name>@&lt;mail domain name>/&lt;email address>\_&lt;envelope ID>.

Users can access to these messages using web interface in the bounce management page.

Don't confuse with "queuebounce" parameter which defines the spool where incoming error reports are stored and picked by bounced.pl daemon.

### `**arc_path**`

Directory for storing archives

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/lib/sympa/arc`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Where to store HTML archives. This parameter is used by the "archived.pl" daemon. It is a good idea to install the archive outside the web document hierarchy to prevent overcoming of WWSympa's access control.

### `**purge_spools_task**`

Task for cleaning spools

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

This task cleans old content in spools.

### `**clean_delay_queue**`

Max age of incoming bad messages

- Format:

    Number of days.

- Default:

    `7` (days)

- Context:

    site (`sympa.conf`)

Number of days "bad" messages are kept in message incoming spool (as specified by "queue" parameter). Sympa keeps messages rejected for various reasons (badly formatted, looping etc.).

### `**clean_delay_queueoutgoing**`

Max age of bad messages for archives

- Format:

    Number of days.

- Default:

    `7` (days)

- Context:

    site (`sympa.conf`)

Number of days "bad" messages are kept in message archive spool (as specified by "queueoutgoing" parameter). Sympa keeps messages rejected for various reasons (unable to create archive directory, to copy file etc.).

### `**clean_delay_queuebounce**`

Max age of bad bounce messages

- Format:

    Number of days.

- Default:

    `7` (days)

- Context:

    site (`sympa.conf`)

Number of days "bad" messages are kept in bounce spool (as specified by "queuebounce" parameter). Sympa keeps messages rejected for various reasons (unknown original sender, unknown report type).

### `**clean_delay_queueauth**`

Max age of held messages

- Format:

    Number of days.

- Default:

    `30` (days)

- Context:

    site (`sympa.conf`)

Number of days messages are kept in held message spool (as specified by "queueauth" parameter). Beyond this deadline, messages that have not been confirmed are deleted.

### `**clean_delay_queuesubscribe**`

Max age of held requests

- Format:

    Number of days.

- Default:

    `30` (days)

- Context:

    site (`sympa.conf`)

Number of days requests are kept in held request spool (as specified by "queuesubscribe" parameter). Beyond this deadline, requests that have not been validated nor declined are deleted.

### `**clean_delay_queuetopic**`

Max age of tagged topics

- Format:

    Number of days.

- Default:

    `30` (days)

- Context:

    site (`sympa.conf`)

Number of days (automatically or manually) tagged topics are kept in topic spool (as specified by "queuetopic" parameter). Beyond this deadline, tagging is forgotten.

### `**clean_delay_queueautomatic**`

Max age of incoming bad messages in automatic list creation spool

- Format:

    Number of days.

- Default:

    `10` (days)

- Context:

    site (`sympa.conf`)

Number of days "bad" messages are kept in automatic list creation spool (as specified by "queueautomatic" parameter). Sympa keeps messages rejected for various reasons (badly formatted, looping etc.).

### `**clean_delay_queuebulk**`

Max age of outgoing bad messages

- Format:

    Number of days.

- Default:

    `7` (days)

- Context:

    site (`sympa.conf`)

Number of days "bad" messages are kept in message outgoing spool (as specified by "queuebulk" parameter). Sympa keeps messages rejected for various reasons (failed personalization, bad configuration on MTA etc.).

### `**clean_delay_queuedigest**`

Max age of bad messages in digest spool

- Format:

    Number of days.

- Default:

    `14` (days)

- Context:

    site (`sympa.conf`)

Number of days "bad" messages are kept in digest spool (as specified by "queuedigest" parameter). Sympa keeps messages rejected for various reasons (syntax errors in "digest.tt2" template etc.).

### `**clean_delay_tmpdir**`

Max age of temporary files

- Format:

    Number of days.

- Default:

    `7` (days)

- Context:

    site (`sympa.conf`)

Number of days files in temporary directory (as specified by "tmpdir" parameter), including standard error logs, are kept.

## S/MIME and TLS

S/MIME authentication, decryption and re-encryption. It requires these external modules: Crypt-OpenSSL-X509 and Crypt-SMIME.

TLS client authentication. It requires an external module: IO-Socket-SSL.

### `**cafile**`

File containing trusted CA certificates

- Format:

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

This can be used alternatively and/or additionally to "capath".

### `**capath**`

Directory containing trusted CA certificates

- Format:

    /`.+`/

- Default:

    None.

- Context:

    site (`sympa.conf`)

CA certificates in this directory are used for client authentication.

The certificates need to have names including hash of subject, or symbolic links to them with such names. The links may be created by using "c\_rehash" script bundled in OpenSSL.

### `**key_passwd**`

Password used to crypt lists private keys

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    site (`sympa.conf`)

If not defined, Sympa assumes that list private keys are not encrypted.

Example:

    key_passwd your_password

### `**ssl_cert_dir**`

Directory containing user certificates

- Format:

    /`.+`/

- Default:

    `/home/sympa/var/lib/sympa/list_data/X509-user-certs`

- Context:

    site (`sympa.conf`)

## Data sources setup

Including subscribers, owners and moderators from data sources. Appropriate database driver (DBD) modules are required: DBD-CSV, DBD-mysql, DBD-ODBC, DBD-Oracle, DBD-Pg, DBD-SQLite and/or Net-LDAP. And also, if secure connection (LDAPS) to LDAP server is required: IO-Socket-SSL.

### `**inclusion_notification_feature**`

Notify subscribers when they are included from a data source?

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`)

### `**member_include**`

(Paragraph)
Subscribers defined in an external data source

- Multiple occurrences allowed

#### `member_include.source`

the data source

- Format:

    /`[\w-]+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `member_include.source_parameters`

data source parameters

- Format:

    /`.*`/

- Default:

    None.

- Context:

    list (`config`)

### `**owner_include**`

(Paragraph)
Owners defined in an external data source

- Multiple occurrences allowed

#### `owner_include.source`

the data source

- Format:

    /`[\w-]+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `owner_include.source_parameters`

data source parameters

- Format:

    /`.*`/

- Default:

    None.

- Context:

    list (`config`)

#### `owner_include.profile`

profile

- Format:
    - `privileged` - privileged owner
    - `normal` - normal owner
- Default:

    `normal`

- Context:

    list (`config`)

#### `owner_include.reception`

reception mode

- Format:
    - `mail` - receive notification email
    - `nomail` - no notifications
- Default:

    `mail`

- Context:

    list (`config`)

#### `owner_include.visibility`

visibility

- Format:
    - `conceal` - concealed from list menu
    - `noconceal` - listed on the list menu
- Default:

    `noconceal`

- Context:

    list (`config`)

### `**editor_include**`

(Paragraph)
Moderators defined in an external data source

- Multiple occurrences allowed

#### `editor_include.source`

the data source

- Format:

    /`[\w-]+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `editor_include.source_parameters`

data source parameters

- Format:

    /`.*`/

- Default:

    None.

- Context:

    list (`config`)

#### `editor_include.reception`

reception mode

- Format:
    - `mail` - receive notification email
    - `nomail` - no notifications
- Default:

    `mail`

- Context:

    list (`config`)

#### `editor_include.visibility`

visibility

- Format:
    - `conceal` - concealed from list menu
    - `noconceal` - listed on the list menu
- Default:

    `noconceal`

- Context:

    list (`config`)

### `**sql_fetch_timeout**`

Timeout for fetch of include\_sql\_query

- Format:

    Number of seconds.

- Default:

    `300` (seconds)

- Context:

    list (`config`), site (`sympa.conf`)

### `**include_file**`

File inclusion

- Format:

    Multiple occurrences allowed.

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`)

Include subscribers from this file.  The file should contain one e-mail address per line (lines beginning with a "#" are ignored).

### `**include_remote_file**`

(Paragraph)
Remote file inclusion

- Multiple occurrences allowed

#### `include_remote_file.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_file.url`

data location URL

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_remote_file.user`

remote user

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_file.passwd`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_file.timeout`

idle timeout

- Format:

    Number of seconds.

- Default:

    `180` (seconds)

- Context:

    list (`config`)

#### `include_remote_file.ssl_version`

SSL version

- Format:
    - `ssl_any` - any versions
    - `sslv2` - SSL version 2
    - `sslv3` - SSL version 3
    - `tlsv1` - TLS version 1
    - `tlsv1_1` - TLS version 1.1
    - `tlsv1_2` - TLS version 1.2
    - `tlsv1_3` - TLS version 1.3
- Default:

    `ssl_any`

- Context:

    list (`config`)

#### `include_remote_file.ssl_ciphers`

SSL ciphers used

- Format:

    /`.+`/

- Default:

    `ALL`

- Context:

    list (`config`)

#### `include_remote_file.ca_verify`

Certificate verification

- Format:
    - `none` - do nothing
    - `optional` - optional
    - `required` - required
- Default:

    `none`

- Context:

    list (`config`)

#### `include_remote_file.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

### `**include_sympa_list**`

(Paragraph)
List inclusion

- Multiple occurrences allowed

Include subscribers from other list. All subscribers of list listname become subscribers of the current list. You may include as many lists as required, using one include\_sympa\_list paragraph for each included list. Any list at all may be included; you may therefore include lists which are also defined by the inclusion of other lists. Be careful, however, not to include list A in list B and then list B in list A, since this will give rise to an infinite loop.

#### `include_sympa_list.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sympa_list.listname`

list name to include

- Format:

    /`$listname(\@$host)?`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sympa_list.filter`

filter definition

- Format:

    /`.*`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sympa_list.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

### `**include_remote_sympa_list**`

(Paragraph)
remote list inclusion

- Multiple occurrences allowed

Sympa can contact another Sympa service using HTTPS to fetch a remote list in order to include each member of a remote list as subscriber. You may include as many lists as required, using one include\_remote\_sympa\_list paragraph for each included list. Be careful, however, not to give rise to an infinite loop resulting from cross includes.

For this operation, one Sympa site acts as a server while the other one acs as client. On the server side, the only setting needed is to give permission to the remote Sympa to review the list. This is controlled by the review scenario.

#### `include_remote_sympa_list.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_sympa_list.url`

data location URL

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_sympa_list.user`

remote user

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_sympa_list.passwd`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_remote_sympa_list.host`

remote host

- Format:

    /`$host`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

obsoleted.  Use "data location URL".

#### `include_remote_sympa_list.port`

remote port

- Format:

    /`\d+`/

- Default:

    `443`

- Context:

    list (`config`)

obsoleted.  Use "data location URL".

#### `include_remote_sympa_list.path`

remote path of sympa list dump

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

obsoleted.  Use "data location URL".

#### `include_remote_sympa_list.cert`

Deprecated.

#### `include_remote_sympa_list.timeout`

idle timeout

- Format:

    Number of seconds.

- Default:

    `180` (seconds)

- Context:

    list (`config`)

#### `include_remote_sympa_list.ssl_version`

SSL version

- Format:
    - `ssl_any` - any versions
    - `sslv2` - SSL version 2
    - `sslv3` - SSL version 3
    - `tlsv1` - TLS version 1
    - `tlsv1_1` - TLS version 1.1
    - `tlsv1_2` - TLS version 1.2
    - `tlsv1_3` - TLS version 1.3
- Default:

    `ssl_any`

- Context:

    list (`config`)

#### `include_remote_sympa_list.ssl_ciphers`

SSL ciphers used

- Format:

    /`.+`/

- Default:

    `ALL`

- Context:

    list (`config`)

#### `include_remote_sympa_list.ca_verify`

Certificate verification

- Format:
    - `none` - do nothing
    - `optional` - optional
    - `required` - required
- Default:

    `optional`

- Context:

    list (`config`)

#### `include_remote_sympa_list.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

### `**include_ldap_query**`

(Paragraph)
LDAP query inclusion

- Multiple occurrences allowed

This paragraph defines parameters for a query returning a list of subscribers. This feature requires the Net::LDAP (perlldap) PERL module.

#### `include_ldap_query.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_query.host`

remote host

- Format:

    /`$multiple_host_or_url`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_query.port`

Deprecated.

#### `include_ldap_query.use_tls`

use TLS (formerly SSL)

- Format:
    - `starttls` - use STARTTLS
    - `ldaps` - use LDAPS (LDAP over TLS)
    - `none` - do nothing
- Default:

    `none`

- Context:

    list (`config`)

#### `include_ldap_query.ssl_version`

SSL version

- Format:
    - `sslv2` - SSL version 2
    - `sslv3` - SSL version 3
    - `tlsv1` - TLS version 1
    - `tlsv1_1` - TLS version 1.1
    - `tlsv1_2` - TLS version 1.2
    - `tlsv1_3` - TLS version 1.3
- Default:

    `tlsv1`

- Context:

    list (`config`)

#### `include_ldap_query.ssl_ciphers`

SSL ciphers used

- Format:

    /`.+`/

- Default:

    `ALL`

- Context:

    list (`config`)

#### `include_ldap_query.ca_verify`

Certificate verification

- Format:
    - `none` - do nothing
    - `optional` - optional
    - `required` - required
- Default:

    `required`

- Context:

    list (`config`)

#### `include_ldap_query.bind_dn`

remote user

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_query.bind_password`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_query.suffix`

suffix

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_query.scope`

search scope

- Format:
    - `base` - base
    - `one` - one level
    - `sub` - subtree
- Default:

    `sub`

- Context:

    list (`config`)

#### `include_ldap_query.timeout`

connection timeout

- Format:

    Number of seconds.

- Default:

    `30` (seconds)

- Context:

    list (`config`)

#### `include_ldap_query.filter`

filter

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_query.attrs`

extracted attribute

- Format:

    /`$ldap_attrdesc(\s*,\s*$ldap_attrdesc)?`/

- Default:

    `mail`

- Context:

    list (`config`)

#### `include_ldap_query.select`

selection (if multiple)

- Format:
    - `all` - all
    - `first` - first entry
    - `regex` - entries matching regular expression
- Default:

    `first`

- Context:

    list (`config`)

#### `include_ldap_query.regex`

regular expression

- Format:

    /`.+`/

- Default:

    ``

- Context:

    list (`config`)

#### `include_ldap_query.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_query.passwd`

Obsoleted. Use [`bind_password`](#include_ldap_querybind_password).

#### `include_ldap_query.use_ssl`

Obsoleted. Use [`use_tls`](#include_ldap_queryuse_tls).

#### `include_ldap_query.user`

Obsoleted. Use [`bind_dn`](#include_ldap_querybind_dn).

### `**include_ldap_2level_query**`

(Paragraph)
LDAP 2-level query inclusion

- Multiple occurrences allowed

This paragraph defines parameters for a two-level query returning a list of subscribers. Usually the first-level query returns a list of DNs and the second-level queries convert the DNs into e-mail addresses. This feature requires the Net::LDAP (perlldap) PERL module.

#### `include_ldap_2level_query.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.host`

remote host

- Format:

    /`$multiple_host_or_url`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_query.port`

Deprecated.

#### `include_ldap_2level_query.use_tls`

use TLS (formerly SSL)

- Format:
    - `starttls` - use STARTTLS
    - `ldaps` - use LDAPS (LDAP over TLS)
    - `none` - do nothing
- Default:

    `none`

- Context:

    list (`config`)

#### `include_ldap_2level_query.ssl_version`

SSL version

- Format:
    - `sslv2` - SSL version 2
    - `sslv3` - SSL version 3
    - `tlsv1` - TLS version 1
    - `tlsv1_1` - TLS version 1.1
    - `tlsv1_2` - TLS version 1.2
    - `tlsv1_3` - TLS version 1.3
- Default:

    `tlsv1`

- Context:

    list (`config`)

#### `include_ldap_2level_query.ssl_ciphers`

SSL ciphers used

- Format:

    /`.+`/

- Default:

    `ALL`

- Context:

    list (`config`)

#### `include_ldap_2level_query.ca_verify`

Certificate verification

- Format:
    - `none` - do nothing
    - `optional` - optional
    - `required` - required
- Default:

    `required`

- Context:

    list (`config`)

#### `include_ldap_2level_query.bind_dn`

remote user

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.bind_password`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.suffix1`

first-level suffix

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.scope1`

first-level search scope

- Format:
    - `base` - base
    - `one` - one level
    - `sub` - subtree
- Default:

    `sub`

- Context:

    list (`config`)

#### `include_ldap_2level_query.timeout1`

first-level connection timeout

- Format:

    Number of seconds.

- Default:

    `30` (seconds)

- Context:

    list (`config`)

#### `include_ldap_2level_query.filter1`

first-level filter

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_query.attrs1`

first-level extracted attribute

- Format:

    /`$ldap_attrdesc`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.select1`

first-level selection

- Format:
    - `all` - all
    - `first` - first entry
    - `regex` - entries matching regular expression
- Default:

    `first`

- Context:

    list (`config`)

#### `include_ldap_2level_query.regex1`

first-level regular expression

- Format:

    /`.+`/

- Default:

    ``

- Context:

    list (`config`)

#### `include_ldap_2level_query.suffix2`

second-level suffix template

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.scope2`

second-level search scope

- Format:
    - `base` - base
    - `one` - one level
    - `sub` - subtree
- Default:

    `sub`

- Context:

    list (`config`)

#### `include_ldap_2level_query.timeout2`

second-level connection timeout

- Format:

    Number of seconds.

- Default:

    `30` (seconds)

- Context:

    list (`config`)

#### `include_ldap_2level_query.filter2`

second-level filter template

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_query.attrs2`

second-level extracted attribute

- Format:

    /`$ldap_attrdesc(\s*,\s*$ldap_attrdesc)?`/

- Default:

    `mail`

- Context:

    list (`config`)

#### `include_ldap_2level_query.select2`

second-level selection

- Format:
    - `all` - all
    - `first` - first entry
    - `regex` - entries matching regular expression
- Default:

    `first`

- Context:

    list (`config`)

#### `include_ldap_2level_query.regex2`

second-level regular expression

- Format:

    /`.+`/

- Default:

    ``

- Context:

    list (`config`)

#### `include_ldap_2level_query.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_query.passwd`

Obsoleted. Use [`bind_password`](#include_ldap_2level_querybind_password).

#### `include_ldap_2level_query.use_ssl`

Obsoleted. Use [`use_tls`](#include_ldap_2level_queryuse_tls).

#### `include_ldap_2level_query.user`

Obsoleted. Use [`bind_dn`](#include_ldap_2level_querybind_dn).

### `**include_sql_query**`

(Paragraph)
SQL query inclusion

- Multiple occurrences allowed

This parameter is used to define the SQL query parameters. 

#### `include_sql_query.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.db_type`

database type

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_query.db_host`

remote host

- Format:

    /`$host`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.db_port`

database port

- Format:

    /`\d+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.db_name`

database name

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_query.db_options`

connection options

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.db_env`

environment variables for database connection

- Format:

    /`\w+\=\S+(;\w+\=\S+)*`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.db_user`

remote user

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_query.db_passwd`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.sql_query`

SQL query

- Format:

    /`$sql_query`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_query.f_dir`

Directory where the database is stored (used for DBD::CSV only)

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_query.connect_options`

Obsoleted. Use [`db_options`](#include_sql_querydb_options).

#### `include_sql_query.host`

Obsoleted. Use [`db_host`](#include_sql_querydb_host).

#### `include_sql_query.passwd`

Obsoleted. Use [`db_passwd`](#include_sql_querydb_passwd).

#### `include_sql_query.user`

Obsoleted. Use [`db_user`](#include_sql_querydb_user).

### `**ttl**`

Inclusions timeout

- Format:

    Number of seconds.

- Default:

    `3600` (seconds)

- Context:

    list (`config`), site (`sympa.conf`)

Sympa caches user data extracted using the include parameter. Their TTL (time-to-live) within Sympa can be controlled using this parameter. The default value is 3600

### `**distribution_ttl**`

Inclusions timeout for message distribution

- Format:

    Number of seconds.

- Default:

    None.

- Context:

    list (`config`)

This parameter defines the delay since the last synchronization after which the user's list will be updated before performing either of following actions:

\* Reviewing list members

\* Message distribution

### `**include_ldap_ca**`

(Paragraph)
LDAP query custom attribute

- Multiple occurrences allowed

#### `include_ldap_ca.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_ca.host`

remote host

- Format:

    /`$multiple_host_or_url`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_ca.port`

Deprecated.

#### `include_ldap_ca.use_tls`

use TLS (formerly SSL)

- Format:
    - `starttls` - use STARTTLS
    - `ldaps` - use LDAPS (LDAP over TLS)
    - `none` - do nothing
- Default:

    `none`

- Context:

    list (`config`)

#### `include_ldap_ca.ssl_version`

SSL version

- Format:
    - `sslv2` - SSL version 2
    - `sslv3` - SSL version 3
    - `tlsv1` - TLS version 1
    - `tlsv1_1` - TLS version 1.1
    - `tlsv1_2` - TLS version 1.2
    - `tlsv1_3` - TLS version 1.3
- Default:

    `tlsv1`

- Context:

    list (`config`)

#### `include_ldap_ca.ssl_ciphers`

SSL ciphers used

- Format:

    /`.+`/

- Default:

    `ALL`

- Context:

    list (`config`)

#### `include_ldap_ca.ca_verify`

Certificate verification

- Format:
    - `none` - do nothing
    - `optional` - optional
    - `required` - required
- Default:

    `required`

- Context:

    list (`config`)

#### `include_ldap_ca.bind_dn`

remote user

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_ca.bind_password`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_ca.suffix`

suffix

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_ca.scope`

search scope

- Format:
    - `base` - base
    - `one` - one level
    - `sub` - subtree
- Default:

    `sub`

- Context:

    list (`config`)

#### `include_ldap_ca.timeout`

connection timeout

- Format:

    Number of seconds.

- Default:

    `30` (seconds)

- Context:

    list (`config`)

#### `include_ldap_ca.filter`

filter

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_ca.attrs`

extracted attribute

- Format:

    /`$ldap_attrdesc(\s*,\s*$ldap_attrdesc)?`/

- Default:

    `mail`

- Context:

    list (`config`)

#### `include_ldap_ca.email_entry`

Name of email entry

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_ca.select`

selection (if multiple)

- Format:
    - `all` - all
    - `first` - first entry
    - `regex` - entries matching regular expression
- Default:

    `first`

- Context:

    list (`config`)

#### `include_ldap_ca.regex`

regular expression

- Format:

    /`.+`/

- Default:

    ``

- Context:

    list (`config`)

#### `include_ldap_ca.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_ca.passwd`

Obsoleted. Use [`bind_password`](#include_ldap_cabind_password).

#### `include_ldap_ca.use_ssl`

Obsoleted. Use [`use_tls`](#include_ldap_cause_tls).

#### `include_ldap_ca.user`

Obsoleted. Use [`bind_dn`](#include_ldap_cabind_dn).

### `**include_ldap_2level_ca**`

(Paragraph)
LDAP 2-level query custom attribute

- Multiple occurrences allowed

#### `include_ldap_2level_ca.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.host`

remote host

- Format:

    /`$multiple_host_or_url`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.port`

Deprecated.

#### `include_ldap_2level_ca.use_tls`

use TLS (formerly SSL)

- Format:
    - `starttls` - use STARTTLS
    - `ldaps` - use LDAPS (LDAP over TLS)
    - `none` - do nothing
- Default:

    `none`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.ssl_version`

SSL version

- Format:
    - `sslv2` - SSL version 2
    - `sslv3` - SSL version 3
    - `tlsv1` - TLS version 1
    - `tlsv1_1` - TLS version 1.1
    - `tlsv1_2` - TLS version 1.2
    - `tlsv1_3` - TLS version 1.3
- Default:

    `tlsv1`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.ssl_ciphers`

SSL ciphers used

- Format:

    /`.+`/

- Default:

    `ALL`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.ca_verify`

Certificate verification

- Format:
    - `none` - do nothing
    - `optional` - optional
    - `required` - required
- Default:

    `required`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.bind_dn`

remote user

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.bind_password`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.suffix1`

first-level suffix

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.scope1`

first-level search scope

- Format:
    - `base` - base
    - `one` - one level
    - `sub` - subtree
- Default:

    `sub`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.timeout1`

first-level connection timeout

- Format:

    Number of seconds.

- Default:

    `30` (seconds)

- Context:

    list (`config`)

#### `include_ldap_2level_ca.filter1`

first-level filter

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.attrs1`

first-level extracted attribute

- Format:

    /`$ldap_attrdesc`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.select1`

first-level selection

- Format:
    - `all` - all
    - `first` - first entry
    - `regex` - entries matching regular expression
- Default:

    `first`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.regex1`

first-level regular expression

- Format:

    /`.+`/

- Default:

    ``

- Context:

    list (`config`)

#### `include_ldap_2level_ca.suffix2`

second-level suffix template

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.scope2`

second-level search scope

- Format:
    - `base` - base
    - `one` - one level
    - `sub` - subtree
- Default:

    `sub`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.timeout2`

second-level connection timeout

- Format:

    Number of seconds.

- Default:

    `30` (seconds)

- Context:

    list (`config`)

#### `include_ldap_2level_ca.filter2`

second-level filter template

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.attrs2`

second-level extracted attribute

- Format:

    /`$ldap_attrdesc`/

- Default:

    `mail`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.select2`

second-level selection

- Format:
    - `all` - all
    - `first` - first entry
    - `regex` - entries matching regular expression
- Default:

    `first`

- Context:

    list (`config`)

#### `include_ldap_2level_ca.regex2`

second-level regular expression

- Format:

    /`.+`/

- Default:

    ``

- Context:

    list (`config`)

#### `include_ldap_2level_ca.email_entry`

Name of email entry

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_ldap_2level_ca.passwd`

Obsoleted. Use [`bind_password`](#include_ldap_2level_cabind_password).

#### `include_ldap_2level_ca.use_ssl`

Obsoleted. Use [`use_tls`](#include_ldap_2level_cause_tls).

#### `include_ldap_2level_ca.user`

Obsoleted. Use [`bind_dn`](#include_ldap_2level_cabind_dn).

### `**include_sql_ca**`

(Paragraph)
SQL query custom attribute

- Multiple occurrences allowed

#### `include_sql_ca.name`

short name for this source

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.db_type`

database type

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_ca.db_host`

remote host

- Format:

    /`$host`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.db_port`

database port

- Format:

    /`\d+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.db_name`

database name

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_ca.db_options`

connection options

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.db_env`

environment variables for database connection

- Format:

    /`\w+\=\S+(;\w+\=\S+)*`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.db_user`

remote user

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_ca.db_passwd`

remote password

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.sql_query`

SQL query

- Format:

    /`$sql_query`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_ca.f_dir`

Directory where the database is stored (used for DBD::CSV only)

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.email_entry`

Name of email entry

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `include_sql_ca.nosync_time_ranges`

Time ranges when inclusion is not allowed

- Format:

    /`$time_ranges`/

- Default:

    None.

- Context:

    list (`config`)

#### `include_sql_ca.connect_options`

Obsoleted. Use [`db_options`](#include_sql_cadb_options).

#### `include_sql_ca.host`

Obsoleted. Use [`db_host`](#include_sql_cadb_host).

#### `include_sql_ca.passwd`

Obsoleted. Use [`db_passwd`](#include_sql_cadb_passwd).

#### `include_sql_ca.user`

Obsoleted. Use [`db_user`](#include_sql_cadb_user).

## DKIM/DMARC/ARC

DKIM signature verification and re-signing. It requires an external module: Mail-DKIM.

ARC seals on forwarded messages. It requires an external module: Mail-DKIM.

### `**dkim_add_signature_to**`

Which service messages to be signed

- Format:

    /`(?:list|robot)(?:,(?:list|robot))*`/

- Default:

    `robot,list`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Inserts a DKIM signature to service messages in context of robot, list or both

### `**dkim_signer_identity**`

The "i=" tag as defined in rfc 4871

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Default is null.

### `**dkim_feature**`

Insert DKIM signature to messages sent to the list

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

If set to "on", Sympa may verify DKIM signatures of incoming messages and/or insert DKIM signature to outgoing messages.

### `**dkim_parameters**`

(Paragraph)
DKIM configuration

- Single occurrence

A set of parameters in order to define outgoing DKIM signature

#### `dkim_parameters.private_key_path`

File path for DKIM private key

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The file must contain a PEM encoded private key

#### `dkim_parameters.selector`

Selector for DNS lookup of DKIM public key

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The selector is used in order to build the DNS query for public key. It is up to you to choose the value you want but verify that you can query the public DKIM key for "&lt;selector>.\_domainkey.your\_domain"

#### `dkim_parameters.header_list`

Deprecated.

#### `dkim_parameters.signer_domain`

DKIM "d=" tag, you should probably use the default value

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The DKIM "d=" tag, is the domain of the signing entity. The list domain MUST be included in the "d=" domain

#### `dkim_parameters.signer_identity`

DKIM "i=" tag, you should probably leave this parameter empty

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`)

DKIM "i=" tag, you should probably not use this parameter, as recommended by RFC 4871, default for list brodcasted messages is i=&lt;listname>-request@&lt;domain>

### `**dkim_signature_apply_on**`

The categories of messages sent to the list that will be signed using DKIM.

- Format:

    Multiple values allowed, separated by `,`.

    - `md5_authenticated_messages` - authenticated by password
    - `smime_authenticated_messages` - authenticated by S/MIME signature
    - `dkim_authenticated_messages` - authenticated by DKIM signature
    - `editor_validated_messages` - approved by moderator
    - `none` - do nothing
    - `any` - any messages

- Default:

    `md5_authenticated_messages,smime_authenticated_messages,dkim_authenticated_messages,editor_validated_messages`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This parameter controls in which case messages must be signed using DKIM, you may sign every message choosing 'any' or a subset. The parameter value is a comma separated list of keywords

### `**arc_feature**`

Add ARC seals to messages sent to the list

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Enable/Disable ARC. This feature requires Mail::DKIM::ARC to be installed, and maybe some custom scenario to be updated

### `**arc_srvid**`

SRV ID for Authentication-Results used in ARC seal

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Typically the domain of the mail server

### `**arc_parameters**`

(Paragraph)
ARC configuration

- Single occurrence

A set of parameters in order to define outgoing ARC seal

#### `arc_parameters.arc_private_key_path`

File path for ARC private key

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The file must contain a PEM encoded private key. Defaults to same file as DKIM private key

#### `arc_parameters.arc_selector`

Selector for DNS lookup of ARC public key

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The selector is used in order to build the DNS query for public key. It is up to you to choose the value you want but verify that you can query the public DKIM key for "&lt;selector>.\_domainkey.your\_domain". Default is the same selector as for DKIM signatures

#### `arc_parameters.arc_signer_domain`

ARC "d=" tag, you should probably use the default value

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

The ARC "d=" tag is the domain of the signing entity. The DKIM d= domain name is used as its default value

### `**dmarc_protection**`

(Paragraph)
DMARC Protection

- Single occurrence

Parameters to define how to manage From address processing to avoid some domains' excessive DMARC protection

#### `dmarc_protection.mode`

Protection modes

- Format:

    Multiple values allowed, separated by `,`.

    - `none` - do nothing
    - `all` - all
    - `dkim_signature` - DKIM signature exists
    - `dmarc_reject` - DMARC policy suggests rejection
    - `dmarc_any` - DMARC policy exists
    - `dmarc_quarantine` - DMARC policy suggests quarantine
    - `domain_regex` - domain matching regular expression

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Select one or more operation modes.  "Domain matching regular expression" (domain\_regex) matches the specified Domain regular expression; "DKIM signature exists" (dkim\_signature) matches any message with a DKIM signature header; "DMARC policy ..." (dmarc\_\*) matches messages from sender domains with a DMARC policy as given; "all" (all) matches all messages.

Example:

    dmarc_protection.mode dmarc_reject,dkim_signature

#### `dmarc_protection.domain_regex`

Regular expression for domain name match

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Regular expression match pattern for From domain

#### `dmarc_protection.other_email`

New From address

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This is the email address to use when modifying the From header.  It defaults to the list address.  This is similar to Anonymisation but preserves the original sender details in the From address phrase.

#### `dmarc_protection.phrase`

New From name format

- Format:
    - `display_name` - "Name"
    - `name_and_email` - "Name" (e-mail)
    - `name_via_list` - "Name" (via List)
    - `name_email_via_list` - "Name" (e-mail via List)
    - `list_for_email` - "List" (on behalf of e-mail)
    - `list_for_name` - "List" (on behalf of Name)
- Default:

    `name_via_list`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

This is the format to be used for the sender name part of the new From header field.

## List address verification

Checks if an alias with the same name as the list to be created already exists on the SMTP server. This feature requires an external module: Net-SMTP.

### `**list_check_helo**`

SMTP HELO (EHLO) parameter used for address verification

- Format:

    /`\S+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Default value is the host part of "list\_check\_smtp" parameter.

### `**list_check_smtp**`

SMTP server to verify existence of the same addresses as the list to be created

- Format:

    /`$hostport`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

This is needed if you are running Sympa on a host but you handle all your mail on a separate mail relay.

Default value is real FQDN of the host. Port number may be specified as "mail.example.org:25" or "203.0.113.1:25".  If port is not specified, standard port (25) will be used.

### `**list_check_suffixes**`

Address suffixes to verify

- Format:

    /`\S+`/

- Default:

    `request,owner,editor,unsubscribe,subscribe`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

List of suffixes you are using for list addresses, i.e. "mylist-request", "mylist-owner" and so on.

This parameter is used with the "list\_check\_smtp" parameter. It is also used to check list names at list creation time.

## Antivirus plug-in

### `**antivirus_path**`

Path to the antivirus scanner engine

- Format:

    /`.+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Supported antivirus: Clam AntiVirus/clamscan & clamdscan, McAfee/uvscan, Fsecure/fsav, Sophos, AVP and Trend Micro/VirusWall

Example:

    antivirus_path /usr/local/bin/clamscan

### `**antivirus_args**`

Antivirus plugin command line arguments

- Format:

    /`.+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Example:

    antivirus_args --no-summary --database /usr/local/share/clamav

### `**antivirus_notify**`

Notify sender if virus checker detects malicious content

- Format:
    - `sender` - sender
    - `delivery_status` - send back DSN
    - `none` - do nothing
- Default:

    `sender`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

"sender" to notify originator of the message, "delivery\_status" to send delivery status, or "none"

## Miscellaneous

### `**email**`

Local part of Sympa email address

- Format:

    /`\S+`/

- Default:

    `sympa`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Local part (the part preceding the "@" sign) of the address by which mail interface of Sympa accepts mail commands.

If you change the default value, you must modify the mail aliases too.

### `**listmaster_email**`

Local part of listmaster email address

- Format:

    /`\S+`/

- Default:

    `listmaster`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Local part (the part preceding the "@" sign) of the address by which listmasters receive messages.

If you change the default value, you must modify the mail aliases too.

### `**custom_robot_parameter**`

Custom robot parameter

- Format:

    Multiple occurrences allowed.

    /`.+`/

- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Used to define a custom parameter for your server. Do not forget the semicolon between the parameter name and the parameter value.

You will be able to access the custom parameter value in web templates by variable "conf.custom\_robot\_parameter.&lt;param\_name>"

Example:

    custom_robot_parameter param_name ; param_value

### `**cache_list_config**`

Use of binary cache of list configuration

- Format:
    - `binary_file` - use binary file
    - `none` - do nothing
- Default:

    `none`

- Context:

    site (`sympa.conf`)

binary\_file: Sympa processes will maintain a binary version of the list configuration, "config.bin" file on local disk. If you manage a big amount of lists (1000+), it should make the web interface startup faster.

You can recreate cache by running "sympa.pl --reload\_list\_config".

### `**db_list_cache**`

Use database cache to search lists

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    site (`sympa.conf`)

Note that "list\_table" database table should be filled at the first time by running:

    # sympa.pl --sync_list_db

### `**purge_user_table_task**`

Task for expiring inactive users

- Format:

    /`\w+`/

- Default:

    `monthly`

- Context:

    site (`sympa.conf`)

This task removes rows in the "user\_table" table which have not corresponding entries in the "subscriber\_table" table.

### `**purge_logs_table_task**`

Task for cleaning tables

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

This task cleans old logs from "logs\_table" table.

### `**logs_expiration_period**`

Max age of logs in database

- Format:

    Number of months.

- Default:

    `3` (months)

- Context:

    site (`sympa.conf`)

Number of months that elapse before a log is expired

### `**stats_expiration_period**`

Max age of statistics information in database

- Format:

    Number of months.

- Default:

    `3` (months)

- Context:

    site (`sympa.conf`)

Number of months that elapse before statistics information are expired

### `**umask**`

Umask

- Format:

    /`[0-7]+`/

- Default:

    `027`

- Context:

    site (`sympa.conf`)

Default mask for file creation (see umask(2)). Note that it will be interpreted as an octal value.

### `**clean_delay_queuemod**`

Max age of moderated messages

- Format:

    Number of days.

- Default:

    `30` (days)

- Context:

    list (`config`), site (`sympa.conf`)

Number of days messages are kept in moderation spool (as specified by "queuemod" parameter). Beyond this deadline, messages that have not been processed are deleted.

### `**cookie**`

Secret string for generating unique keys

- Format:

    The value to be concealed.

- Default:

    None.

- Context:

    list (`config`), site (`sympa.conf`)

This allows generated authentication keys to differ from a site to another. It is also used for encryption of user passwords stored in the database. The presence of this string is one reason why access to "sympa.conf" needs to be restricted to the "sympa" user.

Note that changing this parameter will break all HTTP cookies stored in users' browsers, as well as all user passwords and lists X509 private keys. To prevent a catastrophe, Sympa refuses to start if this "cookie" parameter was changed.

Example:

    cookie 123456789

### `**custom_attribute**`

(Paragraph)
Custom user attributes

- Multiple occurrences allowed

#### `custom_attribute.id`

internal identifier

- Format:

    /`\w+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `custom_attribute.name`

label

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `custom_attribute.comment`

additional comment

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `custom_attribute.type`

type

- Format:
    - `string` - string
    - `text` - multi-line text
    - `integer` - number
    - `enum` - set of keywords
- Default:

    `string`

- Context:

    list (`config`)

#### `custom_attribute.enum_values`

possible attribute values (if enum is used)

- Format:

    /`.+`/

- Default:

    None.

- Context:

    list (`config`)

#### `custom_attribute.optional`

is the attribute optional?

- Format:
    - `required` - required
    - `optional` - optional
- Default:

    `optional`

- Context:

    list (`config`)

### `**custom_vars**`

(Paragraph)
custom parameters

- Multiple occurrences allowed

#### `custom_vars.name`

var name

- Format:

    /`\S+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `custom_vars.value`

var value

- Format:

    /`.+`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

### `**loop_prevention_regex**`

Regular expression applied to prevent loops with robots

- Format:

    /`\S*`/

- Default:

    `mailer-daemon|sympa|listserv|majordomo|smartlist|mailman`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

If the sender address matches the regular expression, then the message is rejected.

### `**pictures_feature**`

Pictures

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `on`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

Enables or disables the pictures feature by default.  If enabled, subscribers can upload their picture (from the "Subscriber option" page) to use as an avatar.

Pictures are stored in a directory specified by the "static\_content\_path" parameter.

### `**remind_task**`

Periodical subscription reminder task

- Format:

    /`\w+`/

- Default:

    None.

- Context:

    list (`config`), site (`sympa.conf`)

This parameter states which model is used to create a remind task. A remind task regularly sends  subscribers a message which reminds them of their list subscriptions.

### `**latest_instantiation**`

(Paragraph)
Latest family instantiation

- Single occurrence

#### `latest_instantiation.email`

who ran the instantiation

- Format:

    /`listmaster|$email`/

- Default:

    None.

- Context:

    list (`config`)

#### `latest_instantiation.date_epoch`

date

- Format:

    The time in second from Unix epoch.

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `latest_instantiation.date`

Deprecated.

### `**creation**`

(Paragraph)
Creation of the list

- Single occurrence

#### `creation.email`

who created the list

- Format:

    /`listmaster|$email`/

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `creation.date_epoch`

date

- Format:

    The time in second from Unix epoch.

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `creation.date`

Deprecated.

### `**update**`

(Paragraph)
Last update of config

- Single occurrence

#### `update.email`

who updated the config

- Format:

    /`(listmaster|automatic|$email)`/

- Default:

    None.

- Context:

    list (`config`)

#### `update.date_epoch`

date

- Format:

    The time in second from Unix epoch.

- Default:

    None, _mandatory_.

- Context:

    list (`config`)

#### `update.date`

Deprecated.

### `**status**`

Status of the list

- Format:

    Status of list.

- Default:

    `open`

- Context:

    list (`config`)

### `**serial**`

Serial number of the config

- Format:

    /`\d+`/

- Default:

    `0`

- Context:

    list (`config`)

## Web interface parameters

### `**wwsympa_url**`

URL prefix of web interface

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

This is used to construct URLs of web interface.

Example:

    wwsympa_url https://web.example.org/sympa

### `**wwsympa_url_local**`

URL prefix of WWSympa behind proxy

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**static_content_url**`

URL for static contents

- Format:
- Default:

    `/static-sympa`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

HTTP server have to map it with "static\_content\_path" directory.

### `**static_content_path**`

Directory for static contents

- Format:
- Default:

    `/home/sympa/var/lib/sympa/static_content`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**css_path**`

Directory for static style sheets (CSS)

- Format:
- Default:

    `/home/sympa/var/lib/sympa/static_content/css`

- Context:

    site (`sympa.conf`)

After an upgrade, static CSS files are upgraded with the newly installed "css.tt2" template. Therefore, this is not a good place to store customized CSS files.

### `**css_url**`

URL for style sheets (CSS)

- Format:
- Default:

    `/static-sympa/css`

- Context:

    site (`sympa.conf`)

To use auto-generated static CSS, HTTP server have to map it with "css\_path".

### `**pictures_path**`

Directory for subscribers pictures

- Format:
- Default:

    `/home/sympa/var/lib/sympa/static_content/pictures`

- Context:

    site (`sympa.conf`)

### `**pictures_url**`

URL for subscribers pictures

- Format:
- Default:

    `/static-sympa/pictures`

- Context:

    site (`sympa.conf`)

HTTP server have to map it with "pictures\_path" directory.

### `**mhonarc**`

Path to MHonArc mail-to-HTML converter

- Format:
- Default:

    `/usr/bin/mhonarc`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

This is required for HTML mail archiving.

### `**log_facility**`

System log facility for web interface

- Format:
- Default:

    `LOCAL1`

- Context:

    site (`sympa.conf`)

System log facility for WWSympa, archived.pl and bounced.pl. Default is to use value of "syslog" parameter.

## Web interface parameters: Appearances

### `**logo_html_definition**`

Custom logo

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

HTML fragment to insert a logo in the page of web interface.

Example:

    logo_html_definition <a href="http://www.example.com"><img style="float: left; margin-top: 7px; margin-left: 37px;" src="http://www.example.com/logos/mylogo.jpg" alt="My Company" /></a>

### `**favicon_url**`

Custom favicon

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

URL of favicon image

### `color_0`, ..., `color_15`

Colors for web interface

- Format:
- Default:

    See description on web interface.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Colors are used in style sheet (CSS). They may be changed using web interface by listmasters.

### `dark_color`, `light_color`, `text_color`, `bg_color`, `error_color`, `selected_color`, `shaded_color`

Colors for web interface, obsoleted

- Format:
- Default:

    See description on web interface.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**default_home**`

Type of main web page

- Format:
- Default:

    `home`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

"lists" for the page of list of lists. "home" for home page.

### `**archive_default_index**`

Default index organization of web archive

- Format:
- Default:

    `thrd`

- Context:

    site (`sympa.conf`)

thrd: Threaded index.

mail: Chronological index.

### `**review_page_size**`

Size of review page

- Format:
- Default:

    `25`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Default number of lines of the array displaying users in the review page

### `**viewlogs_page_size**`

Size of viewlogs page

- Format:
- Default:

    `25`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Default number of lines of the array displaying the log entries in the logs page.

### `main_menu_custom_button_1_title`, ... `main_menu_custom_button_3_title`, `main_menu_custom_button_1_url`, ... `main_menu_custom_button_3_url`, `main_menu_custom_button_1_target`, ... `main_menu_custom_button_3_target`

Custom menus

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

You may modify the main menu content by editing the menu.tt2 file, but you can also edit these parameters in order to add up to 3 buttons. Each button is defined by a title (the text in the button), an URL and, optionally, a target.

Example:

    main_menu_custom_button_1_title FAQ
    main_menu_custom_button_1_url http://www.renater.fr/faq/universalistes/index
    main_menu_custom_button_1_target Help

## Password validation

Checks if the password the user submitted has sufficient strength. This feature requires an external module: Data-Password.

### `**password_validation**`

Password validation

- Format:
- Default:

    None.

- Context:

    site (`sympa.conf`)

The password validation techniques to be used against user passwords that are added to mailing lists. Options come from Data::Password (http://search.cpan.org/~razinf/Data-Password-1.07/Password.pm#VARIABLES)

Example:

    password_validation MINLEN=8,GROUPS=3,DICTIONARY=4,DICTIONARIES=/pentest/dictionaries

## Authentication with LDAP

Authenticates users based on the directory on LDAP server. This feature requires an external module: Net-LDAP. And also, if secure connection (LDAPS) is required: IO-Socket-SSL.

### `**ldap_force_canonical_email**`

Use canonical email address for LDAP authentication

- Format:
- Default:

    `1`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

When using LDAP authentication, if the identifier provided by the user was a valid email, if this parameter is set to false, then the provided email will be used to authenticate the user. Otherwise, use of the first email returned by the LDAP server will be used.

## SOAP HTTP interface

Provides some functions of Sympa through the SOAP HTTP interface. This feature requires an external module: SOAP-Lite.

### `**soap_url**`

URL of SympaSOAP

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

WSDL document of SympaSOAP refers to this URL in its service section.

Example:

    soap_url http://web.example.org/sympasoap

### `**soap_url_local**`

URL of SympaSOAP behind proxy

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

## Web interface parameters: Miscellaneous

### `**cookie_domain**`

HTTP cookies validity domain

- Format:
- Default:

    `localhost`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If beginning with a dot ("."), the cookie is available within the specified Internet domain. Otherwise, for the specified host. The only reason for replacing the default value would be where WWSympa's authentication process is shared with an application running on another host.

Example:

    cookie_domain .renater.fr

### `**cookie_expire**`

HTTP cookies lifetime

- Format:
- Default:

    `0`

- Context:

    site (`sympa.conf`)

This is the default value when not set explicitly by users. "0" means the cookie may be retained during browser sessions.

### `**cookie_refresh**`

Average interval to refresh HTTP session ID.

- Format:
- Default:

    `60`

- Context:

    site (`sympa.conf`)

### `**purge_session_table_task**`

Task for cleaning old sessions

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

This task removes old entries in the "session\_table" table.

### `**session_table_ttl**`

Max age of sessions

- Format:
- Default:

    `2d`

- Context:

    site (`sympa.conf`)

Session duration is controlled by "sympa\_session" cookie validity attribute. However, by security reason, this delay also need to be controlled by server side. This task removes old entries in the "session\_table" table.

Format of values is a string without spaces including "y" for years, "m" for months, "d" for days, "h" for hours, "min" for minutes and "sec" for seconds.

### `**anonymous_session_table_ttl**`

Max age of sessions for anonymous users

- Format:
- Default:

    `1h`

- Context:

    site (`sympa.conf`)

### `**shared_feature**`

Enable shared repository

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If set to "on", list owners can open shared repository.

### `**use_html_editor**`

Use HTML editor

- Format:
    - `off` - disabled
    - `on` - enabled
- Default:

    `off`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If set to "on", users will be able to post messages in HTML using a javascript WYSIWYG editor.

Example:

    use_html_editor on

### `**html_editor_url**`

URL of HTML editor

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

URL path to the javascript file making the WYSIWYG HTML editor available.  Relative path under &lt;static\_content\_url> or absolute path.

Example is for TinyMCE 4 installed under &lt;static\_content\_path>/js/tinymce/.

Example:

    html_editor_url js/tinymce/tinymce.min.js

### `**html_editor_init**`

HTML editor initialization

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Javascript excerpt that enables and configures the WYSIWYG HTML editor.

Example:

    html_editor_init tinymce.init({selector:"#body",language:lang.split(/[^a-zA-Z]+/).join("_")});

### `**max_wrong_password**`

Count limit of wrong password submission

- Format:
- Default:

    `19`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If this limit is reached, the account is locked until the user renews their password. The default value is chosen in order to block bots trying to log in using brute force strategy. This value should never be reached by real users that will probably uses the renew password service before they performs so many tries.

### `**password_case**`

Password case

- Format:
- Default:

    `insensitive`

- Context:

    site (`sympa.conf`)

"insensitive" or "sensitive".

If set to "insensitive", WWSympa's password check will be insensitive. This only concerns passwords stored in the Sympa database, not the ones in LDAP.

Should not be changed! May invalid all user password.

### `**password_hash**`

Password hashing algorithm

- Format:
- Default:

    `md5`

- Context:

    site (`sympa.conf`)

"md5" or "bcrypt".

If set to "md5", Sympa will use MD5 password hashes. If set to "bcrypt", bcrypt hashes will be used instead. This only concerns passwords stored in the Sympa database, not the ones in LDAP.

Should not be changed! May invalid all user passwords.

### `**password_hash_update**`

Update password hashing algorithm when users log in

- Format:
- Default:

    `1`

- Context:

    site (`sympa.conf`)

On successful login, update the encrypted user password to use the algorithm specified by "password\_hash". This allows for a graceful transition to a new password hash algorithm. A value of 0 disables updating of existing password hashes.  New and reset passwords will use the "password\_hash" setting in all cases.

### `**bcrypt_cost**`

Bcrypt hash cost

- Format:
- Default:

    `12`

- Context:

    site (`sympa.conf`)

When "password\_hash" is set to "bcrypt", this sets the "cost" parameter of the bcrypt hash function. The default of 12 is expected to require approximately 250ms to calculate the password hash on a 3.2GHz CPU. This only concerns passwords stored in the Sympa database, not the ones in LDAP.

Can be changed but any new cost setting will only apply to new passwords.

### `**one_time_ticket_lifetime**`

Age of one time ticket

- Format:
- Default:

    `2d`

- Context:

    site (`sympa.conf`)

Duration before the one time tickets are expired

### `**one_time_ticket_lockout**`

Restrict access to one time ticket

- Format:
- Default:

    `one_time`

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

Is access to the one time ticket restricted, if any users previously accessed? (one\_time &#124; remote\_addr &#124; open)

### `**purge_one_time_ticket_table_task**`

Task for expiring old one time tickets

- Format:

    /`\w+`/

- Default:

    `daily`

- Context:

    site (`sympa.conf`)

### `**one_time_ticket_table_ttl**`

Expiration period of one time ticket

- Format:
- Default:

    `10d`

- Context:

    site (`sympa.conf`)

### `**pictures_max_size**`

The maximum size of uploaded picture

- Format:

    Number of bytes.

- Default:

    `102400` (bytes)

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

### `**spam_protection**`

Protect web interface against spam harvesters

- Format:
    - `at` - replace @ characters
    - `javascript` - use JavaScript
    - `none` - do nothing
- Default:

    `javascript`

- Context:

    list (`config`), domain (`robot.conf`), site (`sympa.conf`)

There is a need to protect Sympa web sites against spambots which collect email addresses from public web sites. Various methods are available in Sympa and you can choose to use them with the spam\_protection and web\_archive\_spam\_protection parameters. Possible value are:

javascript: 

the address is hidden using a javascript. A user who enables javascript can see a nice mailto address where others have nothing.

at: 

the @ char is replaced by the string " AT ".

none: 

no protection against spammer.

### `**reporting_spam_script_path**`

Script to report spam

- Format:
- Default:

    None.

- Context:

    domain (`robot.conf`), site (`sympa.conf`)

If set, when a list moderator report undetected spams for list moderation, this external script is invoked and the message is injected into standard input of the script.

### `**domains_blacklist**`

Prevent people to subscribe to a list with adresses using these domains

- Format:
- Default:

    None.

- Context:

    site (`sympa.conf`)

This parameter is a comma-separated list.

Example:

    domains_blacklist example.org,spammer.com

### `**quiet_subscription**`

Quiet subscriptions policy

- Format:
    - `on` - enabled
    - `optional` - optional
    - `off` - disabled
- Default:

    `optional`

- Context:

    site (`sympa.conf`)

Global policy for quiet subscriptions: "on" means that subscriptions will never send a notice to the subscriber, "off" will enforce a notice sending, and "optional" (default) allows the use of the list policy.

### `**show_report_abuse**`

Add a "Report abuse" link in the side menu of the lists

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    site (`sympa.conf`)

The link is a mailto link, you can change that by overriding web\_tt2/report\_abuse.tt2

### `**allow_account_deletion**`

EXPERIMENTAL! Allow users to delete their account. If enabled, shows a "delete my account" form in user's preferences page.

- Format:
    - `on` - enabled
    - `off` - disabled
- Default:

    `off`

- Context:

    site (`sympa.conf`)

Account deletion unsubscribes the users from his/her lists and removes him/her from lists ownership. It is only available to users using internal authentication (i.e. no LDAP, no SSO...). See https://github.com/sympa-community/sympa/issues/300 for details

## Obsoleted `sympa.conf` parameters

These parameters were used in `sympa.conf` or `robot.conf` on Sympa 6.2.56 or earlier and are no longer recommended.

### `arc_private_key_path`

See [`arc_parameters.arc_private_key_path`](#arc_parametersarc_private_key_path).

### `arc_selector`

See [`arc_parameters.arc_selector`](#arc_parametersarc_selector).

### `arc_signer_domain`

See [`arc_parameters.arc_signer_domain`](#arc_parametersarc_signer_domain).

### `archive_mail_access`

See [`archive.mail_access`](#archivemail_access).

### `archive_web_access`

See [`archive.web_access`](#archiveweb_access).

### `bounce_halt_rate`

See [`bounce.halt_rate`](#bouncehalt_rate).

### `bounce_warn_rate`

See [`bounce.warn_rate`](#bouncewarn_rate).

### `d_edit`

See [`shared_doc.d_edit`](#shared_docd_edit).

### `d_read`

See [`shared_doc.d_read`](#shared_docd_read).

### `default_archive_quota`

See [`archive.quota`](#archivequota).

### `default_bounce_level1_rate`

See [`bouncers_level1.rate`](#bouncers_level1rate).

### `default_bounce_level2_rate`

See [`bouncers_level2.rate`](#bouncers_level2rate).

### `default_list_priority`

See [`priority`](#priority).

### `default_max_list_members`

See [`max_list_members`](#max_list_members).

### `default_remind_task`

See [`remind_task`](#remind_task).

### `default_shared_quota`

See [`shared_doc.quota`](#shared_docquota).

### `default_sql_fetch_timeout`

See [`sql_fetch_timeout`](#sql_fetch_timeout).

### `default_ttl`

See [`ttl`](#ttl).

### `dkim_header_list`

See [`dkim_parameters.header_list`](#dkim_parametersheader_list).

### `dkim_private_key_path`

See [`dkim_parameters.private_key_path`](#dkim_parametersprivate_key_path).

### `dkim_selector`

See [`dkim_parameters.selector`](#dkim_parametersselector).

### `dkim_signer_domain`

See [`dkim_parameters.signer_domain`](#dkim_parameterssigner_domain).

### `dmarc_protection_domain_regex`

See [`dmarc_protection.domain_regex`](#dmarc_protectiondomain_regex).

### `dmarc_protection_mode`

See [`dmarc_protection.mode`](#dmarc_protectionmode).

### `dmarc_protection_other_email`

See [`dmarc_protection.other_email`](#dmarc_protectionother_email).

### `dmarc_protection_phrase`

See [`dmarc_protection.phrase`](#dmarc_protectionphrase).

### `tracking`

See [`tracking.tracking`](#trackingtracking).

### `tracking_default_retention_period`

See [`tracking.retention_period`](#trackingretention_period).

### `tracking_delivery_status_notification`

See [`tracking.delivery_status_notification`](#trackingdelivery_status_notification).

### `tracking_message_disposition_notification`

See [`tracking.message_disposition_notification`](#trackingmessage_disposition_notification).

# FILES

- `/etc/sympa/sympa.conf`

    Sympa main configuration file.

- `$SYSCONFDIR/<mail domain name>/robot.conf`

    Configuration specific to each mail domain.

- `$EXPLDIR/<list name>/config`
or `$EXPLDIR/<mail domain name>/<list name>/config`

    List main configuration file.

# SEE ALSO

_Sympa Administration Manual_.
[https://sympa-community.github.io/manual/](https://sympa-community.github.io/manual/).

[auth.conf(5)](./auth.conf.5.md),
[charset.conf(5)](./charset.conf.5.md),
[crawlers\_detection.conf(5)](./crawlers_detection.conf.5.md),
[edit\_list.conf(5)](./edit_list.conf.5.md),
[ldap\_alias\_manager.conf(5)](./ldap_alias_manager.conf.5.md),
[nrcpt\_by\_domain.conf(5)](./nrcpt_by_domain.conf.5.md),
[sympa\_scenario(5)](./sympa_scenario.5.md),
[topics.conf(5)](./topics.conf.5.md).
