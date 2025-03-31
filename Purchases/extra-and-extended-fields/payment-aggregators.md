---
title: "Payment Aggregators"
slug: "payment-aggregators"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Aug 10 2020 05:25:46 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Mar 23 2023 06:19:02 GMT+0000 (Coordinated Universal Time)"
---
> 🚧 Limited Acquirer Support For Payment Aggregators
> 
> Processing transactions as a Payment Aggregator is not supported by all Australian acquirers. If these methods are used where support is not yet available the transactions may be declined or return errors. Contact the Fat Zebra support team for more information.

The Payment Aggregator fields allow merchants who act as a Payment Aggregator to specify sub-merchant details required by their acquirers. This is currently only supported for a handful of banks, and must be enabled before use by contacting the Fat Zebra support team.

Payment Aggregator fields are specified in the field **sub_merchant** of type **Hash**. They can be specified on authorisation, purchase, and refund transactions.

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "**id**",
    "0-1": "String  \n_(max 20 characters)_",
    "0-2": "The sub merchant's id as specified by your acquirer  \n  \nThis field is mandatory for Westpac merchants",
    "1-0": "**aggregator_name**",
    "1-1": "String  \n_(max 38 characters)_  \n  \n_Note: **aggregator_name** + **name** must not exceed 37 characters_",
    "1-2": "The aggregator name assigned to you by your acquirer  \n  \nFor Westpac merchants this is a 3 character string",
    "2-0": "**name**",
    "2-1": "String  \n_(max 38 characters)_  \n  \n_Note: **aggregator_name** + **name** must not exceed 37 characters_",
    "2-2": "The business name of the sub merchant",
    "3-0": "**address**",
    "3-1": "String  \n_(max 38 characters)_",
    "3-2": "The street address of the sub merchant  \n  \nThis field is mandatory for Westpac merchants",
    "4-0": "**city**",
    "4-1": "String  \n_(max 21 characters)_",
    "4-2": "The city of the sub merchant",
    "5-0": "**state**",
    "5-1": "String  \n_(max 3 characters)_",
    "5-2": "The state of the sub merchant",
    "6-0": "**postcode**",
    "6-1": "String  \n_(max 15 characters)_",
    "6-2": "The postcode of the sub merchant  \n  \nThis field is mandatory for Westpac merchants",
    "7-0": "**country_code**",
    "7-1": "String  \n_(max 2 characters)_",
    "7-2": "The country code of the sub merchant in 2-letter ISO 3166-2  \n  \nE.g. use **AU** for Australia",
    "8-0": "**phone**",
    "8-1": "String  \n_(max 20 digits)_",
    "8-2": "The merchants phone number (for customers to contact if required)",
    "9-0": "**email**",
    "9-1": "String  \n\\*(max 40 characters)",
    "9-2": "The merchants email address (for customers to contact if required)  \n  \n_Optional_"
  },
  "cols": 3,
  "rows": 10,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


```json Example: Payment Aggregator fields
{
  "extra": {
    "sub_merchant": {
      "id": "ABC",
      "aggregator_name": "FZ",
      "name": "ABC Pty Ltd",
      "address": "58 Kippax Street",
      "city": "Surry Hills",
      "state": "NSW",
      "postcode": "2010",
      "country_code": "AU",
      "email": "contact@abc.com.au",
      "phone": "0290371840"
    }
  }
}
```
