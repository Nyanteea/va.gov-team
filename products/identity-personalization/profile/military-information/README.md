# Product outline: Military information in the VA.gov profile

**Last Updated: January 11, 2023**

### Table of Contents

- [POCs](#pocs)
- [Overview](#overview)
- [User problem statements](#user-problem-statements)
- [Analytics](#analytics)
- [Projects](#projects)
- [How to access and test](#how-to-access-and-test)
- [Backend](#backend)
- [Design and UX](#design-and-ux)

### POCs
- **Slack channel**: [#accountexp-authexp](https://dsva.slack.com/channels/accountexp-authexp); [#va-profile](https://dsva.slack.com/channels/va-profile)

#### Roles  
[This is currently managed by the VA.gov profile team](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/identity-personalization/profile/README.md#roles).

## Overview

We pull in a small amount of military information to the VA.gov profile. This information is read-only and uneditable, as it is official government record.

**Currently, we show:**
- Branch(es) of service
- Period start dates
- Period end dates
- Multiple periods of service, if applicable
- Link to information on how to request records (DD214)

## User problem statements
- As a Veteran, I want to see what service history information the VA has on file for me to validate that it's correct.

## Analytics
[Google Analytics GET data](https://analytics.google.com/analytics/web/?authuser=0#/dashboard/-x0K5pQPRTaQCa_WzXnEDg/a50123418w177519031p176188361/)

## Projects

|Project|Launch date|
|-------|-----------|
|[Integrate military information through VA Profile](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/profile/military-information/vaprofile-integration#readme)| Launched August 2022|

## Backend
[Backend Technical Documentation](https://github.com/department-of-veterans-affairs/va.gov-team-sensitive/blob/master/products/identity-personalization/profile/military_info/backend_documentation.md)

- Military integrates through [VA Profile](https://depo-platform-documentation.scrollhelp.site/developer-docs/partner-services-upstream-services) as of August 2022. 
- Military information used to integrate through [eMIS](https://depo-platform-documentation.scrollhelp.site/developer-docs/emis), but the organization plans to retire that service.

### Service periods without an end date

A user can have multiple service history episodes.  It is also possible for a user that is still serving to have an open history episode (an episode without end date). The termination reason code provides the reason for the end of a service history episode. 

A service episode that is missing an end date with a termination reason code of "C", "D", or "S" indicates a data issue, and requires a follow up with  DoD for explanation or correction.

A service episode that is missing an end date with a termination reason code of "W" indicates an open (current) service period and is a valid situation.

The following provides a description of the different termination reason codes:
- "S" Separation From Personnel Category
- "C" Completion of Active Service Period
- "D" Death while in personnel category or organization
- "W" Not Applicable

## Design and UX
- [Military Information sketch files](https://www.sketch.com/s/fc96664a-1c62-40ed-9fcd-90218c54e775)
- [Use cases](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/identity-personalization/profile/military-information/use-cases)
- [High-level user flow with screenshots](https://www.sketch.com/s/fc96664a-1c62-40ed-9fcd-90218c54e775/v/nqRRpz/a/l1LzOgv/r/EYLLpY)
