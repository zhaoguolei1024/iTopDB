# Multiple email per contact

- name:

  Multiple email per contact

- description:

  Identify sender on multiple email addresses for Ticket creation from email

- version:

  1.0.1

- release:

  2019-05-16

- code:

  combodo-email-alias

- state:

  Stable

You need to track multiple email addresses for a Contact? Then this extension is for you.

You are annoyed with [Mail to Ticket Automation](https://www.itophub.io/wiki/page?id=extensions%3Aticket-from-email) which does only support a single email address per Person? This extension will also address this issue.

## Features

This extension adds a new class EmailAlias linked to a Contact, to store alternate email addresses for the same Contact.

When requester send an email with an email address which is not the one registered on their Person in iTop, their email request is usually rejected, because of spams. With this extension, once you have defined the various email addresses associated with your Persons, the creation of ticket from email, will retrieve the right caller whatever registered address the person used.

## Revision History

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2019-05-16 | 1.0.1   | Add recognition of related contacts (CC) also by their email alias |
| 2019-02-15 | 1.0.0   | First version                                                |

## Limitations

Only works with iTop 2.3.0 and above

## Requirements

This extension expends [Mail to Ticket Automation](https://www.itophub.io/wiki/page?id=extensions%3Aticket-from-email) from version 3.0.1, but can be used without it.
It is not compatible with older version before [2.6.12](https://www.itophub.io/wiki/page?id=extensions%3Aticket-from-email_2_6) included.

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

No configuration required

## Usage

#### Documenting Email Aliases

1. Open a Contact, for which you want to document additional email addresses
2. Go to the new tab `Email aliases`
3. Create a new Email Alias
4. Fill the form and Submit

![img](https://www.itophub.io/wiki/media?media=extensions%3Aemail-alias-create.png)

You can create multiple Email Aliases for the same Person![img](https://www.itophub.io/wiki/media?media=extensions%3Aemail-alias-edit.png)

| Field   | Usage                                                        |
| ------- | ------------------------------------------------------------ |
| Email   | the email address in unix format                             |
| Contact | the Contact associated with this email address               |
| Type    | to differentiate: `Personal`: non-professional email `Professional - by function`: associated with a **function** `Professional - by name`: based on Person **name** |
| Comment | Free text                                                    |

#### Moving a functional email to another Person

Later a functional email address may not be linked to the right person anymore, in which case you can edit it and change the associated Contact.![img](https://www.itophub.io/wiki/media?w=400&tok=aa6f0c&media=extensions%3Aemail-alias-modif.png)

#### Notifying on Email Alias

It is possible to notify the persons using one of their email alias, based on its type for example.

```
SELECT EmailAlias AS e JOIN Person AS p ON e.contact_id = p.id JOIN [...] WHERE e.type = "functional"
```