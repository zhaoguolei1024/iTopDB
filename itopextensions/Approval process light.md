# Approval process light

- name:

  Approval process light

- description:

  Approve a request via a simple email

- version:

  2.0.1

- release:

  2020-03-18

- itop-version-min:

  2.4.0

- code:

  combodo-approval-process-light

- state:

  stable

- diffusion:

  iTop Hub

**Other versions of this component:** [1.3.5](https://www.itophub.io/wiki/page?id=extensions%3Aapproval_light_1_3)

This module provides the capability to handle a simple approval process for a user request. It notifies a selected approver by email in order to approve or reject a user request. This approver do not need a login in iTop to approve the request.

Only one level of approbation is supported by this module, and the approver has to be selected manually by a support agent

## Features

- Simple approval mechanism with one approver per ticket
- Approvers can approve or reject a request in one click (no need to have an iTop account)
- Tickets waiting for Approval and bulk approval available in Portal.
- Passive or active approval
- Configurable timeout delay
- Graphical view of the approval status on each ticket

## Revision history

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2020-03-18 | 2.0.1   | Fix TWIG template not found when trying to open object form  |
| 2020-03-12 | 2.0.0   | * Add compatibility with iTop 2.7+ * Update DE translations * from and reply_to can be specified in ActionEmailApprovalRequest objects (were only available in approval_base module settings) |
| 2019-03-26 | 1.4.5   | Fix: Approval reminder in edit mode : double pop-up          |
| 2018-12-13 | 1.4.4   | - Add missing reconciliation key to the ApprovalScheme class - Fix UI glitch on approval form - Update spanish translations (Thanks to Miguel Turrubiates!) - Improve jQuery compatibility (jQuery 3 since iTop 2.6) |
| 2018-06-27 | 1.4.3   | DE translation update                                        |
| 2018-06-26 | 1.4.2   | - New translations (ES, BR) and fix CSV import of TriggerOnApprovalRequest. - Fix attachments unavailable in portal when object waiting for approval was not within user's scopes. |
| 2018-01-26 | 1.4.1   | Bug fix: Extension could not be installed if Enhanced Portal was not selected. |
| 2017-11-14 | 1.4.0   | Requires iTop 2.4.0: Include Approval management into Enhanced Portal |
| 2017-11-14 | 1.3.5   | Fix approval tooltips mixed-up between 2 cycles              |
| 2017-09-27 | 1.3.4   | Compatibility fix with iTop 2.4 portal                       |
| 2017-09-01 | 1.3.3   | - Comments recorded in the log: losing carrier returns - Check/Uncheck All on portal summary page - Missing index, slowing down the display of a ticket |
| 2016-11-30 | 1.3.2   | - Emails configured by the mean of triggers/actions - Email/Form templates to use the html placeholders (correctly escaped HTML entities) - The menu group “Helpdesk” cannot be moved by the mean of an XML delta |
| 2016-08-09 | 1.2.1   | - XML-based implementation in order to ease some customizations - include a library for the support of approvals in the enhanced customer portal (requires further customizations though) |
| 2016-07-11 | 1.2.0   | Now requires iTop 2.2.0! - Bug fix: “Portal users” redirected to the customer portal when trying to approve - Date and time correctly formatted (if iTop version >= 2.3.0) |
| 2015-09-29 | 1.1.3   | It is now mandatory to select an approver. It the previous version, leaving the approver undefined would cause the ticket to be in the state “waiting for approval” with no way to get out of there! |
| 2014-12-18 | 1.1.2   | Manually send a reminder ; Support of several executions on the same ticket (works retroactively with data recorded prior to this version) ; Record something into the log even if the comment is left empty (was already done when bypassing the process) ; If an approver already gave her answer the approve/reject menus must be hidden; If a user bypasses the process, and if her account has a contact defined, then the identifier of the user (shown in the header of the new log entry) must be the contact friendly name (not the user login) ; Changed the misleading message “is now complete with failure” into “is now complete with result REJECTED” ; Prevent the CRON from creating one CMDBChange record per minute ; Fixed typos in the french dictionary |
| 2014-04-24 | 1.0.3   | Better error reporting when an email address is wrong or missing. In particular when the module has just been installed, if the configuration entry `sender_email` was left empty this used to produce a scary error message when the email transport was SMTP |
| 2014-03-07 | 1.0.2   | Integration of the German translation (thanks to ITOMIG GmbH) |
| 2014-02-27 | 1.0.1   | First release                                                |

## Installation

- Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.
- Check `Approval process light` in the list of extensions at the end of the interactive wizard.

## Configuration

After installing this module, configure a proper `email_sender` and configure `trigger/action` to ensure “Approval eMails” delivery.

The following settings are available to configure the module:

| Module         | Parameter              | Type    | Description                                                  | Default Value                               |
| -------------- | ---------------------- | ------- | ------------------------------------------------------------ | ------------------------------------------- |
| approval-base  | email_sender           | string  | Sender eMail address, as seen in the approval email. If left blank, sending the email will likely fail. |                                             |
| approval-base  | email_reply_to         | string  | Default “reply to” eMail address for the approval email.     | (optional) defaults to email_sender         |
| approval-base  | comment_attcode        | string  | Attribute into which the user comments will be reported. Can be a case log or text. The comments are all aggregated. Note: the comment can also be viewed as a tooltip. | (optional)                                  |
| approval-base  | list_last_first        | boolean | In case several execution occur, drives the order in which the executions are displayed (vertically). | false                                       |
| approval-base  | enable_reminder        | boolean | Enable the feature “send a reminder”.                        | true                                        |
| approval-light | approval_timeout_delay | int     | Delay to get the answers given in days. Use 0 to disable the timeout (= infinite duration to approve or reject the request). Note the first negative answer marks the request as rejected without waiting for the further answers. | 5                                           |
| approval-light | approve_on_timeout     | boolean | Set to true for a passive approval scheme, false for an active approval scheme. | false                                       |
| approval-light | approver_select        | string  | OQL to display the possible approvers (must define a set of objects derived from the class Contact). Use :this->*attcode* to add conditions based on the user request's properties. | SELECT Person AS p WHERE id = :this->org_id |
| approval-light | bypass_profiles        | string  | CSV list of profiles. Having any of the given profiles is sufficient to be allowed to bypass approval processes. Set to an empty string to deny the feature to anybody. | Administrator, Service Manager              |

The following [standard settings](https://www.itophub.io/wiki/page?id=latest%3Aadmin%3Aitop_configuration_file) might be of interest when setting up the approval feature:

- email_asynchronous
- email_transport

### Notification (trigger/action)

Email notification is based on Trigger/Action and email content can be tailored to your need with HTML format and placeholders.

A default trigger is created at installation[![img](https://www.itophub.io/wiki/media?w=400&tok=bb849c&media=extensions%3Aapprovaltrigger.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovaltrigger.png)as well as 3 default actions with body in English, French and German.[![img](https://www.itophub.io/wiki/media?w=400&tok=84e14a&media=extensions%3Aapprovalnotif.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovalnotif.png)

You can of course edit this message to make it yours, here is the english default version for example of possible placeholders:

Dear `$approver→html(friendlyname)$`,
Please take some time to approve or reject ticket `$this→html(ref)$`

**Caller**: `$this→html(caller_id_friendlyname)$`
**Title**: `$this→html(title)$`
**Service**: `$this→html(service_name)$`
**Service subcategory**: `$this→html(servicesubcategory_name)$`

**Description**:
`$this→html(description)$`

**Additional information**:
`$this→html(service_details)$`

```
$approval_link$
```

[![img](https://www.itophub.io/wiki/media?w=400&tok=17f54b&media=extensions%3Aapprovaldefaultnotif.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovaldefaultnotif.png)You must **create the linkage between trigger and action** of the language you want to use.[![img](https://www.itophub.io/wiki/media?w=400&tok=509268&media=extensions%3Aapprovaltriggeredit3.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovaltriggeredit3.png)

You can create your own trigger and action
If you need to send different notification depending on the organization of the caller, the service, the service family, or any data available on the Ticket, this can be done by creating multiple trigger/action couples, using a filter on the Trigger.

## Usage

### Cinematics

A specific action *Wait for approval* is available on all User Requests in state *New*.

When the user selects this action, she will be prompted to select the Approver contact.

Then the User Request enters the state *Waiting for approval* and a notification is sent to the Approver. The Approver can approve or reject the request by clicking on the link provided in the email (an iTop login is not mandatory for this action). Alternatively, she can approve or reject from within iTop.

If there is no answer within 5 days (configurable), the answer defaults to *Rejected* (configurable).

The User Request will then continue its way through its lifecycle, depending on the approval status: *Rejected* or *Approved*.

### My ongoing approvals

From the Helpdesk menu, click on Ongoing approvals:

[![img](https://www.itophub.io/wiki/media?media=extensions%3Aapproval-menu.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapproval-menu.png)

The page shows a list of the User Requests having an approval process running, and for which your approval is being requested:

[![img](https://www.itophub.io/wiki/media?w=600&tok=9c9fd7&media=extensions%3Aapproval-monitoring.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapproval-monitoring.png)

### Approve or reject

From the user request, open the **Other actions** menu and select **Approve or Reject**:![img](https://www.itophub.io/wiki/media?media=extensions%3Aapproval_menu_reply.png)

The approval form is displayed:![img](https://www.itophub.io/wiki/media?w=600&tok=205bb9&media=extensions%3Aapproval_reply.png)

After the reply has been given, you are redirected to the user request and a banner reminds you the outcome of your reply.![img](https://www.itophub.io/wiki/media?w=600&tok=f3f290&media=extensions%3Aapproval_back.png)

### Bypass the approval process

If you are an administrator, and if the setup allows it, then you have a menu to bypass the process:![img](https://www.itophub.io/wiki/media?media=extensions%3Aapproval_menu_bypass.png)

The approval form is then a little different than the standard reply form: it reminds you that bypassing the process is a little different.

![img](https://www.itophub.io/wiki/media?w=600&tok=38e99d&media=extensions%3Aapproval_bypass.png)

If you are both an approver and allowed to bypass the process, then both menus are allowed. Using one or the other will just change the way the approval process result gets recorded and further displayed in the status tab.

### Status

As soon as a user request has been through an approval process, the tab **Approval status** shows detailed information about the ongoing or terminated approval.

![Ongoing approval](https://www.itophub.io/wiki/media?media=extensions%3Aapproval_status_ongoing.png)

In the above example, the deadline is displayed in bold: 21st of january at 12:47.

Click on the button “send a reminder” to send a new message to the approver (confirmation required). This feature can be disabled by setting the parameter *enable_reminder* to false.

After the reply has been given, the status appears in clear:

![Rejected approval](https://www.itophub.io/wiki/media?media=extensions%3Aapproval_status_rejected.png)

Move your mouse over the image next to the approver's name, and you will get the date of the answer and her comment if any has been given:

![img](https://www.itophub.io/wiki/media?media=extensions%3Aapproval_status_comment.png)

The status will be entirely reset anytime the user request enters the state “waiting for approval”.

## Approval in portals

A new menu appears in the Enhanced Portal, which allow an approver to retrieve all User Requests waiting for her approval, and one by one or in bulk mode, accept or reject them.[![img](https://www.itophub.io/wiki/media?w=600&tok=10bb58&media=extensions%3Aapprovalportal.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovalportal.png)

A comment is required in case of rejection, so the button is disabled as long as the comment is empty. A confirmation is required in both cases.[![img](https://www.itophub.io/wiki/media?w=600&tok=ec0a4c&media=extensions%3Aapprovalportalconfirmation.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovalportalconfirmation.png)

When clicking on the link to a User Request, the ticket's details are displayed with an extra comment field and two buttons at the bottom of the details to accept or reject it:[![img](https://www.itophub.io/wiki/media?w=600&tok=e71d4c&media=extensions%3Aapprovalportalonerequest.png)](https://www.itophub.io/wiki/media?media=extensions%3Aapprovalportalonerequest.png)