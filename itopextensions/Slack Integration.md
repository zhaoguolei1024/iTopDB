# Slack Integration

- name:

  Slack Integration

- version:

  17.4.0

- release:

  2017-12-20

- description:

  Send notification to Slack

- itop-version-min:

  2.0.0

- keyword:

  [slack](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dslack), [notification](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dnotification), [action](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Daction), [trigger](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dtrigger)

- dependencies:

  itop-config-mgmt

- author:

  ITOMIG GmbH

[Buy it](https://www.itomig.de/fr_FR/shop/product/itop-slack-integration-203?search=slack)

This extension adds the capability to send notifications based on actions and triggers to collaboration tool [Slack](http://slack.com/). This page describes how to configure and work with the extension in order to send notifications to Slack.

## Features

By default the only available kind of action consists in sending email. This extension defines a new type of Action: Slack Notification. You are able to:

- Send notifications to Slack
- Configure the target of the notification (slack workspace, channel, person)
- Configure display bot name of the incoming notification in Slack
- Format the messages by adding Headlines, links, edit the color etc.
- notice and react faster to changes in your iTop

## Revision History

| Version | Release Date | Comments         |
| ------- | ------------ | ---------------- |
| 17.4.0  | 2017-12-20   | Initial release. |

## Limitations

- While iTop works with HTML to format messages, Slack uses an own markdown like language. This extensions transform HTML to markdown. But due to the limitations of the slack markdown currently images will not send to Slack and headings will only be displayed as bold.
- Until now it is not possible to send slack notifications asynchronous. So keep an eye on the config parameter “timeout”.

## Requirements

- Existing [Slack workspace](https://slack.com/create)
- Configured [webhook](https://get.slack.help/hc/en-us/articles/115005265063-Incoming-WebHooks-for-Slack)
- URL of the webhook (it looks like: `https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX`)

## Installation

- Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.
- Check `Slack Integration` in the list of extensions at the end of the interactive wizard.

## Configuration

The following settings are available to configure the module:

| Parameter         | Type    | Description                                                  | Default Value |
| ----------------- | ------- | ------------------------------------------------------------ | ------------- |
| certificate_check | boolean | Whether to check the ssl certificate of slack server.        | true          |
| certificate_file  | string  | Path to an custom certificate file.                          |               |
| timeout           | Integer | Determine how many seconds iTop shall wait for a response of Slack | 5             |

## Usage

Slack Notification is a special type of Action. It is based on [Action/Triggers](https://www.itophub.io/wiki/page?id=2_4_0%3Aadmin%3Anotifications). The usage is quite similar to an email notification.

To view your Slack notifications use the link “Notifications” in the “Admin tools” menu and click on the tab “Actions”.

[![img](https://www.itophub.io/wiki/media?w=400&tok=f26bfa&media=extensions%3Aslack_integration.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitomig-slack-integration&media=extensions%3Aslack_integration.png)

See the example Slack Notification “Send ticket information to Slack”
The installation of this extension provides a sample Slack notification “Send ticket information to Slack”. Have a look at this to learn how to build your own notifications.

### Creating a Slack notification action

To create a new action, go to the “Actions” tab and click on “New…”. The following wizard appears: [![img](https://www.itophub.io/wiki/media?w=600&tok=23ff1e&media=extensions%3Aslack_create.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitomig-slack-integration&media=extensions%3Aslack_create.png)

The mandatory fields for a slack notification are:

- Name: iTop Name of the Slack Notification
- Slack URL: URL of the Slack webhook. (see: https://get.slack.help/hc/en-us/articles/115005265063-Incoming-WebHooks-for-Slack)
- Status: Only in state production notifications will send to slack (Default: Being tested)
- Debug trace: If enabled the extension writes an on log for debug purpose in `log/slackintegration.log` (Default: no)

Without any other Information iTop will send an empty notification to Slack.

### Edit Slack connection information

Beside the Slack URL you are able to specify the following attributes:

- Channel or Person: If you enter a channel name (i.e. #general) or a person name (i.e. @personname) the message will to this channel or person. If left blank the message will send to the default channel configured in the Slack webhook.
- App name: Enter a bot name which will displayed as the sender name of the notification in slack. If left empty the default name configured in the slack webhook will be displayed.

### Message Text and placeholders

You can add content to your notification by editing the attribute “simple text”. It is possible to format your message via HTML and add placeholders. Placeholders works in the same way like they do in the email notification. Fore more information please see [this site](https://www.itophub.io/wiki/page?id=2_4_0%3Aadmin%3Anotifications#message_contents_and_placeholders).

### Add Slack attachment

For an improved formatting you can use a [slack message attachment](https://api.slack.com/docs/message-attachments). An attachment will be shown below the simple text, indented and marked with a color at the left side.

[![img](https://www.itophub.io/wiki/media?w=300&tok=d5ba9d&media=extensions%3Aslack_attachment.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitomig-slack-integration&media=extensions%3Aslack_attachment.png)

To enable the attachment set the attribute “Use an attachment?” to “yes” and edit the following attributes:

- Attachment title: Title above the attachment text.
- Attachment link: Enter an OQL query to an Object. The Slack notification will add a link to the attachment title pointing to the Object defined in the OQL. If the OQL matches more than one object currently just the first object will be linked. You are allowed to use placeholders in the OQL. For instance:

```
SELECT Ticket WHERE id= :this->id
```

- Attachment Color: Specify the color of the attachment message by using hexadecimal color value
- Attachment Text: Text of the attachment. You are able to using HTML and placeholders.
- Attachment Fallback: Fallback in case of Slack is not able to display the the Attachment (i.e. in a notification preview) You are able to using HTML and placeholders.

### Add Trigger to a Slack notification

To define **when** an notification have to be sent, you have to define a Trigger and link the notification to the trigger. Switch to the tab “Related Triggers” an click “Add Triggers…” to add an existing Trigger to your Notification. [![img](https://www.itophub.io/wiki/media?w=600&tok=3d1910&media=extensions%3Aadd_trigger_slack.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitomig-slack-integration&media=extensions%3Aadd_trigger_slack.png)