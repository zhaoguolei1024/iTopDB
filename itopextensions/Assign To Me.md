# Assign To Me

- name:

  Assign To Me

- version:

  0.1.2

- release:

  2016-02-02

- description:

  Assign tickets to connected agent

- itop-version-min:

  2.2.0

- dependencies:

  itop-ticket, itop-auto-assignment

- code:

  itop-assign-to-me

- state:

  public

This extension adds a menu to directly assign any kind of ticket to the agent currently connected.

## Features

When a ticket is in a state where an agent can be assigned (or reassigned) to it, the extension adds the capability to directly assign (or reassign) the ticket to the person currently connected, through an additional option in the menu : “Assign to me”.

This feature can be deployed for any kind of ticket. This is is controlled by configuration parameters. By default, the extension enables the “Assign to me” feature to User Requests and Incidents.

For each class of ticket, the list of states where the “Assign to me” menu is available is defined through the configuration options. Furthermore, the stimulus that should be applied to the ticket in these given states to trigger the assign action is, as well, a configuration parameter.

## Revision History

| Version | Release Date | Comments                                                     |
| ------- | ------------ | ------------------------------------------------------------ |
| 0.1.2   | 2016-01-22   | Accept combodo-autodispatch-ticket as dependency. This makes the extension compatible with iTop 2.4 |
| 0.1.1   | 2016-11-22   | Accept extension itop-auto-dispatch-ticket as dependency     |
| 0.1.0   | 2016-01-22   | First version                                                |

## Limitations

The extension has been designed to be, as much as possible, independant from the datamodel. This is why, configuration parameters define, for each class of ticket, what state is concerned and what stimulus should be applied. Nevertheless, the extension has dependencies with attributes from the standard datamodel

- Agent ID in a ticket is supposed to be 'agent_id',
- The ticket is expected to handle a support team and this team's id is supposed to be 'team_id',
- The class lnkPersonToTeam is expected to be the class linking persons to teams.

The `Assign` transition performed in background, **does not handle flags on transition**, so if other fields are expected to be provided during this transition, they will not and your Ticket will end-up in an unexpected situation with missing data in a state where they are expected to be documented

An alternative to this extension, with 2 clicks instead of one, but with less limitations, is to do it through [Form Prefill](https://www.itophub.io/wiki/page?id=2_6_0%3Acustomization%3Aform_prefill#prefill_transition_form)

## Requirements

The extension “Assign to me” requires iTop 2.2.0, at least, and the extensions iTop Tickets 2.2.0 and [Auto Dispatch Ticket](https://www.itophub.io/wiki/page?id=extensions%3Acombodo-autodispatch-ticket) to a team

## Installation

1. Expand the zip file of the extension, copy the folder `itop-assign-to-me` into the `extensions` folder of iTop, and make sure that the folder can be read by the web server process.
2. If iTop is already installed, change the configuration file to read-write mode.
3. Launch the setup program by pointing your browser to http://<itop>/setup/
4. When prompted to select the extensions to install, check “iTop Assign to me” and complete the setup.

[![Installation screen](https://www.itophub.io/wiki/media?w=450&tok=8a37dd&media=extensions%3Aitop-assign-to-me-install.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aassign_to_me&media=extensions%3Aitop-assign-to-me-install.png)

## Configuration

Default configuration of the extension is done through XML. This configuration can be altered through XML and / or completed through the standard configuration file.

By default, the extension enables the “Assign to me” action to User Requests and Incidents:

```
  <module_parameters>
    <parameters id="itop-assign-to-me" _delta="define">
      <allowed_classes type="hash">
        <UserRequest type="hash">
          <dispatched>ev_assign</dispatched>
          <assigned>ev_reassign</assigned>
          <redispatched>ev_assign</redispatched>
        </UserRequest>
        <Incident type="hash">
          <dispatched>ev_assign</dispatched>
          <assigned>ev_reassign</assigned>
          <redispatched>ev_assign</redispatched>
        </Incident>
      </allowed_classes>
    </parameters>
  </module_parameters>
```

For each class of Ticket, the states where an assignment can be done are listed together with the stimulus triggering that action. These XML lines can be modified through XML customization like any other XML entry of iTop datamodel.

Should an iTop administrator wish to enable the “Assign to me” to another type of tickets (like the simple change tickets), just add equivalent lines to the configuration file:

```
  'itop-assign-to-me' => array (
                'allowed_classes' => array (
                  'Change' => 
                  array (
                    'new' => 'ev_assign',
                    'rejected' => 'ev_reopen',
                  ),
                ),
        ),
```

Should your life cycle allow direct transitions from state new to assigned, like in the example above, a team_id attribute must still exist and must be set to the right team before being authorized to apply the stimulus.

## Usage

Some filters have been set to authorize, or not, the “Assign to me” action:

- The user should be different from the agent currently assigned to the ticket,
- The user should have a profile that enables such action,
- The person linked to the connected user should belong to a team which the ticket can be dispatched to,
- Configuration parameters should be consitent with the datamodel.

If these conditions are met and if the ticket is in a state where assignment to an agent can be done (as defined through the configuration), the “Assign to me” menu appears in the “Other Actions” menu available for your ticket.

[![img](https://www.itophub.io/wiki/media?media=extensions%3Aitop-assign-to-me-menu.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-assign-to-me-menu.png)

Just select it and the stimulus defined in the configuration file will be applied. Note that action is directly done. No confirmation is required.