---
title: "Overview"
slug: "direct-entry-overview"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Sep 10 2018 21:36:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Jan 16 2023 20:30:54 GMT+0000 (Coordinated Universal Time)"
---
Direct Entry (DE) payments are a method of receiving or sending money directly from or to a customers bank account. Most merchants will require Direct Debit payments, however in some cases Direct Credit is also used.

In order to make Direct Debit or Direct Credit payments, a Direct Entry (DE) facility is required. This can usually be established through your financial institution, or through a payment services provider such as Fat Zebra.

In addition to stand-alone Direct Debit payments, it is also possible to process Batch Payments, which are especially useful for large payment runs.

Fat Zebra can support debiting bank accounts in Australia and New Zealand.

# Direct Entry Facility

If you would like to make Direct Debit or Direct Credit payments and already have a Direct Entry (DE) facility, you will need to provide us with the following:

- Your Direct Entry User ID (DE ID)
- Your institution code (such as WBC)
- Your User Preferred Specification (UPS) - commonly known as the display name
- Your BSB and Account Number for the source/destination account

# Asynchronous Processing

Direct Entry processing is an asynchronous payment method, which means that this is not a real-time process due to the way that the banks process the payment files. Completion and rejection cannot be guaranteed until after 3 business days, as this is dependent on the network of banks to return payment statuses back to the originating bank.

# Handling Rejections

The status of a direct debit can take up to 3 business days to be returned from the account holder's bank. We recommend merchants set up a webhook to receive notifications when direct debits are updated to rejected. Please see our [Webhooks Overview](doc:webhooks-overview) for more information.

Please note that Direct Debit batches allow 3 business days for all rejections to be received before they are available to be downloaded.

# Direct Entry Statuses

There are five states a direct entry record can be in:

- New - the record has been created in Fat Zebra's system and has not been submitted to the financial institution
- Pending - the record has been submitted to the financial institution for processing
- Completed - the record has been successfully processed
- Rejected - the record was rejected - check the result field for details
- Delete - the record has been deleted and was not submitted for processing

# Testing

In the sandbox environment, the cent-amount of a direct entry can be used to simulate a specific outcome. The possible results are as follows:

| Amount | Result                                                             |
| :----- | :----------------------------------------------------------------- |
| $x.01  | Invalid BSB Number                                                 |
| $x.02  | Payment Stopped                                                    |
| $x.03  | Account Closed                                                     |
| $x.04  | Customer Deceased                                                  |
| $x.05  | No Account/Incorrect Account Number                                |
| $x.06  | Refer to Customer                                                  |
| $x.08  | Invalid User ID number (configuration error with your DE facility) |
| $x.09  | Technically Invalid                                                |

Any other value will result in a successfully completed DE.
