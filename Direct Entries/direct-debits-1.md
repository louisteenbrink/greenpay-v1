---
title: "Direct Debits"
slug: "direct-debits-1"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Sep 10 2018 21:19:04 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 19:41:53 GMT+0000 (Coordinated Universal Time)"
---
Direct Debit is the process of debiting money from a customer's bank account through the asynchronous Direct Entry batch process.

In order to take Direct Debit payments, you must establish a Direct Debit facility through your bank or through a payment services provider like Fat Zebra. Your account manager can assist with this if required.

To debit a customer, you will require:

- The Direct Debit facility enabled for your merchant account
- The customer's BSB
- The customer's Account Number
- The name of the customer's account

Direct Debits are processed in a nightly batch with the cutoff for payments being 5PM, UTC+10 (or UTC+11 during Australian Daylight Saving Time). 

Once a Direct Debit has been submitted for processing, the results will be updated overnight. However it is important to remember that it can take up to 3 business days from the date of the Direct Debit for rejections to come through from the banking network.

Due to the asynchronous nature of this payment method, it is recommended that you implement [Webhooks](doc:webhooks) so that your system is updated upon the completion or rejection of payments.
