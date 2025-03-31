---
title: "Issue a refund"
slug: "issue-a-refund"
excerpt: "Issue a refund against a purchase or standalone"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jan 18 2018 06:44:53 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:40:36 GMT+0000 (Coordinated Universal Time)"
---
# Standalone Refunds

It is possible to issue a Standalone Refund (i.e. a refund that is not against an existing purchase), such as when refunding from a central account or some other kind of out-of-band refund scenario. 

To issue a Standalone Refund, simply provide the `card_token` or provide `card_number`, `card_holder` and `card_expiry` in lieu of the `transaction_id`.

Support for Standalone Refunds may vary among banks, so please contact Fat Zebra support if you are unable to successfully issue a Standalone Refund.
