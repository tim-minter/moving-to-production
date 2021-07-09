# Moving to Production
Moving to production? Simple checklist to get you there.

## Introduction
Moving your solution into production may be something you've planned for from the beginning or something that's suddenly become really important and stressfull, or somewhere inbetween. This document is intended to help get you there or even get you thinking about how "production ready" your system really is if it's suddenly become a production system by default as these things sometimes do.

Here are the six categories we need to look at.

- Scalabilty
- Resiliency
- Recoverability
- Support
- Organisation
- Cost

## Scalabilty

## Resiliency
- Any single points of failure
- What happens during and after a failure
  - Does the system/what the user was intending to happen pick up where it left off and carry on?
  
## Recoverability
- What level of recoverability is needed? Can it wait for whatever failed to come back on line or does it need to be moved somewhere else?
- Who does what and how do they do that, in a disaster
- Where do things get recovered to

## Support
- Who supports what, and is it to the right level to support your overall availability goal
- How is any open source code/product supported?
- How to handle service version changes and/or deprecation (particularly important in cloud solutions)

## Organisation
- Roles and responibilities clear and actually cover all requirements eg keeping data? Do you have a data controller? 
- See !here(https://github.com/tim-minter/MVO) for a "minimum viable organisation" diagram

## Cost
- Do we really know what the costs look like for 
  - Just running it with nousers/customers 
  - With 1 user/customer 
  - With 10, 100, 500, 1000, 1,000,000 etc etc. customers
  - How do support and people costs change?


