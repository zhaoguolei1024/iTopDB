# Customer Survey

- name:

  Customer Survey

- description:

  Create a quizz, send it to your customers, collect the replies.

- version:

  2.4.2

- release:

  2020-03-06

- itop-version-min:

  2.3.2

- code:

  customer-survey

- state:

  stable

- diffusion:

  iTop Hub

For iTop versions older than 2.1.0 use a previous version of this component, for iTop 2.1.0 or newer use this version of the component.

**Other versions of this component:** [2.1.1](https://www.itophub.io/wiki/page?id=extensions%3Acustomer-survey_2_1)

Integrates with the iTop CMDB so that you can send a statisfaction survey to the customers documented in iTop.

## Features

A quizz is made of a list of questions of the following type:

- a free text comment
- a choice within a list
  - either a list defined once for all in your quizz (usually a rating, from *bad* to *good*)
  - or a list defined only for that question (e.g. types of products)

The quizz can be split on several pages. It has an introduction and a footer message.

A quizz will be used in one or more survey campaigns.

The survey defines to whom the quizz will be sent (scope given as an OQL query). Customers will receive an email with an URL to reply to the quizz.

The results can be viewed and exported to an Excel file.

By default, the module keeps track of the link between the reply and the contact. As this is prohibited in some countries, depending on local regulations, the module has a anonymous mode.

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2020-03-06   | 2.4.2   | * Update DE translations                                     |
| 2019-05-31   | 2.4.1   | * Remove unused external keys pointing to obsolescence flags |
| 2019-03-06   | 2.4.0   | * Migrate code to XML * Add horizontal scrollbar to large survey * Hide buttons on a already answered survey * Fix paging in survey's progress tab * Fix survey a preview/send compatibility issue with iTop 2.3+ * Fix Excel and CSV export error * Once a survey is finished, you now can't edit contact list or send them another notification for this survey |
| 2018-12-07   | 2.3.0   | * Update translations * JQuery compatibility (JQuery 3 since iTop 2.6) |
| 2018-06-26   | 2.2.1   | ES translation, 2.5 compatibility                            |
| 2015-04-16   | 2.2.0   | Fixed a compatibility issue with iTop 2.1.0. On the other hand, it now requires iTop 2.1.0+. Note that iTop core has been updated so that any 2.1.x version of customer survey will be compatible with iTop 2.2.0+ |
| 2014-04-18   | 2.1.1   | Fixed the notification to the survey sender (on behalf of), integrated the German translation, completed the French translation |
| 2014-03-03   | 2.1.0   | Requires iTop 2.0.2. Added the printable results report. Removed change tracking breaking the anonymity |
| n/a          | 2.0.1   | Compatible with iTop 2.0.1. Has never been released          |
| n/a          | 2.0     | Compatible with iTop 2.0. Has never been released            |
| n/a          | 1.2.1   | Compatible with iTop 1.2.1. Has never been released          |

## Limitations

A quizz and its questions can be modified even when surveys are running on it. The effects are unpredictible. Similarly, editing a survey when it is running has unpredictible effects (except adding recipients).

With iTop 2.5, 2.5.1 and 2.6.0 :

- “Export Raw Answers” “For Excel” or “As CSV” from “Results” tab doesn't work
- “Send Again” from Progress Tab doesn't work

## Requirements

Requires iTop 2.1.0

## Installation

Copy the contents of the zip file into the `extensions/customer-survey` folder of iTop and launch the setup again.

Make sure that the web server has enough rights to read the content of the `extensions` folder and all its sub-folders before launching the setup

When prompted to select the extensions to install, check “Customer Survey” in the list of available extensions.

## Configuration

The following settings can be adjusted in the iTop configuration file, in the section `customer-survey`:

| Parameter        | Type    | Description                                                  | Default Value                           |
| ---------------- | ------- | ------------------------------------------------------------ | --------------------------------------- |
| anonymous_survey | boolean | Set to true to garantee that the module will not keep track of who did a given reply | false                                   |
| quiz_scale       | string  | CSV list of labels (5 must be given?) that define the default scale labels | Very bad, Bad, Average, Good, Very good |

## Usage

This module creates two new entries in the menu group *Helpdesk*:

![img](https://www.itophub.io/wiki/media?w=200&tok=dfa17e&media=extensions%3Acustomer-survey-menus.png)

Quizzes and surveys are two new types of data:

- A quizz is a series of questions in a given language.
- A survey defines the targetted people. It is also the way to follow-up on the progress and get a report on the replies.

## Create a quizz

The first step is to create a Quizz, i.e. a series of questions.

### Properties

In the tab “Properties”, you will have to specify the following properties:

| Property              | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| Name                  | A name for internal identification of the quizz              |
| Description           | A description for internal usage                             |
| Quizz Language        | The language in which the quizz must be displayed. This choice has an effect on the labels of the buttons and other things like “this question is mandatory” |
| Default Quizz Choices | Standard choices for questions of type “predefined choices”. Leave it blank to use the setting from the configuration file: *quiz_scale* |
| Title                 | The first page title: *<title> page 1 of 2*                  |
| Introduction          | Just below the title, an introduction message (optional)     |
| Conclusion Message    | Displayed after the quizz has been completed and submitted. This is the place to say thank you! |

### Questions

In the tab “Questions”, enter your questions and page breaks.

To modify a question, save the Quizz first, then from the “Questions” tab, click on the link to display the details of the desired question. You can then click on the “Modify” button to alter the question, as you would do for any element in iTop.

We recommend to use non-consecutive ordering numbers (e.g. 100, 200, 300) in order to easily insert a new question without having to renumber (i.e. modify) all the questions.

| Type of question   | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| Free text          | This is the place for a user comment.                        |
| Predefined choices | The user is asked to select an item out of a list defined for the whole quizz, in the property *Default Quizz Choices*. This is the way to have a standard defined at the quizz level or at the application level. |
| Specific choices   | The user is asked to select an item ouf of a list defined solely for this question. |
| Page break         | Though this is not a real question, a page break is inserted into the stream of questions. The title and description of the page break replace respectively the quizz title and introduction, for the page that comes AFTER the break. |

### Preview

Once the quizz has been created, click on the tab “Preview” to display the quizz as it will be seen by your customers:

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-quiz-preview.png)

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-quiz-preview2.png)

## Start a survey

### Create the survey

In the tab “Properties”, set the following properties:

| Property                 | Description                                                  |
| ------------------------ | ------------------------------------------------------------ |
| Quizz                    | Select the quizz amongst the already created quizzes. Note: the language is displayed right above: it will be updated after the quizz is saved. |
| On behalf of             | The sender of the survey. The email will be sent with *from* set to this person. The list proposes any person documented in iTop. |
| Email on completion      | If set to *yes*, and if the sender has an email address, then she will receive an email each time a recipient completes the survey |
| Email subject            | The email title.                                             |
| Email body               | The email body, in HTML.                                     |
| Recipients of the survey | An OQL phrase, from the *Query phrasebook* (in the menu *Admin tools*) |

It is possible to complete the list of target contacts defined by the OQL: go into the Additional contacts tab, and add them one by one.

### Tune the survey

Creating the survey does not send the message. You still have the possibility to adjust the settings, review the quizz.

In the *Other Actions* menu, click on *Send me a sample message*.

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-action-samplemsg.png)

It reminds you the settings of the survey.

Confirm by clicking the *Send me a sample message* button.

You will receive a sample email, and see what your customers should receive. In particular, this is the opportunity to check language consistency.

### Send the survey

In the *Other Actions* menu, click on *Start the survey*.

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-action-start.png)

It reminds you the settings of the survey.

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-start.png)

Confirm by clicking the *Start the survey* button.

The survey is now started:

- its name is made of the quizz name and the survey start date
- two new tabs have been added: *Progress* and *Results*

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-started.png)

All target contacts will receive an email with a link to the quizz form.

When the survey is running, it is still possible to add recipients: edit the survey and add contacts into the *Additional Recipients* tab. The newcomers will be notified as you save the changes on the survey.

A survey is not closed automatically: when 100% of the users have given their answer, it is still possible to add new contacts and wait for their replies.

### Replying to the survey

Replying does not require to login to iTop.

The customer has the capability to *suspend* the quizz at any time by clicking on the *suspend* button.

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-suspend.png)

Resuming can be done either by using the URL provided in the above popup, or by using again the URL provided in the received email.

### Monitoring the progress

The tab *Progress* gives an overview of who has received the quizz:

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-progress.png)

Select a contact and click on *Send again* to resend the email:

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-resend.png)

Email subject and body are prepopulated with the orginal values. Adjust them and confirm by clicking on the button *Send!*.

### Exploiting the resuls

Just after the survey has been started, the result tab will look like this:

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-results.png)

With data, the results look like this:

![img](https://www.itophub.io/wiki/media?media=extensions%3Acustomer-survey-results-completed.png)

You can use the links Export Raw Answers “For Excel” and “As CSV” at the bottom of the page to export the results of the survey, or the link at the top-right “Printable version” to obtain a printable version of the results page.