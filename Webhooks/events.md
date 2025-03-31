---
title: "Events"
slug: "events"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Sep 07 2018 06:15:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jul 06 2023 01:03:20 GMT+0000 (Coordinated Universal Time)"
---
Each webhook that is sent is the result of an event within the payment gateway. These events are usually named with the following convention:

`subject:event`

For example, when a purchase succeeds your system (if configured) may receive the `purchase:success` event.

Currently the following events are published out of the gateway:

| Name                           | Description                                                                                     |
| :----------------------------- | :---------------------------------------------------------------------------------------------- |
| purchase:success               | A purchase has successfully been processed                                                      |
| purchase:failed                | A purchase was not processed successfully                                                       |
| refund:success                 | A refund has successfully been processed                                                        |
| refund:failed                  | A refund was not processed successfully                                                         |
| direct_entry:submitted         | A direct entry was submitted to the bank for processing                                         |
| direct_entry:completed         | A direct entry successfully completed processing                                                |
| direct_entry:rejected          | A direct entry was rejected by the bank and did not successfully complete processing            |
| direct_entry:disbursed         | A direct entry was disbursed                                                                    |
| payment_plan:activated         | A payment plan has been activated                                                               |
| payment_plan:suspended         | A payment plan was suspended                                                                    |
| payment_plan:cancelled         | A payment plan was cancelled                                                                    |
| payment_plan:completed         | A payment plan was completed                                                                    |
| payment_plan_payment:completed | A payment plan payment was completed                                                            |
| payment_plan_payment:declined  | A payment plan payment was declined                                                             |
| payment_plan_payment:error     | A payment plan payment failed due to an error                                                   |
| dispute:opened                 | A new dispute has been opened                                                                   |
| dispute:status_changed         | The status of an existing dispute has changed                                                   |
| card_account:update            | There is an update to an existing card account - see [Card Account events](card-account-events) |

# Filtering Events

New webhook events may be added as the gateway evolves, so it is important that you ensure the systems receiving these events checks the event type before attempting to process the data received.

If an event is received that is not supported it is recommended that you discard the request.
