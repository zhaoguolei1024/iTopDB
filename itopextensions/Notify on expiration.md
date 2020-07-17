# Notify on expiration

- name:

  Notify on expiration

- description:

  Get a notification when a date is about to be reached

- version:

  1.0.1

- release:

  2019-02-18

- itop-version-min:

  2.3.0

- download:

  https://store.itophub.io/en_US/products/combodo-notify-on-expiration

- code:

  combodo-notify-on-expiration

- state:

  stable

## Features

This extension allow to trigger notification when an expiration date is about to be reached.

- You can define various Expiration rules, for different usage. Targeted for **Contract & License** expiration, it can be used with any class having a date attribute.
- You can set multiple rules for the same class with different term of notice, for example one '3 months ahead' and another 'one month before' the deadline. You can even create a third one '5 days after' the deadline if you want.

- Notification for a particular object reaching Expiration, unless configured differently, will occur only once.
- Notification message is configurable as any standard trigger/action.
- For advanced need, you can define the objects in scope of the notification with an OQL.

## Limitations

- Expiration Notification occurs **daily** only.
- It is not designed to handle time, only date.

## Requirements

iTop 2.3.0 or above

## Revision history

| Date       | Version | Description                                            |
| ---------- | ------- | ------------------------------------------------------ |
| 2019-02-18 | 1.0.1   | Fix missing menu and improve robustness on time format |
| 2019-01-10 | 1.0.0   | First official version - deprecated                    |
| 2018-03-28 | 0.1.0   | First release                                          |

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

Once the new module has been installed, edit the configuration file config-itop.php and look for the following new section:

```
  'combodo-notify-on-expiration' => array (
                'time' => '03:00',
                'enabled' => true,
                'debug' => false,
        ),
```

The following settings are available to configure the module:

| Parameter | Type        | Description                                           | Default Value |
| --------- | ----------- | ----------------------------------------------------- | ------------- |
| time      | hour:minute | Time of the day, when the process should start.       | 03:00         |
| enabled   | boolean     | Should the process run?                               | true          |
| debug     | boolean     | Should the CRON log be enrich with debug information? | false         |

The Notification on Expiration is handled by the service cron.php once a day. Make sure this one is scheduled to run on your system. More information in the chapter about [Background tasks](https://www.itophub.io/wiki/page?id=latest%3Aadmin%3Acron).

To check the status of this service, use the command:

```
php webservices/cron.php --auth_user=admin --auth_pwd=admin --status_only=1
```

The task *NotifyOnExpiration* will not be listed here if the CRON has not **run at least once** since the extension has been installed.

## Usage

Example: Setup a notification 20 days before a License expires

- Create a Expiration Rule
- Create a Trigger
- Create a Notification

### Expiration Rule

The extension brings a new Menu entry **Expiration rules** in the “Service Management” category

To create a new one:

- Give it any **Name** you like,
- Define the **Class** on which the rule will be applied, a Class code is expected, for eg. `CustomerContract`
- Give it a **Status**: `Active` to enable the cron to execute this Expiration rule in the Background task.
- Choose an **Applied option** by filling the fields either in **…option 1 (simple)** or in **…option 2 (advanced)** fieldset:

#### Simple

- Define the **Date to check**, which must be the code of a date attribute, *not the label*.
- **Term of notice** is configurable and says when to trigger the notification, by specifying a number of days **before** the deadline,

![img](https://www.itophub.io/wiki/media?media=extensions%3Aexpirationrulesimple.png)

Example: setting `Class`=*Licence*, `Date to check`=*end_date* and `Term of notice`=*20* the resulting OQL will be:

```
SELECT Licence WHERE end_date = DATE_ADD(CURRENT_DATE(), INTERVAL 20 DAY)
```

#### Advanced

- Define the **OQL scope** with an OQL query returning the objects on which to apply the trigger. *As soon as an OQL is entered, the advanced option is used, even if the simple one is also documented.*
- With the advanced mode, you can trigger notification after a date, which is not possible in simple mode.

![img](https://www.itophub.io/wiki/media?media=extensions%3Aexpirationruledetails.png)

You can create as many `Expiration Rule` as you want, for License, Customer Contract and even multiple for the same class but with a different `term of notice`

#### Preview

- You can check anytime which objects would be trigger if the Expiration Rule is run.

![img](https://www.itophub.io/wiki/media?media=extensions%3Aexpirationrulepreview.png)

### Trigger

Create a Trigger using the extension added: **Trigger (on expiration)**

![img](https://www.itophub.io/wiki/media?w=600&tok=e658fa&media=extensions%3Aexpirationtrigger.png)

You may `filter` it further, with an OQL:

```
SELECT Licence WHERE perpetual='no'
```

If you have high volume of objects, it's more efficient to filter as much as possible in the Expiration Rule

### Notification

Create a Notification, defining who should receive it and the body of the message
On top of the standard [placeholders](https://www.itophub.io/wiki/page?id=latest%3Aadmin%3Aplaceholders), this extension brings also:

| Placeholder            | Purpose                                                      |
| ---------------------- | ------------------------------------------------------------ |
| $rule->name$           | The name of the **Expiration rule** which has trigger this notification |
| $rule->description$    | The **Description** *of the Expiration rule which has trigger this notification* |
| $rule->term_of_notice$ | The **Term of notice** in days *defined in the Expiration rule which has trigger this notification* |

![img](https://www.itophub.io/wiki/media?media=extensions%3Aexpirationnotification.png)

Link the Notification to the above created Trigger.

## Troubleshooting / Q&A

**Q: The sub-Menu `Expiration rules` does not appear under `Service Management`**
A: Also the root cause of this issue is not understood yet, there are many possibilities to create Expiration rules without that Menu.

1. Add to one of your Dashboards, a Dashlet Badge on class `ExpirationRule`: it provides a mean to create a new rule and list existing.
2. Use under Menu `Admin tools`, the sub-menu `Run queries`: `SELECT ExpirationRule` it should propose you a link to create a new one.
3. Use under Menu `Admin tools`, the sub-menu `Universal Search` and search for class `ExpirationRule`, it will list the existing rules and offer to create one with the `New` menu