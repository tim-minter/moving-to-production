# Moving to Production
Moving to production? Simple checklist to get you there.

## Introduction
Moving your solution into production may be something you've planned for from the beginning or something that's suddenly become really important and stressful, or somewhere in-between. This document is intended to help get you there or even get you thinking about how "production ready" your system really is if it's suddenly become a production system by default as these things sometimes do.

Here are the categories we need to look at.

- Scalability
- Resiliency
- Monitoring and Logging
- Recoverability
- Support (Dev/Ops)
- Organisation
- Cost

## Scalability


## Resiliency
- Any single points of failure
- What availability is actually required. Do we need to think about replicating the system to different cities or countries so that is continues to work during a data center failure. Although rare, these can happen due to technical failure, attack or natural disaster of course.
  - The default resiliency of any cloud service will vary. Some will be easy to set up a geographically disbursed services with a few clicks (and associated multiplying of costs) and some will need to be configured manually and need some kind of load balancer in front of them.
  - The architecture of your database is critical to resiliency. 
- What happens during and after a failure
  - Does the system/what the user was intending to happen pick up where it left off and carry on?
  
## Recoverability
- What level of recoverability is needed? Can it wait for whatever failed to come back on line or does it need to be moved somewhere else?
- Who does what and how do they do that, in a disaster
- Where do things get recovered to

## Monitoring and Logging
- Cloud based services will be creating log and metric data, however this data normally has to be captured by another cloud service for you to be able to see and use it.
- Remember that as well as your actual system, you also have a cloud to manage and monitor in some way. You need to know "what just happened to my system?". Cloud will also be emitting data which will also need to be captured by something. With IBM Cloud, adding the 

## Support
- Who supports what, and is it to the right level to support your overall availability goal
- How is any open source code/product supported?
- How to handle service version changes and/or deprecation (particularly important in cloud solutions)

## Organisation
- Roles and responsibilities clear and actually cover all requirements eg keeping data? Do you have a data controller? 
- See !here(https://github.com/tim-minter/MVO) for a "minimum viable organisation" diagram

## Cost
- Do we really know what the costs look like for 
  - Just running it with no users/customers 
  - With 1 user/customer 
  - With 10, 100, 500, 1000, 1,000,000 etc etc. customers
  - How do support and people costs change?


# Quick Checklist (for IBM Cloud)
1. Add [IBM Cloud Activity Tracker](https://cloud.ibm.com/catalog/services/ibm-cloud-activity-tracker?callback=%2Fobserve%2Factivitytracker%2Fcreate) service to your cloud account. 
2. Add [IBM Cloud Monitoring](https://cloud.ibm.com/catalog/services/ibm-cloud-monitoring?callback=%2Fobserve%2Fmonitoring%2Fcreate) and set up monitoring of key metrics etc CPU and memory utilisation and performance of any messaging system eg Kafka (IBM Event Streams) or MQ etc.
3. Add [IBM Log Analysis](https://cloud.ibm.com/catalog/services/ibm-log-analysis?callback=%2Fobserve%2Flogging%2Fcreate).
4. Decide on required availability and ensure system architecture supports that.
5. Eliminate any single points of failure if they will possibly cause availability to be lower than required.
6. Ensure data is backed up and recovery of that backup is possible. Put in place a backup test process.
8. Select the size of your server/serverless/container infrastructure.
9. Test scalability by running a load generator for example [K6](https://k6.io) and monitor performance with IBM Cloud Monitoring.
10. Change the size of your server/serverless/container infrastructure and add auto scaler functions.
11. Create plan for disaster recovery (complete or partial system failure and deletion).
12. Put in place a disaster recovery test process.
13. Review security of Cloud account and put controls in place for access management going forwards (starters and leavers process, and periodic revalidation of min required access to do the job).
14. Set up problem and change management processes.
15. Ensure all roles and responsibilities are defined and assigned in the organisation. See [Minimum Viable Organisation](https://github.com/tim-minter/MVO)
