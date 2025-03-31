---
title: "Create a purchase, with fraud screening"
slug: "create-a-purchase-with-fraud-screening"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Sep 07 2018 06:48:14 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 13 2018 06:15:31 GMT+0000 (Coordinated Universal Time)"
---
## Fraud Request Payload

To process fraud checking before the transaction is processed the following details should be added to the request payload:

```json
{
    "fraud": {
        "customer": {
            "address_1": "23 Smith Road",
            "city": "Canberra",
            "country": "AUS",
            "created_at": "2014-05-28T21:38:51+11:00",
            "date_of_birth": "1994-05-28T00:00:00+11:00",
            "email": "deny@email.com",
            "existing_customer": true,
            "first_name": "James",
            "home_phone": "0421858999",
            "id": "ABD123",
            "last_name": "Smith",
            "post_code": "2600"
        },
        "device_id": "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",
        "items": [
            {
                "cost": 23.3,
                "description": "Widgets",
                "line_total": 23.3,
                "product_code": "9999-A",
                "qty": 1,
                "sku": "9999"
            }
        ],
        "recipients": [
            {
                "address_1": "1 Fairfield Road",
                "city": "Austin",
                "country": "USA",
                "email": "james@smith.com",
                "first_name": "James",
                "last_name": "Smith",
                "phone_number": "555-555-55555",
                "post_code": "55555-1234",
                "state": "TX"
            }
        ],
        "shipping_address": {
            "address_1": "23 Smith Road",
            "city": "Canberra",
            "country": "AUS",
            "email": "deny@email.com",
            "first_name": "James",
            "home_phone": "0421858999",
            "last_name": "Smith",
            "post_code": "2600",
            "shipping_method": "express"
        },
        "custom": {
            "3": "Facebook"
        },
        "website": "http://www.website.com"
    }
}
```

The Fraud Request payload consists of base data and 4 sub-data elements.  
Base data includes:

- `website`: This field is optional yet highly recommended if your website URL differs from that on record with the gateway. For example, if you have country-specific websites.
- `device_id`

### Sub-data elements

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`customer`",
    "0-1": "Object",
    "0-2": "",
    "1-0": "`customer.first_name`",
    "1-1": "String. Max length: 30.",
    "1-2": "The customer's first name",
    "2-0": "`customer.last_name`",
    "2-1": "String. Max length: 30.",
    "2-2": "The customer's surname",
    "3-0": "`customer.email`",
    "3-1": "String. Max length: 45.",
    "3-2": "The customer's email address",
    "4-0": "`customer.date_of_birth`",
    "4-1": "String. Date.",
    "4-2": "The customer's DOB, if applicable",
    "5-0": "`customer.id`",
    "5-1": "String. Max length: 16.",
    "5-2": "The customer record identifier in your database ,if available",
    "6-0": "`customer.address_1`",
    "6-1": "String. Max length: 30.",
    "6-2": "The customer's primary address line",
    "7-0": "`customer.address_2`",
    "7-1": "String. Max length: 30.",
    "7-2": "The customer's secondary address line (e.g. building name)",
    "8-0": "`customer.city`",
    "8-1": "String. Max length: 20.",
    "8-2": "The customer's city/suburb",
    "9-0": "`customer.post_code`",
    "9-1": "String. Max length: 9.",
    "9-2": "The customers postal code",
    "10-0": "`customer.home_phone`",
    "10-1": "String. Max length: 19.",
    "10-2": "The customers primary phone number",
    "11-0": "`customer.work_phone`",
    "11-1": "String. Max length: 19.",
    "11-2": "The customers secondary or work phone number",
    "12-0": "`customer.country`",
    "12-1": "String. Max length: 3. ISO-3166 alpha-3 country code.",
    "12-2": "The ISO-3166 alpha-3 country code for the customer",
    "13-0": "`customer.existing_customer`",
    "13-1": "Boolean",
    "13-2": "Indicates if this is a customer already in the merchants records or not",
    "14-0": "`customer.created_at`",
    "14-1": "String. Date.",
    "14-2": "The date/time the customer record was created",
    "15-0": "`shipping_address`",
    "15-1": "Object",
    "15-2": "",
    "16-0": "`recipients`",
    "16-1": "Array of Objects.  \nMax length: 99",
    "16-2": "",
    "17-0": "`items`",
    "17-1": "Array of Objects.  \nMax length: 99",
    "17-2": "",
    "18-0": "`custom`",
    "18-1": "Object",
    "18-2": ""
  },
  "cols": 3,
  "rows": 19,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]
