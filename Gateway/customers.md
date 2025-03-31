---
title: "Customers"
slug: "customers"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Dec 04 2017 02:30:44 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Sep 29 2018 11:05:39 GMT+0000 (Coordinated Universal Time)"
---
A customer represents an entity (business or individual) and the associated payment methods (Credit Card or Bank Account), which can then be used for payment methods such as direct debits and payment plans.

## Response object

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`id`",
    "0-1": "String",
    "0-2": "Unique ID for the customer",
    "1-0": "`email`",
    "1-1": "String",
    "1-2": "The customer’s email address (used to deliver email receipts if requested).",
    "2-0": "`reference`",
    "2-1": "String",
    "2-2": "A reference for the customer record (e.g. your database ID).",
    "3-0": "`first_name`",
    "3-1": "String",
    "3-2": "The customer’s first name.",
    "4-0": "`last_name`",
    "4-1": "String",
    "4-2": "The customer’s last name.",
    "5-0": "`created_at`",
    "5-1": "Date as String (ISO 8601)",
    "5-2": "The date that the customer was created.",
    "6-0": "`address`",
    "6-1": "hash",
    "6-2": "Hash | | |  \n------------ \\| ------------- \\| ------------  \n`address` | string | The customer’s address.  \n`city` | string | The customer’s city.  \n`state` | string | The customer’s state.  \n`postcode` | string | The customer’s postcode.  \n`country` | string | The customer’s country.",
    "7-0": "`card_token`",
    "7-1": "string",
    "7-2": "The customer’s card token.",
    "8-0": "`card_number`",
    "8-1": "string",
    "8-2": "The customer’s card number.",
    "9-0": "`bank_account`",
    "9-1": "string",
    "9-2": "The customer's bank account BSB and account number. e.g. \"012-345 012345678\"",
    "10-0": "`metadata`",
    "10-1": "hash",
    "10-2": "Hash of key/value pairs attached to the customer during creation only."
  },
  "cols": 3,
  "rows": 11,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]
