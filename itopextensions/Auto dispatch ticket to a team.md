# Auto dispatch ticket to a team

- name:

  Auto dispatch ticket to a team

- description:

  Automatically dispatch tickets based on the configurable OQL rules.

- version:

  1.0.8

- release:

  2019-06-16

- itop-version-min:

  2.4.0

- code:

  combodo-autodispatch-ticket

- state:

  stable

- diffusion:

  iTop Hub

Automatically dispatch tickets to teams when entering a state.

## Features

Allow to **dispatch automatically** Ticket based on predefined `Dispatch rules`, **to a team** and trigger a transition.

Each time a Ticket enter a state, iTop searched for `Dispatch rules` which apply to this class and state. If it finds one, then it uses each `Team rules` in order to retrieve a team. The Ticket is assigned to the first team found and Ticket is moved to a different state. If no team is found, the Ticket is left unchanged.

Example: when a Ticket is created, it is automatically dispatched to the team with role 'Support level1' defined on the customer Delivery Model, and moved to status 'Dispatch'.

This extension allows to define:

- different rules for different sub-class of Ticket,
- ordered queries to retrieve the team to use,
- force an automatic transition, if a team was set *(thus triggering notification)*

Team can be assigned based on:

- customer of the ticket
- service or sub-service of the ticket
- location of the caller
- current time and applicable coverage windows
- or any other logic you may need…

And any combination of those.

If more than one team is returned, first will be used without guarantee that it will always be the same one.

## Revision History

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2019-06-16 | 1.0.8   | * When team rules return no team and ticket is not dispatched, don't log success in ticket's log * When a stimulus is not applicable, log the error and pursue the object's operation * Fix inactive target rules being used for matching * Fix a bug when creating coverage window within a dispatch rule |
| 2019-03-19 | 1.0.7   | Fix dispatch rule not working for Tickets created by a user with silos |
| 2019-01-17 | 1.0.6   | Add Combodo license                                          |
| 2018-12-07 | 1.0.4   | Update translations                                          |
| 2018-06-26 | 1.0.3   | Fix english translation                                      |
| 2017-10-27 | 1.0.2   | Added German translation. (thanks to ITOMIG GmbH)            |
| 2017-09-26 | 1.0.0   | First official version.                                      |

## Limitations

This extension is executed after *combodo-approval-light* or *combodo-approval-extended*, therefore if an *Approval rule* changes the object's state, *Dispatch rules* that should have been applied on the previous state will not be computed.

Dispatch rules must be defined on each final class, not on abstract class. This extension is not designed to set a team without changing the state.

## Requirements

- iTop 2.4 or later
- Extension SLA considering business hours v2.1 or more

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

There is no parameter defined in the iTop configuration file.

## Usage

### Dispatch Rule

A `dispatch rule` is defined for one Class of Ticket. It must contain at least one `Team rule` and one `State rule`.

First create a new *Dispatch rule* by opening the corresponding menu under *Service Management*.

[![img](https://www.itophub.io/wiki/media?w=600&tok=f73901&media=extensions%3Acombodo-autodispatch-ticket-01.png)](https://www.itophub.io/wiki/media?media=extensions%3Acombodo-autodispatch-ticket-01.png)

| Name                  | Mandatory | Description                                                  |
| :-------------------- | --------- | ------------------------------------------------------------ |
| Name                  | Mandatory | A name describing the dispatch rule                          |
| Class                 | Mandatory | Ticket class the rule will apply to                          |
| Team attribute        | Mandatory | Attribute code of the *Ticket Class* that will be set by the matching *Team rule* |
| Explain log attribute | Optional  | Attribute code of the *Ticket Class* that will be set with a text explaining how a *Team rule* matched |
| Disabled contexts     | Optional  | A CSV list of context tags in which the *Dispatch rule* will be inactive. Typically a portal (“GUI:Portal”), cron tab (“CRON”), a rest/json call (“REST/JSON”), … |

As of iTop 2.4, the following contexts are available (more can be added from extensions) :

- **GUI:Console**: The administration console
- **GUI:Portal**: Any portal
- **Portal**:<PORTAL_ID>: A specific portal instance
- **Synchro**: Any synchro datasource
- **Synchro:<DATASOURCE_RAWNAME>**: A specific synchro datasource
- **CRON**: Any CRON task
- **CRON:Task:<TASK_CLASSNAME>**: A specific CRON task
- **REST/JSON**: A REST/JSON call

### State Rule

A `State rule` defines the state in which you want to auto-assign a team, and which transition must be applied if a team was found.

Create at least one *State rule* in the *States* tab.

[![img](https://www.itophub.io/wiki/media?w=600&tok=ae4bac&media=extensions%3Aautodispatch-newstaterule.png)](https://www.itophub.io/wiki/media?media=extensions%3Aautodispatch-newstaterule.png)

| Name          | Mandatory | Description                                                  |
| :------------ | --------- | ------------------------------------------------------------ |
| State code    | Mandatory | Code of the Ticket state. Entering this state will trigger the *Dispatch rule* |
| Stimulus code | Mandatory | Code of the *Stimulus* that will be applied if a team is found |

### Team Rule

A `Team rule` defines how to retrieve the team to assign.

Create at least one *Team rule* in the corresponding tab.

[![img](https://www.itophub.io/wiki/media?w=600&tok=ac0756&media=extensions%3Aautodispatch-newteamrule.png)](https://www.itophub.io/wiki/media?media=extensions%3Aautodispatch-newteamrule.png)

| Name            | Mandatory | Description                                                  |
| :-------------- | --------- | ------------------------------------------------------------ |
| Name            | Mandatory | Free name of the rule, for humans.                           |
| OQL             | Mandatory | Query which must return *Team* objects                       |
| Coverage window | Optional  | The *Team rule* will be used only if we are within the *Coverage window* |
| Rank            | Mandatory | Order for using the Team rules, lowest number first.         |
| Active          | Mandatory | Allow to prepare *Team rules*, without activating them. Rules with 'No' will not be used. |

## Examples of usage

### Criteria to assign a team

Remember that, there is a filter on Ticket.team_id:

```
SELECT Team AS t 
  JOIN lnkDeliveryModelToContact AS l1 ON l1.contact_id=t.id 
  JOIN DeliveryModel AS dm ON l1.deliverymodel_id=dm.id 
  JOIN Organization AS o ON o.deliverymodel_id=dm.id 
WHERE o.id = :this->org_id
```

Teams auto-assigned on a Ticket should be compliant with the filter defined on Ticket.team_id

You may have to change that filter or to put all applicable teams under the Delivery Model

#### Default Team

In beta version of auto-dispatch, iTop assigned a team using this logic

```
SELECT Team AS t 
  JOIN lnkDeliveryModelToContact AS l1 ON l1.contact_id=t.id 
  JOIN ContactType AS ct ON l1.role_id=ct.id
  JOIN DeliveryModel AS dm ON l1.deliverymodel_id = dm.id 
  JOIN Organization AS o ON o.deliverymodel_id=dm.id 
WHERE o.id=:this->org_id AND ct.name='Support level1'
```

#### Assigning a team based on Service

You may want to define a support team per Service, in which case, the best is to add a new attribute `support_team_id` on *Service*, as an ExternalKey to a *Team*.

But you may also keep the default datamodel and ensure that only one single team is linked to each service.

You may want to use the team defined on the Service when there is one, otherwise use the default team defined on the delivery model of the customer. In which case you will create 2 Team rules, one based on Service with the lowest rank and the other using the OQL above.

### Disabled contexts

It is quite common that you want to Auto-Dispatch tickets created by users through the Portal, Ticket creation from Email, but do not want to do it, when the ticket is created by a synchro, a script or maybe an agent in the console. That's the purpose of the *Disabled contexts* field.

It is even possible to disable a *Dispatch rule* just for one particular Portal or a particular DataSynchro. The syntax to use is:

- `Portal:<portal-id>` where `<portal-id>` is the portal id defined in the XML
- `Synchro:<synchro-name>` where `<synchro-name>` is the name of that particular Datasynchro

Examples: Let's say you have created a special portal for your agents and you want Tickets created through that portal **not** to be auto-dispatched.

```
  <portals>
    <portal id="agent-portal" _delta="define">
    ...
```

Then to disable the Dispatch rule, set *Disabled contexts* = `Portal:agent-portal`.