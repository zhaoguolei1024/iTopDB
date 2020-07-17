- # Configurator for automatic object creation

  - name:

    Configurator for automatic object creation

  - description:

    Templating based on existing objects.

  - version:

    1.1.2

  - release:

    2019-03-26

  - itop-version-min:

    2.6.0

  - code:

    combodo-configurator-for-automatic-object-creation

  - state:

    stable

  - download:

    https://store.itophub.io/en_US/products/combodo-configurator-for-automatic-object-creation

  - alternate-name:

    Stencils (templating)

  - diffusion:

    iTop Hub

  **Other versions of this component:** [1.0.14](https://www.itophub.io/wiki/page?id=extensions%3Aitop-stencils_1_0)

  This extensions aims at improving the end-users productivity. It automatically creates a set of prefilled objects out of existing data.

  Amongst the possible usages, you can:

  - Preset work orders on a user request, depending on the selected service, to be executed when the request is being assigned to an agent.
  - Preset a list of characteristics on a contract, depending on the selected service, to be recorded right when a contract is being created.
  - Preset the SLAs depending on …
  - Preset server interfaces

  This can be combined with Object Copier… for instance: Create a “Move to production” request from a CI. The request gets automatically (or not) assigned, then the work orders are prefilled.

  Note that in most cases you will have to alter the existing data model to define your template class.

  ## Principles

  ### Triggering

  The templates will be copied under the following circumstances:

  - *either* when an object is **being created**
  - *or* when an object is **reaching a given state** (lifecycle required)

  The objects being in the scope of the trigger can be filtered out by the mean of an OQL: SELECT UserRequest WHERE team_id_friendlyname='Doers'.

  ### Actions

  Once the triggering conditions have been met, the module will perform the following:

  1. Look for the **templates**. This is done by the mean of an OQL. E.g. SELECT WorkOrderTemplate WHERE service_id = :trigger->service_id
  2. For each *template*,
     1. Instantiate an object called the **copy**
     2. Perform a series of action on the *copy*. This is formalized as a list of actions. For instance, “clone(description)+set(ticket_id,$trigger->id$)” will copy the attribute *description* from the *template*, then set the parent ticket to be the ticket that triggered the copy
     3. Optionaly find the children of the current *template*, and for each child perform the same operations; (i.e. a + b + c, recursively)
  3. Optionaly perform a series of actions (set a value, apply a stimulus) back on the *triggering object*.

  A report is displayed (though this is optional) on the triggering object:![img](https://www.itophub.io/wiki/media?media=extensions%3Areport.png)

  ## Revision history

  | Date       | Version | Description                                                  |
  | ---------- | ------- | ------------------------------------------------------------ |
  | 2019-03-26 | 1.1.2   | - Fix Issue when copying list with object copier - Fix Custom Date format in Stencils actions |
  | 2019-01-16 | 1.1.1   | Security hardening                                           |
  | 2018-12-19 | 1.1.0   | - Support for attachment copy - Fix duplicated links on Ticket creation from CI |
  | 2018-06-26 | 1.0.14  | Add copy_head verb for CaseLog attributes, ES translation    |
  | 2017-11-15 | 1.0.13  | Fix error displayed in error message or tooltip, about read-only attributes being set. |
  | 2017-09-29 | 1.0.12  | Showing action in object details only when target class is writable. |
  | 2017-04-04 | 1.0.11  | Case logs : when using set on a case log, the entry was set twice, the HTML formatting was lost, and if the log was first copied from the source, it was broken. |
  | 2017-03-27 | 1.0.10  | With some customizations (preset on ticket dates), the refresh of dependent fields was broken. Regression introduced in iTop 2.3 |
  | 2017-03-23 | 1.0.9   | Fix for XSS vulnerability                                    |
  | 2016-08-09 | 1.0.8   | Fix for compatibility with iTop 2.3.0 (still backward compatible): properly handle the breadcrumb + bug fix when using hidden fields and case logs. |
  | 2015-10-05 | 1.0.7   | Fix for compatibility with iTop 2.2.0 (backward compatible)  |
  | 2015-09-30 | 1.0.6   | New verb: nullify. Usefull for leaving a date or datetime undefined (differs from the verb *reset* because the default value for such attributes is “now”) |
  | 2015-07-02 | 1.0.5   | Transfer data from the triggering object to the copies: copy_from_trigger. New verb for custom actions: call_method. |
  | 2015-04-08 | 1.0.3   | Retrofit data from the copies to the triggering object: retrofit_from_copy |
  | 2015-02-13 | 1.0.2   | Handle the case of an object created (no lifecycle)          |
  | 2015-02-06 | 1.0.1   | Fixed bug on the reporting: when several rules apply, then only the last report is being displayed |
  | 2015-02-03 | 1.0.0   | First released version                                       |

  ## Installation

  Expand the ZIP file, then copy the contents of the folders `itop-stencils` and `itop-object-copier` into the `extensions` folder of iTop and launch the setup again.

  Make sure that the web server has enough rights to read the content of the `extensions` folder and all its sub-folders before launching the setup

  When prompted to select the extensions to install, check “Object copier” and “Stencils” in the list of available extensions.

  ## Configuration

  | Setting name | Description       | Example |
  | ------------ | ----------------- | ------- |
  | rules        | an array of rules |         |

  A rule is made of…

  | Rule setting name  | Description                                                  | Example                                                      |
  | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | name               | A unique identifier (not used yet)                           |                                                              |
  | trigger_class      | The class of objects triggering the copy                     | UserRequest                                                  |
  | trigger_scope      | Any OQL returning objects of the class *trigger_class*       | SELECT UserRequest JOIN Team … WHERE Team.org_id = 123       |
  | trigger_state      | Optional: the reached state. If left blank, then the object creation will trigger the actions. If a lifecycle is defined, specifying “new” has the same effect as leaving the parameter blank | assigned                                                     |
  | report_label       | Optional: Label or dictionary entry for the report displayed on the created/modified triggering object (additional banner). The feedback is disabled if this entry is missing | A task list has been created for the ticket                  |
  | templates          | An OQL. The parameters :trigger->xxx are available to filter on the triggering object | SELECT Template WHERE team_id = :trigger->team_id            |
  | copy_class         | The class of objects to create for each template             | WorkOrder                                                    |
  | copy_actions       | A series of **actions** (see below explanations) that will be executed on each couple template/copy | …                                                            |
  | copy_hierarchy     | Optional. Must be set to copy a hierarchy of templates       | array('template_parent_attcode'⇒'parent_id', 'copy_parent_attcode'⇒'parent_id') |
  | retrofit_from_copy | Optional: A series of **actions** (see below explanations) to be executed back on the triggering object, for each copy (the copy being the object from which values will be picked) | …                                                            |
  | copy_from_trigger  | **New in 1.0.4** - Optional: A series of **actions** (see below explanations) to be executed on the copy, the triggering object being the data source | …                                                            |
  | retrofit           | A series of **actions** (see below explanations) to be executed back on the triggering object. Will be executed once, and after all the retrofit_from_copy actions have been performed | …                                                            |

  report_label can be localized without the burden of create dictionaries. To do so, create the settings report_label/<language_code> (e.g. “menu_label/FR FR”) for each supported language. The setting report_label will be the default value.

  If copy_hierarchy is set, then make sure that the query *templates* will **not** return at the same time templates and one of their children. Otherwise, children templates will be instantiated a number of times (first as a template, then and as child of one of the templates). Adding the condition *AND parent_id = 0* will be sufficient in most of the cases.

  An **action** is specified as a string having formatted as “verb(arg1[,arg2[…]])”. It implies a **source** object and a **destination** object. *Source* and *destination* objects both depend on the context in which the *series of actions* is defined:

  - copy_actions: *source* is the current template object, *destination* is the corresponding copy
  - copy_from_trigger ( **new in 1.0.4** ): *source* is the triggering object, *destination* is a copy
  - retrofit_from_copy: *source* is a top level copy, *destination* is the triggering object
  - retrofit: *source* and *destination* are the triggering object

  ![img](https://www.itophub.io/wiki/media?media=extensions%3Astencils-actions.png)

  The following *verbs* are available:

  | Verb              | Parameters                     | Description                                                  |
  | ----------------- | ------------------------------ | ------------------------------------------------------------ |
  | clone_scalars     | <none>                         | Copy all the scalar attributes from *source* to *destination* |
  | clone             | attcode1,attcode2, …           | Copy the given attributes from *source* to *destination*     |
  | reset             | attcode                        | Reset the attribute (on *destination*) to its default value  |
  | nullify           | attcode                        | **New in 1.0.6** - Reset the attribute to its null value (will appear to be *undefined* from the end users perspective) |
  | copy              | att_to_read,att_to_write       | Copy from att_to_read (*source*) to att_to_write (*destination*) |
  | append            | attcode,string                 | Append the string to the attribute (*destination*). The string can contain **placeholders** (see explanations below). Commas must be escaped with a backslash. Newlines (\n) are allowed. The character set must be utf-8. |
  | set               | attcode,value                  | Set a value (*destination*). If the value is a string, it can then contain **placeholders** (see explanations below). Commas must be escaped with a backslash. Newlines (\n) are allowed. The character set must be utf-8. |
  | add_to_list       | attRead,attWrite,attLink,value | attRead (*source*) is an external key, attWrite (*destination*) is a N-N link set, attLink is an attribute on the link class that will be set to <value> |
  | apply_stimulus    | stimulus code                  | Applies a stimulus on *destination*. Note that this verb does record the object |
  | call_method       | function name                  | **New in 1.0.4** - Calls the provided method on the written object. Its prototype must be “public function xxxx($oSource)”. The function can send exceptions in case of failure. In such a case, the error message gets displayed in the log/error.log file |
  | clone_attachments | <none>                         | **New in 1.1.0** - Copy all the attachments from *source* to *destination* |

  There is no verb for recording (insert/update), because the module is in charge of that. This is of particular interest when implementing *call_method*: you do not need to call DBUpdate on the *destination*. On the other hand, should you modify the *source* object, then you have to save it to the DB. Anyhow it is wiser to perform the modification from another actions set, where the modified object will actually be the *destination*.

  Available *placeholders*:

  - $this->attcode$ where *this* represents the *source* object
  - $trigger->attcode$, where *trigger* represents the triggering object (only for copy actions)
  - $current_contact_id$
  - $current_contact_friendlyname$
  - $current_date$
  - $current_time$

  *Limitations*

  - **Before 1.1.2** with iTop 2.4.0 or above, if you have defined a custom date format for your iTop, the a date attribute is not decoded correctly when using *$this->attcode$* or *$trigger->attcode$*, leading to an error `| Error | itop-stencils: rule #3 - Action: set(start_date,$trigger->start_date$) - Wrong format for date attribute start_date, expecting "Y-m-d H:i:s" and got "13-12-2018 00:00:00"`.
  - **From 1.1.2 (and iTop from 2.4.0) for Date (or DateTime) attributes only,** the following syntax as to be used:
    - *$this->raw(attcode)$* or *$trigger->raw(attcode)$*

  ## Configuration example

  ```
  'itop-stencils' => array(
     'rules' => array(
        array(
           'name' => 'Work orders',
           'trigger_class' => 'UserRequest',
           'trigger_scope' => 'SELECT UserRequest',
           'trigger_state' => 'assigned', // triggered when reaching this state
           'report_label' => 'A task list has been created for the ticket', // Label or dictionary entry
           'report_label/FR FR' => 'Une liste de tâche a été créée pour ce ticket',
           'templates' => 'SELECT WorkerOrderTemplate WHERE service_id = :trigger->service_id', // A query to define how to look for the templates
           'copy_class' => 'WorkOrder', // Class of the copied templates
           'copy_actions' => array( // Series of actions to preset the object in the creation form
              'clone(name)',
              'clone(description)',
              'set(ticket_id,$trigger->id$)',
              'set(team_id,$trigger->team_id$)',
              'set(agent_id,$trigger->agent_id$)',
           ),
           'copy_hierarchy' => array(
              'template_parent_attcode' => 'parent_id',
              'copy_parent_attcode' => 'workorder_parent_id'
           ),
           'retrofit' => array( // Series of actions to retrofit some information from the created object to the source object
              'set(private_log,A task list has been created for the ticket)',
           ),
        ),
     ),
  ),
  ```

  ## Limitations

  These are the limitations of Object Copier.

  The following types of attributes are currently not handled and therefore cannot be preset (and no error message is given):

  - 1-N links (e.g. Server Interfaces)
  - Attachments
  - Blobs
  - Stop watches

  The workaround is to use the verb 'call_method' (new in 1.0.4) and implement your need as a method of the destination object.

  ## Troubleshooting

  All errors are logged to the file log/error.log

  The behavior from the end-user perspective is:

  - If no template have been found, the rule is ignored
  - If an error is found (wrong OQL, the target object cannot be written, …) nothing is shown in the GUI.