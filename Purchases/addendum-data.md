---
title: "Addendum Data"
slug: "addendum-data"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 07:38:02 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Sep 29 2018 08:35:36 GMT+0000 (Coordinated Universal Time)"
---
For some switching paths and acquirers it may be possible to include addendum data which is passed onto the card issuer - this is primarily used for corporate purchasing cards, American Express cards etc.

To include this data with your transactions, the field `addendum_data` should be added to the request payload with the appropriate data payload for the transaction type - these different payload types are detailed below.

```json
{
  "card_holder": "Jim Smith",
  "card_number": "5123456789012346",
  "card_expiry": "05/2023",
  "cvv": "987",
  "amount": 1000,
  "reference": "ORD98976",
  "customer_ip": "111.222.111.123",
  "currency": "AUD",
  "addendum_data": {
    "corp_l2": {
      "cardmember_reference": "ORD 123456 PO 08789",
      "description_1": "Box of paper",
      "quantity_1": 5,
      "total_1": 5000           
    }
  }
}
```

Addendum data is accepted for Purchase (Pre-auth and Purchase), and Captures, and should be included in the normal request payload, for example to include addendum data in a capture request:

```json
{
  "amount": 10000,
  "addendum_data": {
    "corp_l2": {
      "cardmember_reference": "ORD 123456 PO 08789",
      "description_1": "Box of paper",
      "quantity_1": 5,
      "total_1": 5000           
    }
  }
}
```

If addendum data was presented with the original transaction (such as for a pre-auth) the data will be merged, with the most recent data overwriting the older data.

## Corporate Purchasing Level 2 Data

Level 2 data for corporate purchase cards may be included which can detail the order reference, purchase order numbers, line item details etc.

| Field Name                    | Type (Length)                             | Description                                                                                                                      |
| :---------------------------- | :---------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------- |
| cardmember_reference          | String (20), Alphanumeric and Spaces only | The card member's reference number, such as a store order number and/or customer PO Number                                       |
| description_1 - description_4 | String (40), Alphanumeric and Spaces only | The description for (up to) the first four line items. These should be descriptive and avoid generic terms such as 'Merchandise' |
| quantity_1 - quantity_4       | Integer (3)                               | The quantity of items for each line item                                                                                         |
| shipping_postcode             | String (15), Alphanumeric and Spaces only | The post code for the shipping address                                                                                           |
| total_1 - total_4             | Integer (5)                               | The total for each line item as a whole number in the smallest unit (e.g. $155.60 will be 15560)                                 |

```json Full Corporate Level 2 data example:
{
  "corp_l2": {
    "cardmember_reference": "ORD 123456 PO 08789",
    "description_1": "Box of paper",
    "quantity_1": 5,
    "total_1": 5000,
    "description_2": "Pencils",
    "quantity_2": 10,
    "total_2": 1000,         
    "description_3": "Pens",
    "quantity_3": 10,
    "total_3": 1500,
    "description_4": "White Out",
    "quantity_4": 1,
    "total_4": 500,
    "shipping_postcode": "EC1A 1AA"
  }
}
```
