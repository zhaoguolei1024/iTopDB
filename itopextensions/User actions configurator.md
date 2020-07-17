# User actions configurator

- name:

  User actions configurator

- description:

  Configure user actions to simplify and automate processes. Eg create an incident from a CI.

- version:

  1.3.2

- release:

  2019-03-26

- itop-version-min:

  2.6.0

- code:

  combodo-user-actions-configurator

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-user-actions-configurator

- alternate-name:

  Object Copier

- diffusion:

  iTop Hub

**Other versions of this component:** [1.0.3](https://www.itophub.io/wiki/page?id=extensions%3Aitop-object-copier_1_0), [1.2.1](https://www.itophub.io/wiki/page?id=extensions%3Aitop-object-copier_1_2)

This extensions aims at improving the end-users productivity. It adds a menu to create an item prefilled with information coming from an existing item.

Amongst the possible usages, you can:

- Provide a mean to quickly clone CIs (clone all the attributes but still force the user to enter a new name)
- Provide a shortcut to create a ticket from a Contact that will be the caller of the ticket
- Provide a shortcut to create a parent ticket (and record the information into the child ticket)
- Provide a shortcut to create a ticket from a CI (and record the information into the child ticket)
- Provide a shortcut to create a change ticket from a user request (and record the information into the user request)

Let's use the last example to illustrate the possibilities of the module:

Users have a menu in the **Other Actions** drop-down menu of a *User Request*:

![img](https://www.itophub.io/wiki/media?media=extensions%3Aitop-object-copier-ticketfromchange1.png)

Clicking on the menu, opens the standard creation form with prepopulated data:

![img](https://www.itophub.io/wiki/media?media=extensions%3Aitop-object-copier-ticketfromchange2.png)

The user can adjust the values, then create the item. In addition to the standard report, a message indicates that something has been retrofitted back to the *source* item.

![img](https://www.itophub.io/wiki/media?media=extensions%3Aitop-object-copier-ticketfromchange3.png)

## Principles

A shortcut is governed by a *rule definition*.

The menu is visible if a series of conditions are met:

- The item being visited is in the scope of the rule (given by an OQL). For instance, you may want to propose the shortcut only for user request being assigned or pending: SELECT UserRequest WHERE status IN ('assigned', 'pending')
- The current user has a profile allowed for the rule (can be anybody)

Several rules can coexist for a single *source object*: there will be as many menus as there are rules that match the conditions.

A rule defines which kind of object to create:

- Either a given class (can be an abstract class, the user will have to select a subclass)
- Or the exact same class as the *source object*

A rule specifies what has to be done to *preset* or *prepopulate* the form. This is done by the mean of *actions*. The following kind of actions are available:

- Set the value of an attribute depending on the value of one or several attributes from the *source object*.
- Copy N-N links (eg. Documents on a Ticket, while cloning a Ticket. Documents are not duplicated, just the links are)
- Copy 1:n link by duplicating the 1-N linked objects (e.g. Server Interfaces, WorkOrders on a Change)
- Add an N-N link to the *source object* or to an external key of the *source object*.

Additionaly, the rule specifies what has to be done to *retrofit* some information from the *created object* to the *source object*.

## Limitations

The following types of attributes are currently not handled and therefore cannot be preset (and no error message is given):

- Blobs
- Stop watches

Using *apply_stimulus()* on the *created object* does not work. *If used in preset, the form is shown with the object id and the relevant buttons depending on the new state but then it fails to “create” the object because it was created already during the stimuli processing*

## Requirements

n/a

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2019-03-26   | 1.3.2   | * Fix Issue when copying list with object copier * Fix Custom Date format in Stencils actions |
| 2019-01-16   | 1.3.1   | Security hardening                                           |
| 2018-12-19   | 1.3.0   | New feature enabled: copy of Attachments                     |
| 2018-06-26   | 1.2.1   | ES translation                                               |
| 2018-01-26   | 1.2.0   | Add copy_head verb for CaseLog attributes - allow creation of a new ticket from the latest log |
| 2017-11-13   | 1.1.9   | Fix error displayed in error message or tooltip, about read-only attributes being set. |
| 2017-09-29   | 1.1.8   | Showing action in object details only when target class is writable. |
| 2017-04-04   | 1.1.7   | Case logs : when using set on a case log, the entry was set twice, the HTML formatting was lost, and if the log was first copied from the source, it was broken. |
| 2017-03-27   | 1.1.6   | With some customizations (preset on ticket dates), the refresh of dependent fields was broken. Regression introduced in iTop 2.3 |
| 2017-03-23   | 1.1.5   | Fix for XSS vulnerability.                                   |
| 2016-08-09   | 1.1.4   | Fix for compatibility with iTop 2.3.0 (still backward compatible): properly handle the breadcrumb + bug fix when using hidden fields and case logs. |
| 2015-10-05   | 1.1.3   | Fix for compatibility with iTop 2.2.0 (still backward compatible) |
| 2015-09-30   | 1.1.2   | New verb: nullify. Useful for leaving a date or datetime undefined (differs from the verb *reset* because the default value for such attributes is “now”) |
| 2015-07-01   | 1.1.1   | New verb: call_method. Allows any kind of modification on the target object (and/or the source object) |
| 2015-02-03   | 1.1.0   | Added placeholders $current_date$ and $current_time$. Added the verb apply_stimulus. Exposed some APIs to allow the reuse of actions in other modules like itop-stencils |
| 2014-12-18   | 1.0.3   | Translated the default configuration in french (while keeping the engish version as the default) |
| 2014-07-18   | 1.0.2   | Added placeholders for set() and append(): $current_contact_id$ (already documented) and $current_contact_friendlyname$ (new!) |
| 2014-04-03   | 1.0.1   | Fixes an issue with linksets: the links were correctly created into the clone, but they were deleted from the source object |
| 2014-03-04   | 1.0.0   | First officialy released version                             |

## Installation

Copy the folder `itop-object-copier` into the `extensions` folder of iTop and launch the setup again.

Make sure that the web server has enough rights to read the content of the `extensions` folder and all its sub-folders before launching the setup

When prompted to select the extensions to install, check “Object copier” in the list of available extensions.

## Configuration

| Setting name     | Description                                                  | Example                                        |
| ---------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| source_scope     | The OQL to define the *source objects*. The only parameter available is *current_contact_id* | “SELECT UserRequest WHERE status = 'assigned'” |
| allowed_profiles | CSV list of profiles allowing the shortcut. The user must have at least one profile to have the shortcut available. Wrong profiles names are ignored. Set as an empty string to allow the shortcut to anybody. | “Administrator,Support Agent”                  |
| menu_label       | Optional: Label or dictionary entry for the new menu entry. It is optional and defaults to “Clone…” |                                                |
| form_label       | Optional: Label or dictionary entry for the form header. It is optional and defaults to “Cloning %1$s” |                                                |
| report_label     | Optional: Label or dictionary entry for the report once the object has been created. It is optional and defaults to “Cloned from %1$s” |                                                |
| dest_class       | Class of the object to create. If empty, it defaults to the class of the source object | “Change”                                       |
| preset           | Array of *actions* to preset the object in the creation form. More information below. | array()                                        |
| retrofit         | Array of *actions* to retrofit some information from the created object to the source object. More information below. | array()                                        |

menu_label, form_label and report_label can be localized without the burden of create dictionaries. To do so, create the settings menu_label/<language_code> (e.g. “menu_label/FR FR”) for each supported language. The setting menu_label will be the default value.

### Actions

An action is specified as a string formatted as `verb(arg1[,arg2[…]])`
The same action can be requested multiple times.

The following *verbs* are available:

| Verb              | Parameters                     | Description                                                  |
| ----------------- | ------------------------------ | ------------------------------------------------------------ |
| clone_scalars     | <none>                         | Copy all the scalar attributes                               |
| clone             | attcode1,attcode2, …           | Copy the given attributes                                    |
| reset             | attcode                        | Reset the attribute to its default value                     |
| nullify           | attcode                        | **New in 1.1.2** - Reset the attribute to its null value (will appear to be *undefined* from the end users perspective) |
| copy              | att_to_read,att_to_write       | Copy from att_to_read to att_to_write                        |
| copy_head         | att_to_read,att_to_write       | **New in 1.1.11** - Copy last entry in the att_to_read caselog attribute to att_to_write. An exception (non blocking) is thrown if att_to_read is not a caselog |
| append            | attcode,string                 | Append the string to the attribute. The string can contain placeholder like $this->attcode$ (or $current_contact_id$, $current_contact_friendlyname$, $current_date$, $current_time$). Commas must be escaped with a backslash. Newlines (\n) are allowed. The character set must be utf-8. |
| set               | attcode,value                  | Set a value. If the value is a string, it can then contain placeholder like $this->attcode$ (or $current_contact_id$, $current_contact_friendlyname$, $current_date$, $current_time$). Commas must be escaped with a backslash. Newlines (\n) are allowed. The character set must be utf-8. |
| add_to_list       | attRead,attWrite,attLink,value | attRead is an external key on the read object, attWrite is a N-N link set on the written object, attLink is an attribute on the link class that will be set to <value> |
| apply_stimulus    | stimulus code                  | Applies the given stimulus (saves the object). To be used in **retrofit ONLY.** Best practice: It is strongly recommanded to set transition mandatory fields as well, otherwise they will stay empty and could break reporting. |
| call_method       | function name                  | **New in 1.1.1** - Calls the provided method on the written object. Its prototype must be “public function xxxx($oSource)”. The function can send exceptions in case of failure. In such a case, the error message gets displayed in the log/error.log file |
| clone_attachments | <none>                         | **New in 1.3.0** - Copy all the attachments from *source* to *destination* |

## Configuration example

```
'itop-object-copier' => array(
        'rules' => array(
                array(
                        'source_scope' => 'SELECT UserRequest WHERE status IN ("assigned", "pending")',
                        'allowed_profiles' => 'Administrator,Support Agent',
                        'menu_label' => 'Issue a change ticket...',
                        'form_label' => 'Issue a change from request %1$s. Please review the description before create the change ticket. After creation of the change ticket, the request ticket will be automatically updated.',
                        'report_label' => 'Issued from the request %1$s. The request has been updated.',
                        'dest_class' => 'Change',
                        'preset' => array(
                                'clone(contacts_list,functionalcis_list,org_id,title,caller_id)',
                                'set(description,Original description:\n\$this->description\$)',
                        ),
                        'retrofit' => array(
                                'copy(id, parent_change_id)',
                                'set(private_log,Issued change $this->ref$)',
                        ),
                ),
                array(
                        'source_scope' => 'SELECT FunctionalCI',
                        'allowed_profiles' => '',
                        'dest_class' => '',
                        'preset' => array(
                                'clone_scalars(*)',
                                'reset(name)',
                        ),
                        'retrofit' => array(
                        ),
                ),
        ),
),
```

## Troubleshooting

All errors are logged to the file log/error.log

The behavior from the end-user perspective is:

- When the parameters source_scope is wrong, the rule is ignored
- When dest_class is not a valid class, the rule is ignored
- When source_scope/dest_class/allowed_profiles/preset/retrofit are missing, the rule is ignored
- When the list of profiles contain wrong names, those names are simply ignored, and if all the names in the list are wrong then no one will have the menu to clone the object.
- When a preset action is wrong (syntaxically or grammatically), the preset is stopped at that point, the form is displayed with a message explaining the issue: “An error has been encountered while presetting the object to create: <error message>. Please contact your administrator.” The user can proceed with the object creation.
- When a retrofit action is wrong, the retrofit is stopped at that point, the operation completes (object created as expected) and the report contains: “An error has been encountered while retrofitting some information back to the source object: <error message>. Please contact your administrator.”