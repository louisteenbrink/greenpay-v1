---
title: "Create Purchases with Direct Post"
slug: "create-purchases-with-direct-post"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Sep 13 2018 06:52:28 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Sep 17 2018 00:16:45 GMT+0000 (Coordinated Universal Time)"
---
# Request paremeters

When performing a Direct Post purchase the following parameters are required:

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "card_holder",
    "0-1": "String",
    "0-2": "The name of the credit card holder",
    "1-0": "card_number",
    "1-1": "String",
    "1-2": "The credit card number",
    "2-0": "expiry_month",
    "2-1": "Integer (m or mm)",
    "2-2": "The card expiry month, 1 or 2 digits (e.g. 5, 12, 06)",
    "3-0": "expiry_year",
    "3-1": "Integer (yyyy)",
    "3-2": "The card expiry year, 4 digits (eg. 2023)",
    "4-0": "cvv",
    "4-1": "String",
    "4-2": "The CVV or Security Code on the back of the card - 3 digits  \nAMEX Note: this number is printed on the front of an AMEX and is 4 digits in length"
  },
  "cols": 3,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


In addition to these fields the following hidden fields should also be included:

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "amount",
    "0-1": "Integer",
    "0-2": "The purchase amount, as an integer in the smallest currency unit (e.g. AU$100.50 will be 10050)",
    "1-0": "currency",
    "1-1": "String",
    "1-2": "The purchase currency (3-letter [ISO-4217 Code](http://en.wikipedia.org/wiki/ISO_4217))",
    "2-0": "return_path",
    "2-1": "String",
    "2-2": "The URL to redirect the customer to with the response.  \nThis will normally be a URL on the merchants website but it can also be a custom-scheme registered for mobile applications.",
    "3-0": "verification",
    "3-1": "String",
    "3-2": "The verification value. Details on how to calculate this are below."
  },
  "cols": 3,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


The URL for the Direct Post form should be: 

- **Sandbox**: `https://gateway.pmnts-sandbox.io/v2/purchases/direct/[MERCHANT USERNAME]`
- **Live**: `https://gateway.pmnts.io/v2/purchases/direct/[MERCHANT USERNAME]`

## Calculating the Verification Value

There are several hidden fields in this form which are submitted to the Gateway from the customers browser. These are:

- **reference** - the purchase reference (e.g. invoice or order number)
- **amount** - the purchase amount
- **currency** - the currency for the transaction
- **return_path** - the URL to return the customer to on completion 

In order to ensure these values are not changed a verification value is also included, which is determined by the following:
