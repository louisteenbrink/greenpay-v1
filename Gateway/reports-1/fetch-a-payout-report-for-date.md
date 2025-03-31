---
title: "Fetch a payout report for date"
slug: "fetch-a-payout-report-for-date"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Oct 04 2022 00:21:20 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Oct 05 2022 03:35:46 GMT+0000 (Coordinated Universal Time)"
---
## Payout Reports

Payout reports contain information about your purchases, refunds, and disputes for a given date.

## Response Object

The table below outlines the fields that are returned by the `/payouts` namespace. Expect an array of objects with these fields if you have payouts to multiple accounts on the same day.

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`payout_date`",
    "0-1": "String / Date YYYY-MM-DD",
    "0-2": "The date of the payout.",
    "1-0": "`payouts `",
    "1-1": "Array",
    "1-2": "An array of payouts.",
    "2-0": "`method`",
    "2-1": "- VISA/MASTERCARD  \n- UPI  \n- AMEX  \n- BECS",
    "2-2": "This represents the method associated with the payout.",
    "3-0": "`funding_account `",
    "3-1": "Object",
    "3-2": "This stores the account number and bsb.",
    "4-0": "`bsb `",
    "4-1": "String / “NNN-NNN”",
    "4-2": "The bsb of the funding account object.",
    "5-0": "`account_number`",
    "5-1": "String",
    "5-2": "The account number of the funding account object.",
    "6-0": "`reference `",
    "6-1": "String / “FZ-YYYYMMDD-<string>”",
    "6-2": "The reference displayed on the merchant’s bank statement.",
    "7-0": "`amount `",
    "7-1": "Float",
    "7-2": "The total payout disbursed that day. Can be a negative value denoting a claw back (direct debit).",
    "8-0": "`detail `",
    "8-1": "Object",
    "8-2": "Contains the breakdown of the figures that determine the payout figure.",
    "9-0": "`gross_processing_amount `",
    "9-1": "Float",
    "9-2": "The total **gross** value of your purchases minus refunds and chargebacks.",
    "10-0": "`transaction_count `",
    "10-1": "Integer",
    "10-2": "The count of all transactions processed for the day.",
    "11-0": "`processing_fees_amount `",
    "11-1": "Float",
    "11-2": "The total of all charges withheld. This excludes dispute charges.",
    "12-0": "`dispute_charges_amount `",
    "12-1": "Float",
    "12-2": "The total chargeback fees incurred (and deducted).",
    "13-0": "`disputes_count `",
    "13-1": "Integer",
    "13-2": "The count of all disputes processed for the day."
  },
  "cols": 3,
  "rows": 14,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]
