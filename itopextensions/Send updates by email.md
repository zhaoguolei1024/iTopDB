# Send updates by email

- name:

  Send updates by email

- description:

  Send an email to pre-configured contacts when a ticket log is updated

- version:

  1.2.1

- release:

  2019-03-26

- itop-version-min:

  2.0.3

- code:

  combodo-send-updates-by-email

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-send-updates-by-email

- alternate-name:

  Email Reply

- diffusion:

  iTop Hub

For iTop versions older than 2.0.3 use a previous version of this component

**Other versions of this component:** [1.0.3](https://www.itophub.io/wiki/page?id=extensions%3Aemail_reply_1_0)

This extension allows to send an email when updating the case log (either the public log or private log) of a Ticket. Email reply works with any type of Ticket. Attachments added while editing the ticket are automatically sent as attachments to the email.

## Features

This extension allows an administrator to define notifications in order to inform contacts (for instance the caller, or the agent) when a case log is updated on a Ticket.

This allows support agents to communicate with the callers directly by updating either the public log or the private log of the ticket.

The configuration relies on a specific type of Trigger (“on log update”) and the usual Email Actions. The definition of the Trigger object determines which field of the ticket (public_log, private_log…) is used for the feature.

The user can select the attachments to be sent with the message. Newly added attachments are automatically selected but can be manually deselected if needed.

## Limitations

This feature works only with attributes of type “Case log”, since it modifies the case log input.

Any update of the log through the portal will not trigger the notification, use for this the standard trigger `(when updated from the portal)`.

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2019-03-26   | 1.2.1   | Queries performance improvement                              |
| 2018-11-27   | 1.2.0   | * Fix an issue where wrong attachments were sent * JQuery compatibility (JQuery 3 since iTop 2.6) |
| 2018-06-27   | 1.1.14  | DE translation update                                        |
| 2018-06-26   | 1.1.13  | ES translation                                               |
| 2018-01-26   | 1.1.12  | Add Russian translation.                                     |
| 2017-06-14   | 1.1.11  | Support for any type of ticket (used to require the installation of User Request Management). |
| 2016-12-07   | 1.1.10  | Fix for IE9 (removed the placeholder “please enter a comment” on all browsers) since it no longer works with HTML formatted case logs. |
| 2016-07-21   | 1.1.9   | Support of HTML formatted case logs (iTop 2.3.0), but still backwards compatible. |
| 2015-10-26   | 1.1.7   | Allow the module to be installed with only the Incident type of ticket |
| 2015-10-05   | 1.1.6   | Fixed two regressions introduced in 1.1.2: all existing attachments selected by default, fatal error when removing a selected attachment |
| 2015-09-25   | 1.1.5   | Compatibility with iTop 2.2.0 and custom portals (backward compatible) |
| 2015-09-24   | 1.1.4   | TriggerOnLogUpdate: allow read for anyone (category = application instead of bizmodel) |
| 2015-03-05   | 1.1.3   | Bug fix: the file “ajax.php” was missing from the 1.1.2 package. |
| 2015-01-21   | 1.1.2   | Adds the capability for the user to select which attachment to send with the reply. |
| 2014-04-03   | 1.1.1   | Adds the capability to send various notifications, depending on any condition that can be expressed by the mean of an OQL. Fixes issue #850: Contacts added while updating the tickets could not be notified (by the mean of a query in the email action) |
| 2014-03-04   | 1.0.1   | First officially qualified version                           |

## Requirements

Requires an iTop version 2.0.3 or higher.

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

From the *Admin tools/Notifications* menu, create a trigger “when log is updated”, and select the expected object class and case log attribute code:

![Example of a Trigger "on log update"](https://www.itophub.io/wiki/media?w=450&tok=0ea5d3&media=extensions%3Aemail-reply-trigger_with_filter.png)

The optional argument 'Filter' is used to specialize the trigger. The filter is an OQL specifying which objects will be taken into account by the trigger. In the given example, the created trigger will be activated only for User Request having a Service named like “…Network…”.

Create an email action for this trigger. This email action can be configured as follows:

- Status = any active state (e.g 'In production' or 'Being tested')
- TO = `SELECT Person WHERE id = :this->caller_id`
- Body = `Dear $this->caller_id_friendlyname$, … $this->head(public_log)$ …`
- … plus other fields required to send notifications

[![Example of an Email Action](https://www.itophub.io/wiki/media?w=600&tok=7edc0d&media=extensions%3Aemail-reply-screenshot3.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-reply-screenshot3.png)

The installation of the module automatically creates a default Trigger and its associated action (in test mode). As the test email recipient is a dummy address, that cannot work without adjustments.

The feature will not be available if the Email action is not in an active state.

The syntax `$this->head(public_log)$` adds the latest entry from the `public_log` field into the body of the notification.

Starting with iTop 2.3.0, the case log (and the notifications) contain HTML formatted text. There the syntax to add the latest entry of a case log into a notification is `$this->head_html(public_log)$`.

There is one single parameter that can be adjusted in the configuration file:

| Module      | Parameter       | Type    | Description                                                  | Default Value |
| ----------- | --------------- | ------- | ------------------------------------------------------------ | ------------- |
| email-reply | enabled_default | boolean | Determines if the checkbox must be checked by default when the agent opens the form to edit the ticket | true          |

## Usage

Once this extension is installed and configured, you just have to modify the case log of a ticket to use it.

For instance if you modify a User Request, a small check box and paper clip icon appear on top of the public log to define if the public log update should trigger the notification or not:

[![Email Reply on a case log](https://www.itophub.io/wiki/media?media=extensions%3Aemail-reply-screenshot4b.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-reply-screenshot4b.png)

The default behavior of the check box is configured in the iTop configuration file. If you uncheck it, no notification is sent.

All new attachments added during this modification of the Ticket will be sent along with the notification. As soon as a new attachment is added to the Ticket (while it is being edited) the number next to the paper clip increases. Moving the mouse over the paper clip icon displays a small tooltip with the list of files that will be sent as attachments with the notification.

**[new since 1.1.2]** The user can select the attachments to be sent along with the reply, by pressing the “Select Attachments…” button. This displays the following dialog box:

[![Attachments selection](https://www.itophub.io/wiki/media?w=400&tok=82344e&media=extensions%3Aemail-reply-screenshot5.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-reply-screenshot5.png)

Click on the check-box in front of each desired attachment then click “Ok” to validate the choice.

If a filter has been given, it will be taken into account when it comes to activate the trigger for the current object. On the other hand, the clues that say to the end-user “an email will be sent” are always visible. In practice, this is not an issue if you have configured several triggers so that a notification will be sent in ANY case.