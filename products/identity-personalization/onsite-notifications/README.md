# Product outline: Onsite Notifications (ie. personalized notifications that show on VA.gov)

**Last updated: May 31, 2023 -- added link to security documentation**

### Communications

- **GitHub Label**: vsa-authenticated-exp; onsite-notifications
- **Slack channel**: [#accountexp-authexp](https://dsva.slack.com/channels/accountexp-authexp)

### Roles

#### On-site notifications team

|Name|Role|Email|
|----|----|-----|
|Samara Strauss |OCTO Lead| samara.strauss@va.gov |
|Anastasia Jakabcin (AJ)|Product Manager| ana@adhocteam.us |
|Berni Xiong| Delivery Manager | berni.xiong@agile6.com |
|Angela Agosto |Designer| angela.agosto@adhocteam.us |
|Allison Lu| FE Engineer|	allison@cityfriends.tech |
|Derrick Ellerbie| Full Stack Engineer | Derrick.ellerbie@Agile6.com|


#### Partners

|Name|Role|Email|
|----|----|-----|
|Beverly Nelson| OCTO lead for VANotify| beverly.nelson@va.gov |
|Melanie Jones | VANotify PM | melanie.jones@oddball.io |

### Table of Contents

- [Overview](#overview)
- [Onsite notification criteria](#onsite-notification-criteria)
- [Problem Statement](#problem-statement)
- [User Outcomes](#user-outcomes)
- [Business Outcomes](#business-outcomes)
- [Measuring Success](#measuring-success)
- [Projects](#projects)
- [Security](#security)
- [Backend](#backend)
- [Frontend](#frontend)
- [Design](#design)

## Overview

VA.gov is in the process of implementing a comprehensive communication strategy to support email, text, and in-app (ie. on VA.gov) notifications. Currently, the VANotify team  builds and manages email notification support for VA.gov, and they are working in tandem with VEText to integrate support for text messages into their platform. The authenticated experience team aims to cover information around the third and final pillar -- notifications that show to logged-in users on VA.gov.

## Onsite notification criteria

### In scope

[This is reflective of the overall priorities for My VA and personalization](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/my-va#opportunities--priorities).

1. **Action items**: Our top priority for onsite notifications are any items that require a veteran to take action in order to move along a process. Examples might include alerting a veteran to an outstanding debt or copay that's due; alerting veterans to unread messages from their health care team; prompting Veterans to upload evidence to a disability claim; etc.
2. **Communicate high-priority benefit status & updates that don’t require action**: Our second priority is to communicate know high-priority updates that are generally important to people but don't necessarily require them to take any action. Examples might include an update to a claim; prescription shipment; a direct deposit payment to their account, etc.

### Out of scope

- **Benefit suggestions**: Currently, onsite notifications should not be used as a place to surface benefit suggestions. In the event VA.gov is able to support eligibility information, we need to think about if and how onsite notifications might fit into this.
- **Organizational announcements**: Onsite notifications should be personalized, so organization-wide announcements, emergency or otherwise, are out of scope.
- **Confirmation messages**: We do not need to show onsite notifications that confirm an action a person just took (eg. submitting a form).

## Problem Statement

- As a customer of the VA, I need to know if there are tasks I need to complete so that I can receive or manage my benefits.

## User outcomes

### Desired User Outcomes

- VA.gov users will be able to find and complete necessary tasks more quickly.
- As a result, VA.gov users may receive benefits or other outcomes more quickly.
- VA.gov users may also more easily avoid unideal outcomes if we can get information in front of them more quickly (eg. updating the number of dependents they have so their compensation payments are correct).

### Undesired User Outcomes

- Confusion or lack of syncing between on-site notifications/action items and email, text, or mail communications (data integrity). We can avoid this by building on the VANotify platform to ensure a synchronous experience between email, text, and notifications on VA.gov.
- An overwhelming amount of notifications makes it so that this update feels more like noise than a helpful tool.

## Business outcomes

### Desired Business Outcomes

- To create a unified experience through the VANotify platform. 
- Once the notification infrastructure is in place, it will be easy for VA business lines to get necessary action items in front of users with little lift.
- We'll be able to build more nuanced logic to get messages in front of certain audiences (eg. show a notification to all people who have a BVS hearing within the next 30 days). 
- We'll be able to show notifications on more than one page, or in a central location (eg. a notification center) that is accessible from all pages.

### Undesired Business Outcomes

- This tool becomes a bandaid for bad information architecture and navigation.
- This tool is over-utilized and results in more noise than guidance.

## Measuring success

- Initial metrics will be tracked as part of the [on-site notifications MVP](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/onsite-notifications/mvp#measuring-success).

## Projects

|Project| Launch date|
|-------|------------|
| Notification center MVP | In development |
|[Notification center discovery](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/onsite-notifications/2023-scaling-onsite-notifications/notification-center-discovery)| Discovery work complete Spring 2023|
|[Update design system component build](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/identity-personalization/onsite-notifications/update-design-system-component/README.md) | In development  |
|[Onsite notifications v2](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/onsite-notifications/2023-scaling-onsite-notifications#initiative-outline-scaling-onsite-notifications)|In development|
|[Onsite notifications MVP](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/onsite-notifications/mvp)| Launch completed October 24, 2022|

## Security
[Onsite Notifications Security Playbook](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/identity-personalization/onsite-notifications/mvp/launch-materials/onsite-notifications-security-playbook.md)

## Backend

### How it works

We receive on-site notifications from [VA Notify](https://depo-platform-documentation.scrollhelp.site/developer-docs/partner-services-upstream-services). For the MVP, the system works as follows:

- The debt management center backend (DMC) will add debts for a given set of users. Those debts will show up in the debt tool in VA.gov.
- Once a day, the DMC backend will send a batch request to VA Notify to send out notifications to folks alerting them that they have a new debt.
- VA Notify will then send out notifications:
  - An email notification (this existed prior to the on-site notification MVP and was an entirely separate effort).
  - A notification that shows on someone's My VA personalized dashboard if they are logged in and identity-verified (LOA3) on VA.gov.
  - Users receive notifications based on their preferences. Email notifications can be turned off; _on-site notifications can not_. 
- If VA Notify determines it should send the "you have a new debt" notification to VA.gov, it will send a `user id` and `template id` to VA.gov. This is what tells us (My VA) to show the "you have a new debt" notification and to whom.

[Additional technical documentation from VA Notify on how the on-site notification functionality works on VA.gov](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/va-notify/onsite-notifications/README.md#workflow-overview)

See [Onsite Notification Technical Overview](https://github.com/department-of-veterans-affairs/va.gov-team-sensitive/blob/master/products/identity-personalization/my-va/onsite_notifications/technical-overview.md) for more detailed technical workflows and explanations about the solution.

### How to test

Currently, there is only one notification to test (2022). In the future, there may be multiple notifications that need to be tested in different ways. 

- For information on how to test the on-site notification MVP ("you have a new debt"), [please refer to the project outline](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/onsite-notifications/mvp#how-to-test).

## Frontend

### Overview

- The frontend connects to VA Notify via an API we set up.
- Currently, the frontend code stores the content for on-site notifications. This may be stored by VA Notify some time in the future, but not for the MVP.
- If VA Notify determines it should send a notification to VA.gov, it will send a `user id` and `template id` to VA.gov. This is what tells us to show which notification and to whom.

### When are the notifications fetched from the server?

The notifications are pulled on load using a GET request to the api `/v0/onsite_notifications` if they have no MPI errors and they are an LOA3 user. 

* If there are any notifications, that are not dismissed, we show the notifications.
* If there are no notifications we do not show the section.
* If there is an error on the backend preventing notifications from appearing, then we do not display the Notifications section on the page.
* If there is an error when the user attempts to dismiss the notification, we show an error.

### If a user dismisses a notification

When a user dismisses a notification, we send a PATCH request to the api `/v0/onsite_notifications/${id}`. If they have an error we show the dismissal failed error. If there is no error we remove the notification from the page.

### [Adding a new notification](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/identity-personalization/onsite-notifications/frontend/adding-new-onsite-notification.md)

## Design

- [Sketch file](https://www.sketch.com/s/9b0e6efc-423a-4354-9db3-ab2083d566c9/a/uuid/FC0B70C7-FF70-4A54-8247-DC0AD864E5ED)
- [Use cases](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/onsite-notifications/use-cases)

### Before

*My VA 2.0*

![My VA 2.0](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/identity-personalization/my-va/2.0-redesign/design-ia/assets/My%20VA%202.0_Desktop_%20All%20sections.jpg)

### After

![My VA desktop inline notifications](https://user-images.githubusercontent.com/97965610/199740911-2331edf4-2e37-4081-a0fb-2a82817e75f7.jpg)
