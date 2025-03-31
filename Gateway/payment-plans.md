---
title: "Payment Plans"
slug: "payment-plans"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Mar 01 2018 04:28:28 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jan 09 2020 02:31:40 GMT+0000 (Coordinated Universal Time)"
---
Payment Plans allow a merchant to setup a billing schedule for a customer which can charge their credit card, or (if the merchant is configured for Direct Debit) debit from a bank account. 

Prior to setting up a Payment Plan, a customer record needs to be setup in the system with an associated payment method (i.e. Credit Card or Bank Account). Details on how to create a customer can be found under the Customers section.

## Processing and Retries

Payment Plans are processed daily at 3am Sydney time. When a payment succeeds, the payment plan is 'Rolled Over' which will either generate the next payment to replace the one just processed, or update the payment plan (for example, marking as completed, suspending, re-activating etc).

Payments will be retried up to 3 times before suspending a plan, with a delay between retries (this delay is defined when setting up a plan as retry_interval, however it will default to 3 days).

## Response object

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`id`",
    "0-1": "String",
    "0-2": "Unique identifier for this payment plan.",
    "1-0": "`customer`",
    "1-1": "String",
    "1-2": "Unique identifier for this payment plan's customer.",
    "2-0": "`amount`",
    "2-1": "Integer",
    "2-2": "The recurring payment amount in the smallest unit for the currency e.g. 1000 = AU$10.",
    "3-0": "`currency`",
    "3-1": "String",
    "3-2": "The currency code for the plan.",
    "4-0": "`setup_fee`",
    "4-1": "Integer",
    "4-2": "A setup fee to be charged upon creation of the payment plan.",
    "5-0": "`frequency`",
    "5-1": "String",
    "5-2": "The frequency of the payments. Acceptable values are: Weekly, Fortnightly, Monthly, 4-Weekly, Quarterly and Annually",
    "6-0": "`anniversary`",
    "6-1": "Integer",
    "6-2": "The anniversary of the recurring payments.  \n  \nFor Weekly and Fortnightly payments this will be the day of the week (1 - Monday, 2 - Tuesday, 3 - Wednesday, 4 - Thursday, 5 - Friday)  \nFor Monthly this will be the day of the month. If the day of the month is greater then 28, and the month is shorter  \nthen the anniversary this date will be moved forward to the nearest possible date (i.e. a payment for the 31st will fall on the 30th for monthly like September etc).",
    "7-0": "`start_date`",
    "7-1": "Date (yyyy-mm-dd)",
    "7-2": "The date the payment plan should start. This must be in the future.",
    "8-0": "`end_date`",
    "8-1": "Date (yyyy-mm-dd)",
    "8-2": "The date the payment plan should end on. This must be in the future and greater then the start_date. Optional.",
    "9-0": "`total_count`",
    "9-1": "Integer",
    "9-2": "The total number of payments to process for this plan. Optional.",
    "10-0": "`total_amount`",
    "10-1": "Integer",
    "10-2": "The total amount of all payments to be processed for this plan. Optional.",
    "11-0": "`payment_method`",
    "11-1": "String",
    "11-2": "The payment method for the plan - this can be Credit Card or Direct Debit.  \nNote: if a merchant is not configured for Direct Debit, or a customer is not setup with the defined payment method, an error will be returned.",
    "12-0": "`reference`",
    "12-1": "String",
    "12-2": "Your reference for the payment plan.",
    "13-0": "`description`",
    "13-1": "String",
    "13-2": "A description for the payment plan (e.g. Model 200R Blender Lay-by)",
    "14-0": "`status`",
    "14-1": "String",
    "14-2": "The status of the payment plan.",
    "15-0": "`status_reason`",
    "15-1": "String",
    "15-2": "The reason the status was most recently changed.",
    "16-0": "`created_at`",
    "16-1": "Date as String (ISO 8601)",
    "16-2": "The date that the payment plan was created.",
    "17-0": "`failed_payment_fee`",
    "17-1": "Integer",
    "17-2": "A fee to apply to the retried payment in the event of any declined payment. Default: 0  \nNote: This amount will compound for the total number of retries (3) performed.",
    "18-0": "`retry_interval`",
    "18-1": "Integer",
    "18-2": "The number of days between payment retries for any declined payments. Default: 3",
    "19-0": "`status_change_date`",
    "19-1": "Date (yyyy-mm-dd)",
    "19-2": "The date at which the status will roll over from Active to Suspended or vice versa.",
    "20-0": "`payments`",
    "20-1": "Array of Payment objects",
    "20-2": "Payment object | | |  \n------------ \\| ------------- \\| ------------  \n`id` | string | Unique identifier for this payment.  \n`payment_plan` | string | Unique identifier for this payment's plan.  \n`amount` | integer | The amount for the payment.  \n`currency` | string | The currency code for the payment.  \n`scheduled_date` | Date (yyyy-mm-dd) | The date of the scheduled payment.  \n`payment_method` | string | The payment method for the payment - this can be Credit Card or Direct Debit  \n`status` | string | The status of the payment. Possible values are: Scheduled, Completed, Declined, Error and Error - Contact Support.  \n`result` | string | The result of the payment - this will be any of the Response Codes messages.  \n`records` | Array | This is an array of the payment method records (i.e. Purchases or Direct Debits). This will include any declined and approved payments."
  },
  "cols": 3,
  "rows": 21,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


Note that on Payment Plan bounds (End Date, Total Count, Total Amount): If a plan is bounded by an end date, total count or total amount there may be a balloon payment (large final payment) at the end of the plan. For example, if a plan is setup to start on 16/07/2015, end on 31/07/2015, has an amount of $100 and a total amount of $1,000 then the payment amounts created will be: $100, $100, $800. The final large amount is due to the bounding implied by the end date, along with the expectation that a total of $1,000 for the plan will be collected.
