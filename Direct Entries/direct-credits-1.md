---
title: "Direct Credits"
slug: "direct-credits-1"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Sep 10 2018 21:19:32 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 13 2018 06:16:09 GMT+0000 (Coordinated Universal Time)"
---
Direct Credit is the process of crediting (sending) money from your bank account (the funding account or source account) to a customer's bank account (the destination account), through the asynchronous Direct Entry batch process. Usually this is used for the distribution/disbursal of funds, reimbursements, etc.

In order to send Direct Credit payments, you must establish a Direct Credit facility through your bank. Your account manager can assist with this if required.

To credit funds to a customer, you will require:

- The Direct Credit facility enabled for your merchant account
- The customer's BSB
- The customer's Account Number
- The name of the customer's account

Direct Credits are processed in a nightly batch, with the cutoff for payments being 5PM, UTC+10 (or UTC+11 during Australian Daylight Saving Time). If there is insufficient funds to process the whole file submitted to the bank, your Direct Credits will fail and will be updated accordingly.

Once a Direct Credit has been submitted for processing, the funds will arrive in the destination account within 24 hours, usually the next business day.

Due to the asynchronous nature of this payment method, it is recommended that you implement [Webhooks](doc:webhooks) so that your system is updated upon the completion or rejection of payments.
