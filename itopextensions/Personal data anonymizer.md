# Personal data anonymizer

- name:

  Personal data anonymizer

- description:

  Helper extension to quickly anonymize Persons in iTop.

- version:

  1.0.0

- release:

  2018-07-04

- itop-version-min:

  2.4.0

- download:

  https://store.itophub.io/en_US/products/combodo-anonymizer

- code:

  combodo-anonymizer

An helper extension to quickly anonymize Persons in iTop.

## Features

- Remove the personal data from a given person without deleting the Person object in iTop by “anonymizing” this person.
- Can be done one by one, or in bulk (from a list of Persons)
- Remove the information from the Person, its history and the Case Logs written by this person (not the actual text written by this person, but the header mentioning this person)
- Can be scheduled to automatically anonymize all persons which have been marked as obsolete for a given period (i.e. 60 days)

## Revision History

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2018-07-04 | 1.0.0   | First public version, fixes an issue in the menu creation for iTop 2.4.x. |
| 2018-06-07 | 0.0.3   | Bug fix: fixed the anonymization of case logs.               |
| 2018-06-06 | 0.0.2   | Second version, compatibility extended to iTop 2.4.0.        |
| 2018-05-31 | 0.0.1   | First version compatible with 2.5.x only                     |

## Limitations

It is very difficult to guarantee an effective and complete anonymization of a person since the relations of this person can be used to (re) discover who this person was actually.

What this extension performs is actually called a “Pseudonymization”. Unless you are dealing with sensitive data (medical records, credit card numbers…) such a pseudonymization is generally considered as sufficient to protect the personal data in a business context.

In the context of iTop, with extension such as `Mail to Ticket Automation`, the ticket description and caselog entries can contain the person signature, which will not be cleaned-up by this extension.

A good practice would be to archive then delete Tickets related to anonymized caller.

If you have two persons with the same name and you anonymize one, then history entries from both persons will be anonymized.
If a person name changes, then history and caselog headers entries related to its former name will not be anonymized.

## Requirements

This extension requires iTop 2.4.0 or above

## Configuration

You can configure whether or not to activate the automatic anonymizations (performed by a background task) using the “Admin tools / Configuration / Anonymization” menu:

[![Configuration of the Automatic Anonymization](https://www.itophub.io/wiki/media?w=600&tok=9a5d2b&media=extensions%3Aanonymization-configuration.png)](https://www.itophub.io/wiki/media?media=extensions%3Aanonymization-configuration.png)

If enabled, the anonymization background task will **run once a day** and automatically anonymize the obsolete contacts based on the delay defined by the configuration, and delete **all** notifications, *not only those which were sent to that person* which are older than a number of days.

## Usage

This extension adds a new custom action “Anonymize” in the “Other Actions” menu on the Person class.

[![Anonymize One Contact](https://www.itophub.io/wiki/media?w=600&tok=1adef8&media=extensions%3Aanonymize_one.png)](https://www.itophub.io/wiki/media?media=extensions%3Aanonymize_one.png)

After a confirmation message, the person is anonymized and the result is displayed:

[![img](https://www.itophub.io/wiki/media?w=600&tok=cd13da&media=extensions%3Aanonymized.png)](https://www.itophub.io/wiki/media?media=extensions%3Aanonymized.png)

All the relations beween the person and the other objects are preserved, but:

- The history of the person object is cleared (with just an entry showing that this person has been anonymized)
- The case log *headers* (in all the classes which contain a case log) are purged for any reference to the name of this person
- The history entries (for the changes made by the user account associated with this person) are purged from the name of the person.

The same action can be performed on a list (but the list MUST be a list of Persons only)

[![img](https://www.itophub.io/wiki/media?w=600&tok=706431&media=extensions%3Aanonymize_all.png)](https://www.itophub.io/wiki/media?media=extensions%3Aanonymize_all.png)

If you have chosen (in the “Preferences” menu) not to display the obsolete items, the list of anonymized contacts will appear empty after the anonymization has been performed, because all contacts are now 'inactive' and thus marked has obsolete.

## The anonymization mechanism

For a given Person, the anonymization process consists in:

- clearing all non-mandatory fields
- filling mandatory fields with predefined values (the `name` is set to “Contact” and the `first_name` is set to “Anonymous”)
- marking the contact as “inactive”
- saving the contact in the database
- clearing the history of the contact, with just one history entry remaining to indicate that this contact was *anonymized*.
- replacing the *friendlyname* of the contact in all case log headers by a string of “*” (considering the design of the case logs it is much simpler and faster to preserve the exact same length for each case log header)
- replacing the *friendlyname* of the contact in all CMDBChange records by its anonymized name.

### Adapting the anonymization to your datamodel

The extension adds several methods to the `Person` class. Since these methods are defined in XML you can easily alter / redefine them in XML.

- `Anonymize()`: This is the function called by the anonymizer extension. Unless you want to completely redefine the anonymization mechanism, you should not need to modify it.
- `SetAnonymousValues()`: Fill the mandatory fields of the current Person with anonymous values. Adapt this method if you have altered the standard data model by adding mandatory fields on the Person class. The default implementation is the following:

```
/**
 * Fill the mandatory fields of the current Person with anonymous values.
 *
 * Adapt this method if you have altered the standard data model by  adding 
 * mandatory fields on the Person class.
 */
public function SetAnonymousValues()
{
    // Put some more fancy values
    $this->Set('name', Dict::S('Anonymization:Person:name'));
    $this->Set('first_name', Dict::S('Anonymization:Person:first_name'));
    // Mark the contact as obsolete
    $this->Set('status', 'inactive');
}
```

- `PurgeHistory($sOriginalName, $sAnonymizedName)`: this function removes all references to original name of the Person from the history of modifications and replaces them with the new anonymized name.
- `CleanupCaseLogs($sPersonFriendlyName)`: removes the given *friendlyname* from all case log headers entries which where entered by this person.

The change history contains only the friendlyname of the person who made the change. As a result, if you have **two persons with the same name** and you anonymize one, then history entries from both persons will be anonymized.

If a **person name changes**, then history and caselog headers entries related to its former name will not be anonymized.