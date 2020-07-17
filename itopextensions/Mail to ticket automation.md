# Mail to ticket automation

- name:

  Mail to ticket automation

- description:

  Scan several mailboxes to create or update tickets.

- version:

  3.1.1

- release:

  2019-11-22

- itop-version-min:

  2.3.0

- code:

  combodo-mail-to-ticket-automation

- state:

  stable

- alternate-name:

  Ticket Creation from eMails

- diffusion:

  iTop Hub

**Other versions of this component:** [2.2](https://www.itophub.io/wiki/page?id=extensions%3Aticket-from-email_2_2), [2.6.12](https://www.itophub.io/wiki/page?id=extensions%3Aticket-from-email_2_6)

## Summary

This extension runs in the background to scan the defined mail inbox(es) and either create or update tickets based on the content of the incoming emails.

- On Ticket creation, it fills the **description** of the ticket with the **content** of the email, set the caller, the customer, copy attachments, add contacts and many other fields…
- On Ticket update, it extracts as best as possible, the **last reply part** of the email to update the **Public Log** of the ticket, copy attachment, change the status of the ticket and add contacts

## Features

- Determine if the sender is an existing Person (found by its email), then based on configuration it can reject the email in error or create a new Person.
- Determines whether a Ticket must be created or updated based either on the custom headers added by iTop in the eMail (in case of replies) or based on a configurable pattern in the title
- Connect to any mailbox using either the POP3 or IMAP protocol
- Interactive configuration of the mail inboxes
- Processes the incoming eMails in both HTML or plain text format
- Support both Incidents and User Request tickets
- Ticket's attachments are automatically turned into attachments of the Ticket (“dangerous” types of attachments can be excluded)
- Automatic detection of duplicate attachments (like signature images)
- Keeps the messages in the mailbox until the corresponding Ticket is either closed or deleted
- Manual retry in case an error occurs when processing an eMail
- Images embedded inside an HTML mail are displayed inline in iTop as well.
- Images “too small” (below configurable dimensions) are **not** imported as attachments (to exclude signatures)
- Images bigger than configurable dimensions can be resized automatically before uploading into iTop
- “Inline images” are displayed at a reduced (configurable) size and can be “zoomed-in” by clicking on them.
- Automatically reject “Autoreply” emails, based on a set of configurable patterns to be tested against the subject of the email
- Add the other recipients of the email (To: and CC:) as additional contacts on the ticket (configurable). The contact must already exist with that exact email, it won't be created, just linked to the Ticket..
- Apply a stimulus (configurable, depending on the state of the ticket) to change the state of the ticket upon reception of an email.
- Add a new type of Trigger: **Trigger (when updated by mail)** which allow to notify when a Ticket is updated through a received email.

If you want to trigger a Notification '(on object creation)' limited to Ticket created by email, use **origin='email'** in the OQL.

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2019-11-22   | 3.1.1   | * Compatibility with iTop 2.7 * Fix bad encoded non breaking space by outlook * Update DE translations * ID for incoming email are checked from reference |
| 2019-05-21   | 3.1.0   | * Contacts in To/cc with the same email as current mailbox are not added to the ticket anymore * Handle signed emails with an “enveloped format” * Store eml for all the messages |
| 2019-03-19   | 3.0.17  | Dictionnaries internal updates                               |
| 2019-03-13   | 3.0.16  | * Store eml for message in error * Error log attached to the corresponding message |
| 2018-12-19   | 3.0.15  | * Update spanish translations (Thanks to Miguel Turrubiates) * JQuery compatibility (JQuery 3 since iTop 2.6) * Fix OQL used to set caller_id (thanks Jeffrey ! SF#1628) * Fix invalid ES dictionary (“UTF-8 Characters Malformed” error) * Fix unnecessary trace 'invalid line in the “stimuli” configuration' when no stimulus is configured |
| 2018-06-27   | 3.0.14  | Add DE translation                                           |
| 2018-03-01   | 3.0.13  | Fix corrupted (binary) attachments on some emails (none UTF8 emails and wrong content-transfer-encoding format). |
| 2018-02-21   | 3.0.12  | Enable 2.5.0 menu overriding capabilities.                   |
| 2018-02-06   | 3.0.11  | Fix attachments stored as inline images when content-disposition was not specified correctly. |
| 2018-02-05   | 3.0.10  | Fix PHP 5.3 compatibility broken in revision 3.0.8           |
| 2018-01-29   | 3.0.9   | Allow trigger to filter with an OQL                          |
| 2018-01-25   | 3.0.8   | SPAM messages flagged as 'undesired' and deleted after a delay. An generic email reply can be sent in case of 'Unknown caller'. Update Russian translation |
| 2017-08-28   | 3.0.7   | Duplicated dictionary entries collision during CSV import (attributes behavior and error_behavior from MailInboxStandard class). |
| 2017-03-31   | 3.0.6   | EmailReplica error message would throw a fatal error if it could not be persisted to DB (eg. With 4 bytes unicode characters). We now save a default error message when it is not possible to persist it, and we dump the original message in the IssueLog. |
| 2016-11-10   | 3.0.5   | Now supports several MailInbox scanning a single email address mailbox, as long as they have distinct folders (Mailbox (for IMAP) property). Also, fixed a regression introduced in 3.0.x, use_message_id_as_uid configuration parameter was not working anymore. |
| 2016-10-05   | 3.0.4   | Support of inline images in messages issued by Lotus Notes.  |
| 2016-08-26   | 3.0.3   | Fixed regressions introduced in 3.0.x: Apply stimulus not working. CRON interrupted by a fatal error when the sender is unknown (in case of a ticket update). Empty description if the target field is in plain text. Losing CR in the case log if the email is in plain text (email created with thunderbird, and no rich text formatting) |
| 2016-08-09   | 3.0.2   | Make sure that the setup does not crash if some of the prerequisites (PEAR or IMAP) are not installed. |
| 2016-07-26   | 3.0.1   | Support of adding more contacts (To: and CC:) to the ticket. Ability to apply a stimulus (to change the state of a ticket) when receiving an update by email. |
| 2016-06-07   | 2.6.12  | Security: only administrators can see the password of mail inboxes. Regression: properly import all attachments (not only the last one if it's not an image). Enhancement: preserve hyperlinks when converting from HTML to plain text. |
| 2016-02-02   | 2.6.11  | Developers only: fixed a compatibility issue with alternatives to the module itop-standard-email-synchro. The regression has been introduced in 2.6.6 and does not impact the behavior of the component unless you have developped your own alternative to itop-standard-email-synchro. |
| 2015-10-28   | 2.6.10  | Automatically reject “Autoreply” emails (cf `undesired-subject-patterns` below). Support of emails with no subject. |
| 2015-09-29   | 2.6.9   | Properly initialize ENUM values (#1102), prevent updating tickets of a different class than the one configured in the mail inbox. |
| 2015-03-09   | 2.6.8   | Fixed the processing of the `images_maximum_size` parameter to prevent errors when the images are not to be resized. Fixed the pattern for detecting `blockquote` tags inside HTML replies. |
| 2015-03-05   | 2.6.7   | Suppressed a warning when ignoring small images. Change the default value for “body_parts_order”. |
| 2015-01-21   | 2.6.6   | Support of inline images, filtering of “too small” images and resizing of “big” images. |
| 2014-08-01   | 2.6.5   | New configuration parameter to workaround a problem with Gmail/IMAP. |
| 2014-07-21   | 2.6.4   | Enhancement: allow to delete the emails from the server immediately after processing them. French translation of the “TriggerOnMailUpdate” and make the trigger importable. |
| 2014-06-04   | 2.6.3   | Enhancement: support the creation of Change and Problem tickets. |
| 2014-04-09   | 2.6.2   | Bug fix in order to support mailboxes containing a backslash in their name (likely to happen using IMAP). |
| 2014-04-08   | 2.6.1   | Addition of the German localization (though it's not 100% translated). |
| 2014-03-05   | 2.6.0   | Improved error processing (e.g. keeping the errors in the mailbox, manual retry) and better decoding of the “new part” of the message when it is a reply. Enhanced HTML to text conversion, fixed the processing of “Outlook's forwarded messages” as attachments. |
| n/a          | 2.5     | Support of several mail inboxes. Interactive configuration of the mail inboxes via the iTop user interface. Various improvements for the parsing/decoding of the eMails |
| 2013-07-22   | 2.2     | “Legacy” version supporting only one mailbox (configured from the iTop configuration file). The documentation for this version is available here: [Ticket Creation from eMails (legacy)](https://www.itophub.io/wiki/page?id=extensions%3Aticket_creation_from_emails) |

## Requirements

- PHP 5.2.1+ with the [IMAP extension](http://www.php.net/manual/en/book.imap.php) enabled if you want to connect to an IMAP server, or [PEAR::NetSocket](http://pear.php.net/package/Net_Socket) (iTop comes with its own copy of PEAR::POP3) if you want to connect to a POP3 server.
- A connection to a POP3 or IMAP server with a valid mailbox.
- [cron.php](https://www.itophub.io/wiki/page?id=latest%3Aadmin%3Acron) must be running to enable the processing of incoming eMails.
- For the debug trace, [PHP MBString](https://www.php.net/manual/en/book.mbstring.php) must be installed.
- For resizing big images, [PHP GD](https://php.net/manual/en/book.image.php) must be installed.

On Ubuntu 16.04 the prerequisites can be installed using the `php-pear`, `php-net-socket` and `php-imap` packages:

```
sudo apt-get install php-pear php-net-socket php-imap
```

## Installation & upgrade

- Expand the content of the zip file in the “extensions” folder of iTop.

**Compatibility issue**: for iTop version lower than 2.4.0, there is a [special installation/upgrade process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation#itop_before_240).

- Make sure that the web server has enough rights to read all the files in the “extensions” folder.
- Launch the setup program, and when prompted for the list of extensions to install, check “Mail to ticket automation” from the list

Using IMAP on Ubuntu (prior to 16.04): the package php5-imap does not enable the IMAP module. To use the IMAP module on Ubuntu you must install it and then enable it explicitly:

```
sudo apt-get install php5-imap
sudo php5enmod imap
```

In any case, you may need to restart the web server to take into account the newly installed packages:

```
sudo service apache2 restart
```

# Usage

## Data Mapping

When creating a new ticket from an incoming email message, the application automatically fills the following fields of the ticket:

- **Title** = subject of the mail
- **Description** = body of the mail
- **Caller** (caller_id) = sender of the mail (identified by her/his email address)
- **Organization** (org_id) = organization of the caller
- **Origin** (if this field exists on the ticket) = 'mail'

Default (i.e. constant) values **must** be supplied, via the “Ticket Default Values” setting, for any other mandatory field of the Ticket, otherwise the creation of the Ticket will fail.

When updating an existing Ticket, the application add an entry into the **public_log** field (configurable, see below), with the “new part” of the message. See below for more explanation about how the “new part” is extracted from the message.

## Specifying default values

The syntax for specifying default values is the following:

- One field per line, with the syntax:
- `field_code:default_value`

If the field to initialize is a key to another object (for the fields like org_id, service_id, etc…) you can specify either the numeric identifier of the target object (e.g. `service_id:153`) or its name (e.g. `org_id:Demo`), provided that the name is unique.

The default values are applied *after* the standard data mapping described above. Therefore it is possible to override the default data mapping with some constant values.

If the incoming email has no subject, you can specify the default title to be set for the Ticket via the field “Default Title (if subject is empty)”. This is different from the default values listed above, since this value will be used only if the email has no subject. If the “Default Title (if subject is empty)” the system will supply a default value (“No Subject”) since the title is mandatory to create the Ticket.

# Configuration

The behavior for each mailbox (which messages to process and whether to create or update a Ticket) is managed via the menu “Incoming eMail Inboxes” in the “Admin tools” section:

![img](https://www.itophub.io/wiki/media?media=extensions%3Aemail-synchro-menu.png)

Click, “Create a new Mail Inbox” to create a new configuration for a mail inbox. This displays the following form:

[![New mail inbox](https://www.itophub.io/wiki/media?w=600&tok=89f538&media=extensions%3Amailboxinbox-details.png)](https://www.itophub.io/wiki/media?media=extensions%3Amailboxinbox-details.png)

## Mailbox Configuration

The “Mailbox configuration” defines how the application connects to the mail inbox:

| Field              | Meaning                                                      | Sample Value                        |
| ------------------ | ------------------------------------------------------------ | ----------------------------------- |
| Mail Server        | The IP address or fully qualified hostname of the mail server | 10.153.20.142 or pop3.mycompany.com |
| Login              | The name of the mail account used for connecting to the mailbox | test@mycompany.com                  |
| Password           | The password for the above mentioned account                 |                                     |
| Protocol           | The protocol to connect to the mail server: either POP3 or IMAP. If you need to use IMAP with SSL or TLS, refer to the imap_options configuration parameter below. | POP3                                |
| Port               | The TCP port to connect to the server. The standard values are 110 (secured: 995) for POP3 and 143 (secured: 993) for IMAP | 110                                 |
| Mailbox (for IMAP) | The IMAP mailbox (folder) to scan for incoming messages. If omitted the default (root) mailbox will be scanned. This option is ignored when using the POP3 protocol. | INBOX.Folder.Subfolder              |
| Active             | If set to “Yes”, the inbox will be polled. Otherwise no.     | Yes                                 |
| Debug trace        | Use this setting for tracing all the background operations related to this inbox for debugging and troubleshooting purposes. It is not recommended to activate this option for long periods on production since it tends to generate a lot of output which slows down the server | No                                  |

## Emails in Error

This section defines the behavior when an incoming email cannot be processed properly. The email can be either kept in the mailbox (and remembered as an “Error” and no longer processed) or deleted immediately from the mailbox. Furthermore the original message can be forwarded to an administrator (as an attachment) along with some explanation about the cause of the error.

| Field             | Meaning                                                      | Sample Value                    |
| ----------------- | ------------------------------------------------------------ | ------------------------------- |
| Behavior          | Whether or not the emails processed with an error should be kept in the mailbox. If so, the message will be flagged as “Error” and no longer processed, but still available for reading from the mailbox. | Keep the message in the mailbox |
| Forward eMails to | The email address to which to forward the email when an error occurs. The forwarded message contains some explanation about the error and the original email as an attachment. If this address is left empty, the incoming emails which cannot be processed will simply be deleted from the inbox without further notice. | itopadmin@mycompany.com         |
| (From)            | The IP address to be used as the “sender” of the error notification. For security reasons, many mail servers do not relay messages if the sender address is not a known address. | itopadmin@mycompany.com         |

## Behavior on Incoming eMails

This section defines the behavior of the application when processing incoming emails.

| Field                               | Meaning                                                      | Sample Value                      |
| ----------------------------------- | ------------------------------------------------------------ | --------------------------------- |
| Behavior                            | The behavior when a new message arrives in the inbox. The possible values are: **Create or Update**: create a new Ticket or Update an existing one if a matching Ticket is found **Create new ticket**: each new message creates a new Ticket **Update existing tickets**: all incoming messages which do **not** match an existing Ticket are treated as errors. | Create or Update                  |
| After processing the eMail          | The action to be taken after successfully processing an incoming eMail: either keep the eMail on the mail server (until the associated ticket is closed or deleted) or delete the eMail immediately. | Keep the eMail on the mail server |
| Ticket Class                        | The class of Tickets to create or update when receiving an email. Make sure that you select a valid class for your iTop configuration. | User Request                      |
| Ticket default Values               | The syntax for “Ticket Default Values” and “New Person's Default Values” are: - one field to initialize per line - `<field_code>:<constant_value>` | service_id:Networking             |
| Default Title (if subject is empty) | The value to be used as the title of the Ticket, if the subject of the incoming email is empty. If this field is left empty the system will supply a default value (“No Subject”) | Empty subject                     |
| Title pattern                       | Each notification sent by the application contains a reference to the “source” Ticket in the MessageID field of the email. Email client applications generally store this identifier in the “in-reply-to” or “references” header of the reply email. This is the primary mean of identifying that an email message is related to a ticket. If this header is not present in the incoming message, the application can parse the “subject” field to look for a given match. This pattern determines how to parse the subject. The pattern specified here must follow the [PCRE](http://www.php.net/manual/en/reference.pcre.pattern.syntax.php) syntax. | /R-([0-9]{6})/                    |
| Stimuli to apply                    | A list of `state_code`:`stimulus_code` (one per line) to define the stimulus to apply (after updating a ticket), for the given state of the ticket. This is useful for example to automatically reassign a ticket which is in the state “pending”. | pending:ev_assign                 |

## Unknown Callers

This section determines the behavior of the application when the sender of an email (From:) does not correspond to a known email address in the application. There are two possibilites:

- Reject the eMail: the incoming email is treated as an error and thus either forwarded to an administrator or deleted.
- Create a new person: a new Person will be created based on the email of the sender and constant values defined below.

| Field                              | Meaning                                                      | Sample Value                                     |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------ |
| Behavior in case of Unknown Caller | What to do when the sender of the incoming email message does not correspond to any Person recorded in the application | Create a new person                              |
| Unknown Caller rejection reply     | Optional reply to sender when the unknown caller behavior is set to “Reject the eMail” (no message is sent when left empty) | empty                                            |
| New Person's Default Values        | Default values for initializing the new Person. The application automatically fills the `email` field with the email address of the sender of the message. All other mandatory fields must be initialized with constant values provided here, otherwise the creation of the new Person will fail. | `first_name:Unknown` `name:Caller` `org_id:Demo` |

## Behavior for Additional Contacts

This section determines the behavior of the application regarding the additional recipients of the incoming email (persons in To: and CC: of the message). It is possible to specify if/when the email addresses which correspond to a valid contact in iTop are added to the ticket (via the `Contacts` tab). Email addresses which do not correspond to a valid contact in iTop are *always* ignored.

| Field                      | Meaning                                                      | Sample Value |
| -------------------------- | ------------------------------------------------------------ | ------------ |
| Add more contacts (To, CC) | Whether or not to add the To: and CC: email addresses as additional contacts to the ticket. The possible values are: * `Never`: no additional contact will be added * `Always`: additional contacts will be added when creating and updating a ticket * `When creating a ticket`: additional contacts will be added only when creating a new ticket * `When updating a ticket`: additional contacts will be added only when updating an existing ticket | Never        |

## Other configuration parameters

In addition to the configuration performed by creating a Mail Inbox object using the user interface of the application, a few parameters are available in the configuration file to fine tune the behavior of the application.

The parameters listed below apply to **all** the Mail Inboxes

The recommended value for the configuration parameter `body_parts_order` is `text/html,text/plain`. Indeed in order to properly import the images embedded inside an HTML email, the HTML version of the email must be processed instead of the plain text version.

```
   'combodo-email-synchro' => array (
      'debug' => false,
      'periodicity' => 30,
      'body_parts_order' => 'text/html,text/plain',
      'pop3_auth_option' => 'USER',
      'imap_options' => array (
            0 => 'imap',
      ),
      'exclude_attachment_types' => array (
            0 => 'application/exe',
      ),
      'maximum_email_size' => '10M',
      'recommended_max_allowed_packet' => 10485760,
      'introductory-patterns' => array (
            0 => '/^le .+ a écrit :$/i',
            1 => '/^on .+ wrote:$/i',
            2 => '|^[0-9]{4}/[0-9]{1,2}/[0-9]{1,2} .+:$|',
      ),
      'multiline-delimiter-patterns' => array (
            0 => '/\\RFrom: .+\\RSent: .+\\R/m',
            1 => '/\\R_+\\R/m',
            2 => '/\\RDe : .+\\R\\R?Envoyé : /m',
            3 => '/\\RDe : .+\\RDate d\'envoi : .+\\R/m',
            4 => '/\\R-----Message d\'origine-----\\R/m',
            5 => '/\\RExpéditeur: .+\\RDate:/m',
            6 => '/\\RDe : .+\\RDate : /m',
            7 => '/\\TO:.+\\RCC:/m',
      ),
      'delimiter-patterns' => array (
            '/^>.*$/' => false,  // "false" remove only the line, "true" remove the rest of the message
      ),
      'big_files_dir' => '',
      'use_message_id_as_uid' => false, // Don't change this unless you know what you are doing!
      'images_minimum_size' => '100x20',
      'images_maximum_size' => '',
      'undesired-subject-patterns' => array (
            0 => '/^Out Of Office/i',
            1 => '/^Automatic answer$/i',
            2 => '/^Réponse automatique:/',
      ),
      'undesired-purge-delay' => 7,
      'html-tags-to-remove' => array(
           'blockquote' => array(), 
           // No class specified, remove any blockquote tag
           'div' => array('gmail_quote', 'moz-cite-prefix'),
           'pre' => array('moz-signature'),
      );
 
   ),
```

| Parameter                      | Meaning                                                      | Default Value                   |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------- |
| debug                          | Set to true to turn on debug output                          | false                           |
| periodicity                    | Interval (in seconds) at which to check for incoming messages | 30                              |
| body_parts_order               | Comma separated, ordered, list of MIME types, determining the preferred part of the message to retrieve for populating the `description` or `public_log` of the Ticket. In order to import as inline images the images embedded in HTML, the HTML part of the email must be processed in priority over the text part. Therefore the recommended configuration is `text/html,text/plain`. | text/html,text/plain            |
| pop3_auth_options              | POP3 authentication options. Possible values are: 'CRAM-MD5', 'APOP' , 'PLAIN' , 'LOGIN', 'USER' | USER                            |
| imap_options                   | Additional IMAP options. Possible values are listed here: [IMAP flags](http://www.php.net/manual/en/function.imap-open.php). For example to use SSL you could specify : `array(0 ⇒ 'imap', 2 ⇒ 'ssl')` **Warning**: Do NOT use the `pop3` flag to connect to a POP3 mailbox using the PHP IMAP extension. Due to a limitation of the IMAP extension this will not work! If you want to connect to a POP3 server, use the POP3 protocol instead. | array('imap')                   |
| exclude_attachment_types       | Array of MIME types to exclude when retrieving attachments   | array('application/attachment') |
| html-tags-to-remove            | **new in 3.0.0** Used for computing the “new part” of HTML messages by removing the specified tags. The syntax is an array of `tag_name` => array of CSS class names. | *see above*                     |
| maximum_email_size             | If an incoming email is bigger than the specified size, the message will saved to the `big_files_dir` if it is configured and deleted from the inbox. A notification message will be sent to the administrator as for other “errors” happening when processing the mail inbox. The size can be specified using the 'short' notation: 100K, 3M, 2G… If set to zero, no limit will be enforced… with the risk of a PHP crash if there is not enough memory to decode an incoming email. | 10M                             |
| introductory-patterns          | **only for plain text emails** When computing the “new part” of a message, lines matching this pattern and preceding what looks like an “old part” of the message, are removed. Adapt this list to your localization… and favorite email client dialect. The pattern specified here must follow the [PCRE](http://www.php.net/manual/en/reference.pcre.pattern.syntax.php) syntax. | *see above*                     |
| multiline-delimiter-patterns   | **only for plain text emails** and **only for mail for ticket update** Multi-line regular expression patterns used for computing the “new part” of a message. each of theses patterns determine the beginning of the “old part” of a message, when a message is a “Reply” to another message. Everything that matches this pattern (and all the text that follows this match) will be removed for the “new part”. All patterns are tested successively. The pattern that provides a match closer to the beginning of the text will be used. Adapt this list to your localization and to the dialect of your favorite email clients… Patterns must follow the [PCRE](http://www.php.net/manual/en/reference.pcre.pattern.syntax.php) syntax. | *see above*                     |
| delimiter-patterns             | **only for plain text emails** and **only for mail for ticket update** this regular expression patterns are used for detecting the lines beginning “old part” of a message, in case none of the multiline-delimiter-patterns did match. Patterns must follow the [PCRE](http://www.php.net/manual/en/reference.pcre.pattern.syntax.php) syntax. | *see above*                     |
| big_files_dir                  | The path to a directory where to store emails bigger than `maximum_email_size`. If this directory is not configured, the emails are simply deleted before notifying the administrator. |                                 |
| use_message_id_as_uid          | Boolean. For IMAP connections only. Whether or not to use the identifier from the message (MessageID) instead of the Mailbox' unique identifier (UID) to uniquely identify the already processed messages. This can be useful to workaround problems when the UID of the messages on the server changes between sessions (like with Gmail). If you toggle this value, make sure that you first empty the mailbox (and stop the cron job), since all messages present in the mailbox when the setting is changed will be considered as new and processed again. | false                           |
| images_minimum_size            | Minimum dimensions for importing images. Images smaller than the given dimensions will be ignored and not imported as attachments. The dimensions are expressed as a string *width*`x`*height* (where *width* and *height* are integer numbers, in pixels). | 100×20                          |
| images_maximum_size            | Images bigger than these dimensions (for example `1000×1000`) will be resized to fit in the given dimensions. The dimensions are expressed as a string *width*`x`*height* (where *width* and *height* are integer numbers, in pixels). **Note** this feature is available only if PHP GD is installed. If no dimensions are given, the images are never resized. |                                 |
| undesired-subject-patterns     | An array of regular expression patterns (as PHP text strings) that will be used to test the subject of the incoming email. If any of these pattern matches, the email will be considered as “undesirable” and rejected (the same processing as for any other error case will then be applied). The patterns specified here must follow the [PCRE](http://www.php.net/manual/en/reference.pcre.pattern.syntax.php) syntax. | array()                         |
| undesired-purge-delay          | Delay in days to remove automatically the undesired messages (0 means that the messages are removed immediately) | 7                               |
| recommended_max_allowed_packet | Display a warning on the 'Mailbox Content' screen if the database parameter 'max_allowed_packet' is less than the one configured | 10*1024*1024                    |

When specifying PCRE patterns inside the configuration file, make sure that you double the backslash characters, since backslashes must be escaped inside PHP litteral text strings.

```
        'itop-standard-email-synchro' => array (
                'ticket_log' => array (
                          'UserRequest' => 'public_log',
                          'Incident' => 'public_log',
                        ),
        ),
```

| Parameter  | Meaning                                                      | Default Value |
| ---------- | ------------------------------------------------------------ | ------------- |
| ticket_log | An associative array (hash) defining, for each class of Ticket, the code of the attribute to set when updating a ticket from an incoming message. You don't need to change this value unless you modified the Data Model. | *see above*   |

# Troubleshooting

## Limitations

- Each mail inbox configured corresponds to one type of Ticket (i.e. User Requests or Incidents, but not both).
- Connecting to a POP3 mailbox via the php IMAP extension does **not** work. You **must** use the POP3 configuration via PEAR::NetSocket for such a case.
- There is no validation that the target class of the Mail Inbox is an existing class in iTop. (i.e. don't try to create incidents if the Incident Management module is not installed).
- The support of inline images works only if the preferred order for email parts is configured as “text/html,text/plain” (i.e. HTML first), which is now the default for all new installations.

When processing an email considered as an update to a ticket, the extensions tries to extract the “new part” of the message (excluding the content from previous messages). However, depending on the format of the reply (which itself depends on the email client software used) it may not be possible to extract this information in a reliable manner. In such a case the whole text of the email will be used. Unfortunately, the widely used MS Outlook is an example of such client software where the replies cannot reliably be identified. Refer to the configuration parameter `html-tags-to-remove` for explanations about how to adjust this behavior.

## Checking the connection

Once the Mail Inbox object has been created, you can use the tab “Mailbox Content” in the details of the object to check that the application can properly connect to the mail server and retrieve messages from it.

![Mailbox Content tab](https://www.itophub.io/wiki/media?w=600&tok=6543e2&media=extensions%3Astandard_mail_inbox.png)

To deeply inspect the content of the mailbox it is always better to use a real mail client application. The view provided in this tab is just use to help troubleshooting connection problems.

This view also allows to perform two different kind of actions on a set of messages:

- “Reset Status”: for messages which are either flagged as “Error” or “Already processed”, this status will be reset and the email will considered again as “New” and thus candidate for processing the next time cron.php runs.
- “Delete eMail”: deletes the message(s) from the mailbox. No confirmation will be asked !!
- “Ignore eMail”: mark new messages as “ignored” to avoid processing them.

## Debugging

**New in 3.0.15**: Access to the eml used and to the message specific logs without activating the debug mode for every processed message.

Since the processing of the incoming emails occurs in the background, it is not always easy to understand what happens when a ticket is not processed as expected. In order to trace the execution of this background task, several levels of tracing are available:

- by setting the “Debug trace” field to “Yes”, more trace will be generated when processing the mailbox. This trace goes to the output of the cron job, and is also captured (limited to 256 KB) in the database. This captured trace is visible in the “Debug Trace” tab of the Mail Inbox object.
- the configuration setting `debug` for the module `combodo-email-synchro` can be set to true in the configuration file. This activates even more traces for all the configured mail inboxes. This additional trace appears only in the output of the cron job.
- the cron job can be passed the optional parameter `--verbose=1` to activate some debug trace for all the background tasks. This additional trace also goes into the output of the cron job.

If the cron job is not already running in the background it is convenient to run it manually from the command line, to see what's happening:

```
php cron.php --auth_user=<user> --auth_pwd=<pwd> --verbose=1
```

![Debug trace tab](https://www.itophub.io/wiki/media?w=600&tok=62b1be&media=extensions%3Aemail-synchro-debug-trace.png)

*Known issue until 3.0.17 included*: When activating debug trace, logging trace may truncate an UTF8 character which breaks MySQL insertion and stop current email processing. Because of this, don't use this mode as a permanent mode, but only for temporary debug.

## Questions & Answers

**Question: Mails are no more processed?**
Answer:

1. It might be due to a email message with a too big attachment, which can end-up crashing the database. In that case, to quickly process the following emails, open the Mail Inbox in iTop, tab: Mailbox Content; identify the faulty email, probably the oldest “new” message and check it and press the `Ignore` button.
2. To limit the above situation, check coherence between `allowed_max_packet`, `recommended_max_allowed_packet` and `maximum_email_size` parameters.
3. It might be due to the cron.php not running

**Question: a particular mail is in error, why?**
Answer: There can be multiple reasons, which leads to flagging a mail in error. When browsing the `Mailbox Content` tab on the `Incoming eMail Inboxes` the error message should explain you the reason. Attachment too big, mail in an unkown format (encrypted for eg.),…