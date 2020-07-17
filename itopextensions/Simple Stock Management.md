# Simple Stock Management

- name:

  Simple stock management

- description:

  Manage stock elements: decrease automatically stock on User Requests and refill manually

- version:

  1.0.0

- release:

  2019-09-02

- itop-version-min:

  2.5

- diffusion:

  iTop Hub

- download:

  http://www.combodo.com/itop-extensions/

This extension adds to iTop the capability to manage stock of various elements.

## Features

Stock Management extension introduces the capability to manage stock through a new “Stock” class. Such stock element can be of different type: stock of RJ45, stock of cables, stock of video cards… defined through a simple typology class “Stock Type”.

A Stock follows a life cycle: once created, it can be supplied (ie available quantity can be increased) and quantity can be consumed. Stock increase is done through a life cycle action. Where consumption is done when a Ticket is linked to the Stock with a quantity specified on the link between the stock and the Ticket. Multiple Tickets can be attached to a Stock.

If the Stock falls below the user defined `Warning level`, a background task running every minute, moves the stock to `Empty` state and a notification may be sent, if configured.

When listing the stocks, the empty ones are highlighted:

![Empty stocks ](https://www.itophub.io/wiki/media?media=extensions%3Astock-list.png)

The stock moves back to the `Restocked` state if enough quantity is added to the stock.

If after an audit, you discover that some items have disappeared from the Stock or are broken, then you can decrease the stock by adding a negative number to the Stock.

## Revision History

| Version | Release Date | Comments                                                     |
| ------- | ------------ | ------------------------------------------------------------ |
| 1.0.0   | 2019-09-02   | Add location, description, provider,… Allow Support Agent and Change Implementor to consume Stocks |
| 0.1.0   | 2016-06-07   | First version                                                |

## Limitations

Attachment of ticket to a Stock can only be done from the details screen of a Stock, not from the details of the Ticket. Consumption of stock elements is done when attaching Ticket to it.

`Status` being computed in background, it can be misleading in some cases:

- When a Ticket consumed enough items to set the Stock quantity below the threshold, the status isn't refreshed immediately.
- When you add to an empty Stock, any quantity, it assumes it is “supplied” again, which is the most common situation, but when you add a negative number, the resulting status looks confusing, as it says “Restocked” during 60 seconds, until the `cron.php` does its job.

## Requirements

The extension requires iTop 2.5.0, at least, as well as the extensions itop-config-mgmt 2.5.0 and itop-tickets 2.5.0.

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

1. When prompted to select the extensions to install, check “iTop Stock Management” and complete the setup.

[![Installation screen](https://www.itophub.io/wiki/media?w=450&tok=18f0c1&media=extensions%3Aitop-stock-management-install.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitop-stock-mgmt&media=extensions%3Aitop-stock-management-install.png)

## Configuration

No specific configuration parameter is required for the extension.

“iTop Stock Management” relies on the service [cron.php](https://www.itophub.io/wiki/page?id=latest%3Aadmin%3Acron).

Make sure this one is scheduled to run on your system. To check the status of this service, use the command:

```
php webservice/cron.php --auth_user=user --auth_pwd=password --status_only=1
```

## Usage

[![img](https://www.itophub.io/wiki/media?media=extensions%3Astock-element.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitop-stock-mgmt&media=extensions%3Astock-element.png)The “Stocks” menu available under the Configuration management section allows you to list, filter and search the stock element objects that have been created in iTop.[![img](https://www.itophub.io/wiki/media?media=extensions%3Astock-menu.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitop-stock-mgmt&media=extensions%3Astock-menu.png)

### Stock properties

A stock element has the following attributes…

| Field            | Type                           | Comment                                                      | Mandatory ? |
| ---------------- | ------------------------------ | ------------------------------------------------------------ | ----------- |
| Name             | Alphanumeric string            |                                                              | Yes         |
| Organization     | Foreign key to an Organization |                                                              | Yes         |
| Location         | Foreign key to a Location      | not limited to the organization                              | No          |
| Type             | Foreign key to a Stock Type    | Stock type is a simple topology                              | No          |
| Provider         | Foreign key to an Organization |                                                              | No          |
| Status           | Enumeration                    | Possible values: New, Restocked, Empty                       | Yes         |
| Restocking date  | Date and time                  | Set when the stock was supplied for the last time            | No          |
| Warning level    | Integer                        | Stock quantity under which a notification can be sent        | No          |
| Current quantity | Integer                        | Current quantity of elements in stock. Figure is automatically computed. | No          |
| Owner            | Foreign key to a Contact       |                                                              | No          |
| Description      | HTML text                      | Information on how to manage this stock                      | No          |

#### Internal fields

| *Stock status to be checked*   | Boolean                 | Indicates that the stock status is NOT up to date and that it needs to be recomputed | No        |
| ------------------------------ | ----------------------- | ------------------------------------------------------------ | --------- |
| *Cumulated quantity*           | Integer                 | Quantity that have been supplied from the date the Stock has been created. Figure is automatically computed | Mandatory |
| *Quantity to add to the stock* | Signed integer 4 digits | Quantity to add to the Stock. It can be negative. Value is kept from one supply to another. | Optional  |

Quantity in stock is the difference between the sum of all quantities that have been added to the stock element and the sum of all quantities consumed by the linked user requests. Computation of remaining quantity is asynchronous: it is done regularly by the cron and can be manually launched through a specific action.

*Those fields are not displayed by default. `Quantity to add to the stock` is required during “Add to stock” action.*

#### Tabs

… and links (next to the history tab):

| Tab       | Description                    |
| --------- | ------------------------------ |
| Tickets   | Tickets related to the stock   |
| Documents | Documents related to the stock |

### Life cycle

This is the life cycle followed by a Stock element:

[![ Life cycle](https://www.itophub.io/wiki/media?media=extensions%3Aitop-stock-element-life-cycle.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aitop-stock-mgmt&media=extensions%3Aitop-stock-element-life-cycle.png)

From a list or the detail screen of Stock, clicking on the “New” button displays the following form:

![ New stock element ](https://www.itophub.io/wiki/media?media=extensions%3Astock-new.png)

Once created, the Configuration Manager can supply the Stock through the “Add to stock” button available in the “other actions” menu. The figure entered at this stage indicates the quantity added to the stock for that element. It can be negative, to . Once done the whole detail screen is displayed:

![ Supplied stock](https://www.itophub.io/wiki/media?media=extensions%3Astock-add-menu.png)![ First "Add to stock" ](https://www.itophub.io/wiki/media?media=extensions%3Astock-first-add.png)![ First "Supplied" ](https://www.itophub.io/wiki/media?media=extensions%3Astock-first-supplied.png)

The “Add to stock” action can be done any time from that state or from the empty state. The “Cumulated quantity” attribute stores the global quantity of objects that have been added to the current stock element. This figure never decreases.

Current quantity decreases when tickets are attached to the stock by a Support Agent or a Change Implementor with a consumed quantity.

![ First "Consumption" ](https://www.itophub.io/wiki/media?media=extensions%3Astock-consumption-0.png)![ After "Consumption" ](https://www.itophub.io/wiki/media?media=extensions%3Astock-after-consumption.png)

Situation where the status is temporarly inaccurate:![ Second "Consumption" ](https://www.itophub.io/wiki/media?media=extensions%3Astock-consumption-2.png)![ After second "Consumption" ](https://www.itophub.io/wiki/media?media=extensions%3Astock-compute-status.png)It can be fixed manually with the menu “Check stock status”, or just wait 60 seconds for the cron.php to do the job

### Status computation

Computation of stock status is done in an asynchronous way. As a result, it can be temporarily wrong (*less than 60 seconds*):![ Before cron ](https://www.itophub.io/wiki/media?media=extensions%3Astock-before-cron.png)

- when the cron is running, it recomputes the status to its correct value:

![ After cron ](https://www.itophub.io/wiki/media?media=extensions%3Astock-after-cron.png)

- or when the user press the `Check stocks status` menu available in the Other Actions menu:

![ Compute status menu ](https://www.itophub.io/wiki/media?media=extensions%3Astock-check-multiple-status-menu.png)![ Compute status result ](https://www.itophub.io/wiki/media?media=extensions%3Astock-check-multiple-status-result.png)

In order to move the current quantity above the threshold, the stock needs to be supplied again. It could also come back by “chance”, if the quantity consumed by the tickets is decreased.

### Stock type

New type of stock can be created on the fly while editing a stock, with the + button. The Configuration Manager can see all Stock types at once in the dashboard displayed by the menu `Data administration / Typology configuration`

### Notification

The extension doesn't automatically create any notification. Should you wish to notify the stock owner or any other contact that the quantity in stock has fallen below the threshold, ask your iTop administrator to create the notification first.

For that purpose, a trigger on entering a state must be created, like:

![Empty stock element](https://www.itophub.io/wiki/media?media=extensions%3Aitop-stock-element-trigger.png)

The associated trigger action is standard. Only point to keep in mind: the owner of the stock element is defined by the attribute `owner_id`. Destination of the mail can be, therefore, defined like this:

```
SELECT Person WHERE id= :this->owner_id
```