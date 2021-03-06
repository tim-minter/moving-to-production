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
- Security
- Cost

## Scalability
- What happens to your system components under load? If using managed cloud based services these will **generally** scale with workload as needed (and this is one very good reason to choose to use managed services over something that you host/manage yourself). If not using a managed service then this is something you will definitely need to consider.
- Testing your system under different loads is required and making sure these tests are realistic is critical. Free load testing services or software are available but may only hit your system in a specific way for example by trying to open a single web page or just from one geographical place. You should build tests carefully.
- Using a content delivery network such as CloudFlare or Akamai or [IBM Content Delivery Network](https://cloud.ibm.com/catalog/infrastructure/cdn-powered-by-akamai) (which uses Akamai behind the scenes) is something that should be seriously considered. This removes the load from systems that deliver content i.e. web pages, video, files etc and can increase performance for web, mobile and APIs. Call to databases wont be reduced by default but it is possible to distribute traffic geographically using this service (so you could have multiple databases around the world for example and distribute traffic amongst those).
- If using Redhat Openshift or Kubernetes, auto scaling can be put in place both at the pod level and infrastructure level. Knowledge of how your system responds under load will allow you to plan for increased costs and when to add resources (and how much to add) before they are needed potentially too.
- Is the communication architecture between services and/or applications scalable? What happens if you need to add more services in the future. REST communication may be suitable for some situations but using a messaging layer such as MQ allows you to scale the architecture of your system in the future.

## Resiliency
- Any single points of failure
- If using managed cloud services, different services will have different architectures so it's important to understand what you getting "out of the box". With IBM Cloud services most will be highly available by default, but some (as with any cloud) will require specific configurations to be classed as highly available. If running your own services e.g. your own database or messaging/integration layer then 
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
- Remember that as well as your actual system, you also have a cloud to manage and monitor in some way. You need to know "what just happened to my system?". Cloud will also be emitting data which will also need to be captured by something. With IBM Cloud, adding the IBM Cloud Activity Tracker will achieve this goal.

## Support
- Who supports what, and is it to the right level to support your overall availability goal
- How is any open source code/product supported?
- How to handle service version changes and/or deprecation (particularly important in cloud solutions)

## Organisation
- Roles and responsibilities clear and actually cover all requirements e.g. keeping data? Do you have a data controller? Who will coordinate a recovery, who will spot when a service used by the solution is being upgraded/changed?
- See [here](https://github.com/tim-minter/MVO) for a "minimum viable organisation" diagram

![MVO Diagram](https://github.com/tim-minter/MVO/blob/main/minimum%20viable%20organisation%20(generic).png)

## Security
- Penetration testing
- Onboarding and off boarding of people and devices
- Source code security
- Secret handling
- Certificate management
- Vulnerability scanning

## Cost
- Do we really know what the costs look like for 
  - Just running it with no users/customers 
  - With 1 user/customer 
  - With 10, 100, 500, 1000, 1,000,000 etc etc. customers
  - How do support and people costs change?


# Quick Checklist (for IBM Cloud)
1. Add [IBM Cloud Activity Tracker](https://cloud.ibm.com/catalog/services/ibm-cloud-activity-tracker?callback=%2Fobserve%2Factivitytracker%2Fcreate) service to your cloud account. 
2. Add [IBM Cloud Monitoring](https://cloud.ibm.com/catalog/services/ibm-cloud-monitoring?callback=%2Fobserve%2Fmonitoring%2Fcreate) and set up monitoring of key metrics etc CPU and memory utilisation and performance of any messaging system eg Kafka (IBM Event Streams) or MQ etc.
3. Add [IBM Log Analysis](https://cloud.ibm.com/catalog/services/ibm-log-analysis?callback=%2Fobserve%2Flogging%2Fcreate). Note: Cost is based on data retained. Start by turning everything off and then add key metrics as you go if cost is a consideration.
4. Ensure SSL certificates are in place and certificate management process is in place (automatic or manual)
5. Perform penetration testing and code scanning and remediate.
6. Decide on required availability and ensure system architecture supports that. Typical availabilities quoted can be 95%, 99%, 99.5% 99.9%, 9.99% and 99.999%. Each of these dictates different architectures.
7. Eliminate any points of failure if they will possibly cause availability to be lower than required.
8. Ensure data is backed up and recovery of that backup is possible. Put in place a backup test process.
9. Select the size of your server/serverless/container infrastructure based on anticipated workload.
10. Test scalability by running a load generator for example [K6](https://k6.io) and monitor performance with IBM Cloud Monitoring.
11. Change the size of your server/serverless/container infrastructure and add auto scaler functions. Loop back to previous point.
12. Create plan for disaster recovery (complete or partial system failure and deletion).
13. Put in place a disaster recovery plan test process and schedule it.
14. Review security of Cloud account and put controls in place for access management going forwards (starters and leavers process, and periodic revalidation of min required access to do the job).
15. Set up problem and change management processes.
16. Ensure all roles and responsibilities are defined and assigned in the organisation. See [Minimum Viable Organisation](https://github.com/tim-minter/MVO)
