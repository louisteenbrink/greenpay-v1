---
title: "Managing Merchant Application Lifecycle"
slug: "onboarding-managing-merchant-application-lifecycle"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Nov 25 2020 05:16:43 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Dec 01 2020 02:20:48 GMT+0000 (Coordinated Universal Time)"
---
Below are the states that a merchant application can have

| State              | Description                                                                     |
| :----------------- | :------------------------------------------------------------------------------ |
| pending            | As soon as a new application is submitted and accepted by FatZebra backend.     |
| under_review       | When the review process starts for the application.                             |
| more_info_required | More information is required                                                    |
| approved           | Application is approved.                                                        |
| rejected           | Application is rejected. Application resubmission or update will return errors. |

You will be notified on application state changes via webhook events. The event content contains (1) event name, and (2) affected application’s application_uuid.

The approved webhook event will also contain merchant’s username (unique handle for identifying the merchant). It will be used for retrieving basic auth credentials in order to process payments for this merchant.
