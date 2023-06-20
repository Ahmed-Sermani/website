---
title: "Safe Live Testing"
description: ""
type:
    - "posts"
    - "post"
tags:
    - "development"
    - "testing"
date: "2020-04-02"
categories:
    - "Development"
---
# Business Critical Services Safe Live Testing

When startups transition from monolith to microservices, they typically begin by identifying business domains. Some of the domains would be extremely critical to the company (for example, payment processing, fraud detection, and so on). The migration may require extensive refactoring to address the tech debt that has accrued as a result of the company’s rapid growth. How can the team safely move those services and ensuring their reliability and correctness without risking blocking those domains?

## The Solution

In most situations, extensively using the unit and integration testing can be extremely beneficial, but it is still not enough to deal with real scenarios in production.

When there is a shared database between the new service and the monolith during the first stage of the migration. The concept is to route a portion of the responses from the old service to a new service endpoint that is configured to accept such data.

The new end-point will compare and contrast the old and new implementation methods. It will use the same input data to call the new service, validate the desired output using the old service response, and report any anomalies.

![](https://cdn-images-1.medium.com/max/2000/1*N_BS2kOThoiZhF2G_d1mDw.jpeg)

### Points To Keep In Mind

* To avoid blocking the old service, it’s best to use a message broker or some other background job method.

* If the endpoint performs any alterations or posts data to any third party you have to mock those calls with the desired response and roll back any database updates at the end of the execution.

* If you integrate with an observability platform that supports custom events (e.g., new relic, data dog, etc. ), it’s best to fire the events there rather than storing them because it will give you more options for visualization and analysis.

* You have to keep in mind that there is a chance for the anomalies to be sourced from the old service.

* Be sure not to run the experiment on each request, as this will cause your database’s traffic to double.

## Validation

Any irregularities will be reported by the structure, which will provide the opportunity to correct them without ever impacting the end-user. Many indicators can be used to verify performance and provide real-time analytics for the new service.

If you reach a certain confidence level in the new service you can start incrementally routing traffic directly.

## Conclusion

Live testing will always be a matter of taste, and certain situations will require a different approach. However, I find that this approach provides the most confidence and insight without facing any risks.
I’d love to hear your thoughts or if you have a different approach than the ones outlined above!
