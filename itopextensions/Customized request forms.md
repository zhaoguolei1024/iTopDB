# Customized request forms

- name:

  Customized request forms

- description:

  Define personalized request forms based on the service catalog. Add extra fields for a given type of request.

- version:

  2.1.2

- release:

  2020-03-27

- itop-version-min:

  2.3.2

- code:

  combodo-customized-request-forms

- state:

  stable

- alternate-name:

  Request Templates

- diffusion:

  iTop Hub

Check the upgrade process, if you upgrade from a version before 2.1.0 of this extension

**Other versions of this component:** [1.0.5](https://www.itophub.io/wiki/page?id=extensions%3Arequest-templates_1_0)

## Features

This module provides the capability to add dynamically additional fields on a User Request in order to better qualify it. The additional fields proposed will be different based on the selected Service / Service Subcategory.

For instance when a user asks for a “new virtual machine”, then we may want him to provide the number of CPUs, the quantity of RAM and the type of OS in structured fields rather than hoping that the user will provide them by himself, in the `Description` field.

You just have to define your template and then when a user creates a ticket, the additional fields will appear in the ticket edition form, based on the selected service subcategory.

A request template is related to a service subcategory. A request template can add one or multiple additional fields to User Requests. The additional fields can be of the following types:

- Date and Date Time
- String (formated with regular expression if needed)
- Text area
- CSV list
- List based on OQL query
- Duration
- Readonly/hidden fields

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2020-03-26   | 2.1.1   | - Fix regression when submitting with transition form - Fix remove TemplateFieldValue on object deletion |
| 2019-12-04   | 2.1.0   | - Request template fields are now queryable - Fix missing menus on request template view - Update DE translations |
| 2019-01-30   | 2.0.14  | Fix regression introduced in 2.0.10: custom date formats no longer working |
| 2018-12-19   | 2.0.13  | - Fix unnecessary error messages popping on the screen when a DoCheckToWrite fails - Fix execution notice (check array existence) - Update spanish translations (thanks to Miguel Turrubiates!) |
| 2018-06-27   | 2.0.12  | Add DE translation                                           |
| 2018-06-26   | 2.0.11  | ES + BR translations, default search attributes              |
| 2018-01-26   | 2.0.10  | Ticket fields can now be used in customized forms. Also fixed 2 bugs for usage in notifications templates ($service_details$) : - N°1079 When the user leaves it undefined, then this is shown as an error message in the email: “Custom field error: Wrong format: missing template_data” ; - N°1080 When a field aims at selecting an object, the email body shows the id of the selected object. |
| 2018-01-05   | 2.0.9   | Customized forms are now compatible with Incident            |
| 2017-11-13   | 2.0.8   | Service_details is now documented on UserRequest creation before notification |
| 2017-09-08   | 2.0.7   | Request template value not set in notification when creating an object |
| 2017-03-01   | 2.0.6   | Added module setting to reset template fields value when changing to a different template that contains fields with same codes |
| 2016-12-13   | 2.0.5   | Fixed issues when used in cunjunction with the legacy portal. Requires iTop > 2.3.2 for the date/time pickers to work fine |
| 2016-11-29   | 2.0.4   | Implemented placeholders (e.g. $this->html(service_details)$. Requires iTop > 2.3.1 for the placeholders to work fine. |
| 2016-09-08   | 2.0.3   | Added validation pattern to Date and DateTime fields. Fixed a PHP Warning when launching the cron manually. |
| 2016-09-02   | 2.0.2   | Hidden and Read-only fields are now rendered like multiline strings (like a textarea, though it is read-only) - Note that this will work fine in the console with iTop 2.3.0+, but requires iTop > 2.3.1 to take advantage of this enhancement in the enhanced customer portal (no change in the legacy portal!) |
| 2016-08-03   | 2.0.1   | Support of the console and the enhanced customer portal (both require iTop 2.3.0, otherwise the behavior is the same as 1.0.5) |
| 2015-11-26   | 1.0.5   | Fix for crash when submitting a ticket from the portal for a template with an ENUM field containing some special characters. |
| 2015-09-29   | 1.0.4   | Fix for a crash when a “drop-down list” field contains some weird characters (accents, question marks…) at the beginning of the list of values. |
| 2014-12-10   | 1.0.3   | Cosmetics on the module name.                                |
| 2014-04-03   | 1.0.2   | Minor fix to allow non admin users to import Template fields in CSV. |
| 2014-03-10   | 1.0.1   | Bug fix for template fields with the same name as an attribute of the object. |
| 2014-02-05   | 1.0.0   | First version, never validated.                              |

## Limitations

The placeholders will not work with iTop 2.3.1 and older.

## Installation & upgrade

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

*Upgrade*: In order to be able to search for old User Requests which do have a particular value set in a request template, the iTop administrator need to run once a special page which explode every (*User Request*) template data into new tables, so it can be queried with OQL.

```
php populateTemplateFieldValue.php --append
```

You can either use “--append” or “--reset”, same results, might differ in execution time.

- --reset recomputes from scratch
- --append explode only the template data which have not been exploded yet

## Configuration

The following settings can be adjusted in the iTop configuration file, in the section `itop-request-template`:

| Parameter   | Type   | Description                                                  | Default Value |
| ----------- | ------ | ------------------------------------------------------------ | ------------- |
| copy_to_log | string | The attribute into which the template values should be copied. Set to an empty string to disable this behavior. | public_log    |

The following settings can be adjusted in the iTop configuration file, in the section `templates-base`:

| Parameter                       | Type    | Description                                                  | Default Value |
| ------------------------------- | ------- | ------------------------------------------------------------ | ------------- |
| hidden_fields_profiles          | string  | CSV list of profiles. If the user has ANY of the listed profile, she will NOT see the fields of type “hidden”. | Portal user   |
| reset_fields_on_template_change | boolean | If set to “true”, fields value will be reset when changing template, even if some of the fields have the same code. | false         |
| view_extra_data                 | string  | ![FIXME](https://www.itophub.io/lib/images/smileys/fixme.gif) | relations     |

## Usage

### Create request template

From the Service Management menu, click on “Request template”:[![img](https://www.itophub.io/wiki/media?w=200&tok=23c619&media=extensions%3Aitop-request-template-menu.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-menu.png)

The pages show a list of already defined request templates. Click on the button “new” to create a new one:

[![img](https://www.itophub.io/wiki/media?w=300&tok=cd18b3&media=extensions%3Aitop-request-template-new.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-new.png)

A request template is identified by its name the related service and service sub category.

The label is used on the portal to select a template if several are defined for a given service sub category.

The tab “Fields” is used to define the fields of the template:

[![img](https://www.itophub.io/wiki/media?w=800&tok=b80b46&media=extensions%3Aitop-request-template-list-field.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-list-field.png)

Click on “Create a new field” to define a new one:

[![img](https://www.itophub.io/wiki/media?w=300&tok=c4b80b&media=extensions%3Aitop-request-template-create-field.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-create-field.png)

Here is a complete description of the properties:

| Property            | Description                                                  | Example                                        |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Code                | Unique identifier, that can be used in the queries defined in another field. This value must be made of alphanumeric characters and cannot start with a number | model                                          |
| Order               | An integer that defines in which order the fields are displayed in the form | 3                                              |
| Label               | Label seen by the user who is prompted for entering a value  | Device Model                                   |
| Mandatory           | Wether or not the user must enter/select a value             | yes                                            |
| Input type          | … see a detailed description hereabove                       | List                                           |
| Values (OQL or CSV) | Used **for drop-down lists only** to define the list of allowed values for this element. This can be either a comma separated list of values (e.g. “`high,medium,low`”). The OQL can have a parameter in the form `:template->code`, where code is the code of another field. It can also use placeholder like `:current_contact->org_id` or `:this->org_id` which refer to the customer of the Ticket | SELECT Model WHERE brand_id = :template->brand |
| Initial value       | Used to set an initial value for text or text area fields    | xyz                                            |
| Format              | Allows you to define a regular expression for validating text fields | `^[a-zA-Z]$`                                   |

When providing “Values” in **CSV: write all values in one line**, without carriage return

When providing “Values” in OQL: **do not use friendlyname** in the OQL query.

| To limit to …  | use this regex within `Format`                               |
| -------------- | ------------------------------------------------------------ |
| an email       | [a-zA-Z0-9._&'-]+@[a-zA-Z0-9.-]+\.[a-zA-Z0-9-]{2,}           |
| a phone number | ^\+?[0-9\ ]{8,20}$                                           |
| a url          | https?,ftp)\://([a-zA-Z0-9+!*(),;?&=\$_.-]+(\:[a-zA-Z0-9+!*(),;?&=\$_.-]+)?@)?([a-zA-Z0-9-.]{3,})(\:[0-9]{2,5})?(/([a-zA-Z0-9%+\$_-]\.?)+)*/?(\?[a-zA-Z+&\$_.-][a-zA-Z0-9;:[\]@&%=+/\$_.-]*)?(#[a-zA-Z_.-][a-zA-Z0-9+\$_.-]*)? |

The input type can have one of the following values:

| Input type     | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| Date           | A pure date, entered by the mean of a calendar, or directly typed in |
| Date and time  | Date and time, entered by the mean of a calendar, or directly typed in |
| Drop-down list | A list as defined by the property **Values**                 |
| Duration       | A time lapse                                                 |
| Hidden         | A value that will not be seen by the end-user (customer portal), but it will be seen by an agent (console). The value is set by the mean of the property **Initial value** |
| List           | A value to select amongst a list of proposed values. These values are defined by the mean of the property **Values …** |
| Read-only      | A value defined in **Initial value**, and which cannot be modified by anybody |
| Text           | A single line of text, which format may be enforced by setting **Format** |
| Text area      | A text with several lines                                    |

The tab “Preview” displays a preview of the template as it will be displayed in the console:

[![img](https://www.itophub.io/wiki/media?w=300&tok=883cbf&media=extensions%3Aitop-request-template-preview.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-preview.png)

### Behavior on the Customer Portal

If a end-user selects a service sub-category on the customer portal which is related to a request template, the specific fields for this template are displayed, grouped under the denomination **Service details**.

[![img](https://www.itophub.io/wiki/media?w=500&tok=2335d0&media=extensions%3Aitop-request-template-portal-enhanced.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-portal-enhanced.png)

This additional information is copied into the Public log when the User Request is created:

[![img](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-public-log-enhanced.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-public-log-enhanced.png)

It is also possible for a Support Agent to see or edit the information in the details of the User Request, from the console:

[![img](https://www.itophub.io/wiki/media?w=500&tok=ae4406&media=extensions%3Aitop-request-template-console.png)](https://www.itophub.io/wiki/media?media=extensions%3Aitop-request-template-console.png)

### Template placeholders

In a notification template, or anywhere else where a template can be used, the following placeholders will be available.

Assuming that *this* is a UserRequest:

- $this->service_details$: a plain text representation of the selected values. This is suitable for a plain text email. Though it seems possible to use it within an HTML document, by using a PRE tag, this is NOT recommended because HTML entities (like <) still need to be escaped.
- $this->html(service_details)$: an HTML representation of the selected values.

Hidden fields are forcibly excluded from the placeholders.

When a template value corresponds to an object selected into iTop, the returned value will be the friendly name of the object.

## Questions & Answers

**Question: Can I get the UserRequest which do not have a associated Request Template**
Answer: Yes & No.

Query like this will fails

```
 SELECT UserRequest WHERE ISNULL(service_details) = 1
```

While such query will work, with the limitation that if you have added or removed Request Template to service subcategories after the creation of User Request using those service Subcategories, then the result will be wrong.

```
SELECT u,rt FROM UserRequest AS u
JOIN ServiceSubcategory AS ss ON u.servicesubcategory_id=ss.id
JOIN RequestTemplate AS rt ON rt.servicesubcategory_id=ss.id
WHERE ISNULL(rt.name) = 1
```

**Question: Can I search for UserRequest which do have a particular value in a field of the associated Request Template**
Answer: Yes with a recent enough version (above 2.1.0)

- [Searching for a value](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Arequest-templates&codeblock=2)

  `SELECT UserRequest AS u   JOIN TemplateFieldValue AS v ON v.obj_key=u.id  WHERE v.template_name="Laptop ordering"    AND field_code='size'     AND field_value='wide'`

You must specify the name (or id) of the Request Template, as the `field_code` may not be sufficient to identify uniquely a particular template, the same code could be used on multiple Templates.

- [Searching for a related object](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Arequest-templates&codeblock=3)

  `SELECT u,m FROM UserRequest AS u   JOIN TemplateFieldValueLnk AS v ON v.obj_key=u.id  JOIN Model AS m ON v.field_target_key = m.id  WHERE v.template_name="Desktop ordering details"    AND field_code='model'     AND field_target_class='Model'`

**Question: I have installed version 2.1, but OQL queries does not return old User Request.**
Answer: With version 2.1.0 or above of this extension, if you want to perform queries over User Requests made prior to the deployement of this version, you have to launch once, a cli script which will explode the data created before into the new queryable objects.

The command requires to be on iTop server using the `web` user:

```
cd /path/to/itop/
cd env-production/templates-base/
php populateTemplateFieldValue.php --append
```

This command explodes not-yet-exploded CustomAttribute data into new objects TemplateFieldValue and TemplateFieldValueLnk.

Note: An alternate mode is `php populateTemplateFieldValue.php –reset` which empty the new tables and rebuild them from scratch. Just after the upgrade to 2.1, the 2 modes are pretty similar.

Always run this kind of heavy script on your integration environment first, with a copy of your production data

You should run this command with your webserver user, otherwise you may have difficulties to access cache files inside data/cache-production/