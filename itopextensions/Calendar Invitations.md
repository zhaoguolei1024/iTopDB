# Calendar Invitations

- name:

  Calendar Invitations

- description:

  Send a meeting request as an attachment of a mail notification

- version:

  1.0.4

- release:

  2018-11-28

- itop-version-min:

  2.3.0

- download:

  https://store.itophub.io/en_US/products/itop-icalendar-action

- code:

  itop-icalendar-action

- state:

  stable

This extension provides a new type of “Action” which can be associated with any trigger: Calendar Invitation

## Features

- Send an invitation (also known as meeting request) to any number of recipients defined by an OQL query (with placeholders)
- If the End Date is not provided, the duration of the meeting is 1 hour

## Revision history

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2018-11-28 | 1.0.4   | * Fix invitations when end date was prior to start date * Handle empty start date * Add Combodo license |
| 2018-11-27 | 1.0.3   | Add support for different data time formats                  |
| 2018-08-28 | 1.0.2   | Compatibility improvement for Outlook, Zimbra.               |
| 2016-02-09 | 1.0.1   | First official release of the component. Includes a fix for building the attachments in “Test” mode. |

## Limitations

- The 15min reminder added to the invitation does not seem to be taken into account.

## Requirements

iTop 2.3.0 or above

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.
When prompted with the list of extensions to install, check **Calendar Invitations**.

## Configuration

There is no configuration parameter for this extension in the iTop configuration file.

This extension requires the PHP parameter date.timezone to be set.

For instance date.timezone = Europe/Paris

## Usage

This extension is used to create a new type of “Action” to be associated with Trigger. To create such an action go to “Admin Tools / Notifications”, in the “Actions” tab, click “New…” and pick “Calendar Invitation” from the list.

The following form will be displayed:

[![New Calendar Invitation](https://www.itophub.io/wiki/media?w=600&tok=bc2b81&media=extensions%3Aicalendar-inviation-new.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aicalendar_invitations&media=extensions%3Aicalendar-inviation-new.png)

| Field               | Meaning                                                      | Sample Value                                   |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Name                | Name of the action. Any value that is meaningful to distinguish this action | Invitation for implementing changes            |
| Description         | A longer explanation about the purpose of this action. for information only. |                                                |
| Status              | Whether or not the action is active (= In Production), Being tested or Inactive. | In Production                                  |
| Test Recipient      | An email address for testing the notification. used when the status is “Being tested”. | test@demo.com                                  |
| From (address)      | The email address used as the sender of the email. Depending on its security settings, your mail server may block the email if the sender is not a valid email address | itop@demo.com                                  |
| From (label)        | A human readable label for the above email address. Will be used in the description of the invitation. | ITop Change Management                         |
| Reply To            | The email address to which the replies must be addressed, if different from the “From (address)”. |                                                |
| To                  | An OQL query which returns the list of the mandatory attendees to the meeting. Placeholders are supported, prefixed with a colon (`:`) | SELECT Person WHERE id=:this->agent_id         |
| CC                  | An OQL query which returns the list of the mandatory attendees to the meeting. Placeholders are supported, prefixed with a colon (`:`) | SELECT Person WHERE id=:this->changemanager_id |
| Subject             | The subject of the email. Placeholders are supported, surrounded by `$`. | Invitation for implementing $this->ref$        |
| Start Date/Time     | The start date and time of the meeting. The format is YYYY-MM-DD hh:mm:ss. Placeholders are supported, surrounded by `$`. | $this->start_date$                             |
| End Date/Time       | The start date and time of the meeting. The format is YYYY-MM-DD hh:mm:ss. Placeholders are supported, surrounded by `$`. If this field is left blank, the meeting is assumed to have a duration of one hour. |                                                |
| Meeting Subject     | The subject of the meeting. Placeholders are supported, surrounded by `$`. If this field is left blank, the subject of the email will be used. |                                                |
| Meeting Description | A longer description for the meeting. Placeholders are supported, surrounded by `$`. | $this->hyperlink$                              |
| Meeting Location    | A location for the meeting. Placeholders are supported, surrounded by `$`. |                                                |

Don't forget to associate the action with a Trigger, otherwise it will never be activated.